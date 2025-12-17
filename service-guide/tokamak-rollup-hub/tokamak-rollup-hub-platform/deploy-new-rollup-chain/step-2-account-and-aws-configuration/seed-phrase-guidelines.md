# Seed phrase guidelines

Prepare a seed phrase for the L1 account. The platform will ask you to provide a 12-word seed phrase to generate EVM accounts for deployment. If you don’t have a seed phrase, you can generate one directly from the platform. Please make sure to store it safely for future use. \
You need to fund at least the first four EVM accounts with Sepolia ETH.

These accounts will be assigned to different roles: **admin**, **sequencer**, **batcher**, and **proposer**. While you can use the same account for multiple roles, we recommend using separate accounts to avoid a single point of failure.

Each account requires a minimum ETH balance. Please fund them accordingly based on the information below.

* Admin account (minimum 0.5 ETH required) // Sometime the cost may vary, depending upon the network status
* Sequencer account (**no need of ETH balance**)
* Batcher account (0.3 ETH recommended)
* Proposer account (minimum 0.3 ETH recommended)
