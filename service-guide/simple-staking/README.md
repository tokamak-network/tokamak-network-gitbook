---
description: 토카막 네트워크가 제공하는 스테이킹 시스템을 소개합니다.
---

# Simple staking

{% hint style="warning" %}
**공식적으로 호스팅되던 스테이킹 웹사이트는 운영이 중단되었습니다.**

스테이킹 자체는 완전히 온체인에서 스마트 컨트랙트를 통해 계속 동작합니다. 다음 두 가지 방법으로 이용할 수 있습니다.

* **이더스캔(Etherscan)** — 스테이킹 컨트랙트와 온체인에서 직접 상호작용합니다. 프론트엔드와 무관하게 동작하며 가장 신뢰할 수 있는 방법입니다. [이더스캔으로 상호작용하기](interact-via-etherscan.md)를 참고하세요.
* **커뮤니티 에디션(Community edition)** — 커뮤니티가 유지보수하는 스테이킹 dApp으로, 직접 호스팅하거나 커뮤니티가 호스팅하는 인스턴스를 이용할 수 있습니다(아래 **이용 방법** 참고).
{% endhint %}

{% hint style="info" %}
**리소스**

* 문서 허브: [https://github.com/tokamak-network/TokamakStaking](https://github.com/tokamak-network/TokamakStaking)
* 컨트랙트: [https://github.com/tokamak-network/ton-staking-v2](https://github.com/tokamak-network/ton-staking-v2)
* 컨트랙트 주소: [link](https://docs.tokamak.network/home/service-guide/simple-staking/contract-addresses)
* 감사 보고서: [DAO & TON Staking v2 audit report](https://medium.com/tokamak-network/dao-ton-staking-v2-audit-report-2fa7bb1a9291)
* 지난 공지: [Medium (staking)](https://medium.com/tokamak-network/search?q=staking)
{% endhint %}

### 1. 특징

토카막 네트워크의 스테이킹서비스는 스테이킹 과정을 통해 DAO 위원회(committee) 맴버 3인이 선정되는 것이 특징입니다. 구체적인 특징은 다음과 같습니다.&#x20;

* 첫째, DAO 후보자에게 TON 또는 WTON을 스테이킹을 해서 일정한 스테이킹 보상을 거둘 수 있습니다.&#x20;
* 둘째, 스테이킹 물량의 순서대로 상위 DAO 후보자 3명은 DAO committee에서 각종 의사결정을 담당하는 맴버로 활동할 수 있습니다.

### 2. 이용 방법

공식 웹사이트가 더 이상 호스팅되지 않으므로, 아래 접근 방법 중 하나를 선택하세요.

<table><thead><tr><th width="220">방법</th><th>설명</th><th>언제 사용하나요</th></tr></thead><tbody><tr><td><strong>이더스캔(Etherscan)</strong></td><td>이더스캔의 "Read/Write Contract" 탭에서 스테이킹 컨트랙트 함수를 직접 호출합니다.</td><td>항상 이용 가능하며 프론트엔드에 의존하지 않습니다. 스테이킹, 언스테이킹, 재스테이킹, 인출, 보상 수령에 권장됩니다. <a href="interact-via-etherscan.md">이더스캔으로 상호작용하기</a>를 참고하세요.</td></tr><tr><td><strong>커뮤니티 에디션 (직접 호스팅)</strong></td><td>오픈소스 스테이킹 프론트엔드를 저장소 가이드에 따라 직접 실행합니다.</td><td>익숙한 dApp UI를 직접 호스팅해서 사용하고 싶을 때. 저장소: <a href="https://github.com/tokamak-network/staking-community-version">staking-community-version</a>.</td></tr><tr><td><strong>커뮤니티 에디션 (커뮤니티 호스팅)</strong></td><td>커뮤니티 구성원이 공개 인스턴스를 호스팅합니다.</td><td>편의를 위해, 아래 위험을 감수할 수 있다면 사용합니다. 인스턴스: <a href="https://staking-community-version.vercel.app/">staking-community-version.vercel.app</a>.</td></tr></tbody></table>

{% hint style="danger" %}
커뮤니티 호스팅 링크는 커뮤니티 구성원이 운영하며 **토카막 네트워크가 보증하지 않습니다.** 사용에 따른 책임은 본인에게 있으며, 토카막 네트워크는 해당 링크에 대해 어떠한 보증이나 지원도 제공하지 않습니다. 확신이 서지 않으면 커뮤니티 에디션을 직접 호스팅하거나 이더스캔을 직접 사용하세요. 트랜잭션에 서명하기 전에 반드시 [컨트랙트 주소](https://docs.tokamak.network/home/service-guide/simple-staking/contract-addresses) 페이지에서 컨트랙트 주소를 확인하세요.
{% endhint %}

아래 페이지들([Stake](stake.md), [Withdraw](withdraw.md), [Staking reward](staking-reward.md))은 스테이킹 dApp 인터페이스를 기준으로 설명합니다. 커뮤니티 에디션도 동일한 인터페이스를 사용하므로, 직접 호스팅하거나 커뮤니티 호스팅 인스턴스를 사용할 때 이 설명을 그대로 적용할 수 있습니다.

### 3. 페이지 구성

<figure><img src="../../.gitbook/assets/image (322).png" alt="" width="375"><figcaption><p>스테이킹 페이지의 초도화면</p></figcaption></figure>

1. **Home**

* Connect Wallet 버튼을 클릭하여 메타마스크(Metamask) 지갑 또는 트레저(Trezor) 지갑을 연결합니다.
* 파란색 그래프는 스테이커가 토카막 네트워크에 매일 스테이킹한 금액을, 회색 그래프는 매일 실제 APY를 보여줍니다. 그래프 위에 마우스를 가져가면 일일 총 스테이킹 금액과 실제 APY를 확인할 수 있습니다.

2. **Staking**

* 스테이킹 페이지에서 DAO 후보에 대한 정보를 확인할 수 있습니다. 지갑을 연결한 경우 각 운영자의 오른쪽에 있는 파란색 화살표를 클릭하면 DAO 후보에 대한 자세한 정보와 스테이킹 버튼을 볼 수 있습니다. 지갑을 연결하지 않은 상태에서는 운영자의 세부 정보만 볼 수 있습니다.
* 지갑이 연결되면 Staking 버튼을 클릭하여 귀하가 보유한 TON(혹은 WTON)을 특정 DAO 후보자에게 스테이킹 할 수 있습니다.&#x20;

3. **Account**

* Account 페이지는 귀하가 보유한 자산에 대한 정보를 제공합니다.
* 본 서비스를 이용하려면 먼저 우상단의 지갑연결을 통해 로그인을 해야 합니다.&#x20;
* 제공되는 정보는 아래와 같습니다
  * Total Staked: 스테이킹된 TON의 합계입니다.&#x20;
  * Pending Withdrawal: Unstake 된 TON의 합계액입니다. 이 금액은 DAO 후보가 설정한 출금 지연 기간(기본값은 93,046블록 경과후, 약 14일)이 지난 후에만 출금할 수 있습니다.&#x20;
  * History: 스테이킹 관련 거래 내역을 보여줍니다. 이 정보에는 트랜잭션 해시, 관련 DAO후보, 유형, 금액, 실행시각이 포함됩니다.&#x20;

### **4. 로그인**

스테이킹 및 계정 정보와 같은 일부 기능에 액세스하려면 지갑연결을 통해 로그인을 먼저 해야 합니다. 화면 오른쪽 상단의 지갑 연결 버튼을 클릭해 지갑 연결 방법을 선택할 수 있습니다.

1. Metamask 연결로 로그인하기

* 이더리움 메인넷 네트워크에 연결되어 있는지 확인합니다. 그런 다음 Connect Wallet 버튼을 클릭합니다.&#x20;
* 팝업창에서 Metamask 아이콘을 클릭합니다.&#x20;
* 브라우저 확장 프로그램 목록에서 Metamask 아이콘을 클릭하고 서비스에 연결할 계정을 선택합니다.
* 메타마스크 설치방법은 아래를 참고하여 주십시오

<details>

<summary>메타마스크 설치 (Install Metamask) 방법</summary>

1. 메타마스크로 당사 서비스에 연결하려면 [Google Chrome](https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn) 또는 [Firefox](https://addons.mozilla.org/en-US/firefox/addon/ether-metamask/)브라우저에 메타마스크 확장 프로그램을 설치하세요. 이미 메타마스크 지갑에 TON이 있는 경우 해당 지갑에 로그인하거나 이미 TON이 있는 계정(account)을 가져오세요.

<img src="../../.gitbook/assets/image (1) (1) (1).png" alt="Metamask in Google Chrome Extenstion" data-size="original">

2. 지갑에 TON을 추가하려면 이더리움 메인넷 네트워크에 연결되어 있는지 확인하세요. 그런 다음 토큰 추가 버튼을 클릭합니다.
3. Custom Token 탭을 클릭합니다.&#x20;
4. 아래의 컨트랙트 주소를 입력합니다. 토큰 심볼과 소수 자릿수는 자동으로 채워집니다.&#x20;
   * Token Contract Address: 0x2be5e8c109e2197D077D13A82dAead6a9b3433C5
5. Next 버튼을 클릭합니다.&#x20;
6. 토큰 추가 버튼을 눌러 계정에 TON을 추가합니다.

<img src="../../.gitbook/assets/image (4) (1).png" alt="How to add TON in your wallet" data-size="original">

</details>

2. Trezor 연결로 로그인하기

* Trezor 지갑을 연결할 수 있습니다.&#x20;

<figure><img src="../../.gitbook/assets/image (324).png" alt="" width="188"><figcaption><p>암호화폐지갑 연결을 통한 로그인</p></figcaption></figure>
