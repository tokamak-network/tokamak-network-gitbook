# Advanced configurations

This step is to let the users set the advanced chain config parameters:

* L2 Block Time (default: 2 seconds): The time it takes to produce a new block on the L2 chain.
* Batch Submission Frequency (Default: 120 L1 blocks ≈ 1440 seconds, must be a multiple of 12): The frequency of L2 block batch submission to the L1 chain.
* Output Root Frequency (Default: 120 L2 blocks ≈ 240 seconds, must be a multiple of 2): The frequency of L2 output root submission to the L1 chain.
* Challenge Period (Default: 12 seconds): The time window during which participants can contest or submit fraud proofs against a posted Layer 2 transaction before it becomes final.

{% hint style="danger" %}
**Note:** The advanced chain config parameters set above can affect deposits and withdrawals. For example, if you use the default value, you can expect a withdrawal delay of `Max(1440, 240) + 12 seconds`, but please note that unexpected delays may occur depending on the L1 network.
{% endhint %}
