---
description: DAO 후보자에 대한 전체적인 설명을 하는 페이지 입니다.
---

# DAO candidates

{% hint style="info" %}
DAO candidate 등록 : [link](https://github.com/tokamak-network/TokamakDAO/blob/main/docs/KR/candidate_registration.md)
{% endhint %}

### Overview Of DAO Candidates

* DAO의 Candidate는 누구나 될 수 있습니다.
* DAO Contract를 통해서 Candidate로 등록 후 Candidate로써 역할을 하기 위해서는 SeigManager의 minimumAmount값 이상으로 Candidate에 operator가 staking해야합니다. (현재의 minimumAmount값은 1000.1 TON으로 1000.1 TON이상 staking을 하여야합니다.)
* TON 홀더들은 DAO의 Candidate에게 TON을 Staking할 수 있습니다. 스테이킹은 마치 지지 투표처럼 후보자를 지원하는 방식입니다.
* 전체 DAO 후보자 (candidate) 중에서, staking된 TON 물량을 기준으로 상위 3명이 DAO 위원회 멤버로 활동 할 수 있는 권한이 있습니다.
* DAO의 Member는 DAO의 Candidate라면 누구나 challenge를 통해 Member가 될 수 있습니다. (Candidate의 Staking이 더 많이 되어있는 Candidate가 Member가 됩니다.)
* DAO의 Member는 언제든 retireMember함수를 통해 retire할 수 있고 자진해서 retire하게 되면 retire를 신청한 Member는 더 이상 활동의 의지가 없는 것으로 판단되어서 blacklist에 등록되고 해당 Member자리는 공석이 됩니다. (blacklist에 등록된 후에 추후 아젠다를 통해서 blacklist에서 제외 가능합니다.)
* Member는 활동하는 기간동안 reward로 WTON을 받게되며 claimActivityReward함수를 통해서 reward를 claim할 수 있습니다.



### **DAO Candidate에게 TON을 Staking하는 방법**

* [staking-community-version](https://github.com/tokamak-network/staking-community-version)을 이용하여 staking-community-version을 local에서 실행합니다.
* 실행 후 [http://localhost:3000/](http://localhost:3000/) 에 접속하면 아래와 같이 표시됩니다.

<figure><img src="../../.gitbook/assets/image (400).png" alt=""><figcaption></figcaption></figure>

* Connect wallet 버튼을 클릭하여서 자신의 지갑에 연결해줍니다.
* 연결 후 아래와 같이 Staking이 가능한 Candidate들이 나옵니다.

<figure><img src="../../.gitbook/assets/image (401).png" alt=""><figcaption></figcaption></figure>

* 다음 중 하나의 Candidate를 클릭하여서 아래의 하면이 나오면 TON 또는 WTON을 이용하여서 Staking할 수 있습니다.

<figure><img src="../../.gitbook/assets/image (402).png" alt=""><figcaption></figcaption></figure>



### **DAO Candidate의 Member 확인**

* dao-community-version의 [sample-1](https://github.com/tokamak-network/dao-community-version/tree/main/sample-1)을 이용하여서 dao-community-version을 local에서 실행합니다.
* 실행 후 [http://localhost:3000/](http://localhost:3000/) 에 접속하면 아래와 같이 표시됩니다.

<figure><img src="../../.gitbook/assets/image (411).png" alt=""><figcaption></figcaption></figure>

* view DAO Committee Members 버튼을 클릭하면 Member를 확인할 수 있습니다.

<figure><img src="../../.gitbook/assets/image (412).png" alt=""><figcaption></figcaption></figure>



