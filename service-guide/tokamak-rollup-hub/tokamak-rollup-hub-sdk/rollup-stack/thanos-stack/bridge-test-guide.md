---
description: Step-by-step guide for testing L1<->L2 bridge deposits and withdrawals on a Thanos Stack appchain.
---

# Bridge Test Guide

{% hint style="warning" %}
Before following this guide, make sure the network you want to test is running correctly.
{% endhint %}

## 1. Build Packages

```bash
cd tokamak-thanos/packages/tokamak/contracts-bedrock

./scripts/start-deploy.sh build
```

## 2. Set Environment Variables and Fund Assets

TON is used as the L2 native token in devnet. Before running bridge tests, configure the required environment variables. Contract addresses are available in `.devnet/addresses.json`, which is generated after L1 contract deployment.

```bash
# Change directory
cd packages/tokamak/sdk

# Open the example env file
vi tasks/example.env

# Edit and save the following variables
export PRIVATE_KEY=${your_private_key}
export NATIVE_TOKEN=${address_L2NativeToken}
export ADDRESS_MANAGER=${address_AddressManager}
export L1_CROSS_DOMAIN_MESSENGER=${address_L1CrossDomainMessengerProxy}
export L1_STANDARD_BRIDGE=${address_L1StandardBridgeProxy}
export OPTIMISM_PORTAL=${address_OptimismPortalProxy}
export L2_OUTPUT_ORACLE=${address_L2OutputOracleProxy}
export L1_URL=${url_l1}
export L2_URL=${url_l2}

# Copy to the SDK .env file
cp tasks/example.env .env
```

Next, fund ETH and TON on L1.

### Fund ETH in L1 (Devnet only)

{% hint style="info" %}
On Sepolia, use a public faucet such as [Infura](https://docs.metamask.io/developer-tools/faucet/), [Quicknode](https://faucet.quicknode.com/ethereum/sepolia), or [Alchemy](https://www.alchemy.com/faucets/ethereum-sepolia).
{% endhint %}

```bash
# Change directory
cd packages/tokamak/contracts-bedrock

# Fund ETH to your address
cast send --from 0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266 \
  --rpc-url http://localhost:8545 \
  --unlocked \
  --value ${amount} ether \
  ${your_address}
```

Example output (funding 10 ETH):

```bash
cast send --from 0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266 --rpc-url http://localhost:8545 --unlocked --value 10ether 0x90358f827D81D988355D709A06CeE594a4E38BA6

blockHash               0x06a9c98e91b4970465768d27fb82055fc5a1065533758daec4b92e9ce1450a04
blockNumber             244
contractAddress         
cumulativeGasUsed       21000
effectiveGasPrice       1000000007
from                    0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266
gasUsed                 21000
logs                    []
logsBloom               0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
root                    
status                  1 (success)
transactionHash         0x024156b4501db26f913f39b3a46a38251b04db4c612528477109bb0955f3ee7d
transactionIndex        0
type                    2
to                      0x961b6fb7D210298B88d7E4491E907cf09c9cD61d
```

### Fund TON in L1 (Devnet only)

{% hint style="info" %}
On Sepolia, refer to the [TON faucet guide](https://docs.tokamak.network/home/service-guide/faucet-testnet).
{% endhint %}

```bash
# Change directory
cd packages/tokamak/sdk

# Fund TON
npx hardhat fund-native-token --amount ${amount}
```

Example output (funding 200,000,000 TON):

```bash
npx hardhat fund-native-token --amount 200000000000000000000000000

Faucet amount: 200000000000000000000000000
Native token address: 0xC7844340d14deAedfDD2f2dD9360c336661b2F0A
Native token balance in L1 before funding: 0
Faucet transaction hash:  0x1332e290ce1ebd00399c6f489da8329759787385312810ec99faad259b0b468a
Native token balance in L1 after funding: 200000000000000000000000000
```

## 3. Deposit & Withdraw

Test bridge operations using the [Thanos SDK](https://github.com/tokamak-network/tokamak-thanos/tree/codeReview/packages/tokamak/sdk). The following asset types are supported:

- L2 native token (TON)
- ETH
- ERC-20 tokens (other than TON)

### L2 Native Token (TON)

Test script: [`deposit-withdraw-native-token.ts`](https://github.com/tokamak-network/tokamak-thanos/blob/codeReview/packages/tokamak/sdk/tasks/deposit-withdraw-native-token.ts)

#### Deposit

```bash
npx hardhat deposit-native-token --amount ${amount}
```

Example output (depositing 2 TON):

```bash
npx hardhat deposit-native-token --amount 2000000000000000000

Setup task...
Deposit Native token: 2000000000000000000
Native token address: 0xC7844340d14deAedfDD2f2dD9360c336661b2F0A
L1 contracts: {
  StateCommitmentChain: '0x0000000000000000000000000000000000000000',
  CanonicalTransactionChain: '0x0000000000000000000000000000000000000000',
  BondManager: '0x0000000000000000000000000000000000000000',
  AddressManager: '0xA8452Ec99ce0C64f20701dB7dD3abDb607c00496',
  L1CrossDomainMessenger: '0x416C42991d05b31E9A6dC209e91AD22b79D87Ae6',
  L1StandardBridge: '0x4f559F30f5eB88D635FDe1548C4267DB8FaB0351',
  OptimismPortal: '0x62c20Aa1e0272312BC100b4e23B4DC1Ed96dD7D1',
  L2OutputOracle: '0xDEb1E9a6Be7Baf84208BB6E10aC9F9bbE1D70809'
}
L2 native token balance in L1 before depositing: 200000000000000000000000000
Balance in L2 before depositing:  0
Approve tx: 0xa646746b9ae1916432f5cc99ecf8afe3f0622e3e61758ef1dc11e5907f3e0b36
Deposit native token from L1 to L2, tx_hash: 0x179e3194319caf6d90f827d15856c13ea038042eda451e02e4e7dae2a6453abd amount: 2000000000000000000
Verify balances
L2 native token balance in L1 after depositing: 199999998000000000000000000
Balance in L2 after depositing:  2000000000000000000
```

#### Withdraw

```bash
npx hardhat withdraw-native-token --amount ${amount}
```

Example output (withdrawing 0.02 TON):

```bash
npx hardhat withdraw-native-token --amount 20000000000000000

Setup task...
Withdraw Native token: 20000000000000000
L2 native token: balance in L1:  199999998000000200000000000
L2 native token: balance on L2:  1999762858499808999
L2 native token: balance after depositing 1979577198999651878
L1 cost actual: 33348
L2 cost actual: 185659500123773
Total cost: 185659500157121
Withdrawal amount 20000000000000000
Spent amount = L1 cost actual + L2 cost actual + Withdrawal Amount = 20185659500157121
Balance changed  20185659500157121
Prove the message
Proved the message:  0x8e09aa35750eb61c864378d82a9b5165de3c596da4147fc547aa3abc81ca0f3f
L2 native token: balance in L1 after proving:  199999998000000200000000000
Finalized message tx 0x134209acbf130d709da72254d54a75bffc8c8df41ee4aae66c2ecd3c55476c38
Finalized withdrawal
L2 native token: balance in L1 after finalizing:  199999998020000200000000000
```

### ETH

Test script: [`deposit-withdraw-eth.ts`](https://github.com/tokamak-network/tokamak-thanos/blob/codeReview/packages/tokamak/sdk/tasks/deposit-withdraw-eth.ts)

#### Deposit

```bash
npx hardhat deposit-eth --amount ${amount}
```

Example output (depositing 0.5 ETH):

```bash
npx hardhat deposit-eth --amount 500000000000000000

Setup task...
Deposit ETH: 5000000000000000000
l1 address: 0x961b6fb7D210298B88d7E4491E907cf09c9cD61d
l2 address: 0x961b6fb7D210298B88d7E4491E907cf09c9cD61d
l1 contracts: {
  StateCommitmentChain: '0x0000000000000000000000000000000000000000',
  CanonicalTransactionChain: '0x0000000000000000000000000000000000000000',
  BondManager: '0x0000000000000000000000000000000000000000',
  AddressManager: '0xA8452Ec99ce0C64f20701dB7dD3abDb607c00496',
  L1CrossDomainMessenger: '0x416C42991d05b31E9A6dC209e91AD22b79D87Ae6',
  L1StandardBridge: '0x4f559F30f5eB88D635FDe1548C4267DB8FaB0351',
  OptimismPortal: '0x62c20Aa1e0272312BC100b4e23B4DC1Ed96dD7D1',
  L2OutputOracle: '0xDEb1E9a6Be7Baf84208BB6E10aC9F9bbE1D70809'
}
l1 eth balance:  9997421129487965271
l2 eth balance: 0
depositTx: 0x77d902dd954bc578a9bd53deb02f187384642ff33cda211e7e79f427b57d0be9
relayed tx: 0x0c09e0defa267cc01c0697bff481661a05121bab9c40a065a8c1a09ce03d4c83
l1 eth balance:  4996516044483741541
l2 eth balance: 5000000000000000000
```

#### Withdraw

```bash
npx hardhat withdraw-eth --amount ${amount}
```

Example output (withdrawing 0.005 ETH):

```bash
npx hardhat withdraw-eth --amount 5000000000000000

Setup task...
Withdraw ETH: 500000000000000000
l1 address: 0x961b6fb7D210298B88d7E4491E907cf09c9cD61d
l2 address: 0x961b6fb7D210298B88d7E4491E907cf09c9cD61d
l1 eth balance:  4996516044483741541
l2 eth balance:  5000000000000000000
 Withdrawal Tx: 0xb8076ea5662461d0bc31d4d4673f1906b9549392db6b06b0e2b01f6e712f530c  Block 1019  hash 0xb8076ea5662461d0bc31d4d4673f1906b9549392db6b06b0e2b01f6e712f530c
l2 eth balance:  4500000000000000000
Prove the message
Proved the message: 0xe4d4b9c2e7de2939e89c7e2aa6d4328ae365f86849b0d14316065a71e23c8690
l1 eth balance: 4996250808482503773
Finalized message tx 0x181f979c30d1f5e49c9cb060b98b5eb8751f957034ddb6a78c1a557cf344a7e0
l1 eth balance: 5495920203980960952
```

### ERC-20 Token (not L2 native token)

The ERC-20 test script deploys 1 WTON on L1 and deposits it to L2. Test script: [`deposit-withdraw-erc20.ts`](https://github.com/tokamak-network/tokamak-thanos/blob/codeReview/packages/tokamak/sdk/tasks/deposit-withdraw-erc20.ts)

#### Deposit

```bash
npx hardhat deposit-erc20
```

Example output:

```bash
npx hardhat deposit-erc20

Deploying WTON to L1
Sending deployment transaction
WTON deployed: 0xae2d920cf5c7b90019ca7a6ad4b19b1b3ff5f5384364ea37fc935bffeda5603d
Deployed to 0xe7f738F1943aE1E7deB37aE9A02F290B733D0482
Creating L2 WTON
Deployed to 0x42ba0E5c3Ad84A5bFf312716C9ea194F883f2983
Approving WTON for deposit
WTON approved
Balance WTON before depositing...
l1 WTON balance:  1000000000000000000
l2 WTON balance: 0
Depositing WTON to L2
ERC20 deposited - 0x27b254b6cac4fe42d3a12d3c3905860d87f324ec8cd2c78d5b7c90850abf972f
relayed tx: 0xc4c7cd64e4ade5163bec3c7e23a326a461ec53fee4a178272f815ea0ea1cae59
Balance WTON after depositing...
l1 WTON balance:  0
l2 WTON balance: 1000000000000000000
Deposit success
```

#### Withdraw

```bash
npx hardhat withdraw-erc20
```

Example output:

```bash
npx hardhat withdraw-erc20

Setup task...
Starting withdrawal
Balance WTON before withdrawing...
l1 WTON balance:  0
l2 WTON balance: 1000000000000000000
 Withdrawal Tx: 0x47d375961611312f6829e5454ac9fa061456409eac39fd226d8ae97a5f64c8bf  Block 1259  hash 0x47d375961611312f6829e5454ac9fa061456409eac39fd226d8ae97a5f64c8bf
Prove the message
Proved the message: 0x5c5e2780a8ffc2c54f534e82a90c228161edd6da6b9387b1d0dc139649a66171
Balance WTON before finalizing...
l1 WTON balance:  0
l2 WTON balance: 0
Finalized message tx 0x81740d7fa7708d9ff6f9c6d6403e5baccc2cd94761175378ad3eee932f2d9a1a
Balance WTON after withdrawing...
l1 WTON balance:  1000000000000000000
l2 WTON balance: 0
Withdrawal success
```
