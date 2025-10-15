# RWA Defi smart contract - Solidity

### Introduction
Real-World-Asset (RWA) DeFi Protocol for Real-Estate Auctions and Mortgage Lending.  

Core Functions:
- Allows lenders worldwide to earn yields, by supplying and lending their mortgage capital to the residents of a city/jurisdiction.
- Brings mortgage access to residents of a city/juridiction (such as Prospera) who are blo

### Contact
If you have any question or need help, contact here: [Telegram](https://t.me/shiny0103) | [Twitter](https://x.com/0xTan1319)

### Features
- NFTs: Legally Compliant NFTs, capable of representing RWA (property disputes can also be solved on-chain via arbitrator multisig)
- Lending Pool: Allows anyone to supply capital to the protocol and earn yeilds from mortgages. Includes tUSDC an SEC Compliant interest-bearing token (unavailable to US Citizens)
- On-Chain Mortgages: Gas-Efficient Amortization Schedule
- Auctions: Bidding mechanism to allow seamless real estate transactions. A user with an active mortgage can accept a bid, sell his house, pay off any mortgage debt, and keep the difference (all in one transaction).
- etc

### Architecture
- **protocol**
    - **state**
        - State.sol (holds all protocol state vars. the proxy and all logic contracts inherit from it, to avoid storage collisions)
        - TargetManager.sol (handles upgrade and delegatecall logic)
        - Roles.sol
    - **proxy**
        - ProtocolProxy.sol:  (the proxy responsible for mapping each function selector to the appropriate implementation)
    - **logic** (all non-abstract implementations inherit from State.sol)
        - Auctions.sol
        - Borrowing.sol
        - Info.sol (originally made to contain all external getters, and reduce size of other implementations. might get rid of it. under review)
        - Initializer.sol
        - Lending.sol
        - Residents.sol (Tracks who are the legitimate residents of the jurisdiction, which are the only eligible receivers of the NFT)
        - Setter.sol (originally made to contain all external setters, and reduce size of other implementations. might get rid of it. under review)
        - **interest**
            - InterestConstant.sol: Implementation of a Fixed/Constant Interest Rate Model
            - Interest2Slopes.sol: Implementation of an [Two-Slope Interest Rate Model](https://www.desmos.com/calculator/ryesiw7hau)
            - InterestCurve.sol: Implementation of a [Smooth Curve Interest Rate Model](https://www.desmos.com/calculator/nimb8tbzgb)
        - **loanStatus**
            - Amortization.sol (holds implementation of a flexible & gas-efficient amortization schedule)
            - LoanStatus.sol (inherits from Amortization.sol, to differentiate Active Mortgages from Defaults, and so on)
