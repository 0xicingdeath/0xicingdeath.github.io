+++
date = '2026-04-28T15:49:43-04:00'
draft = false
author = 'Nat Chin' 
title = 'When Bitwise NOT breaks Differential Tests'
+++

When you build your test suite to work for you, it *really* works.

In a recent engagement, I used differential testing to verify if two implementations of the same logic—one in Golang, one in Solidity—were actually identical. This was a perfect use-case for differential fuzzing - logic that looks the same, under manual review. But looks aren't everything. 

To find them, I built a "fuzzing harness." Imagine a monkey smashing a keyboard, taking that random input, and feeding it to the equivalent program in Solidity and Golang. If the Go version succeed on the input but the Solidity version hates it (or vice-versa), the fuzzer errors.

### Diggin' into the code 

The goal was for these two implementations to be identical. 

**Golang Original:**
```golang
// ensure MAP_ANONYMOUS is set and fd == -1
if (flags.val()&0x20) == 0 || fd != u64Mask() {
   addr = u64Mask()
   errCode = toU64(0x4d) // no error
} 
```

**Solidity Original:**
```solidity
switch or(iszero(and(flags, 0x20)), not(eq(fd, u64Mask())))
   case 1 {
      addr := u64Mask()
      errCode := toU64(0x4d)
}
```

### Eureka....or kind of 

At a high level, both codebases were intended to return 1 on their first lines, to enter the `if`/`switch` statement. Instead, the program produced two separate numeric outputs, which was miscalculated. The fuzzer had found a deviation in which one of the calculations uses a padded variable, causing a discrepancy. 

| Step | Golang Logic | Solidity Logic | Match? | 
|------|--------|----------|--------|
| 1. Check Flags | `31&0x20 ==0 -> 1` | `isZero(and(31, 0x20)) -> 1` | ✅ |
| 2. Equality Check ** | `fd == u64Mask() = 1` | `eq(18446744073709551551, u64Mask()) = 0000000000000000000000000000000000000000000000000000000000000000`  | ❓ |
| 3. The NOT | Result is already `1` | `1111111111111111111111111111111111111111111111111111111111111111 -> 0xff.ff` | ❌| 

*Note: Step 2 in Golang logic combines step 2 and 3 in one. This is why the result is already 1.

### What happened? 

In Golang, the result of the check is a literal `1`. The logic is only a single bit - this is **expected behaviour.** 

In Yul, the `not()` operator is applied *bitwise*. When the equality check `eq(fd, u64Mask())` returned a 0, it was interpreted as `00...00`. Applying the `not()` operator on the 32 byte word of zeroes, flipped **every single bit.**

The result in Solidity wasn't a `1` - it was a `1111111111111111111111111111111111111111111111111111111111111111`. 

Because the Solidity code used a `switch` statement, which expected a result of `1`, the control flow did not enter the branch. In Golang, the same path resulted in a `1`, which ran the associated code. This resulted in the final result of both implementations to be mismatched.

#### Evolution of the Fuzzer 

The fuzzer went through four distinct iterations: 

- **V0 (Sanity Check):** - Simple success/failure check - if one version reverts with input, both must revert and vice versa.
- **V0.5 (Error Matching):** - Tightened constraints. If both versions fail, the error codes must match.
- **V1 (Input Targeting):** - Defined specific numeric ranges for inputs to ensure that the fuzzer could explore additional flows.
- **V2 (Coverage Bumper):** - Analyzed branch coverage of unit tests, and realized that this if statement had no coverage. I manually seeded the fuzzer with inputs that should trigger this statement. **The fuzzer found the deviation in seconds**

### *Smart* ~Dumb~ Monkey-Smashing-Keyboard 

I mentioned that fuzzing is like a monkey smashing a keyboard, but a "dumb" monkey uses input space inefficiently. If you're testing liquidity pools or low-level masks, a random `uint256` will almost always just trigger either the same happy paths already discovered, or generic "Balance too low" or more likely, a series of reverts that causes the fuzzer to get nowhere.

A "Smart" Fuzzer (V2) uses directed input generation. By constraining the "monkey" to smash keys within specific numeric ranges (like values just above or below u64Mask), we maximize coveraged reached by the fuzzer.

This is the intersection of security research and development: knowing where the code is likely to have issues and guiding the tools to look there. It is highly improbable the fuzzer would have found this specific bit-flip on its own without those manual adjustments to the harness. It is also highly improbable that this bug would be found via manual review.

### Lessons for the Road

1. **Logical vs. Bitwise:** In Yul, always use `iszero(x)` for negation. Avoid `not()` unless you are actually manipulating bits.
2. **Stop and think:** Focus on the areas your unit tests don't reach. Use coverage reports as a gauge for where to target your fuzzer.
3. **Always Deterministic:** Never ignore a failed test, especially if it's only *sometimes* fails. If any test fails once, you're likely sitting on a bug. Understand it. Investigate it.
