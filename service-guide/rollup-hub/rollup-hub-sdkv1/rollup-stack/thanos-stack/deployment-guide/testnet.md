---
description: Testnet Deployment Instructions
---

# Testnet

{% hint style="info" %}
**Important Links:**

1. Operation guid&#x65;**:** [https://docs.tokamak.network/home/service-guide/rollup-hub/rollup-hub-sdkv1/rollup-stack/thanos-stack/operation-guide/testnet](https://docs.tokamak.network/home/service-guide/rollup-hub/rollup-hub-sdkv1/rollup-stack/thanos-stack/operation-guide/testnet)
2. Quicknode : [https://www.quicknode.com/](https://www.quicknode.com/)
3. Alchemy : [https://www.alchemy.com/](https://www.alchemy.com/)
4. Chainlist : [https://chainlist.org/?testnets=true](https://chainlist.org/?testnets=true)
5. AWS IAM User : [https://repost.aws/knowledge-center/create-access-key](https://repost.aws/knowledge-center/create-access-key)&#x20;
6. Sepolia Gas Tracker : [https://eth-sepolia.blockscout.com/gas-tracker](https://eth-sepolia.blockscout.com/gas-tracker)
{% endhint %}

**Testnet deployment** allows you to launch a Thanos-based appchain using Ethereum Sepolia as the settlement layer and TON as the native gas token. The process consists of three key steps:

1. **Prerequisites** – Prepare prerequisites for testnet deployment
2. **L1 Contract Deployment** – Deploy and configure smart contracts on the L1 network.
3. **Infrastructure Deployment** (**AWS**) – Set up and configure the network infrastructure.

Each step must be completed successfully before proceeding to the next to ensure a smooth deployment.

## Prerequisites

1. Make a note of your L1 RPC URL, as you will need it when using the SDK for deployment. (You can get it from [QuickNode](https://www.quicknode.com/), [Alchemy](https://www.alchemy.com/), [ChainList](https://chainlist.org/?testnets=true) etc.) If you want to use L1 endpoint as a free plan, we recommend to use Alchemy. They provide API credits and RPS suitable for testing purpose.
   * Example : [https://boldest-newest-patron.ethereum-sepolia.quiknode.pro/4ed7d53b815c434c082db3eb2f49612c914afe71/](https://boldest-newest-patron.ethereum-sepolia.quiknode.pro/4ed7d53b815c434c082db3eb2f49612c914afe71/) from QuickNode
2.  Beacon URL (Get your endpoint from [QuickNode](https://www.quicknode.com/) by logging in, selecting Ethereum Sepolia, and opting for a free plan.)

    * Example: [https://boldest-newest-patron.ethereum-sepolia.quiknode.pro/4ed7d53b815c434c082db3eb2f49612c914afe71/](https://boldest-newest-patron.ethereum-sepolia.quiknode.pro/4ed7d53b815c434c082db3eb2f49612c914afe71/)

    > Note: While you can use a single QuickNode URL for both L1 RPC and the Beacon URL, it’s not recommended due to potential rate limiting issues. It’s better to use separate URLs for each. **ℹ️ We recommend you to use Alchemy for L1 RPC and QuickNode for beacon url.**
3.  Prepare AWS credentials & configuration to access AWS EKS.

    * Follow steps 1 to 9 in this [guide](https://docs.tokamak.network/home/service-guide/rollup-hub/mainnet-beta/deploy-with-aws/prerequisites#id-4.-set-up-aws-account) to set up an IAM user with the required privileges and create an access key which will be later used with SDK.
    * [What is IAM?](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) (\*_Note: This IAM user has to have the following policies_)
      * `arn:aws:iam::aws:policy/aws-service-role/AmazonEKSServiceRolePolicy`
    * [How to create aws access key and secret key for a IAM user](https://repost.aws/knowledge-center/create-access-key).

    > ⚠️ The deployment of testnet/mainnet to AWS is not available on AWS free tier.&#x20;
4.  Prepare a seed phrase for the L1 account.

    The SDK will prompt you to provide a 12-word seed phrase to generate EVM accounts for deployment. Prepare a 12-word seed phrase and fund at least the first four EVM accounts with Sepolia ETH.

    These accounts will be assigned to different roles: **admin**, **sequencer**, **batcher**, and **proposer**. While you can use the same account for multiple roles, we recommend using separate accounts to avoid a single point of failure.

    Each account requires a minimum ETH balance. Please fund them accordingly based on the information below.

    * Admin account (minimum `${estimated_cost}` ETH required)&#x20;
      * It depends on the L1 network status and automatically estimated before the deployment.
    * Sequencer account (**no need of ETH balance**)
    * Batcher account (minimum 0.3 ETH recommended)
    * Proposer account (minimum 0.3 ETH recommended)

    **Make sure you meet the above prerequisites before proceeding to the next step.**

## Deploy L1 contracts (15mins \~ 35mins)

> ⚠️ **Gas Price Recommendation for Deployment Testing (**[**Gas tracker on Sepolia**](https://eth-sepolia.blockscout.com/gas-tracker)**)**
>
> * Maximum gas price for testing: **20 Gwei** (Estimated maximum deployment cost is 1.6 ETH)
> * Action Required if Gas Price Exceeds 20 Gwei: Pause deployment testing until gas prices return to acceptable levels.
>
> This recommendation aims to prevent excessive expenditure during testing phases due to volatile gas prices. By setting a gas price cap at 20 Gwei, we can maintain predictable and manageable deployment costs.

After completing the prerequisites, the next step is to deploy the L1 contracts to the target network. This process generates the rollup, genesis, and deployment files.

Upon successful deployment, the SDK will also create `settings.json` and `rollup.json`, which are essential for future infrastructure deployments, allowing you to redeploy the infrastructure anytime without issues.

1. **Create a new root directory for the testnet deployment and run all commands inside it.**

```bash
mkdir trh-testnet
cd trh-testnet
```

2. Run the following command inside the project directory: `trh-sdk deploy-contracts --network ${network} --stack ${stack}`

```bash
trh-sdk deploy-contracts --network testnet --stack thanos
```

3. During contract deployment, you will be prompted with the following questions, which you should answer based on your prerequisite setup.

```bash
# Get the L1 RPC URL, seed phrase, whether to use advanced configuration
Please enter your L1 RPC URL: // Your L1 RPC URL e.g. https://sepolia.rpc.tokamak.network
Please enter your admin seed phrase: // Your admin seed phrase that you prepared as a prerequisite.
Would you like to perform advanced configurations? (Y/n): (Refer to the SDK Guide for more details: https://www.notion.so/tokamak/Testnet-Deployment-Guide-1e0d96a400a3806db1c3ec0cdbc4eeea#1f7d96a400a38031a747c8aec9a8f0b8) 

# The input example advanced configurations
L2 Block Time (default: 2 seconds): 4
Batch Submission Frequency (Default: 120 L1 blocks ≈ 1440 seconds, must be a multiple of 12): 1200
Output Root Frequency (Default: 120 L2 blocks ≈ 480 seconds, must be a multiple of 4): 480
Challenge Period (Default: 12 seconds): 20

# Select accounts for operating L2
Retrieving accounts...
Select an admin account from the following list (minimum ${estmated_cost} ETH required): // The account number that you want to deploy the contracts.
...
Select an sequencer account from the following list: // The account number that you want to deploy the contracts.
...
Select an batcher account from the following list (0.3 ETH recommended): // The account number that you want to deploy the contracts.
...
Select an proposer account from the following list (0.3 ETH recommended): // The account number that you want to deploy the contracts.

------------------------------
// Dependency install/checkup steps
------------------------------
✅ Build the contracts completed!

# Final check the admin balance (example)       
Admin account balance: 16.39 ETH
⛽ Current gas price: 0.0014 Gwei
💰 Estimated deployment cost: 0.0002 ETH
✅ The admin account has sufficient balance to proceed with deployment.

------------------------------
// Contracts Deployment steps
------------------------------
```

#### Advanced configurations

At this step, you will be asked the following question.

```jsx
Would you like to perform advanced configurations? (Refer to the SDK Guide for more details) (Y/n):
```

This step is to let the users set the advanced chain config parameters:

* L2 Block Time (default: 2 seconds): The time it takes to produce a new block on the L2 chain.
* Batch Submission Frequency (Default: 120 L1 blocks ≈ 1440 seconds, must be a multiple of 12): The frequency of L2 block batch submission to the L1 chain.
* Output Root Frequency (Default: 120 L2 blocks ≈ 240 seconds, must be a multiple of 2): The frequency of L2 output root submission to the L1 chain.
* Challenge Period (Default: 12 seconds): The time window during which participants can contest or submit fraud proofs against a posted Layer 2 transaction before it becomes final.

{% hint style="danger" %}
**Note:** The advanced chain config parameters set above can affect deposits and withdrawals. For example, if you use the default value, you can expect a withdrawal delay of `Max(1440, 240) + 12 seconds`, but please note that unexpected delays may occur depending on the L1 network.
{% endhint %}

4. Contract deployment usually takes around 15–30 minutes. After completion, the SDK will display a success message.

```jsx
Generating the rollup and genesis files...
✅ Successfully generated rollup and genesis files!       
 Genesis file path: /home/ubuntu/trh-testnet/tokamak-thanos/build/genesis.json
 Rollup file path: /home/ubuntu/trh-testnet/tokamak-thanos/build/rollup.json
✅ Configuration successfully saved to: /home/ubuntu/trh-testnet/settings.json 
```

#### Resume the contract deployment

If the contract deployment is terminated midway due to an error or other reason, you can resume the deployment. Check that the `deploy_contract_state` field in `settings.json` has a value of 1. (When the deployment is complete, the value will change to 2.)

```json
  # In progress
  "deploy_contract_state": {
    "status": 1
  }
  
  # Done
    "deploy_contract_state": {
    "status": 2
  }
```

If you put the deployment command again, you will see the screen below instead of the L1 RPC URL input screen. If you press "Y", contract deployment will resume from the previous state.

```bash
trh-sdk deploy-contracts --network testnet --stack thanos
The contracts deployment is in progress. Do you want to resume? (Y/n):
```

***

## Deploy Thanos stack (20mins \~ 40mins)

After successfully deploying the contracts, the next step is to set up the infrastructure on AWS to run the L2 chain. Follow the steps below to complete the process.

{% hint style="warning" %}
Note : The Thanos bridge will be deployed along with the stack deployment.
{% endhint %}

1. Run the following command in the same root directory you used for the L1 contract deployment.

```bash
trh-sdk deploy
```

{% hint style="info" %}
&#x20;If the `settings.json` file exists, SDK will deploy the stack by the network and stack written on the config file. And if the `settings.json` file doesn't exist, SDK will deploy the `devnet` network and the stack is `Thanos` by default.
{% endhint %}

2. Upon executing the deploy command, you will receive the following prompts from the SDK. You should be able to answer them easily using the information from your prerequisite preparation.

{% hint style="info" %}
Hint: Use unique identifiers in **chain name** since redeployment with same name is impossible.
{% endhint %}

```bash
Please select your infrastructure provider [AWS] (default: AWS):  // You can put just enter for AWS deployment
-----------------------
// dependency checkup steps
-----------------------
Please enter your AWS access key: // You can put the aws access key that you prepared as a prerequisite
Please enter your AWS access secret key: // You can put the aws secret access key that you prepared as a prerequisite
Please enter your AWS region(default: ap-northeast-2): // You can put the aws region where you want to deploy.
Please enter your chain name: // L2 chain name. e.g. victorsepolia, Please use name without the special characters 
Please enter your L1 beacon URL: // You can put the beacon url that you prepared as a prerequisite
```

3. You can check the result of L2 deployment.

```jsx
✅ Network deployment completed successfully!
🌐 RPC endpoint: http://k8s-opgeth-d3849915e5-749317361.ap-northeast-2.elb.amazonaws.com
Configuration saved successfully to: /home/ubuntu/trh-testnet/settings.json 
--------------------------
Bridge component installation steps...
--------------------------
✅ Bridge component is up and running. You can access it at: http://k8s-bridge-04ae2b39cf-186375366.ap-northeast-2.elb.amazonaws.com
🎉 Thanos Stack installation completed successfully!
🚀 Your network is now up and running.
🔧 You can start interacting with your deployed infrastructure.
```

{% hint style="danger" %}
If the stack and bridge components are deployed successfully, you will receive the URLs for the L1 RPC and the bridge web app. However, please wait 3–4 minutes before using the bridge, as it takes time for the Kubernetes pods to initialize.
{% endhint %}

The L2 endpoint can be checked by the `l2_rpc_url` field value in `settings.json`or by using the `trh-sdk info` command.

4.  Double check if the chain is deployed and running properly following this [guide](https://www.notion.so/Double-check-the-status-of-the-L2-chain-1f2d96a400a38068a101e720d5f8be36?pvs=21).

    > ℹ️ After you deploy the L2 testnet successfully, you can operate it by following this guide [testnet.md](../operation-guide/testnet.md "mention")
5. With the stack and bridge configured, proceed to the Integrations section to add any desired components to your chain.

## Destroy the stack

{% hint style="warning" %}
_Please don’t forget to destroy the stack if you think it is not needed anymore to prevent the waste of resource/money._
{% endhint %}

1. To terminate network and destroy the AWS infra, you can run the following command in the project root directory:

```bash
trh-sdk destroy
```

Like the `deploy` command, this command uses the configuration files in the current directory to identify the network and stack to be destroyed.

2. Success prompt:

```bash
✅The chain has been destroyed successfully!
```

