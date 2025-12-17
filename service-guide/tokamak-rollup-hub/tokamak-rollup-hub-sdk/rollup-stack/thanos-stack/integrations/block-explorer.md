---
description: How to integrate Block Explorer to the deployed chain?
---

# Block Explorer

{% hint style="danger" %}
Available via SDK on Testnet/Mainnet only.
{% endhint %}

The current SDK version supports Block Explorer installation and uninstallation for the deployed network.

Before integrating the **Block Explorer**, ensure you meet the following prerequisites.

### **Prerequisite**

* CoinMarketCap API key: You can get the free one [here](https://pro.coinmarketcap.com/).
* Wallet Connect Id: Read more [here](https://docs.blockscout.com/setup/configuration-options/walletconnect-project-id-for-contract-read-write).

1. Once the prerequisites are fulfilled, execute the following command in the project root directory to install explorer.

```bash
trh-sdk install block-explorer
```

2. The SDK will then prompt you with the following questions via the CLI.

```jsx
Please input your database username: // This is one part of the db credential which will be used for storing chain data. e.g. victor_thanos_db
Please input your database password: // This is the password of the db connection. e.g. 12345678
Please input your CoinMarketCap key(read more): // Prerequisite e.g. c291ce7b-60f0-4e63-8908-e07b04e900b4
Please input your wallet connect id(read more): // Prerequisite e.g. 881053b0dbae8bdf9ba4b67cf6ef9e70
```

3. You can check success prompt here.

```jsx
✅ Block Explorer frontend component installed successfully. Accessible at: <http://k8s-blockscout-b36b1c9bc4-196703783.ap-northeast-2.elb.amazonaws.com>
```

> ℹ️ Note: After you install the explorer, you should wait for a couple of minutes due to network ingress propagation. It is same for the bridge operation.

4. To uninstall the explorer, you may execute the following command in the project root directory:

```bash
trh-sdk uninstall block-explorer
```

5. You can check success prompt here.

```
2025-05-06T06:40:19.835Z	Destroy complete! Resources: 4 destroyed.
2025-05-06T06:40:19.845Z	
```
