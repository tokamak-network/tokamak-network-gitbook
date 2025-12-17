# How to use the Bridge?

## Introduction <a href="#introduction" id="introduction"></a>

The  bridge can be configured and integrated into the deployed Thanos stack. Its key functionality includes Deposit/Withdraw support for ETH, Native token, USDT, and USDC. You can learn more about the thanos bridge here. As the code is open source, operators and developers can extend its functionalities to suit their specific needs.

## Quick User guide <a href="#quick-user-guide" id="quick-user-guide"></a>

After you deploy the thanos bridge following the Thanos stack deployment guide, you will get the public domain of that bridge where you can move assets across Layer1 and Layer2.

### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

You should have the Metamask wallet installed in your browser. ([guide](https://support.metamask.io/start/getting-started-with-metamask/#how-to-install-metamask))

**Wallet connect**

1. First things first, you can connect your account by clicking `Connect Wallet` button to use the bridge.

<figure><img src="../../../../../../../.gitbook/assets/image (379).png" alt=""><figcaption></figcaption></figure>

2. After you connect your account into the bridge app, you can change the network(L1 & L2) connected and also able to see the token balance of your account.

<figure><img src="../../../../../../../.gitbook/assets/image (380).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../../../.gitbook/assets/image (381).png" alt="" width="375"><figcaption></figcaption></figure>

### **Deposit(L1 → L2)**

1.  Click the `Deposit` tab or set the L1 network chain connected to deposit tokens to the L2 network.

    <figure><img src="../../../../../../../.gitbook/assets/image (382).png" alt=""><figcaption></figcaption></figure>
2. Select the token and input the amount to deposit. `To address` is the address to be deposited; it is your current account as a default, but you can put another account if needed. (pic1: connected account, pic2: another account)

<figure><img src="../../../../../../../.gitbook/assets/image (383).png" alt="" width="375"><figcaption></figcaption></figure>

<figure><img src="../../../../../../../.gitbook/assets/image (384).png" alt="" width="375"><figcaption></figcaption></figure>

3. Click `Deposit` button for ETH deposit and you will need to approve them in case of the other tokens (Native token, USDT, USDC). After the transaction has been confirmed, you will get the link of that transaction.

<figure><img src="../../../../../../../.gitbook/assets/image (385).png" alt="" width="375"><figcaption></figcaption></figure>

### **Withdraw(L2 → L1)**

The withdrawal process contains 3 steps (initiate, prove, finalize) based on Optimistic rollup.

1. Initiate
   1.  You can initiate a withdrawal transaction by clicking `Withdaw` → `Initiate` tab and the operations(token selection, input amount, input address to send, etc) are same as what we did for the deposit process.

       <figure><img src="../../../../../../../.gitbook/assets/image (386).png" alt="" width="352"><figcaption></figcaption></figure>
   2. After the transaction has been confirmed, you will get the Tx hash which will be used for `prove` and `finalize` process.
2.  Prove

    1. You can check the status of your withdrawal transaction in [Layer2 block explorer](https://explorer.thanos-sepolia.tokamak.network/withdrawals) that you deployed in the previous rollup deployment steps.

    <figure><img src="../../../../../../../.gitbook/assets/image (387).png" alt=""><figcaption></figcaption></figure>

    b. Once the transaction is ready to prove, you are ready to prove it. Click `Prove` tab and input the hash of the initiated transaction. Click `Prove` button.

    <figure><img src="../../../../../../../.gitbook/assets/image (388).png" alt=""><figcaption></figcaption></figure>
3. Finalize
   1. Check the status of your withdrawal transaction in Layer2 block explorer and it should be `Ready for relay` to be finalized.
   2.  Go to `Finalize` tab and input the hash of the initiate transaction. Click `Finalize` button.

       <figure><img src="../../../../../../../.gitbook/assets/image (389).png" alt=""><figcaption></figcaption></figure>

## Troubleshooting <a href="#troubleshooting" id="troubleshooting"></a>

1. If you are using an http RPC url for the L2 rollup, instead of https, you will need to manually add the L2 network to your metamask.
   1.  Open the metamask extension in your browser, click on the network dropdown on top left corner and click `Add a custom network`.

       <figure><img src="../../../../../../../.gitbook/assets/image (390).png" alt="" width="273"><figcaption></figcaption></figure>

       <figure><img src="../../../../../../../.gitbook/assets/image (391).png" alt="" width="287"><figcaption></figcaption></figure>
   2. Get the following details from bridge app and fill in the form.
      1. Network Name
      2. New RPC URL
      3. Chain ID
      4. Currency Symbol
      5. Block Explorer URL (Optional)

<figure><img src="../../../../../../../.gitbook/assets/image (392).png" alt="" width="375"><figcaption></figcaption></figure>

<figure><img src="../../../../../../../.gitbook/assets/image (393).png" alt="" width="284"><figcaption></figcaption></figure>

2. Network switch issue in case of http L2 RPC url. If you want withdraw or prove/finalize the withdrawals, you need to switch the network to the L2 rollup network. In this case, if you have http L2 RPC url, you will need to manually switch the network in your metamask.

<figure><img src="../../../../../../../.gitbook/assets/image (394).png" alt="" width="299"><figcaption></figcaption></figure>

After switching the network, you will see the network has been switched to the L2 rollup network successfully and you can continue with the withdraw or prove/finalize process.
