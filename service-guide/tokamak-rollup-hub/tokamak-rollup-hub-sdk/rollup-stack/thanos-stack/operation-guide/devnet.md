---
description: Devnet Operation Guide
---

# Devnet

After successfully deploying Devnet, it is important to maintain a stable operating environment and continuously monitor that each component is operating correctly. This requires familiarity with key operating procedures such as checking container status, checking logs, analyzing port mapping information, and verifying network interoperability by actually testing bridge operations between L1 and L2. This guide provides practical procedures and useful reference links for these operations and tests.

### 1. Deployment Information

You can access essential deployment information from the following paths discussed below. This information is important for client integration, monitoring, and further development.

{% hint style="warning" %}
Please note that the deploy configuration and L1 deployed contract addresses will be deleted when the devnet is stopped using the destroy command using SDK.
{% endhint %}

#### a.  Deploy Configuration

Contains core L2 chain configuration parameters.

* Path: `tokamak-thanos/packages/tokamak/contracts-bedrock/deploy-config/devnetL1.json`
* Source

```json
{
  "l2ChainId": "901",
  "l2BlockTime": 2,
  "maxSequencerDrift": 600,
  "sequencerWindowSize": 3600,
  "channelTimeout": 300,
  "p2pSequencerAddress": "0x...",
  "batchInboxAddress": "0x...",
  "batchSenderAddress": "0x..."
}
```

* Usage:
  * Chain ID: Network configuration for wallets
  * Block Time: Transaction confirmation time estimation
  * Sequencer Address: Sequencer monitoring and performance tracking

#### b. L1 Deployed Contract Addresses

Contains addresses of core contracts deployed on L1. For detailed explanations of each contract, please refer to [here](https://github.com/tokamak-network/tokamak-thanos/tree/main/packages/tokamak/contracts-bedrock#contracts-deployed-to-l1).

* Path: `tokamak-thanos/packages/tokamak/contracts-bedrock/deployments/devnetL1/.deploy`
* Source (example)

```json
{
  "AddressManager": "0xe4EB561155AFCe723bB1fF8606Fbfe9b28d5d38D",
  "AnchorStateRegistry": "0xfc41080c08b25B636a54CBa1969ed3f6f3316F89",
  "AnchorStateRegistryProxy": "0x2AFf8EDE48F3b7Bc5002869124248d6BD12F66aC",
  "DelayedWETH": "0x07F69b19532476c6Cd03056D6BC3F1b110Ab7538",
  "DelayedWETHProxy": "0xd801426328C609fCDe6E3B7a5623C27e8F607832",
  "DisputeGameFactory": "0x20B168142354Cee65a32f6D8cf3033E592299765",
  "DisputeGameFactoryProxy": "0x11c81c1A7979cdd309096D1ea53F887EA9f8D14d",
  "L1CrossDomainMessenger": "0xe3Bee1A468F63462840b3c2886d9eE863F958007",
  "L1CrossDomainMessengerProxy": "0x4d8eC2972eb0bC4210c64E651638D4a00ad3B400",
  "L1ERC721Bridge": "0x44637A4292E0CD2B17A55d5F6B2F05AFcAcD0586",
  "L1ERC721BridgeProxy": "0xfcF38f326CA709b0B04B2215Dbc969fC622775F7",
  "L1StandardBridge": "0xDABDFDda461222a3949e8d1641a446CD8b91A2df",
  "L1StandardBridgeProxy": "0x072B5bdBFC5e66B55317Ef4B4d1AE7d61592ebB2",
  "L1UsdcBridge": "0x2A542df89b944FF40bBE839d617cDfD83a831c90",
...
}
```

#### c.  L2 Predeploy Contract Addresses

Contains fixed addresses of system contracts pre-deployed on L2. For detailed explanations of each contract, please refer to [here](https://github.com/tokamak-network/tokamak-thanos/tree/main/packages/tokamak/contracts-bedrock#contracts-deployed-to-l2).

* Path: `tokamak-thanos/packages/tokamak/contracts-bedrock/src/libraries/Predeploys.sol`
* Source

```solidity
library Predeploys {
    address internal constant L2_TO_L1_MESSAGE_PASSER = 0x4200000000000000000000000000000000000016;
    address internal constant L2_CROSS_DOMAIN_MESSENGER = 0x4200000000000000000000000000000000000007;
    address internal constant L2_STANDARD_BRIDGE = 0x4200000000000000000000000000000000000010;
    address internal constant SEQUENCER_FEE_VAULT = 0x4200000000000000000000000000000000000011;
    address internal constant OPTIMISM_MINTABLE_ERC20_FACTORY = 0x4200000000000000000000000000000000000012;
...
}
```

### 2. Devnet Container Overview

The Devnet environment comprises several Docker containers, each serving a specific role:

| Container Name            | Description                               | Endpoint                                       |
| ------------------------- | ----------------------------------------- | ---------------------------------------------- |
| ops-bedrock-l1-1          | Layer 1 (L1)                              | [http://localhost:8545](http://localhost:8545) |
| ops-bedrock-l2-1          | Layer 2 (L2                               | [http://localhost:9545](http://localhost:9545) |
| ops-bedrock-op-node-1     | Consensus node between L1 and L2          | N/A                                            |
| ops-bedrock-op-proposer-1 | Proposes L2 state root to L1              | N/A                                            |
| ops-bedrock-op-batcher-1  | Batches L2 transactions for L1 submission | N/A                                            |

{% hint style="info" %}
Note: The container configurations are defined in the [docker-compose.yml](https://github.com/tokamak-network/tokamak-thanos/blob/main/ops-bedrock/docker-compose.yml) file.
{% endhint %}



### 3. Docker Commands for Devnet Management

* List running containers:

```bash
docker ps

# Result (example)
CONTAINER ID   IMAGE                                      COMMAND                  CREATED         STATUS         PORTS                                                                                                    NAMES
d3346c06e094   tokamaknetwork/thanos-op-proposer:latest   "/bin/sh -c 'while !…"   3 minutes ago   Up 3 minutes   0.0.0.0:6062->6060/tcp, 0.0.0.0:7302->7300/tcp, 0.0.0.0:6546->8545/tcp                                   ops-bedrock-op-proposer-1
d9c91d1507cf   tokamaknetwork/thanos-op-batcher:latest    "/bin/sh -c 'while !…"   3 minutes ago   Up 3 minutes   0.0.0.0:6061->6060/tcp, 0.0.0.0:7301->7300/tcp, 0.0.0.0:6545->8545/tcp                                   ops-bedrock-op-batcher-1
bef4d03a5270   nginx:1.25-alpine                          "/docker-entrypoint.…"   3 minutes ago   Up 3 minutes   0.0.0.0:8080->80/tcp                                                                                     ops-bedrock-artifact-server-1
a4267094c5d2   tokamaknetwork/thanos-op-node:latest       "/bin/sh -c 'while !…"   3 minutes ago   Up 3 minutes   0.0.0.0:6060->6060/tcp, 0.0.0.0:7300->7300/tcp, 0.0.0.0:9003->9003/tcp, 0.0.0.0:7545->8545/tcp           ops-bedrock-op-node-1
383ea5253f08   ops-bedrock-l2                             "/bin/sh /entrypoint…"   3 minutes ago   Up 3 minutes   8546/tcp, 30303/tcp, 0.0.0.0:8551->8551/tcp, 30303/udp, 0.0.0.0:8060->6060/tcp, 0.0.0.0:9545->8545/tcp   ops-bedrock-l2-1
b6418eea69c5   ops-bedrock-l1                             "/bin/bash /entrypoi…"   3 minutes ago   Up 3 minutes   0.0.0.0:8545-8546->8545-8546/tcp, 0.0.0.0:9999->9999/tcp, 30303/tcp, 30303/udp, 0.0.0.0:7060->6060/tcp   ops-bedrock-l1-1
```

* Check container logs: Check the logs of the currently running container. (-f option outputs real-time logs)

```bash
docker logs -f ${CONTAINER_NAME}

# example
docker logs -f ops-bedrock-op-proposer-1
```

* Start/Stop/Restart Containers: Control the behavior of currently running containers individually.

```bash
docker start ${CONTAINER_NAME}

docker stop ${CONTAINER_NAME}

docker restart ${CONTAINER_NAME}
```

* Verify container port mapping: Verify port mapping information for inter-container communication.

```bash
docker port ${CONTAINER_NAME}
```



### 4. Testing Bridge Transactions Using Thanos SDK <a href="#testing-bridge-transactions" id="testing-bridge-transactions"></a>

You can move assets between L1 and L2 via bridge transactions using the SDK provided by Thanos Stack. Please refer to the [guide](https://www.notion.so/Bridge-Test-Guide-1d1d96a400a38095b391c01bb2d9410b?pvs=21) link for the commands and execution methods.

**The assets that support bridges on the Thanos Stack:**

1. TON
2. ETH
3. ERC-20 asset (except TON)

{% hint style="info" %}
### Relevant Links and Resources

* **Thanos SDK Technical Documentation:**
  * [Bridge ERC-20 Token](https://docs.tokamak.network/home/service-guide/rollup-hub/mainnet-beta/operation-guide/developer-tools/sdk/bridge-erc-20-tokens-with-the-thanos-sdk)
  * [Bridge Native Token](https://docs.tokamak.network/home/service-guide/rollup-hub/mainnet-beta/operation-guide/developer-tools/sdk/bridge-the-native-token-with-the-thanos-sdk)
  * [Bridge ETH](https://docs.tokamak.network/home/service-guide/rollup-hub/mainnet-beta/operation-guide/developer-tools/sdk/bridge-eth-with-the-thanos-sdk)
* **GitHub Repository:** [tokamak-thanos](https://github.com/tokamak-network/tokamak-thanos)
{% endhint %}
