<img src="https://raski-hqaaa-aaaap-qplmq-cai.icp0.io/bkm-social-card.png" />

## Fair Distribution Through Proof-of-Work.

We see proof-of-work as the fairest token distribution method. By requiring users to contribute computational power, PoW ensures everyone has a **level playing field** to earn tokens. This process also reflects a **token's true underlying value**, as it's directly tied to the effort required to acquire them.

Blockminer.fun leverages the power of **proof-of-work** to deliver the **most equitable and transparent**Bitcoin fungible token distribution available.

Through Blockminer.fun, users can participate in the PoW process and receive their preferred Bitcoin fungible tokens as block rewards. This fosters a community-driven distribution where everyone has the opportunity to be involved.

By eliminating hidden agendas and pre-allocated distributions, Blockminer.fun creates a **equitable and transparent trustworthy and transparent environment for both token creators and participants**.


## Summary

Blockminer integrates various components to support Proof-of-Work (PoW) mining and token management, utilizing the scalability and efficiency of the Internet Computer. It provides robust functionality, including:

- **Secure Access Control**: Principal-based authentication ensures controlled access to system features.
- **Optimized Mining Operations**: Batch-based PoW execution and difficulty adjustment improve mining efficiency and performance.
- **Comprehensive Reward Management**: Logging and ledger systems provide clear tracking of mining activity, rewards, and token statistics.

The architecture is designed to support scalable PoW systems with robust management of mining tasks, tokens, and user interactions.

## Architecture Components:

1. **Index Canister**:

   - Manages core functions like creating miner canisters, storing miner information, managing mining tasks, and processing rewards.
   - Holds data structures (like Maps) to keep track of miners, users, tokens, ledger, and logs.
   - Authenticates actions with a principal controller check.
   - Interacts with mining canisters and components for functionality like creating miners, handling mining tasks, generating targets and adjusting difficulty.

2. **Miner Canister**:

   - Handles proof-of-work (PoW) computations using a batch-based approach.
   - Executes mining tasks by hashing messages and validating hash results against a target.
   - Contains methods for starting and validating PoW.

3. **Utilities**:

   - Contains helper functions for generating random strings, hashing with SHA-256, and managing difficulty adjustments.
   - Provides functionality for general system utilities.

4. **Data Structures**:

   - **Maps**: Store miners, users, tokens, token stats, ledgers, and mining tasks.
   - **Stable Data Structures**: Preserve specific data across canisters and interactions.
   - **Mining Task Queue**: Stores ongoing mining tasks to handle batch processing.

5. **Principal and IC Management**:
   - Implements access control with principals to manage who can execute specific actions.
   - Uses IC management capabilities to manage canisters, deposit cycles, update settings, and handle canister lifecycle events.

## Diagram Interactions:

1. **User Interaction**: Users interact with the Index Canister for registering, managing tokens, and starting mining.
2. **Mining Task Management**: The Index Canister queues mining tasks, delegates PoW to the Miner Canister, and processes results.
3. **Difficulty Adjustment**: Based on mining performance, the system dynamically adjusts mining difficulty.
4. **Logging and Rewards**: Logs mining activity and updates rewards upon task completion.

[Architecture Diagram](https://docs.google.com/drawings/d/11XaH8V3ldf7cATQyHO9MuEW0zSnZ0Jg9Cfi_tVZD0J0/edit?usp=sharing)

## Data Flow Explanation

1. **User Interaction**:

   - **User Registration**: Users interact with the Index Canister to register their details, which are stored in stable data structures like `user` and `token`.
   - **Token and Ledger Management**: Users can register and manage tokens, which are stored in the `ledger` and `token_stats` Maps for tracking balances and transaction logs.

2. **Mining Task Initiation**:

   - When a user initiates mining, the Index Canister checks if the user is authorized and add it to the specified token mining queue. Which starts the mining process by delegating tasks to the Miner Canister.

3. **Proof-of-Work (PoW) Execution**:

   - The Miner Canister receives the mining task with parameters like `message`, `target`, `leading_zero_bits`, and `batch_size`. It executes the PoW by hashing messages and checking if the hash meets the difficulty target.
   - If a valid hash (nonce) is found, the Miner Canister returns the result to the Index Canister.

4. **Mining Task Queue Processing**:

   - The Index Canister collects mining results in a queue. When the queue reaches a set batch size, it processes and clears it.
   - Mining results are stored in the `block_reward_log` Map, logging details like `token_reward` and `miner_id` for tracking rewards.

5. **Difficulty Adjustment**:

   - Based on the mining task completion time, the system adjusts the difficulty target by tightening or loosening it for future mining tasks. This adjustment is done in the Miner Canister based on time performance metrics.

6. **Logging and Rewards**:
   - The Index Canister logs completed mining tasks and rewards users based on mining results. Rewards are updated in `ledger` and `token_stats` to track block rewards and mining performance.

[Data Flow Diagram](https://docs.google.com/drawings/d/1L680Q1gp_lJZK2xB4RPDVknhKmBHsL2-e1hbuVm3xXc/edit?usp=sharing)
