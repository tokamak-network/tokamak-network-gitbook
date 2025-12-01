---
description: This page provides a comprehensive description of the DAO candidates.
---

# DAO candidates

{% hint style="info" %}
DAO candidate registration: [link](https://github.com/tokamak-network/TokamakDAO/blob/main/docs/EN/candidate_registration.md)
{% endhint %}

### Overview Of DAO Candidates

* Anyone can become a Candidate for DAO.
* To register as a Candidate through the DAO Contract and act as a Candidate, the operator must stake a minimum amount equal to or greater than the minimum amount set by SeigManager. (The current minimum amount is 1000.1 TON, requiring a minimum stake of 1000.1 TON.)
* TON holders can stake TON to support a DAO candidate. Staking is a way to support a candidate, much like voting for their support.
* Among all DAO candidates, the top three based on the amount of TON staked are eligible to serve as DAO committee members.
* Any candidate can become a DAO Member through a challenge. (The candidate with the most stake becomes a Member.)
* Any DAO member can retire at any time using the retireMember function. If they voluntarily retire, the member who requested retirement is deemed to have no further intention of participating and is placed on a blacklist, leaving their position vacant. (After being placed on the blacklist, they can be removed from the blacklist later through an agenda.)
* Members receive WTON as a reward during their active period and can claim the reward through the claimActivityReward function.



### **How to Stake TON with DAO Candidate**

* Run staking-community-version locally using [staking-community-version](https://github.com/tokamak-network/staking-community-version).
* After running, if you access [http://localhost:3000](http://localhost:3000/), you will see the following:

<figure><img src="../../.gitbook/assets/image (395).png" alt=""><figcaption></figcaption></figure>

* Click the Connect wallet button to connect to your wallet.
* After connecting, candidates available for staking will appear as shown below.

<figure><img src="../../.gitbook/assets/image (396).png" alt=""><figcaption></figcaption></figure>

* You can stake using TON or WTON by clicking on one of the following Candidates and then seeing the screen below.

<figure><img src="../../.gitbook/assets/image (397).png" alt=""><figcaption></figcaption></figure>



### **DAO Candidate Member Check**

* Run dao-community-version locally using [sample-1](https://github.com/tokamak-network/dao-community-version/tree/main/sample-1) of dao-community-version.
* After running, if you access [http://localhost:3000/](http://localhost:3000/), you will see the following

<figure><img src="../../.gitbook/assets/image (398).png" alt=""><figcaption></figcaption></figure>

* You can check the members by clicking the view DAO Committee Members button.

<figure><img src="../../.gitbook/assets/image (399).png" alt=""><figcaption></figcaption></figure>

