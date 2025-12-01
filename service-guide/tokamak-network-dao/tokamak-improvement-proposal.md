---
description: >-
  Tokamak DAO는 제안을 체계적으로 다루고, 커뮤니티가 적극적으로 참여할 수 있도록 Tokamak Improvement
  Proposal(TIP) 라이프사이클을 운영합니다.
---

# Tokamak Improvement Proposal

## 1. **RFC(Request for Comment)의 작성**

RFC 작성은 DAO github의 [Discussion-RFC](https://github.com/tokamak-network/tokamak-dao-contracts/discussions/categories/discussion-rfc) 채널에서 작성할 수 있으며, 작성된 RFC은 Discord 내 [전용 채널](https://discord.com/channels/696270789472682034/1430107114071789620)( `#💡｜proposal-rfc`)과 [X](https://x.com/Tokamak_Network/), [Telegram](https://t.me/tokamak_network)에서 공유됩니다. 아래는 RFC 작성 시 포함해야 할 주요 요소입니다.

{% hint style="info" %}
RFC로 작성된 Sample은 [링크](https://github.com/tokamak-network/tokamak-dao-contracts/discussions/11)에서 확인가능합니다.
{% endhint %}

### 1-1. 필수 요소

1. **제목 및 작성자 (Title And Author)**
   * 제안의 제목과 작성자(또는 팀명)를 명확히 기재합니다.
   * 필요할 경우 Tokamak DAO 제안 번호나 태그를 함께 포함할 수 있습니다.
   * 예: _“거버넌스 보상 구조 개선”_
2. **요약 (Summary)**
   * 제안의 핵심 내용을 두세 문장으로 간결하게 정리합니다.
   * 무엇을 제안하는지 한눈에 파악할 수 있도록 작성합니다.
3. **배경 및 동기 (Background & Motivation)**
   * 제안이 나오게 된 배경과 문제 인식을 서술합니다.
   * 현재 어떤 문제가 있는지, 그리고 이 제안이 Tokamak 생태계에 어떤 가치를 제공하는지 명확히 설명합니다.
4. **세부 제안 내용 (Specification)**
   * 제안을 구현하거나 실행하기 위한 구체적 계획을 단계별로 작성합니다.
   * 스마트 컨트랙트 변경이 필요한 경우, 어떤 부분을 어떻게 수정/추가하는지 명시합니다.
   * 필요 시 타 프로젝트의 유사 사례를 참고하여 스펙, 변경사항, 이전 버전과의 호환성 등을 함께 기술합니다.
5. **예상 효과 및 영향 (Expected Impact)**
   * 제안이 실행되었을 때 기대되는 효과를 설명합니다.
   * 긍정적 영향(예: 프로토콜 성능 향상, 참여 증가)뿐 아니라 잠재적 리스크나 부작용도 함께 고려합니다.

### 1-2. 보조 요소

1. **이전 버전과 호환성 (Backwards Compatibility)**
   * 제안이 기존 시스템과 어떻게 호환되는지, 필요한 기술적 변경사항과 예상 개발 일정을 간략히 설명합니다.
2. **참조 구현 (Reference Implementation)**
   * 제안된 기능을 다른 Contract에서 어떻게 활용할 수 있는지 예시를 포함해 설명합니다.
3. **보안 고려 사항 (Security Considerations)**
   * 제안 또는 코드 변경으로 인해 고려해야 할 보안 요소를 정리합니다.
4. **추가 자료 및 참고문헌 (Additional Materials and References)**
   * 제안의 타당성을 뒷받침하는 외부 자료, 참고 문서, 기술 명세서, 유사 사례 등을 포함합니다.

#### **RFC 논의 기간**

RFC가 제출되면 **최소 7일간 커뮤니티 의견 수렴 기간**을 거칩니다.\
제안자는 이 기간 동안 제기된 의견을 반영하여 초안을 자유롭게 수정할 수 있습니다.

이 단계는 제안의 완성도를 높이고, 커뮤니티 합의를 이끌어내며, 불필요한 오해를 줄이는 데 큰 도움이 됩니다.\
또한 RFC 생성 시 Discord, X, Telegram 등을 통해 홍보하여 더 많은 사용자들이 제안을 확인하고 거버넌스에 참여할 수 있도록 유도합니다.

***





