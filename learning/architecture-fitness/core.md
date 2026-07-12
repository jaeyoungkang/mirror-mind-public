---
layout: default
title: Architecture Fitness 핵심 판단 퀴즈
---

# Architecture Fitness 핵심 판단 퀴즈

- 문항: 5개
- 권장 시간: 10분
- 답변 길이: 문제마다 두 문장 이내

## 1. 구현과 outcome

논문 검색 acceptance test는 모두 통과했다. 그러나 PDF 열기, 라이브러리 추가, 논문을 고르는 시간은
측정하지 않는다.

**지금 증명된 것과 아직 증명되지 않은 것을 하나씩 적어라.**

<details markdown="1">
<summary>정답·판단 기준</summary>

검색 기능이 선언한 구현 계약을 충족했다는 사실은 증명됐다. 연구자가 유용한 논문을 더 잘 또는 더
빨리 골랐다는 사용자 outcome은 아직 증명되지 않았다.

PDF 열기와 라이브러리 추가는 강도가 다른 proxy다. 검색부터 첫 행동까지의 시간과 전환율을 측정하되,
“더 빨라졌다”고 말하려면 비교 가능한 기준선이나 cohort가 필요하다.

</details>

## 2. State owner와 verdict

검색 조건의 최종 기준을 URL로 정했다.

- 상황 A: 실제 코드가 URL을 기준으로 동작하는지 evidence가 없다.
- 상황 B: URL은 `q=agent-memory`인데 코드가 client store의 `q=graph-rag`를 최종 검색어로 사용한다.

**상황 A와 B를 각각 `unknown` 또는 `degraded`로 판정하라.**

<details markdown="1">
<summary>정답·판단 기준</summary>

- A: `unknown` — desired policy는 있지만 observed evidence가 없다.
- B: `degraded` — URL을 최종 기준으로 삼는 결정과 실제 입력의 불일치가 확인됐다.

State owner는 담당 개발자가 아니라 값이 충돌할 때 따를 최종 기준과 상태 전이 권한이다.

</details>

## 3. Condition과 snapshot

어제와 오늘 동일한 `/search?q=graph-rag`를 열었지만 provider index가 바뀌어 결과 순서가 달라졌다.

**URL이 검색 조건의 owner라는 결정이 깨진 것인가? 정확히 같은 결과를 복원하려면 무엇이 필요한가?**

<details markdown="1">
<summary>정답·판단 기준</summary>

결정이 깨진 것은 아니다. URL은 재실행할 condition을 식별하지 과거 result snapshot의 동일성을
약속하지 않는다. 정확한 복원에는 결과 목록과 생성 당시 source·context를 묶은 snapshot artifact,
별도 identity, 저장·접근 정책이 필요하다.

</details>

## 4. Policy와 측정 장치

운영 policy는 “사용 가능한 결과가 하나 이상 있어야 준비 완료”라고 선언한다. Load harness는 HTTP
2xx만 확인해 결과 없는 degraded 화면도 green으로 처리한다.

**선언과 harness의 일치 여부는 무엇인가? 운영 기준 자체의 적절성도 이 정보만으로 판정할 수 있는가?**

<details markdown="1">
<summary>정답·판단 기준</summary>

선언과 harness의 불일치는 재현됐으므로 `degraded`다. “결과가 하나 이상이어야 한다”는 기준 자체는
정상적인 빈 결과와 provider 장애를 어떻게 구분할지 evidence가 없으므로 `unknown`이다.

</details>

## 5. 단일 종합 점수

판정이 `Q1 healthy, Q2 degraded, Q3 unknown, Q4 healthy, Q5 healthy`다. 팀은 평균 82점으로 바꿔
“전체 healthy”라고 보고하려 한다.

**왜 Architecture Fitness 원칙에 어긋나는가?**

<details markdown="1">
<summary>정답·판단 기준</summary>

평균은 Q2의 확인된 불일치와 Q3의 evidence 부재를 다른 healthy 항목으로 상쇄해 가린다. Lens별 verdict,
원인, owner를 그대로 보존해야 한다.

</details>

[다음: Q1 제품과 기술의 정합](q1)
