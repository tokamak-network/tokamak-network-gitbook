---
description: Testnet Operation Guide
---

# Testnet

## Command Cheetsheet

1. <mark style="color:red;">`info`</mark>: Get the Chain info. (RPC, bridge, explorer urls)

```bash
trh-sdk info
```

With this command, you can get the urls of L1 op node, bridge and block explorer. Be sure to run it from the root directory you used when deploying L2.

<figure><img src="../../../../../../.gitbook/assets/image (372).png" alt=""><figcaption><p>Chain Info</p></figcaption></figure>



2. <mark style="color:red;">`update`</mark>: Update L1 RPC URL (execution node and beacon node) while operating L2

```bash
trh-sdk update
```

With this command, you are able to update the L1 RPC url and L1 beacon url without redeploying the chain.

<figure><img src="../../../../../../.gitbook/assets/image (373).png" alt=""><figcaption><p>SDK Prompt</p></figcaption></figure>

> ℹ️ After you update the urls, you need to wait for a couple of minutes for the k8s pod re-initialization.

3. <mark style="color:red;">`logs`</mark>: Find the logging specific pods

Basically, now SDK is logging your deployment process inside the `logs` directory in your root deployment directory.

<figure><img src="../../../../../../.gitbook/assets/image (374).png" alt=""><figcaption><p>logs</p></figcaption></figure>

`logs` command is to check the log of a pod that is running in real time. The logs printed in real time are also saved to a file in the `logs` directory.

```bash
 # print the log of running op-node
trh-sdk logs -c op-node

# troubleshoot mode: Only print log levels higher than error
trh-sdk logs -c op-node -t

# help
trh-sdk logs -h

NAME:
   trh-sdk logs - Show logs of the running chain

USAGE:
   trh-sdk logs [command [command options]]

OPTIONS:
   --component value, -c value  Component name (allowed: op-node, block-explorer-fe, block-explorer-be, bridge, op-batcher, op-proposer, op-geth)
   --troubleshoot, -t           Show logs of the running chain with troubleshoot mode (default: false)
   --help, -h                   show help
```

4. <mark style="color:red;">`version`</mark>: Find the trh-sdk version. The hash value after semver will be different depending on the latest commit on the main branch.

```
# example
trh-sdk version
Version: v0.0.0-20250514085200-bb4056b96658
```

The L2 chain deployed with SDK consists of a k8s-based cluster. So let's learn how to check and configure a k8s cluster using `kubectl`. Please refer to the [glossary](https://kubernetes.io/docs/reference/glossary) for an explanation of basic terms used in k8s.

5. **Get k8s workloads:**

```bash
kubectl -n ${namespace} get pods

# e.g.,
kubectl -n theo0509 get pods
NAME                                                              READY   STATUS    RESTARTS   AGE
block-explorer-be-1746768413-blockscout-stack-blockscout-8dvqn5   1/1     Running   0          9h
block-explorer-fe-1746768430-blockscout-stack-frontend-7c6zlh2w   1/1     Running   0          9h
external-secrets-5d796f6bb9-nh97t                                 1/1     Running   0          9h
external-secrets-cert-controller-5f988fc8f8-272sn                 1/1     Running   0          9h
external-secrets-webhook-64f479779f-m7nr8                         1/1     Running   0          9h
op-bridge-1746766808-5968488778-jdtsn                             1/1     Running   0          9h
theo0509-1746766783-thanos-stack-op-batcher-78c8bc4956-rhzgz      1/1     Running   0          9h
theo0509-1746766783-thanos-stack-op-geth-0                        1/1     Running   0          9h
theo0509-1746766783-thanos-stack-op-node-0                        1/1     Running   0          9h
theo0509-1746766783-thanos-stack-op-proposer-6fc46c97c-psv6v      1/1     Running   0          9h

kubectl -n ${namespace} get statefulset

# e.g.,
kubectl -n theo0509 get statefulset
NAME                                       READY   AGE
theo0509-1746766783-thanos-stack-op-geth   1/1     9h
theo0509-1746766783-thanos-stack-op-node   1/1     9h

kubectl -n ${namespace} get deployments

# e.g.,
kubectl -n theo0509 get deployments
NAME                                                       READY   UP-TO-DATE   AVAILABLE   AGE
block-explorer-be-1746768413-blockscout-stack-blockscout   1/1     1            1           9h
block-explorer-fe-1746768430-blockscout-stack-frontend     1/1     1            1           9h
external-secrets                                           1/1     1            1           9h
external-secrets-cert-controller                           1/1     1            1           9h
external-secrets-webhook                                   1/1     1            1           9h
op-bridge-1746766808                                       1/1     1            1           9h
theo0509-1746766783-thanos-stack-op-batcher                1/1     1            1           9h
theo0509-1746766783-thanos-stack-op-proposer               1/1     1            1           9

kubectl -n ${namespace} get cm

# e.g.,
kubectl -n theo0509 get cm         
NAME                                               DATA   AGE
kube-root-ca.crt                                   1      9h
op-bridge-1746766808                               1      9h
theo0509-1746766783-thanos-stack-common            2      9h
theo0509-1746766783-thanos-stack-op-batcher        17     9h
theo0509-1746766783-thanos-stack-op-geth           6      9h
theo0509-1746766783-thanos-stack-op-geth-auth      1      9h
theo0509-1746766783-thanos-stack-op-geth-scripts   1      9h
theo0509-1746766783-thanos-stack-op-node           17     9h
theo0509-1746766783-thanos-stack-op-node-scripts   1      9h
theo0509-1746766783-thanos-stack-op-proposer       8      9h
theo0509-1746766783-thanos-stack-wait-scripts      2      9h

kubectl -n ${namespace} get svc

# e.g., 
kubectl -n theo0509 get svc
NAME                                                           TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                                         AGE
block-explorer-be-1746768413-blockscout-stack-blockscout-svc   ClusterIP   10.100.65.64     <none>        80/TCP                                          9h
block-explorer-fe-1746768430-blockscout-stack-frontend-svc     ClusterIP   10.100.115.132   <none>        80/TCP                                          9h
external-secrets-webhook                                       ClusterIP   10.100.96.20     <none>        443/TCP                                         9h
op-bridge-1746766808                                           ClusterIP   10.100.20.113    <none>        3000/TCP                                        9h
theo0509-1746766783-thanos-stack-op-batcher                    ClusterIP   10.100.198.64    <none>        8548/TCP,7300/TCP                               9h
theo0509-1746766783-thanos-stack-op-geth                       ClusterIP   10.100.51.116    <none>        8545/TCP,8546/TCP,8551/TCP,30303/TCP,6060/TCP   9h
theo0509-1746766783-thanos-stack-op-node                       ClusterIP   10.100.235.149   <none>        8545/TCP,7300/TCP,6060/TCP                      9h
theo0509-1746766783-thanos-stack-op-proposer                   ClusterIP   10.100.228.89    <none>        8560/TCP,7300/TCP 

kubectl -n ${namespace} get ingress

# e.g.,
kubectl -n theo0509 get ingress    
NAME                                                               CLASS   HOSTS                                                                  ADDRESS                                                                PORTS   AGE
block-explorer-be-1746768413-blockscout-stack-blockscout-ingress   alb     *                                                                      k8s-blockscout-91aa04c465-227592509.ap-northeast-2.elb.amazonaws.com   80      9h
block-explorer-fe-1746768430-blockscout-stack-frontend-ingress     alb     k8s-blockscout-91aa04c465-227592509.ap-northeast-2.elb.amazonaws.com   k8s-blockscout-91aa04c465-227592509.ap-northeast-2.elb.amazonaws.com   80      9h
op-bridge-1746766808-ingress                                       alb     *                                                                      k8s-bridge-3267f7e291-2110412992.ap-northeast-2.elb.amazonaws.com      80      9h
theo0509-1746766783-thanos-stack-op-geth-ingress                   alb     *                                                                      k8s-opgeth-e11a7a2117-1574770345.ap-northeast-2.elb.amazonaws.com      80      9h
```

You can add resource name and the `-o yaml` option to the command will output the manifest details:

```bash
kubectl -n ${namespace} get pods ${pod_name} -o yaml
kubectl -n ${namespace} get statefulset ${statefulset_name} -o yaml

...
```

6. **Display detailed information about the workloads:**

```bash
kubectl -n ${namespace} describe pods ${pod_name}
```

7. **Display the logs of the pod:**

```bash
kubectl -n ${namespace} logs -f ${pod_name}
```

8. **Access the shell inside the container of the pod:**

```bash
kubectl -n ${namespace} exec -it ${pod_name} -- /bin/sh

# e.g.
kubectl -n theo0509 exec -it theo0509-1746766783-thanos-stack-op-batcher-78c8bc4956-rhzgz -- /bin/sh
```

9. **View environment variables inside the pod:**

```bash
kubectl -n ${namespace} exec -it ${pod_name} -- env

# e.g.,
kubectl -n theo0509 exec -it theo0509-1746766783-thanos-stack-op-batcher-78c8bc4956-rhzgz -- env
Defaulted container "batcher" out of: batcher, wait-for-rollup (init)
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
HOSTNAME=theo0509-1746766783-thanos-stack-op-batcher-78c8bc4956-rhzgz
OP_BATCHER_SAFE_ABORT_NONCE_TOO_LOW_COUNT=3
OP_BATCHER_NUM_CONFIRMATIONS=1
OP_BATCHER_RPC_ENABLE_ADMIN=true
OP_BATCHER_ROLLUP_RPC=http://theo0509-1746766783-thanos-stack-op-node:8545
OP_BATCHER_DATA_AVAILABILITY_TYPE=calldata
OP_BATCHER_SUB_SAFETY_MARGIN=6
OP_BATCHER_MAX_CHANNEL_DURATION=10
OP_BATCHER_RPC_PORT=8548
OP_BATCHER_L1_ETH_RPC=https://eth-sepolia.g.alchemy.com/v2/zPJeUK2LKGg4LjvHPGXYl1Ef4FJ_u7Gn
...
```

10. **How to restart a pod**

Pods are automatically redeployed when deleted. Alternatively, you can redeploy them using a deployment or statefulSet.

```bash
kubectl -n ${namespace} delete pods ${pod_name}

# e.g.,
kubectl -n theo0509 delete pods theo0509-1746766783-thanos-stack-op-node-0
pod "theo0509-1746766783-thanos-stack-op-node-0" deleted

kubectl -n ${namespace} rollout restart deployment ${deployment_name}

# e.g.,
kubectl -n theo0509 rollout restart deployment theo0509-1746766783-thanos-stack-op-batcher
deployment.apps/theo0509-1746766783-thanos-stack-op-batcher restarted

kubectl -n ${namespace} rollout restart statefulset ${statefulset_name}

# e.g.,
kubectl -n theo0509 rollout restart statefulset theo0509-1746766783-thanos-stack-op-geth
statefulset.apps/theo0509-1746766783-thanos-stack-op-geth restarted

```

11. **How to terminate a pod**

You can terminate or start pods by manually adjusting the replica of the deployment or statefulset that controls the pods.

```bash
kubectl -n ${namespace} scale deployment ${deployment_name} --replicas=0

# e.g., terminate pod
kubectl scale deployment theo0509-1746766783-thanos-stack-op-proposer --replicas=0 -n theo0509
deployment.apps/theo0509-1746766783-thanos-stack-op-proposer scaled

# e.g., start pod
ubectl scale deployment theo0509-1746766783-thanos-stack-op-proposer --replicas=1 -n theo0509
deployment.apps/theo0509-1746766783-thanos-stack-op-proposer scaled
```

If you're interested in learning more about the command set and related knowledge beyond the commands introduced above, please refer to the [official k8s documentation.](https://kubernetes.io/docs/home/)

## Troubleshooting Withdrawal Delays

The advanced chain config parameters determine the rollup cycle of the batcher and proposer services, and the withdrawal delay can be changed accordingly. So in the best case, the withdrawal delay can be calculated as `Max(Batch Submission Frequency, Output Root Frequency) + Challenge Period`.

If you proceed without selecting the advanced configuration, the Batch Submission Frequency is set to `1440s` and the Output Root Frequency is set to `240s`. In this case, the withdrawal delay can be expected to be `1440s + 120s = 24m 12s`.

If the withdrawal is delayed more than the expected delay, you can check the following factors:

1. **L1 Node Health:** Check for rate limits or another error in the L1 node logs. If you use a third-party service, they support features to check logs in the dashboard.
2. **L1 network congestion:** If the L1 network is very congested and there are too many transactions piled up in the mempool, submitted rollup transactions may not be included in the block right away.
3.  **Rollup Progress**: Monitor the `L2OutputOracle` for `OutputProposed` events to assess the rollup status and anticipate potential delays.

    * You can check the number of L2 blocks rolled up to date by querying the deployed `L2OutputOracle` contract and checking the recent rollup transactions. By comparing it with the L2 block number containing the withdrawal transaction, you can estimate any additional delays that may occur.

    <figure><img src="../../../../../../.gitbook/assets/image (375).png" alt=""><figcaption><p>Event log of OutputProposed</p></figcaption></figure>

## Manage the Secrets on AWS

The private keys of the selected `batcher`, `proposer`, and `sequencer` entered during the contract deployment phase are automatically entered and managed in AWS Secret Manager during the L2 infrastructure deployment. Secret Manager securely stores sensitive information such as private keys in AWS and manages them as environment variables so that they can be used dynamically by applications.

After deploying the L2 chain, you can check the secrets named `${namespace}/secrets` in AWS Secret Manager > Secrets menu in the AWS Console accessed through your IAM account.

<figure><img src="../../../../../../.gitbook/assets/image (377).png" alt=""><figcaption><p>Find the Secrets with AWS Secret Manager</p></figcaption></figure>

This menu allows administrators to view, modify, or delete the stored private keys of `batcher`, `proposer`, and `sequencer`.

<figure><img src="../../../../../../.gitbook/assets/image (378).png" alt=""><figcaption><p>Retrieve secret value on console</p></figcaption></figure>



