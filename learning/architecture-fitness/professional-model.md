---
layout: default
title: Architecture Fitness 전문성 모델
---

# Architecture Fitness 전문성 모델

Q1부터 Q5까지의 학습을 하나의 실무 모델로 묶는다. 이 모델은 아키텍처 설계와 지속적인 관리에 필요한
능력을 함께 다룬다. 설계자는 제품 약속을 구조와 성능 기준으로 옮긴다. 관리자는 변화가 생길 때도 그
기준이 지켜지는지 증거로 확인한다.

**읽는 법:** 실무에서 쓰는 영어 용어는 그대로 두고, 각 섹션의 `용어 풀이`에 뜻을 덧붙였다. 각
용어가 무엇을 결정하고 무엇을 확인하는지 중심으로 읽는다.

## 전문성의 정의

아키텍처 전문가는 제품 약속에 owner와 구조적 제약을 연결한다. 실제 코드와 runtime을 관찰하고, 선언한
기준과 비교한다. 확인한 결과는 `healthy`, `degraded`, `unknown`으로 구분하며 다음 행동과 재검토 시점을
정한다.

좋은 설계는 중요한 약속을 올바른 경계에서 강제한다. 좋은 관리는 그 사실을 반복해서 확인할 수 있게
만든다.

<details markdown="1">
<summary>용어 풀이</summary>

- `owner`: 기준을 승인하고 충돌할 때 최종 결정을 내리는 주체다. 작업 담당자와 다를 수 있다.
- `runtime`: 프로그램이 실제로 실행되고 있는 상태와 환경이다.
- `evidence`: 주장을 확인할 수 있는 코드 위치, 테스트 결과, 실행 기록 같은 검증 근거다.
- `verdict`: 근거를 기준과 비교해 내린 판정이다. 이 글에서는 `healthy`, `degraded`, `unknown`을 쓴다.

</details>

## 다섯 가지 질문

Q1부터 Q5까지는 서로 다른 실패를 찾는다. 한 질문의 결과가 다른 질문의 결과를 대신하지 않는다.

| 질문 | 전문가가 확인하는 내용 | 관리 대상 |
| --- | --- | --- |
| Q1 | 서비스가 지키려는 약속은 무엇이며 의미와 상태는 누가 결정하는가 | Promise, capability, owner, state authority, outcome |
| Q2 | 그 결정을 어떤 경계와 의존성, topology, 실행 경로로 강제하는가 | 권한 경계, dependency graph, state scope, critical path |
| Q3 | 입력과 부하가 늘어날 때 어느 지점에서 약속이 깨지는가 | workload envelope, queue, tail latency, amplification, break point |
| Q4 | 책임과 복잡성을 어디에 모아 변경을 흡수하는가 | deep module, chokepoint, interface, change propagation |
| Q5 | 계산 결과를 언제까지 재사용하고 언제 폐기하는가 | cache identity, freshness, invalidation, coordination, retention |

<details markdown="1">
<summary>표의 핵심 용어 풀이</summary>

- **Q1:** `Promise`는 제품이 사용자에게 지키려는 약속이다. `capability`는 구성 요소가 실제로 행사할 수
  있는 능력이다. `state authority`는 상태가 충돌할 때 따를 최종 기준이다. `outcome`은 사용자가 얻는
  결과다.
- **Q2:** `dependency graph`는 구성 요소의 의존 관계도다. `topology`는 실행 요소가 배치되고 연결된
  모양이다. `state scope`는 상태가 유효하고 공유되는 범위다. `critical path`는 약속 달성에 꼭 거치는
  핵심 실행 경로다.
- **Q3:** `workload envelope`는 요청 수·입력 크기·지속 시간처럼 검증할 부하 조건의 범위다. `queue`는
  처리 대기열이다. `tail latency`는 느린 요청 집단의 지연 시간이다. `amplification`은 작은 입력 증가가
  훨씬 큰 작업 증가를 만드는 현상이다. `break point`는 약속한 한계를 처음 넘는 지점이다.
- **Q4:** `deep module`은 작은 사용법 뒤에 큰 내부 복잡성을 감춘 모듈이다. `chokepoint`는 관련 책임이
  반드시 거치는 한 지점이다. `interface`는 다른 구성 요소가 사용하는 접점이다. `change propagation`은
  한 변경이 여러 곳의 수정으로 번지는 현상이다.
- **Q5:** `cache identity`는 어떤 계산 결과인지 구별하는 기준이다. `freshness`는 결과를 최신으로 인정할
  기간이다. `invalidation`은 낡은 결과를 무효화하는 일이다. `coordination`은 여러 실행 주체가 중복
  계산을 피하도록 맞추는 일이다. `retention`은 결과를 보관하는 기간이다.

</details>

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

<details markdown="1">
<summary>용어 풀이</summary>

- `architecture need`: 제품 약속을 지키기 위해 구조가 갖춰야 할 조건이다.
- `state`, `effect`, `boundary`: `state`는 프로그램이 기억하는 현재 정보다. `effect`는 데이터 저장이나
  메시지 전송처럼 시스템 밖에 일으키는 변화다. `boundary`는 책임이나 권한을 넘겨주는 경계다.
- `authority`와 `carrier`: `authority`는 어떤 값이 맞는지 정하는 최종 권한이다. `carrier`는 그 값을
  URL·메모리·메시지 등에 실어 나르는 수단이다. 값을 가지고 있다고 최종 권한까지 갖는 것은 아니다.
- `budget break point`: 응답 시간이나 처리량처럼 미리 정한 허용 한도를 처음 넘는 부하 지점이다.
- `cache source`: 캐시에 저장한 결과를 처음 만들 때 사용한 원본 데이터나 계산이다.
- `trigger`: 부하 증가, 정책 변경처럼 기존 결정을 다시 검토하게 만드는 조건이다.
- `failure mode`: 시스템이 실패하는 구체적인 방식이다. 시간 초과, 대기열 폭증, 낡은 캐시 반환이 각각
  다른 실패 방식이다.

</details>

서비스가 지키려는 약속과 실제 failure mode가 설계 품질의 기준이 된다. 같은 패턴도 서비스의 정책과
실행 조건에 따라 다른 결과를 만든다.

## 관리자의 일

관리자는 아키텍처 결정을 현재형으로 유지한다. 문서, 코드, 테스트와 runtime evidence를 같은 결정에
연결하고, 조건이 바뀌면 검토를 다시 연다.

```text
승인된 authority (최종 결정 근거)
  → policy projection (결정을 기계가 확인할 규칙으로 옮김)
  → 정확한 revision에 묶인 observation (특정 코드 버전에서 관찰한 사실)
  → evidence 검증 (근거가 믿을 만한지 확인)
  → deterministic comparison (같은 입력이면 같은 결과가 나오는 비교)
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

<details markdown="1">
<summary>용어 풀이</summary>

- `policy`: 사람이 승인한 규칙과 기준이다.
- `observation`: 특정 코드 버전과 실행 조건에서 실제로 관찰한 사실이다.
- `included`: 이번 검토에 포함해 실제로 확인한 범위다.
- `unsupported`: 확인하고 싶지만 현재 도구나 방법이 아직 지원하지 않는 범위다.
- `excluded`: 이유를 밝히고 이번 검토에서 의도적으로 제외한 범위다.
- `lens`: 상태 경계, 권한 경계, 성능 예산처럼 아키텍처를 살피는 하나의 관점이다.
- `validation failure`: 입력 형식이나 필수 값이 잘못되어 판정을 시작하지 못한 상태다. 아키텍처의
  좋고 나쁨을 판정한 결과는 아니다.

</details>

## 증거를 다루는 법

각 증거는 확인할 수 있는 범위가 다르다. 정적 graph는 import와 call edge를 보여 준다. Negative guard는
새 우회 경로를 막는다. Behavior test는 timeout, retry, abort와 실패 변환을 실행한다. Runtime trace는
callback과 background lifetime처럼 정적 분석이 놓치는 경로를 보여 준다.

증거에는 source revision, 실행 command, exit code, artifact digest와 target을 연결한다. Adapter는 관측
사실을 수집한다. 비교와 verdict는 공통 evaluator가 계산한다.

<details markdown="1">
<summary>용어 풀이</summary>

- `정적 graph`: 프로그램을 실행하지 않고 코드의 연결 관계를 그린 지도다. `import edge`는 모듈을
  가져오는 관계다. `call edge`는 함수를 호출하는 관계다.
- `Negative guard`: 허용되지 않은 의존이나 우회 경로가 새로 생기면 실패하게 만드는 검사다.
- `Behavior test`: 시간 초과, 재시도, 중단처럼 실행 중의 행동이 기대와 맞는지 확인하는 테스트다.
- `Runtime trace`: 실제 요청이 지나간 순서와 시간을 남긴 기록이다. `callback`은 나중에 실행하도록
  넘긴 함수다. `background lifetime`은 응답 뒤에도 백그라운드 작업이 살아 있는 기간이다.
- `source revision`은 검사한 코드 버전이다. `exit code`는 명령의 성공·실패 번호다. `artifact digest`는
  결과 파일이 바뀌지 않았음을 확인하는 지문이다. `target`은 검사의 대상이다.
- `Adapter`는 서비스마다 다른 정보를 공통 관찰 형식으로 바꾸는 연결부다. `evaluator`는 그 관찰을
  승인된 기준과 비교해 판정하는 공통 계산기다.

</details>

## 사람과 기계의 역할

제품 또는 아키텍처 owner는 Promise, trade-off, intended boundary와 위험 수용을 승인한다. Coding
agent는 구조를 조사하고 대안과 evidence candidate를 만든다. 기계는 승인된 policy에 따라 edge, budget,
invariant와 우회 경로를 반복 검증한다.

LLM finding은 검증 전까지 `unverified` candidate로 관리한다. 정책 변경, 구조 수정, 위험 수용과 배포는
사람이 승인한다. 이 분업은 자동화의 범위와 사람 판단의 자리를 분명하게 만든다.

<details markdown="1">
<summary>용어 풀이</summary>

- `trade-off`: 한 이점을 얻는 대신 다른 비용이나 제약을 감수하는 관계다.
- `intended boundary`: 권한이나 책임을 제한하려고 사람이 의도한 경계다.
- `edge`는 구성 요소 사이의 연결이다. `budget`은 허용 가능한 시간·크기·자원 한도다. `invariant`는
  실행 중에도 반드시 계속 참이어야 하는 조건이다.
- `Coding agent`: 코드를 조사하고 수정하는 AI 에이전트다.
- `LLM finding`과 `unverified candidate`: 대규모 언어 모델(LLM)이 찾아낸 의심 사항은 사람이 확인해야
  할 후보로 남긴다. 검증을 마치기 전에는 사실이나 판정 근거로 쓰지 않는다.

</details>

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

<details markdown="1">
<summary>항목 풀이</summary>

`invariant`는 반드시 지킬 조건이다. `허용·금지 경로`는 구성 요소가 연결되어도 되는 방식과 안 되는
방식이다. `Human decision`은 근거를 본 사람이 내린 최종 결정이다. 이 목록을 남기면 다른 사람도 구조를
선택한 이유와 현재 유효성을 다시 확인할 수 있다.

</details>

## 전문성 단계

이 모델은 네 단계의 실무 능력을 요구한다.

| 단계 | 할 수 있는 일 |
| --- | --- |
| 의미 구성 | 제품 약속과 architecture need를 owner, state, effect, boundary로 옮긴다 |
| 구조 설계 | 경계, topology, critical path, module grain과 cache policy를 trade-off와 함께 결정한다 |
| 검증 설계 | 시나리오와 evidence를 만들고 반복 가능한 guard와 evaluator에 연결한다 |
| 지속 관리 | coverage, verdict, risk acceptance와 re-entry trigger를 운영한다 |

<details markdown="1">
<summary>용어 풀이</summary>

- `module grain`: 책임을 얼마나 크거나 작은 모듈 단위로 나눌지에 관한 기준이다.
- `guard`: 금지한 구조나 한도 초과가 생기면 자동으로 알려 주거나 실패시키는 검사다.
- `coverage`: 이번 검토가 전체 대상 중 실제로 확인한 범위다.
- `risk acceptance`: 문제나 불확실성을 알고도 비용과 기한을 고려해 당장은 받아들이는 결정이다.
- `re-entry trigger`: 받아들인 위험이나 과거 결정을 다시 검토해야 하는 조건이다.

</details>

현재 portable core는 Q1의 state boundary, Q2의 least-authority boundary, Q3의 serialized-input budget을
부분적으로 실행한다. Q4와 Q5는 rubric으로 사용한다. 기계가 계산하는 coverage는 `unsupported`,
verdict는 `unknown`으로 남긴다. 전문가는 지식의 범위와 도구가 실제로 검증하는 범위를 함께 밝힌다.

<details markdown="1">
<summary>현재 도구 범위 풀이</summary>

`portable core`는 특정 서비스에 묶이지 않고 재사용하는 공통 판정 도구다. `least-authority boundary`는
각 구성 요소가 꼭 필요한 최소 권한만 갖게 하는 경계다. `state boundary`는 상태의 최종 기준과 변경
권한이 어디에 있는지 정한 경계다. `serialized-input budget`은 전송·저장할 수 있게 변환한 입력 데이터에
허용한 크기 한도다. `rubric`은 사람이 같은 기준으로 검토하도록 돕는 평가 기준표다. Q4·Q5를 설명할 수
있는 범위와 도구가 자동 검증할 수 있는 범위를 구분해야 한다.

</details>

## 마무리

Architecture Fitness는 아키텍처를 지속해서 관리하는 실무 체계를 제공한다. 중요한 약속을 경계와
시나리오에 담고, 증거를 통해 현재 상태를 확인하며, 조건이 바뀔 때 결정을 다시 연다. 이 과정을
반복할 수 있는 능력이 아키텍처 설계자와 관리자의 전문성을 만든다.

[Architecture Fitness 학습 목록으로 돌아가기](./)
