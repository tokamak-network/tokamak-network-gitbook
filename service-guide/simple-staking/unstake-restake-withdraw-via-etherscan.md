---
description: >-
  DepositManager 컨트랙트를 사용하여 이더스캔에서 직접 스테이킹된 TON을 언스테이킹하고, 재스테이킹하고, 인출하는 방법을 안내합니다.
---

# 이더스캔으로 언스테이킹·재스테이킹·인출하기

이 모든 작업은 **DepositManager** 컨트랙트를 통해 이루어집니다.

* DepositManager (Write as Proxy): [0x0b58ca72b12f01fc05f8f252e226f3e2089bd00e](https://etherscan.io/address/0x0b58ca72b12f01fc05f8f252e226f3e2089bd00e#writeProxyContract)
* DepositManager (Read as Proxy): [0x0b58ca72b12f01fc05f8f252e226f3e2089bd00e](https://etherscan.io/address/0x0b58ca72b12f01fc05f8f252e226f3e2089bd00e#readProxyContract)

<figure><img src="../../.gitbook/assets/staking-etherscan-withdraw-write.png" alt=""><figcaption><p>해당 함수들은 DepositManager의 Write as Proxy 탭에서 확인할 수 있습니다.</p></figcaption></figure>

### 전체 흐름

1. **인출 요청 (언스테이킹)** — `requestWithdrawal`
2. **재스테이킹(restake, 선택 사항)** — `redepositMulti`
3. **인출(withdraw)** — `processRequests` (대기 기간이 지난 후 실행)

{% hint style="warning" %}
인출은 요청 시점으로부터 출금지연기간(기본값 **93,046 블록**, 약 **14일**)이 경과한 후에만 가능합니다. `requestWithdrawal` 이후에도 실제 토큰을 받으려면 반드시 `processRequests`를 실행해야 합니다. 단순히 기다리는 것만으로는 자금이 이동되지 않습니다.
{% endhint %}

## Write 함수

### `requestWithdrawal(address layer2, uint256 amount)`

스테이킹된 금액의 [인출을 요청](https://etherscan.io/address/0x0b58ca72b12f01fc05f8f252e226f3e2089bd00e#writeProxyContract)합니다(언스테이킹).

* **파라미터**
  * `layer2`: 인출할 운영자(operator) 주소
  * `amount`: 인출할 수량 (소수점 27자리, Ray 단위)

> `requestWithdrawal`은 호출할 때마다 금액에 관계없이 **요청 1건**으로 기록됩니다. TON 100을 언스테이킹하든 1,000을 언스테이킹하든 각 호출은 단일 인출 요청으로 처리됩니다.

### `redepositMulti(address layer2, uint256 n)`

아직 인출되지 않은 대기 중인 요청을 [재스테이킹](https://etherscan.io/address/0x0b58ca72b12f01fc05f8f252e226f3e2089bd00e#writeProxyContract)합니다.

* **파라미터**
  * `layer2`: 재스테이킹할 운영자 주소
  * `n`: 재스테이킹할 대기 요청 건수

### `processRequests(address layer2, uint256 n, bool receiveTON)`

대기 기간이 경과한 요청을 [인출](https://etherscan.io/address/0x0b58ca72b12f01fc05f8f252e226f3e2089bd00e#writeProxyContract)합니다.

* **파라미터**
  * `layer2`: TON을 인출할 운영자 주소
  * `n`: 처리할 요청 건수
  * `receiveTON`: `true`이면 TON으로 수령, `false`이면 WTON으로 수령

## Read 함수

재스테이킹 또는 인출 전에 DepositManager의 **Read as Proxy** 탭을 사용하여 요청 내역을 확인하세요.

### `numPendingRequests(address layer2, address account)`

특정 운영자에 대해 아직 처리되지 않은(pending) 인출 요청 건수를 조회합니다.

* **파라미터**: `layer2` (운영자 주소), `account` (사용자 주소)
* **반환값**: `uint256` — 대기 중인 요청 건수

### `numRequests(address layer2, address account)`

특정 운영자에 대해 계정이 생성한 인출 요청의 총 건수를 조회합니다.

* **파라미터**: `layer2` (운영자 주소), `account` (사용자 주소)
* **반환값**: `uint256` — 전체 요청 건수

### `withdrawalRequest(address layer2, address account, uint256 index)`

특정 인출 요청의 상세 정보를 조회합니다.

* **파라미터**: `layer2` (운영자 주소), `account` (사용자 주소), `index` (요청 인덱스, 0부터 시작)
* **반환값**
  * `withdrawableBlockNumber`: 인출이 가능해지는 블록 번호 (예: `22579548`)
  * `amount`: 해당 인덱스에서 요청된 수량 (Ray 단위, 예: `10000000000000000000000000000`)
  * `processed`: 해당 요청이 이미 인출 또는 재스테이킹되었는지 여부

{% hint style="info" %}
재스테이킹 또는 인출 시에는 현재 대기 중인 요청만 확인하면 됩니다. `numRequests()`로 전체 건수를 확인한 뒤, `withdrawalRequest`를 가장 높은 인덱스부터 순서대로 내려가며 조회하세요(예: `numRequests`가 4를 반환하면 인덱스 3, 2, 1, … 순으로 확인).

`withdrawableBlockNumber`가 현재 블록 번호 이하이고 `processed`가 `false`인 요청이 인출 가능한 상태입니다. 해당 요청이 1건이면 `processRequests`의 `n`을 `1`로, 2건이면 `2`로 설정하세요. 여러 건이 인출 가능한 경우, **가장 오래된** 요청부터 처리됩니다. 특정 인덱스를 지정하여 처리하는 것은 불가능합니다.
{% endhint %}
