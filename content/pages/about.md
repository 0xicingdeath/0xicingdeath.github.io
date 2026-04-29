---
title: About
author: Nat
---

I bridge the gap between building high-assurance software and breaking it. With a background as a developer, a hackathon organizer, and a 4 year tenure at Trail of Bits, I specialize in invariant-driven security. 
- Authored: [solc-select](https://www.google.com/search?q=%5Bhttps://github.com/crytic/solc-select%5D(https://github.com/crytic/solc-select)) (Standard industry tool for Solidity version management)
- Proven: Led 100+ security reviews for industry leaders like Coinbase, Optimism, Scroll, Frax
- Specialty: Record-breaking invariant engagements (216 custom invariants for Curvance)

### Invariant Development & Open Source
My development background allows me to translate complex protocol logic into formal invariants, creating automated testing suites that uncover edge cases missed by traditional manual reviews.

**Featured Project: Curvance**
I led a 10-week solo high-assurance engagement, resulting in 216 invariants. This remains one of the most comprehensive fuzzing suites ever developed for a smart contract protocol.

[Blog post](https://blog.trailofbits.com/2024/04/30/curvance-invariants-unleashed) | [Report](https://github.com/trailofbits/publications/blob/master/reviews/2024-03-curvance-invariant-development.pdf)

### Open Source Projects
  - [Author of solc-select](https://github.com/crytic/solc-select) – Lead author and maintainer. A CLI tool that allows users to switch between Solidity compiler versions instantly.
  - [Primitive Finance Invariant Development](https://github.com/primitivefinance/rmm-core/tree/main/contracts/crytic) – fuzzing different versions of the Primitive ecosystem during an engagement where manual review and fuzzing was conducted

### Security Reviews

#### Infrastructure and L2s 
 - [Coinbase Aggregate Verifier](https://cantina.xyz/portfolio/b72c7078-f6da-4074-a3bd-4f938f469fb7) - Follow-up review focusing on data addition and CWIA offsets
 - [Coinbase Multiproof](https://cantina.xyz/portfolio/25ba64ea-d6f3-411e-8338-419ffc385ba6) - Review of dispute game checks supporting multiple proof types
 - [Coinbase Verified Pools](https://cantina.xyz/portfolio/d3950206-883f-4308-86b7-c835afd37556) - Arithmetic focused review of a specialized liquidity pool architecture 
 - [Optimism Enclave](https://cantina.xyz/portfolio/568a4994-b8c9-4b29-9014-d0627c5ce124) - Security review of the Op Enclave system 
 - [Scroll L2 Geth Diff Review](https://github.com/trailofbits/publications/blob/master/reviews/2023-08-scrollL2geth-securityreview.pdf) - A depp dive diff review on a fork of `go-ethereum`

#### DeFi and Yield 
 - [Drips Token Streaming](https://cantina.xyz/portfolio/47ff4361-233a-42c4-bb83-6a0beab255c8) - Review of fund-splitting logic for open-source grants
 - [Defi Wonderland](https://cantina.xyz/portfolio/5295cf96-7a54-4150-9d94-396944b3604e) - Bridged USDC standard for the OP stack, focusing on L2-specific risks
 - [Tradeable On Chain V2](https://cantina.xyz/portfolio/427d48c3-3f54-4891-a710-0784ffaded87) - Protocol allowing lending asset managers to tokenize their strategies for institutional assets
 - [Bera Bex](https://cantina.xyz/portfolio/2928a086-0004-4ab4-be62-81f7c6b5d286) - Review of Berachain's DEX, a Balancer Fork
 - [EasyCrypto](https://github.com/trailofbits/publications/blob/master/reviews/2023-08-easycrypto-securityreview.pdf) - An implementation of a USDC-like stablecoin with controlled minting, burning, and pausing operations
 - [Myso Finance](https://github.com/trailofbits/publications/blob/master/reviews/2023-04-mysoloans-securityreview.pdf) - Peer to peer and peer to pool lending protocol
 - [Atlendis Loans](https://github.com/trailofbits/publications/blob/master/reviews/2023-03-atlendis-atlendissmartcontracts-securityreview.pdf) - Review of complex lending structures (bullet, installment, and revolving credit)
 - [Primitive Portfolio, previously "Hyper"](https://github.com/trailofbits/publications/blob/master/reviews/2023-03-primitive-securityreview.pdf)- An automated market maker for custom liquidity distribution strategies
 - [Primitive RMM](https://github.com/trailofbits/publications/blob/master/reviews/Primitive.pdf) - Replicating market maker contracts
 - [Advanced Blockchain](https://github.com/trailofbits/publications/blob/master/reviews/AdvancedBlockchainQ42021.pdf) - A series of Solidity lending projects, Substrate lending, oracle, and call adapter pallets
 - [Frax](https://github.com/trailofbits/publications/blob/master/reviews/FraxFinance.pdf) - Permissionless and non-custodial stablecoin
 - [wAlgo](https://github.com/trailofbits/publications/blob/master/reviews/wALGO.pdf) - A vault implementation of a lending protocol written in Teal

#### NFT Marketplace 
 - [LooksRare](https://github.com/trailofbits/publications/blob/master/reviews/LooksRare.pdf) - An NFT marketplace with buying, selling, and order matching logic

#### Miscellaneous 
 - [Hermez](https://github.com/trailofbits/publications/blob/master/reviews/hermez.pdf) - Zero knowledge proof in circom and related Solidity implementation to support these proofs
 - [ETH2 Deposit CLI](https://github.com/trailofbits/publications/blob/master/reviews/ETH2DepositCLI.pdf) - Review of the python CLI implementation to deposit 32 ETH as a staker

## Thought Leadership and Education
I am a frequent speaker and educator, dedicated to making advanced security concepts accessible to developers and researchers alike.

**Select Presentations:**
  - [Invariant Driven Codebases](https://youtu.be/GfMzS2UVLq0?si=LyEwJo63KqzF46Xg) (2024) @ Defi Security Summit - A concise guide on creating invariant-driven codebases. This helps with not only streamlining your audits, but helps developers with writing nicer code
  - [Finding Bugs: 42 Tips from 4 Security Researchers](https://youtu.be/wMrsL5ipDFE?si=uJAZ1Ti7xPjBJEiI) (2024) @ Defi Security Summit - Advanced techniques for security researchers, focusing on complex testing, fuzzing methodologies, and how to make most of your time on a security review
  - [Professor at George Brown College](https://www.georgebrown.ca/programs/blockchain-development-program-postgraduate-t475)- Developed and delivered curriculum for smart contract development and security to classes of 45+ students


#### Technical Deep Dives
I am a co-founder of the "Fuzzing Workshop" streaming series. At its launch, this was the industry's first advanced course on DeFi invariants and remains a primary resource for security engineers.

  - [Advanced DeFi Invariants Part 1](https://www.youtube.com/watch?v=vQTexNuWDrM&t=2s) (2022) - A simplified version of a client codebase, where I walk through how to find invariants, and how to implement these invariants in this smaller example.  
  - [Advanced DeFi Invariants Part 2](https://www.youtube.com/watch?v=zsjVamRTn5M&t=1s) (2022) - Demonstrates a different style of writing invariants, and touching on the difficulty of non-determinism in fuzzing
  - [Fuzzing 101](https://github.com/trailofbits/publications/tree/master/presentations/How%20to%20Fuzz%20Like%20a%20Pro) (2022) - Comprehensive guide on implementing fuzzing in development workflows
