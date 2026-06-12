---
description: >-
  호스팅된 프론트엔드에 의존하지 않고 이더스캔을 통해 온체인에서 직접 스테이킹을 사용합니다.
---

# 이더스캔으로 상호작용하기

공식 스테이킹 웹사이트가 더 이상 호스팅되지 않으므로, 스테이킹을 사용하는 가장 신뢰할 수 있는 방법은 이더스캔(Etherscan)에서 컨트랙트 함수를 직접 호출하는 것입니다. 이더스캔에서 지갑을 연결한 후, **Read** 탭으로 정보를 조회하고 **Write** 탭으로 트랜잭션을 전송합니다.

{% hint style="info" %}
[GitHub 이슈](https://github.com/tokamak-network/TokamakStaking/issues)를 통해 지원을 요청할 수 있습니다.
{% endhint %}

### 전체 사용 흐름

1. **준비** — 지갑(예: MetaMask)과 TON/WTON 토큰을 준비합니다. 이 가이드에서 참조하는 모든 주소는 [컨트랙트 주소](https://docs.tokamak.network/home/service-guide/simple-staking/contract-addresses)를 확인하세요.
2. **스테이킹** — `approveAndCall` 함수로 TON 또는 WTON을 스테이킹합니다. [이더스캔으로 스테이킹하기](stake-via-etherscan.md)를 참고하세요.
3. **스테이크 해제 / 인출 요청** — `requestWithdrawal`로 스테이크를 해제하고 인출을 요청한 후, `processRequests`로 인출을 완료합니다. [이더스캔으로 언스테이킹·재스테이킹·인출하기](unstake-restake-withdraw-via-etherscan.md)를 참고하세요.
4. **재스테이킹** — `redepositMulti`로 대기 중인 인출을 재스테이킹합니다. [이더스캔으로 언스테이킹·재스테이킹·인출하기](unstake-restake-withdraw-via-etherscan.md)를 참고하세요.
5. **운영자 / L2 정보** — 운영자 및 L2 시퀀서 정보를 조회합니다. [운영자 정보 확인하기](check-operator-information.md)를 참고하세요.

### 쿼리 실행 (Read)

컨트랙트의 **Read Contract** 또는 **Read as Proxy** 탭에서 조회에 사용할 수 있는 함수 목록을 확인할 수 있습니다. 원하는 함수의 파라미터를 입력한 후 쿼리 버튼을 클릭하면 결과를 확인할 수 있습니다.

<figure><img src="../../.gitbook/assets/staking-etherscan-read-proxy.png" alt=""><figcaption><p>Read as Proxy 화면</p></figcaption></figure>

함수에 파라미터가 필요한 경우, 아래와 같이 입력 필드가 표시됩니다. 파라미터를 입력하고 쿼리를 실행하세요.

<figure><img src="../../.gitbook/assets/staking-etherscan-read-params.png" alt=""><figcaption><p>파라미터를 사용한 쿼리 실행</p></figcaption></figure>

### 트랜잭션 실행 (Write)

트랜잭션을 전송하려면 먼저 페이지 상단에서 지갑을 연결합니다("Connect to Web3").

컨트랙트의 **Write Contract** 또는 **Write as Proxy** 탭에서 트랜잭션을 전송하는 함수 목록을 확인할 수 있습니다. 원하는 함수의 파라미터를 입력한 후 **Write**를 클릭하여 실행합니다.

<figure><img src="../../.gitbook/assets/staking-etherscan-write-proxy.png" alt=""><figcaption><p>Write as Proxy 화면</p></figcaption></figure>

트랜잭션에 파라미터가 필요한 경우, 아래와 같이 입력 필드가 표시됩니다. 파라미터를 입력하고 **Write**를 클릭하세요.

<figure><img src="../../.gitbook/assets/staking-etherscan-write-params.png" alt=""><figcaption><p>파라미터를 사용한 트랜잭션 실행</p></figcaption></figure>

{% hint style="warning" %}
토큰 수량은 토큰에 따라 단위가 다릅니다:

* **TON**은 18 decimals(Wei)을 사용합니다.
* **WTON** 및 DepositManager/SeigManager의 수량은 27 decimals(Ray)을 사용합니다.

금액을 입력하기 전에 해당 함수가 요구하는 단위를 반드시 확인하세요.
{% endhint %}
