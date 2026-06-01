---
description: Introducing Tokamak Network's staking system.
---

# Simple staking

{% hint style="warning" %}
**The officially hosted staking website has been discontinued.**

Staking itself is fully on-chain and keeps running through the smart contracts. You can still use it in two ways:

* **Etherscan** — interact with the staking contracts directly on-chain. This works regardless of any frontend and is the most reliable option. See [Interact via Etherscan](interact-via-etherscan.md).
* **Community edition** — a community-maintained version of the staking dApp that you can self-host, or use through a community-hosted instance (see the **How to use staking** section below).
{% endhint %}

{% hint style="info" %}
**Resources**

* Documentation hub: [https://github.com/tokamak-network/TokamakStaking](https://github.com/tokamak-network/TokamakStaking)
* Contracts: [https://github.com/tokamak-network/ton-staking-v2](https://github.com/tokamak-network/ton-staking-v2)
* Contract addresses: [link](contract-addresses.md)
* Audit report: [DAO & TON Staking v2 audit report](https://medium.com/tokamak-network/dao-ton-staking-v2-audit-report-2fa7bb1a9291)
* Past announcements: [Medium (staking)](https://medium.com/tokamak-network/search?q=staking)
{% endhint %}

### 1. Features

Tokamak Network’s staking is used to select the DAO committee members that can vote on agendas. Here's how it works:

* Users can stake their TON or WTON on DAO candidates to earn staking rewards and support the DAO candidate to become one of the DAO committee members.
* The three DAO candidates with the highest staking can become DAO committee members, where they can vote on DAO agendas.

### 2. How to use staking

Because the official website is no longer hosted, choose one of the following access methods:

<table><thead><tr><th width="220">Method</th><th>What it is</th><th>When to use it</th></tr></thead><tbody><tr><td><strong>Etherscan</strong></td><td>Call the staking contract functions directly from the Etherscan "Read/Write Contract" tabs.</td><td>Always available, no dependency on any frontend. Recommended for stake, unstake, restake, withdraw, and claiming rewards. See <a href="interact-via-etherscan.md">Interact via Etherscan</a>.</td></tr><tr><td><strong>Community edition (self-hosted)</strong></td><td>Run the open-source staking frontend yourself by following the repository guide.</td><td>If you want the familiar dApp UI and prefer to host it yourself. Repo: <a href="https://github.com/tokamak-network/staking-community-version">staking-community-version</a>.</td></tr><tr><td><strong>Community edition (community-hosted)</strong></td><td>A community member hosts a public instance of the frontend.</td><td>For convenience, if you accept the risk (see warning below). Instance: <a href="https://staking-community-version.vercel.app/">staking-community-version.vercel.app</a>.</td></tr></tbody></table>

{% hint style="danger" %}
Community-hosted links are operated by community members and are **not endorsed by Tokamak Network**. Use them at your own risk — Tokamak Network provides no guarantee or support for these links. When in doubt, self-host the community edition or use Etherscan directly. Always confirm contract addresses against the [Contract addresses](contract-addresses.md) page before signing any transaction.
{% endhint %}

The pages below ([Stake](stake.md), [Withdraw](withdraw.md), [Staking reward](staking-reward.md)) describe the staking dApp interface. The community edition shares the same interface, so these walkthroughs apply when you self-host or use a community-hosted instance.

### 3. Page Information

{% hint style="info" %}
The screens below come from the staking dApp. The community edition uses the same interface.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (3).png" alt="" width="375"><figcaption><p>The initial screen of the staking page</p></figcaption></figure>

1. **Home**

* Click the Connect Wallet button to link your Metamask or Trezor wallet.
* The blue graph shows the amount staked on Tokamak network by the staker each day, and the grey graph shows the actual APY each day. If you hover your mouse over the graph, you can see the total amount of daily staking and the actual APY.

2. **Staking**

* On the staking page, you can check information about the DAO candidates. If your wallet is connected, you can click the blue arrow on the right of each operator to see detailed information about the DAO candidate and the staking button. If your wallet is not connected, you can only see the details of the operator.
* Once your wallet is connected, you can click the Staking button to stake your TON (or WTON) to a DAO candidate.

3. **Account**

* The account page provides information about the assets you hold.
* To use this service, you must first log in through the wallet connection at the top right.

The information provided is as follows:

* Total Staked: This is the total of staked TON.
* Pending Withdrawal: This is the total amount of Unstake TON. This amount can only be withdrawn after the withdrawal delay period set by the DAO candidate (default is after 93,046 blocks, about 14 days) has passed.
* History: This shows the transaction history related to staking. This information includes transaction hash, related DAO candidate (Candidate), type, amount, and execution time.

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt="" width="375"><figcaption><p>Wallet and history</p></figcaption></figure>

### **4. Login**

You must first log in through wallet connection to access some features like staking and account information. You can select the wallet connection method by clicking the wallet connection button at the top right of the screen.

* Log in with Metamask&#x20;
  * Make sure you are connected to the Ethereum mainnet network. Then click the Connect Wallet button.
  * In the pop-up window, click the Metamask icon.
  * In the list of browser extensions, click the Metamask icon and select the account to connect to the service.
*   Log in with Trezor&#x20;

    * Connect to Trezor wallet

    <figure><img src="../../.gitbook/assets/image (3) (1).png" alt="" width="188"><figcaption><p>Wallet option</p></figcaption></figure>
