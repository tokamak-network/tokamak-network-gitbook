---
description: Bridge service for the deployed chain
---

# Bridge

{% hint style="warning" %}
Available via SDK on Testnet/Mainnet only. For manual bridge testing in Devnet, refer to the operation guide.
{% endhint %}

{% hint style="success" %}
The bridge component is **automatically deployed** along with the appchain infrastructure, as it is considered a core feature for appchain users. So only if you already uninstalled bridge, you can use the below command to reinstall it.
{% endhint %}

Similar to the explorer, you can use the following command to install or uninstall the bridge as needed. Please refer to the next section for how to use the bridge.

```bash
trh-sdk install/uninstall bridge
```

{% hint style="warning" %}
**Note**: Withdrawal transactions are delayed from initialization until they are verified in L1. This delay varies depending on the Batch Submission Frequency and Output Frequency set in the deployment phase. After that , we can finalize withdrawal transaction in L1.
{% endhint %}
