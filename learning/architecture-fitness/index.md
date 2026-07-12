---
layout: default
title: Architecture Fitness 학습 퀴즈
---

# Architecture Fitness 학습 퀴즈

앞으로 만드는 어떤 서비스에서도 구조와 성능의 적합성을 스스로 판단하기 위한 복습 자료다.
Lighthouse는 질문을 구체화하는 사례일 뿐이며, 특정 서비스의 코드나 용어를 암기하는 것이 목표가
아니다.

## 학습 순서

1. [핵심 판단 퀴즈](core) — evidence, owner, condition과 snapshot, 단일 점수 금지
2. [Q1: 제품과 기술의 정합](q1) — Promise, outcome, architecture decision
3. [Q2: 거시 구조](q2) — 책임 있는 경계, topology, 핵심 실행 경로

각 문제는 먼저 자신의 말로 답한 뒤 `정답·판단 기준`을 연다. 틀린 문제가 있으면 전체 내용을 다시
읽기보다 해당 개념 하나만 복습한다.

## 반복해서 사용할 질문

```text
무엇을 약속했는가?
누가 상태와 정책을 소유하는가?
실제 코드와 runtime은 그 약속을 강제하는가?
어떤 evidence로 확인했는가?
확인하지 못했다면 unknown, 불일치가 확인됐다면 degraded인가?
```

원본 학습 프로젝트: `corca/architecture-fitness`
