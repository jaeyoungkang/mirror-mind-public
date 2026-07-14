---
layout: default
title: Architecture Fitness 전문성 모델
---

# Architecture Fitness 전문성 모델

Q1부터 Q5까지의 학습을 하나의 실무 모델로 묶는다. 이 모델은 아키텍처 설계와 지속적인 관리에 필요한
능력을 함께 다룬다. 설계자는 제품 약속을 구조와 성능 기준으로 옮긴다. 관리자는 변화가 생길 때도 그
기준이 지켜지는지 증거로 확인한다.

## 전문성의 정의

아키텍처 전문가는 제품 약속에 owner와 구조적 제약을 연결한다. 실제 코드와 runtime을 관찰하고, 선언한
기준과 비교한다. 확인한 결과는 `healthy`, `degraded`, `unknown`으로 구분하며 다음 행동과 재검토 시점을
정한다.

좋은 설계는 중요한 약속을 올바른 경계에서 강제한다. 좋은 관리는 그 사실을 반복해서 확인할 수 있게
만든다.

## 다섯 가지 질문

Q1부터 Q5까지는 서로 다른 실패를 찾는다. 한 질문의 결과가 다른 질문의 결과를 대신하지 않는다.

| 질문 | 전문가가 확인하는 내용 | 관리 대상 |
| --- | --- | --- |
| Q1 | 서비스가 지키려는 약속은 무엇이며 의미와 상태는 누가 결정하는가 | Promise, capability, owner, state authority, outcome |
| Q2 | 그 결정을 어떤 경계와 의존성, topology, 실행 경로로 강제하는가 | 권한 경계, dependency graph, state scope, critical path |
| Q3 | 입력과 부하가 늘어날 때 어느 지점에서 약속이 깨지는가 | workload envelope, queue, tail latency, amplification, break point |
| Q4 | 책임과 복잡성을 어디에 모아 변경을 흡수하는가 | deep module, chokepoint, interface, change propagation |
| Q5 | 계산 결과를 언제까지 재사용하고 언제 폐기하는가 | cache identity, freshness, invalidation, coordination, retention |

Q1은 설계의 목적과 권위를 정한다. Q2는 그 결정을 시스템 경계에 배치한다. Q3는 부하가 늘어날 때
구조가 보이는 거동을 측정한다. Q4는 내부 복잡성과 변경 비용을 관리한다. Q5는 시간과 실행 topology를
넘어 결과를 재사용하는 조건을 정한다.

전체 흐름은 다음과 같다.

```text
Q1 의미와 권위
  → Q2 경계와 실행 구조
  → Q3 부하 증가에서의 거동
  → Q4 책임 배치와 변경 흡수
  → Q5 결과 재사용과 폐기
```

## 설계자의 일

설계자는 구현을 시작하기 전에 Promise와 architecture need를 확인한다. 누가 정책과 상태를 결정하는지
찾고, 선택한 구조가 어떤 효과와 비용을 만드는지 기록한다.

- 제품 언어를 capability, state, effect, boundary로 옮긴다.
- authority와 carrier를 구분하고 상태 충돌을 해결할 기준을 정한다.
- 호출자가 획득할 수 있는 능력을 경계에서 제한한다.
- dependency, topology, critical path를 실제 실행 흐름과 맞춘다.
- workload와 실패 조건을 시나리오로 만들고 첫 budget break point를 찾는다.
- 작은 interface 뒤에 policy와 복잡성을 모아 내부 변경을 흡수한다.
- cache source, identity, freshness, invalidation과 coordination 범위를 정한다.
- 각 결정에 반대편 비용과 재검토 trigger를 남긴다.

서비스가 지키려는 약속과 실제 failure mode가 설계 품질의 기준이 된다. 같은 패턴도 서비스의 정책과
실행 조건에 따라 다른 결과를 만든다.

## 관리자의 일

관리자는 아키텍처 결정을 현재형으로 유지한다. 문서, 코드, 테스트와 runtime evidence를 같은 결정에
연결하고, 조건이 바뀌면 검토를 다시 연다.

```text
승인된 authority
  → policy projection
  → 정확한 revision에 묶인 observation
  → evidence 검증
  → deterministic comparison
  → 사람의 결정
  → 수정·위험 수용·재검토
```

관리자는 검토 범위를 `included`, `unsupported`, `excluded`로 기록한다. 증거가 부족한 영역은
`unknown`으로 남긴다. 확인한 불일치는 `degraded`로 기록한다. 모든 필수 기준이 신뢰할 수 있는 증거와
일치할 때만 `healthy`를 사용한다.

| 상태 | 의미 |
| --- | --- |
| `healthy` | 승인된 policy와 모든 필수 evidence가 일치한다 |
| `degraded` | 신뢰할 수 있는 evidence가 policy 불일치를 확인했다 |
| `unknown` | policy, observation, coverage 또는 evidence가 부족하다 |
| validation failure | 입력 계약이 잘못되어 verdict를 계산하지 못했다 |

여러 lens의 결과를 평균 점수로 합치지 않는다. 각 결과에 owner와 다음 행동을 연결한다. `degraded`와
`unknown`이 함께 생기면 둘 다 보존한다.

## 증거를 다루는 법

각 증거는 확인할 수 있는 범위가 다르다. 정적 graph는 import와 call edge를 보여 준다. Negative guard는
새 우회 경로를 막는다. Behavior test는 timeout, retry, abort와 실패 변환을 실행한다. Runtime trace는
callback과 background lifetime처럼 정적 분석이 놓치는 경로를 보여 준다.

증거에는 source revision, 실행 command, exit code, artifact digest와 target을 연결한다. Adapter는 관측
사실을 수집한다. 비교와 verdict는 공통 evaluator가 계산한다.

## 사람과 기계의 역할

제품 또는 아키텍처 owner는 Promise, trade-off, intended boundary와 위험 수용을 승인한다. Coding
agent는 구조를 조사하고 대안과 evidence candidate를 만든다. 기계는 승인된 policy에 따라 edge, budget,
invariant와 우회 경로를 반복 검증한다.

LLM finding은 검증 전까지 `unverified` candidate로 관리한다. 정책 변경, 구조 수정, 위험 수용과 배포는
사람이 승인한다. 이 분업은 자동화의 범위와 사람 판단의 자리를 분명하게 만든다.

## 결정의 완료 기준

중요한 아키텍처 결정에는 다음 항목을 남긴다.

1. 해결하려는 Promise 또는 architecture need
2. 결정 owner와 authority source
3. 선택한 구조, 대안과 선택 근거
4. 구조적 invariant와 허용·금지 경로
5. workload 또는 변경 시나리오
6. 정적·행동·runtime evidence
7. 현재 verdict와 남은 `unknown`
8. Human decision, 반대편 비용과 재검토 trigger

비어 있는 항목은 현재 지식의 한계를 드러낸다. 담당자는 필요한 evidence와 수집 시점을 정하고 해당
영역을 `unknown`으로 관리한다.

## 전문성 단계

이 모델은 네 단계의 실무 능력을 요구한다.

| 단계 | 할 수 있는 일 |
| --- | --- |
| 의미 구성 | 제품 약속과 architecture need를 owner, state, effect, boundary로 옮긴다 |
| 구조 설계 | 경계, topology, critical path, module grain과 cache policy를 trade-off와 함께 결정한다 |
| 검증 설계 | 시나리오와 evidence를 만들고 반복 가능한 guard와 evaluator에 연결한다 |
| 지속 관리 | coverage, verdict, risk acceptance와 re-entry trigger를 운영한다 |

현재 portable core는 Q1의 state boundary, Q2의 least-authority boundary, Q3의 serialized-input budget을
부분적으로 실행한다. Q4와 Q5는 rubric으로 사용한다. 기계가 계산하는 coverage는 `unsupported`,
verdict는 `unknown`으로 남긴다. 전문가는 지식의 범위와 도구가 실제로 검증하는 범위를 함께 밝힌다.

## 마무리

Architecture Fitness는 아키텍처를 지속해서 관리하는 실무 체계를 제공한다. 중요한 약속을 경계와
시나리오에 담고, 증거를 통해 현재 상태를 확인하며, 조건이 바뀔 때 결정을 다시 연다. 이 과정을
반복할 수 있는 능력이 아키텍처 설계자와 관리자의 전문성을 만든다.

[Architecture Fitness 학습 목록으로 돌아가기](./)
