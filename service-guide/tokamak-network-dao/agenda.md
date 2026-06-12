---
description: 제안된 안건에 대하여 DAO 위원회의 3인 멤버는 다수결에 의한 투표를 실시하게 됩니다.
---

# Agenda

{% hint style="warning" %}
투표는 DAO 위원회 멤버 3인만 참여할 수 있습니다.

* 일반 유저들은 자신이 지지하는 멤버에게 [스테이킹](../simple-staking/README.md)을 실시하여 간접적으로 참여하게 됩니다.&#x20;
{% endhint %}



### Agenda Rules

* Propose Rules
  * DAO의 Agenda 생성은 누구나 할 수 있습니다.
  * Agenda를 생성할때 Agenda 생성자는 Agenda Create Fee로 10TON을 지불해야하고 해당 Agenda Create Fee는 Burn을 진행합니다.
  * Agenda의 내용은 Tokamak생태계에 관련된 모든 내용을 Propose할 수 있습니다.
* Vote Rule
  * Member가 Agenda에 대해서 투표할 수 있으며 기권,찬성,반대로 투표할 수 있습니다.
  * 3명의 Member 중 2명이 찬성하면 Agenda는 통과되게 됩니다. (투표 값들은 투표 중에는 변경될 수 있습니다.)
  * 투표기간 동안 투표가 되지않은 표들은 기권표로 결정됩니다.
  * Agenda가 생성되고 투표가 시작되기전 멤버가 변경되면 변경된 멤버가 투표할 수 있습니다.
  * 투표가 시작되고 난 뒤 멤버가 변경되어도 이전 멤버만 투표할 수 있습니다.
* Vote Period
  * 기간은 Notice Period, Voting Period, Execute Period로 기간이 나누어집니다.
  * Notice Period의 최소기간은 16일이고 Voting Period의 최소기간은 2일이다.
  * Notice Period와 Voting Period의 정확한 값은 Agenda가 생성될 때 결정되고 최소기간과 같거나 더 커야합니다.
  * Execute Period의 기간은 7일로 고정되어 있습니다.
  * Agenda가 생성되고 Notice Period가 지난 후 누군가 투표를 진행해야 Voting Period와 Execute Period가 결정됩니다.
  * 투표가 통과된 Agenda의 Execute Period에서 누구나 해당 Agenda에 대한 Execute가 가능합니다.



### Agenda Proposal

* dao-community-version의 [sample-1](https://github.com/tokamak-network/dao-community-version/tree/main/sample-1)을 이용하여서 dao-community-version을 local에서 실행합니다.
* 실행 후 [http://localhost:3000/](http://localhost:3000/) 에 접속하면 아래와 같이 표시됩니다.

<figure><img src="../../.gitbook/assets/image (398).png" alt=""><figcaption></figcaption></figure>

*   Agenda 탭을 클릭하면 아래와 같은 화면이 나옵니다.

    <figure><img src="../../.gitbook/assets/image (399).png" alt=""><figcaption></figcaption></figure>
*   New proposal 버튼을 클릭하면 아래와 같은 화면이 나옵니다.

    <figure><img src="../../.gitbook/assets/image (409).png" alt=""><figcaption></figcaption></figure>
* Proposal에 관련된 내용을 채우고 Add Action 버튼을 클릭합니다.

<figure><img src="../../.gitbook/assets/image (410).png" alt=""><figcaption></figcaption></figure>

* 실행하고자 하는 주소와 함수와 함수값들을 세팅하고 Add Action 버튼을 클릭한 후 Preview & Submit 버튼을 클릭합니다.

<figure><img src="../../.gitbook/assets/image (404).png" alt=""><figcaption></figcaption></figure>

* Submit DAO Agenda 버튼을 클릭해서 Agenda를 최종 제출합니다.



### Agenda Status

<figure><img src="../../.gitbook/assets/image (405).png" alt=""><figcaption></figcaption></figure>

* 위의 Agenda 화면에서 View Details 버튼을 클릭합니다.

<figure><img src="../../.gitbook/assets/image (406).png" alt=""><figcaption></figcaption></figure>

* 위의 스크린샷처럼 Agenda에 대한 정보를 확인할 수 있습니다.



### Agenda Vote

<figure><img src="../../.gitbook/assets/image (407).png" alt=""><figcaption></figcaption></figure>

* 위의 Agenda 화면에서 View Details 버튼을 클릭합니다.

<figure><img src="../../.gitbook/assets/image (408).png" alt=""><figcaption></figcaption></figure>

* Agenda의 상태가 투표기간이고 연결된 지갑이 Member라면 Vote버튼을 클릭해서 투표가능합니다. (투표는 찬성, 반대, 기권으로 진행할 수 있습니다.)
