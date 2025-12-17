---
description: 스테이킹된 TON을 인출(withdraw) 하는 과정을 소개합니다.
---

# Withdraw

중요한 점은 첫째, 스테이킹 물량을 인출하기 위해서는 스테이킹 해제(unstake)와 인출(withdraw), 두 단계를 거쳐야 한다는 것이며, 둘째, 인출(withdraw) 은 스테이크 해제(unstake) 이후 93,046 블록이(\~14일) 지나야 가능하다는 점입니다.&#x20;

{% hint style="info" %}
출금지연기간

* 기간 : Unstake 완료 후 93,046 블록이 경과되는 시간(약 14일에 해당)

스테이킹 해제(unstake) 이후 약 2주간의 출금지연기간이 경과했음에도 본인의 지갑에 토큰이 입금되지 않았다는 이슈를 제기하는 경우가 있습니다. 이는 출금지연기간 경과 후 인출(withdraw) 버튼을 실행하지 않았기 때문에 발생하는 현상입니다.&#x20;
{% endhint %}

### &#x20;1. 스테이크 해제(Unstake)

<figure><img src="../../.gitbook/assets/8-unstake.png" alt="" width="375"><figcaption></figcaption></figure>

**언스테이킹(Unstake)이란:**

* **언스테이킹**은 L1에 스테이킹된 금액을 출금하기 위한 과정입니다.
* L2로 출금하고 싶다면 **언스테이킹을 사용하지 마세요** - 대신 Withdraw-L2를 사용하세요.
* 언스테이킹에서 입력할 수 있는 **최대 금액은** "Your Staked Amount"(귀하의 스테이킹 금액)로 제한됩니다.

**언스테이킹 방법:**

1. 스테이킹 포지션에서 Unstake 버튼을 클릭합니다.
2. 언스테이킹하려는 금액을 입력합니다.
3. 지갑에서 트랜잭션을 승인합니다.
4. 브라우저의 Metamask 확장 프로그램에서 열리는 Metamask 팝업의 확인 버튼을 클릭합니다.&#x20;

{% hint style="warning" %}
&#x20;스테이크 해제에 앞서 **받지 못한 스테이킹 보상**(Unclaimed Staking Reward)이 있는지 확인하세요&#x20;

* 스테이크 해제를 완료한 이후에는 **받지 못한 스테이킹 보상**이 버닝 됩니다.&#x20;
* **받지 못한 보상이** 있다면, Your Staked로 먼저 옮겨놓으세요 [link](/broken/pages/5vTrJ2LrMEP5j9I9hHyv)
{% endhint %}

### &#x20;2. 인출(Withdraw)

**옵션 1: L1 출금 (표준)**

<figure><img src="../../.gitbook/assets/4-select_l1_withdraw (1).png" alt="" width="375"><figcaption></figcaption></figure>

1. 스테이킹 포지션에서 출금(withdraw) 버튼을 클릭합니다.
2. 표준 이더리움 네트워크를 위한 L1 출금을 선택합니다.
3. 출금할 토큰 선택 - TON을 받으려면 TON 선택, WTON을 받으려면 WTON 선택
4. 출금 가능 금액이 자동으로 계산되어 입력됩니다.
5. 지갑에서 트랜잭션을 승인합니다.

**옵션 2: L2 출금 (이용 가능한 경우)**

<figure><img src="../../.gitbook/assets/5-select_l2_withdraw.png" alt="" width="375"><figcaption></figcaption></figure>

**L2 출금이란:** L2 출금은 운영자(operator)가 시퀀서(sequencer) 역할을 하는 L2 네트워크(예: 위 이미지의 Poseidon)로 스테이킹된 TON을 출금할 수 있게 해줍니다. L1 출금은 약 2주가 소요되는 반면, L2 출금은 L2 네트워크가 예치된 금액을 처리할 때까지만 기다리면 됩니다.

**L2로 출금하는 방법:**

1. 운영자가 지원하는 경우 L2 출금을 선택합니다.
2. 출금 금액을 선택합니다.
3. 트랜잭션을 승인합니다.
4. 자금이 사용 가능해지기 전에 L2 처리를 기다립니다.

### **3. 스테이킹 재설정 (**&#x52;estake)

스테이킹 해제(unstake)를 실시한 이후, 인출(withdraw)을 하지 않았다면 언제든지 스테이킹을 다시 할 수 있습니다. 이러한 인출대기 물량은 Restake 버튼을 누르면 나타나는 값을 통해 확인할 수 있습니다.

<figure><img src="../../.gitbook/assets/9-restake (1).png" alt="" width="375"><figcaption></figcaption></figure>

**Restaking 방법:**

* 언스테이킹 후 대기 중인 금액을 확인합니다.
* Restake를 클릭하여 확인합니다.
* 지갑에서 트랜잭션을 승인합니다.
