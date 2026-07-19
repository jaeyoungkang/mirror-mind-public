---
layout: default
title: Architecture Fitness 학습
---

# Architecture Fitness 학습

앞으로 만드는 서비스에서 구조와 성능의 적합성을 판단하기 위한 학습 자료다. Lighthouse 사례는 각
질문을 구체적으로 보여 준다. 여기서 익힌 판단 기준을 다른 서비스에 적용하는 데 초점을 둔다.

## 학습 순서

1. [핵심 판단 퀴즈](core) — evidence, owner, condition과 snapshot, 단일 점수 금지
2. [Q1: 제품과 기술의 정합](q1) — Promise, outcome, architecture decision
3. [Q2: 거시 구조](q2) — 책임 있는 경계, topology, 핵심 실행 경로
4. [Q3: 확장성과 부하](q3) — workload envelope, SLO break point, queue, 입력 amplification
5. [Q4: 기술 단위와 변경 결](q4) — 책임 있는 hop, chokepoint, change propagation
6. [Q5: 캐시 전략](q5) — owner, key scope, freshness, invalidation, stampede control
7. [종합: Architecture Fitness 전문성 모델](professional-model) — Q1–Q5 통합, 설계와 지속 관리

## Lighthouse 백엔드 리뷰

Lighthouse 코드를 따라가며 제품 보장부터 API, DB, 동시성, 실패 복구와 운영 증거까지 검토한다.
주니어 백엔드 개발자가 실제 프로젝트를 읽는 순서에 맞췄다.

1. [백엔드 프로젝트 리뷰 가이드](lighthouse-backend-review-guide)
2. [인터랙티브 퀴즈](lighthouse-backend-review-quiz.html) — 46개 실전 문항, 힌트와 브라우저 진도 저장
3. [퀴즈 해설](lighthouse-backend-review-quiz-reference) — 전체 문항과 판단 기준 참고본

각 문제는 먼저 자신의 말로 답한 뒤 `정답·판단 기준`을 연다. 틀린 문제가 있으면 전체 내용을 다시
읽기보다 해당 개념 하나만 복습한다.

전문성 모델은 Q1부터 Q5까지의 관계를 설명한다. 퀴즈 학습을 마친 뒤 설계자와 관리자의 실무 기준을
정리할 때 사용한다.

## 반복해서 사용할 질문

```text
무엇을 약속했는가?
누가 상태와 정책을 소유하는가?
실제 코드와 runtime은 그 약속을 강제하는가?
어떤 evidence로 확인했는가?
확인하지 못했다면 unknown, 불일치가 확인됐다면 degraded인가?
```

원본 학습 프로젝트: `corca/architecture-fitness`
