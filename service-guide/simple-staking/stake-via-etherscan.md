---
description: 이더스캔에서 DAO 후보(운영자)에게 TON 또는 WTON을 직접 스테이킹합니다.
---

# 이더스캔으로 스테이킹하기

**TON** 컨트랙트를 통해 TON을 스테이킹하거나, **WTON** 컨트랙트를 통해 WTON을 스테이킹할 수 있습니다. 두 경우 모두 `approveAndCall`이 승인과 스테이킹을 단일 트랜잭션으로 처리하므로, 별도의 `approve`는 필요하지 않습니다.

* TON 컨트랙트 (Write): [0x2be5e8c109e2197D077D13A82dAead6a9b3433C5](https://etherscan.io/address/0x2be5e8c109e2197D077D13A82dAead6a9b3433C5#writeContract)
* WTON 컨트랙트 (Write): [0xc4A11aaf6ea915Ed7Ac194161d2fC9384F15bff2](https://etherscan.io/address/0xc4A11aaf6ea915Ed7Ac194161d2fC9384F15bff2#writeContract)

<figure><img src="../../.gitbook/assets/staking-etherscan-stake-write.png" alt=""><figcaption><p>컨트랙트의 Write 탭에서 사용 가능한 함수 목록을 확인할 수 있습니다</p></figcaption></figure>

## TON 스테이킹 — `approveAndCall`

[`approveAndCall(address spender, uint256 amount, bytes data)`](https://etherscan.io/address/0x2be5e8c109e2197D077D13A82dAead6a9b3433C5#writeContract) — TON을 스테이킹 컨트랙트에 승인(approve)하고, 선택한 레이어2 운영자에게 단일 트랜잭션으로 스테이킹합니다.

* **파라미터**
  * `spender`: WTON 주소 `0xc4A11aaf6ea915Ed7Ac194161d2fC9384F15bff2`
  * `amount`: 스테이킹할 TON 수량 (18 decimals, Wei 단위)
  * `data`: DepositManager 주소와 스테이킹 대상 운영자 주소를 이어 붙인 값으로, 각각 32바이트로 패딩됩니다

**`data` 파라미터에 대하여**

* `data`는 DepositManager 주소(`0x0b58ca72b12f01fc05f8f252e226f3e2089bd00e`, 고정값)와 스테이킹 대상 운영자 주소(가변값)를 순서대로 각각 32바이트로 인코딩한 값입니다.
* DepositManager 주소는 변경되지 않으며, 운영자 주소만 바꾸면 됩니다.
* 예시 (운영자 `0xF078AE62eA4740E19ddf6c0c5e17Ecdb820BbEe1`):

```
0x0000000000000000000000000b58ca72b12f01fc05f8f252e226f3e2089bd00e000000000000000000000000F078AE62eA4740E19ddf6c0c5e17Ecdb820BbEe1
```

* 앞 32바이트: DepositManager 주소
* 뒤 32바이트: 스테이킹 대상 운영자 주소

> 다른 운영자에게 스테이킹하려면 `data`에서 운영자 부분만 변경하면 됩니다.

## WTON 스테이킹

WTON은 두 가지 방법으로 스테이킹할 수 있습니다.

### 방법 1 — `approveAndCall`

[`approveAndCall(address spender, uint256 amount, bytes data)`](https://etherscan.io/address/0xc4A11aaf6ea915Ed7Ac194161d2fC9384F15bff2#writeContract) — WTON을 승인하고, 선택한 운영자에게 단일 트랜잭션으로 스테이킹합니다.

* **파라미터**
  * `spender`: DepositManager 주소 `0x0b58ca72b12f01fc05f8f252e226f3e2089bd00e`
  * `amount`: 스테이킹할 WTON 수량 (27 decimals, Ray 단위)
  * `data`: 스테이킹 대상 운영자 주소를 32바이트로 인코딩한 값

**`data` 파라미터에 대하여**

* `data`는 스테이킹 대상 운영자 주소(가변값)를 32바이트로 인코딩한 값입니다.
* 예시 (운영자 `0xF078AE62eA4740E19ddf6c0c5e17Ecdb820BbEe1`):

```
0x000000000000000000000000F078AE62eA4740E19ddf6c0c5e17Ecdb820BbEe1
```

### 방법 2 — `approve` 후 `deposit`

`approve`와 `deposit`을 두 개의 별도 트랜잭션으로 실행하면 가스비가 절감될 수 있습니다.

1. WTON 컨트랙트에서 [`approve(address spender, uint256 amount)`](https://etherscan.io/address/0xc4A11aaf6ea915Ed7Ac194161d2fC9384F15bff2#writeContract) 실행
   * `spender`: DepositManager 주소 `0x0b58ca72b12f01fc05f8f252e226f3e2089bd00e`
   * `amount`: 스테이킹할 WTON 수량 (27 decimals, Ray 단위)
2. DepositManager에서 [`deposit(address layer2, uint256 amount)`](https://etherscan.io/address/0x0b58ca72b12f01fc05f8f252e226f3e2089bd00e#writeProxyContract) 실행 (Write as Proxy)
   * `layer2`: 스테이킹 대상 운영자 주소
   * `amount`: 스테이킹할 WTON 수량 (27 decimals, Ray 단위)

{% hint style="info" %}
어떤 운영자 주소를 사용해야 할지 모르겠다면, [운영자 정보 확인](check-operator-information.md) 페이지에서 등록된 운영자 목록을 조회하고 원하는 운영자를 확인하세요.
{% endhint %}
