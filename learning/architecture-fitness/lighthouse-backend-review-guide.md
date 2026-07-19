---
layout: default
title: Lighthouse 백엔드 리뷰 가이드
---

# Lighthouse 사례로 배우는 백엔드 프로젝트 리뷰 가이드

이 문서는 Light House 같은 실제 프로젝트를 처음 검토할 때 사용하는 판단
순서를 정리한다. 코드 스타일보다 제품 보장을 먼저 확인한다.

이 문서는 Lighthouse를 학습 사례로 사용한다. Architecture Fitness의 portable
contract나 verdict 정본은 아니다. 제품 정체성은
[`product-identity.md`](https://github.com/corca-ai/lighthouse/blob/main/docs/product-identity.md),
검색 실행은
[`runtime-flows/search-mechanism.md`](https://github.com/corca-ai/lighthouse/blob/main/docs/runtime-flows/search-mechanism.md),
gap report는
[`runtime-flows/gap-network-analysis.md`](https://github.com/corca-ai/lighthouse/blob/main/docs/runtime-flows/gap-network-analysis.md)가
정본이다.

## 출발 질문

백엔드 리뷰는 다음 질문에서 시작한다.

> 백엔드는 사용자의 어떤 행동에 어떤 결과를 보장해야 하는가?

Light House 검색은 모든 관련 논문을 보장하지 않는다. 외부 provider의 데이터와
검색 품질을 통제할 수 없기 때문이다. 대신 현재 검색 조건을 정확히 전달하고,
받은 결과를 왜곡하지 않으며, 출처와 한계를 드러내야 한다.

이 문장을 먼저 정해야 코드가 좋은지 판단할 기준이 생긴다. 함수가 짧아도 다른
검색어의 결과를 반환하거나 개인 데이터를 섞으면 좋은 백엔드가 아니다.

## 주니어를 위한 읽는 순서

이 가이드는 기술 용어를 이미 안다고 가정하지 않는다. 새 용어는 다음 순서로
이해한다.

```text
발생할 수 있는 문제
→ 일상어로 설명한 동작
→ Lighthouse의 실제 데이터와 코드
→ 기술 용어
→ 테스트와 운영에서 확인할 증거
```

예를 들어 `unique index`를 정의부터 외우지 않는다. 같은 사용자의 같은 reaction이
동시에 두 번 저장될 수 있다는 문제부터 본다. PostgreSQL이 같은 key의 동시
INSERT를 어떻게 조정하는지 확인한 뒤 `unique index`라는 이름을 붙인다.

문서에서 **현재**는 코드와 migration에서 확인한 사실을 뜻한다. **권장**은 아직
구현하지 않은 개선 방향이다. **미확인**은 production 설정이나 실제 DB 증거가
부족한 상태다. 세 상태를 섞지 않는다.

## 검토 모델

제품 보장을 다음 순서로 구체화한다.

```text
사용자 행동
→ 보장할 결과
→ 반드시 성립할 불변식
→ 실패 모드
→ 코드와 운영 증거
```

불변식은 반드시 성립해야 하는 조건이다. 검색에서는 현재 URL 조건과 결과가
일치해야 한다. Gap report에서는 저장한 artifact와 개인 reaction의 identity가
섞이지 않아야 한다.

### 실행 상태

모든 핵심 유스케이스에 세 가지 상태를 적용한다.

| 상태 | 질문                                | Light House 사례                                     |
| ---- | ----------------------------------- | ---------------------------------------------------- |
| 정상 | 올바른 결과를 만드는가?             | query·sort·year가 provider 호출과 결과에 이어지는가? |
| 실패 | 의존성이 실패하면 어떻게 닫히는가?  | provider timeout을 논문 없음으로 오해하지 않는가?    |
| 중단 | 실행 주체가 사라지면 무엇이 남는가? | gap build가 영구 pending으로 남지 않는가?            |

### 검토 렌즈

실행 상태마다 다음 렌즈를 겹쳐 적용한다.

| 렌즈       | 핵심 질문                                    |
| ---------- | -------------------------------------------- |
| 정확성     | 현재 입력에 맞는 결과인가?                   |
| 보안       | 올바른 주체만 실행하고 데이터에 접근하는가?  |
| 회복성     | 실패와 중단 뒤 안전하게 복구하는가?          |
| 부하       | 동시 요청이 늘어도 자원과 비용을 통제하는가? |
| 운영       | 문제를 발견하고 원인을 추적할 수 있는가?     |
| 유지보수성 | 변경할 때 같은 보장을 계속 지킬 수 있는가?   |

정상·실패·중단과 보안·부하는 같은 분류가 아니다. 앞의 셋은 실행 상태이고,
뒤의 항목은 모든 상태에 적용하는 관점이다.

## 실제 리뷰 순서

프로젝트 전체를 처음부터 읽지 않는다. 다음 산출물을 하나씩 만든다.

1. 제품 책임을 사용자 행동과 결과로 한 문장에 적는다.
2. 검색, AI comment, gap report처럼 사용자 행동 단위로 나눈다.
3. 각 행동에서 중요한 필드와 상태를 고른다.
4. 정상·실패·중단과 검토 렌즈를 적용한다.
5. entrypoint부터 DB·응답·테스트까지 실제 경로를 추적한다.
6. 영향도, 발생 가능성, 발견 난이도로 검토 우선순위를 정한다.

코드는 다음 순서로 따라간다.

```text
entrypoint
→ 인증과 입력 검증
→ service 또는 domain-access
→ provider gateway와 repository
→ DB 제약
→ 응답과 client 소비
→ 테스트와 운영 지표
```

코드가 존재한다는 사실만으로 검토를 닫지 않는다. 실패를 재현하는 테스트와
운영 환경에서 확인할 지표가 필요하다.

### 위험 기반 검토 순서

정확성, 실패 계약, 보안, 복구, 부하 순으로 시작하되 고정하지 않는다.
영향도·발생 가능성·발견 난이도가 큰 보장을 앞으로 옮긴다. Light House에서는
malformed year 정책이 미정이었지만 Episteme 부하 제어에는 구현과 테스트가 있었다.
그래서 `query` 정확성을 먼저 보고 provider queue는 부하 검토에서 다뤘다.

### 전문가가 주목하는 배경

| 개념                                     | 반복해서 발생하는 실패                                                                     |
| ---------------------------------------- | ------------------------------------------------------------------------------------------ |
| 제품 보장과 불변식                       | 읽기 좋은 코드도 사용자에게 잘못된 결과를 줄 수 있다.                                      |
| 핵심 필드와 canonical identity           | 여러 변환 경계를 지나면 입력 의미와 상태 identity가 쉽게 달라진다.                         |
| 실패 상태와 partial failure              | 성공·실패 두 값만으로는 유효한 결과, 재시도 범위와 비용을 결정할 수 없다.                  |
| Multi-tenant isolation과 least authority | 필터 한 번의 누락이나 강한 권한의 재사용이 다른 사용자의 데이터를 노출한다.                |
| 영속성, lease와 CAS                      | 프로세스 종료와 중복 요청은 정상 운영에서도 발생하며 작업 유실과 stale overwrite를 만든다. |
| 부하와 실행 범위                         | 한 요청의 fan-out과 retry가 늘면 단일 인스턴스 보호만으로 전체 비용을 막지 못한다.         |
| 테스트와 운영 증거                       | 구현 의도와 green test만으로 실제 동시성, 장애와 production 상태를 증명할 수 없다.         |

## 검색 검토 사례

검색 서비스에서는 `query`가 첫 번째 중요 필드다.

```text
URL query
→ SearchExecutionInput
→ provider request
→ 결과 metadata
→ 화면
```

변환은 허용하지만 추적할 수 있어야 한다. 원본과 정규화 결과가 남아야 사용자가
입력한 조건과 provider가 받은 조건을 비교할 수 있다.

다음 질문을 순서대로 확인한다.

- `query`, `year`, `sort`, filter가 실제 provider 호출까지 전달되는가?
- 잘못된 URL 값이 표시만 되고 실행에는 빠지는 phantom filter가 생기는가?
- 기본 relevance 순서와 사용자가 선택한 정렬을 구분하는가?
- 사용자 라이브러리를 사용한 개인화가 다른 사용자의 데이터와 섞이지 않는가?
- provider 실패, 부분 결과, 정상적인 빈 결과를 구분하는가?
- 이전 검색의 늦은 응답이 새 검색을 덮지 않는가?
- 요청 한 건이 만드는 provider·DB 호출 수와 byte 상한은 얼마인가?

잘못된 `year` URL의 정책 공백은
[#408](https://github.com/corca-ai/lighthouse/issues/408)에 기록했다. 이런 발견은
파서 한 줄의 문제가 아니라 표시 조건과 실제 실행 조건의 불일치로 설명해야 한다.

검색 결과는 영속 artifact가 아니다. URL이 조건의 정본이며 다시 열면 현재
provider와 사용자 context로 재실행한다. Deterministic ID가 있어도 DB 저장을
뜻하지는 않는다.

## 인증과 권한 검토

Multi-tenant isolation은 A의 개인 데이터가 B의 계산이나 응답에 섞이지 않게
보장하는 정책이다. Least authority는 각 코드 경계에 그 작업에 필요한 권한만
제공하는 설계다.

Light House에서 gap report 본문은 인증 회원이 공유한다. Reaction은
`(gap_report_id, viewer_principal_id)`로 분리한 개인 상태다. 공유와 개인 데이터를
모두 creator-owned로 처리해서는 안 된다.

Reaction은 report를 참조하고 `ON DELETE CASCADE`로 함께 삭제된다. 이 데이터
종속성과 접근 권한은 별개다. Reaction 원문은 사용자별로 격리하고, report별
집계만 별도 권한으로 계산해야 한다.

Reaction 수는 사용자가 준비된 설명을 선택한 횟수나 참여도를 보여준다. 현재
reaction에는 유용성 평가가 없으므로 이 수를 report 품질로 바로 해석할 수 없다.
품질을 판단하려면 `helpful` 같은 명시적 피드백이나 후속 연구 행동을 별도
신호로 정의해야 한다.

현재 일반 요청의 DB handle은 service role을 감싼다. Repository의
`.eq("owner_principal_id", userId)`가 빠지면 RLS가 방어하지 못한다.
`RepositoryDbHandle`은 raw client를 감추지만 실제 DB 권한을 줄이지 않는다.
Moonlight 인증 제거, Supabase Auth 단일화, 일반 요청의 admin 접근 제거는
[#410](https://github.com/corca-ai/lighthouse/issues/410)에 기록했다.

보안은 보호할 데이터에서 시작해 호출 주체, 인증, 권한 확인, repository, DB,
응답과 로그까지 따라간다.

## 데이터 저장 경계 검토

DB 코드를 읽기 전에 기본 용어를 동작으로 이해한다.

| 용어                  | 이 가이드에서 사용하는 뜻                                    |
| --------------------- | ------------------------------------------------------------ |
| Row                   | 하나의 저장 기록이다.                                        |
| Column                | 기록을 구성하는 필드다.                                      |
| Key                   | 어떤 row인지 식별하는 값이다.                                |
| Primary key           | 같은 key의 row를 둘 이상 저장하지 못하게 하는 대표 식별자다. |
| Composite primary key | 실제 column 여러 개를 합쳐 하나의 primary key로 사용한다.    |
| Preference            | 공유된 사실이 아니라 사용자별로 저장한 선택 상태다.          |
| Transaction           | 여러 DB 작업을 성공 또는 취소 단위로 묶는다.                 |
| Version               | caller가 읽은 상태가 아직 최신인지 비교하는 변경 번호다.     |
| CAS                   | 기대한 version과 현재 version이 같을 때만 값을 바꾼다.       |

Lighthouse의 Gap report 본문은 공유 artifact다. `gap_report_id`는 특정 사용자의
소유권을 뜻하지 않는다. 반면 사용자가 고른 reaction은 그 사용자의 개인
preference다.

현재 `gap_report_reactions`는 실제 두 column을 합쳐 primary key로 사용한다.

```sql
primary key (gap_report_id, viewer_principal_id)
```

이 규칙은 같은 공유 report에 A와 B의 preference가 각각 존재하도록 허용한다.
대신 같은 report에 A의 preference row가 두 개 생기는 것은 거부한다.

```text
(report-1, user-A) → 허용
(report-1, user-B) → 허용
(report-1, user-A) → 이미 있으면 중복
```

동시에 같은 key를 INSERT할 때 첫 요청의 row는 commit 전이라 일반 `SELECT`에
보이지 않을 수 있다. PostgreSQL unique index는 진행 중인 동일 key INSERT를
별도로 확인한다. 두 번째 요청은 첫 transaction이 끝날 때까지 기다린다. 첫
transaction이 commit하면 두 번째 요청은 `23505 unique_violation`으로 실패한다.
첫 transaction이 rollback하면 두 번째 요청이 계속 진행할 수 있다.

Lighthouse repository는 첫 preference INSERT가 경쟁에서 졌을 때 `23505`를
인식해 `null`을 반환한다. 위 route는 최신 상태를 다시 확인하거나 제한된 충돌
처리를 수행한다. 서버가 두 대여도 모든 write가 같은 DB unique index를 통과하기
때문에 중복 row가 최종 저장되는 것을 막을 수 있다.

이 제약은 데이터 identity만 보장한다. 누가 해당 row를 읽고 쓸 수 있는지는
인증, DB role과 RLS가 별도로 보장해야 한다. 공유 artifact인지와 개인 preference
인지도 primary key만 보고 결정하지 않는다. 제품 정책과 접근 권한 정본이 먼저다.

### Transaction과 version

Transaction은 관련된 변경을 함께 성공시키거나 함께 취소한다. SQL 한 문장도
PostgreSQL에서는 하나의 transaction으로 실행된다. Lighthouse reaction 저장은
`reaction`, `reaction_history`, `reaction_version`을 한 `UPDATE`에 담는다. 세
column은 함께 바뀌거나 모두 바뀌지 않는다.

같은 계정을 두 화면에서 열면 두 요청이 같은 `reaction_version`을 읽을 수 있다.
먼저 도착한 요청이 version을 3에서 4로 올리면, 뒤늦은 요청의
`WHERE reaction_version = 3`은 어떤 row도 찾지 못한다. 오래된 요청이 최신
preference를 조용히 덮지 못한다. 이를 갱신 유실 방지라고 한다.

```sql
UPDATE gap_report_reactions
SET reaction = :reaction,
    reaction_version = 4
WHERE gap_report_id = :report_id
  AND viewer_principal_id = :viewer_id
  AND artifact_version = :artifact_version
  AND reaction_version = 3;
```

Version은 모든 변경 가능한 row에 필요하지 않다. `reviewed_papers`처럼 같은
검토 완료 요청을 반복해도 결과가 같으면 `UNIQUE + upsert`로 충분하다.
Analytics event처럼 기존 row를 수정하지 않고 계속 추가하는 데이터에도 동시
수정용 version이 필요하지 않다. DB가 `count = count + 1`처럼 한 SQL에서 계산하는
원자적 변경도 client가 읽은 version에 의존하지 않는다.

같은 `version` 이름도 역할이 다를 수 있다. `reaction_version`은 동시 수정을
조정한다. `paper_inline_analysis_cache.version`은 어느 분석 계약으로 만든
결과인지 구분한다. 이름만 보고 concurrency 장치라고 판단하지 않는다.

### Transaction 경계와 제품 보장

Transaction 범위는 크게 잡는 것이 목표가 아니다. 사용자에게 함께 보장해야 하는
변경만 묶는다. Gap build 전체를 하나의 transaction으로 묶으면 LLM enrichment를
기다리는 동안 DB 연결과 잠금을 오래 점유한다. Enrichment가 실패할 때 먼저 만든
core까지 rollback되어 partial failure 계약도 깨진다.

현재 Lighthouse는 pending, core, enrichment terminal 상태를 각각 짧게 저장한다.
각 단계의 write는 version 조건으로 오래된 Runner를 거부한다. Core와 enrichment의
분리는 사용자가 core 결과를 유효하게 볼 수 있다는 제품 결정에서 나온다.
사용자가 enrichment 없는 결과를 쓸 수 없다고 결정한 다른 제품이라면 transaction
경계와 노출 상태도 달라질 수 있다.

Lighthouse는 검색 자체를 DB에서 수행하지 않는다. Query는 Episteme provider로
보내고 결과를 현재 route에 전달한다. DB는 `reviewed_papers`, Gap build와
reaction, inline-analysis cache, LLM usage와 운영 기록처럼 재방문·복구·집계에
필요한 상태를 맡는다. Gap report는 평균적인 route가 아니라 DB identity,
동시성, 중단 복구와 partial failure가 가장 밀집된 학습 사례다.

## API route 입구 검토

API route는 외부 요청이 DB, provider, LLM에 도달하기 전 서버가 책임질 범위를
결정한다. 시니어는 요청을 거부하는지만 보지 않는다. 얼마의 메모리, CPU와 외부
비용을 사용한 뒤 거부하는지도 확인한다.

고비용 인증 route는 다음 순서를 기준으로 검토한다.

```text
인증
→ body byte 제한
→ 데이터 형식과 값 검증
→ 호출 빈도·동시 실행 제한
→ DB write, provider 또는 LLM 작업
```

Zod는 JSON 안의 필드 형식과 값을 검사한다. `z.string().min(1)`은 값이 비어 있지
않은 문자열인지 확인한다. 그러나 `req.json()`이 큰 body를 이미 전부 읽은 뒤
Zod를 실행하면 메모리와 JSON parse 비용은 사용한 상태다. Body 크기는
`readBoundedJsonBody` 같은 별도 경계에서 먼저 제한해야 한다.

HTTP 응답도 실패 원인을 구분해야 한다.

| 상태 | 의미                        | 호출자가 취할 행동                          |
| ---- | --------------------------- | ------------------------------------------- |
| 400  | 데이터 형식이나 값이 잘못됨 | 요청을 수정한다.                            |
| 401  | 인증되지 않음               | 로그인하거나 세션을 갱신한다.               |
| 403  | 인증됐지만 권한이 없음      | 다른 권한이나 허용된 자원을 사용한다.       |
| 409  | 최신 상태와 충돌함          | 최신 상태를 읽고 요청을 다시 구성한다.      |
| 413  | Body가 허용 크기를 넘음     | 입력 크기를 줄인다.                         |
| 422  | 형식은 맞지만 의미가 잘못됨 | 같은 command를 반복하지 않고 의미를 고친다. |
| 429  | 호출량이나 동시 실행을 넘음 | 진행 중 결과를 기다리거나 나중에 시도한다.  |
| 5xx  | 서버나 의존성이 실패함      | 안전한 작업만 제한된 횟수로 재시도한다.     |

모든 route에 같은 제한값을 복사하지 않는다. 조회, DB write, provider 호출과 LLM
호출은 비용과 무결성 위험이 다르다. LLM route는 인증과 비용 제한이 중요하다.
Reaction write는 비용이 작아도 사용자 격리와 중복 쓰기 검사가 중요하다.

동일한 사용자의 같은 작업이 동시에 들어오면 in-flight deduplication으로 실행을
하나로 합칠 수 있다. 서로 다른 요청이 허용량을 넘으면 rate limit으로 거부한다.
두 장치는 다른 문제를 해결한다.

현재 Lighthouse의 Gap report, inline analysis와 Gap reaction route는 인증,
bounded body와 schema 검증 순서가 강하다. 모든 API route에는 `maxDuration`
검사가 있다. 반면 일부 검색 보조·LLM route는 body를 먼저 읽은 뒤 인증하거나
명시적인 body·query·호출량 상한이 없다. `withRouteGuard`도 인증과 부하 제한이
아니라 domain error를 HTTP 응답으로 변환하는 wrapper다.

전 route의 공개성, 인증 순서, byte·cardinality·비용 상한을 정렬하는 작업은
[#430](https://github.com/corca-ai/lighthouse/issues/430)에서 추적한다.

오류 상태는 서버 분류로 끝나지 않는다. 서버의 상태와 stable error code가 client의
입력 수정, 로그인 복구, 최신 상태 조회, backoff와 terminal 처리로 이어져야 한다.
현재 inline analysis는 transport failure와 `5xx`만 재시도하는 좋은 기준선이
있다. 반면 search enrichment와 graph hydration은 모든 non-2xx를 같은 오류로
접고 최대 세 번 재시도한다. `400`처럼 같은 payload로 성공할 수 없는 요청도
반복할 수 있다.

HTTP 오류 의미와 client 행동을 정렬하는 작업은
[#433](https://github.com/corca-ai/lighthouse/issues/433)에서 추적한다.

정책 결정과 구조 검증의 책임도 구분한다. 사람은 `400`을 재시도하지 않고
`409`에서는 최신 상태를 읽는다는 정책을 승인한다. 제품 코드는 그 정책을
구현한다. Architecture Fitness는 승인된 오류 identity가 server response,
transport와 client branch를 지나며 끊기지 않는지 반복 검증한다. 정책이 없으면
구현에서 의도를 추정해 `healthy`로 만들지 않고 `authority-missing` 또는
`unknown`으로 남긴다.

## Gap report 검토 사례

Gap report는 다시 열고 공유해야 하므로 DB에 저장한다. 현재 생성 흐름은 다음과
같다.

```text
입력 snapshot과 pending row 저장
→ gapReportId 반환
→ after() runner 시작
→ core 저장
→ LLM enrichment
→ ready 또는 failed 저장
```

Runner는 별도 종류의 서버가 아니다. 같은 `runGapNetworkBuildJob()`이 Gap report
하나를 처리하는 실행 1회를 뜻한다. 서버 runner는 분석과 provider 호출을 맡고,
DB는 공유 attempt·lease·version과 최종 결과를 저장한다.

정상 흐름에는 Runner 1만 존재한다. Runner 1의 lease가 만료된 뒤 사용자가
재방문하거나 recovery를 요청하면 같은 report를 처리하는 Runner 2가 시작될 수
있다. 둘은 같은 코드를 실행하지만 Runner 2가 최신 attempt를 소유한다.

현재 구현을 교차 검토하면 다음과 같다.

| 렌즈   | 현재 확인한 내용                                                                    | 남은 질문                                                             |
| ------ | ----------------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| 정확성 | Canonical digest와 DB unique key가 같은 입력의 중복 artifact를 막는다.              | Digest에서 빠진 값이 분석 의미를 바꾸지 않는가?                       |
| 보안   | 본문은 공유하고 reaction은 viewer별로 분리한다.                                     | DB가 A/B 격리를 직접 강제하는가?                                      |
| 회복성 | Full input을 먼저 저장하고 70초 lease와 version CAS로 runner를 조정한다.            | 별도 worker 없이 사용자 재방문에 의존하는 복구 범위가 충분한가?       |
| 부하   | Body는 1MB, paper는 40개로 제한한다. 같은 artifact는 active runner 하나가 처리한다. | 서로 다른 digest의 대량 생성, polling과 LLM 비용을 어떻게 제한하는가? |
| 운영   | Phase, attempt, lease 만료 시각을 저장한다.                                         | Pending 수명과 recovery 성공률을 실제로 관측하는가?                   |

Core와 LLM enrichment는 독립적으로 실패할 수 있으므로 상태를 분리한다.

```text
core ready + enrichment ready  → 전체 report 제공
core ready + enrichment failed → core 제공, 부분 실패
core failed                    → 전체 report 실패
```

전문가는 이 partial failure contract를 확인한다. 성공·실패 두 상태로 합치면
사용 가능한 core를 버리거나 전체 성공으로 오해하게 만든다. 전체 재시도는
이미 성공한 계산과 LLM 비용도 반복한다.

Enrichment가 실패했을 때 사용자가 “분석 다시 시도” command로 enrichment만
재실행하는 제품 요구사항을 채택했다. 조회, polling과 재방문은 effect를 시작하지
않고 core를 다시 계산하지 않는다. 이 기능은 현재 구현되지 않았으며
[#414](https://github.com/corca-ai/lighthouse/issues/414)에서 추적한다.

같은 사용자의 중복 클릭·탭·재시도는 세 경계에서 줄인다. UI pending 상태가
연속 클릭을 막고, digest unique key가 artifact를 하나로 수렴시킨다. Lease와
version CAS는 같은 artifact의 runner와 최종 commit을 하나로 수렴시킨다.

서버가 죽으면 runner는 사라진다. DB에는 입력과 pending 상태가 남는다. 사용자가
lease 만료를 관찰하면 recovery POST로 작업을 재개한다.

Lease는 70초 뒤 실행되는 timer가 아니다. Runner가 시작할 때 DB에
`leaseExpiresAt = now + 70초`를 저장한다. 시간이 지나도 자동 작업은 실행되지
않는다. 다음 요청이 현재 시각과 비교해 만료를 확인하고 새 attempt를 CAS로
획득한다.

`POST /api/gap-reports` route는 인증, bounded body 검증, 기존 report 조회 또는
pending row 예약, 실패 상태의 retry 전환을 수행한다. Report가 아직 준비되지
않았으면 `after()`에 Runner를 등록하고 `202 pending`을 반환한다. 응답 뒤의
Runner도 같은 server invocation에서 실행되므로 route의 60초 실행 예산에
포함된다.

시간 예산은 안쪽 작업부터 바깥 실행 경계 순서로 잡는다.

```text
LLM 호출 1회 10초
< enrichment critical path 30초
< route 실행 예산 60초
< DB lease 70초
```

Lease가 route보다 짧으면 정상 Runner가 실행 중일 때 recovery Runner가 시작할
수 있다. 너무 길면 process loss 뒤 복구가 늦어진다. 현재 70초는 route 종료와
최종 DB persist를 위한 여유를 남긴다.

따라서 현재 보장은 다음 범위다.

> 작업 정보는 유실되지 않으며 사용자가 다시 관찰하면 복구된다.

이는 정확히 한 번 실행하거나 별도 durable worker가 계속 실행함을 보장하지
않는다. Lease가 만료된 기존 runner와 새 runner의 계산이 잠시 겹칠 수 있다.
CAS는 오래된 결과의 덮어쓰기를 막는다. Lease는 서로 다른 입력의 대량 생성이나
보안 문제를 해결하지 않는다.

## 부하 검토

요청 한 건의 provider·DB·LLM 호출, byte와 실행 시간부터 계산한다. 그다음 동시
요청, fan-out과 retry를 적용한다. Gap report는 입력과 LLM 호출별 상한을 가지지만
여러 사용자의 동시 실행 수까지 제한하지는 않는다.

비슷해 보이는 보호장치의 책임을 구분한다.

| 장치                             | 해결하는 문제                             |
| -------------------------------- | ----------------------------------------- |
| Episteme queue와 circuit breaker | 검색 provider 동시성·장애 확산            |
| in-flight dedupe와 lease/CAS     | 같은 gap artifact의 중복 실행·stale 저장  |
| 사용자별 active build 제한       | 서로 다른 gap report의 LLM 동시 실행·비용 |

Gap build는 Episteme를 다시 호출하지 않는다. 검색 snapshot에 저장된 papers와
`graphSupport`를 사용한다. Episteme 보호는 upstream 검색을 안정화하고, Gap 제한은
Gemini workload를 통제한다. 자원별 bulkhead가 한쪽 장애의 전파를 막는다.

Episteme queue는 process-local이고 core 요청용 슬롯을 남긴다. Gap의 사용자별 active
build 1개 제한은 #417에서 DB 기준으로 추적한다. 평균 시간뿐 아니라 p95·p99, 5xx,
queue, token 비용과 load shedding을 본다. Process-local 상한은 fleet 전체 상한이 아니다.

### 계측과 관측 가능성

로그를 생성하는 계측만으로 운영 판단을 내릴 수는 없다. 기간별 집계, 사용자 영향,
재검토 조건까지 연결돼야 관측 가능성이 생긴다.

| 측정 단위                | 답하는 질문                                                       |
| ------------------------ | ----------------------------------------------------------------- |
| Provider observation     | Episteme의 queue·latency·실패 상태는 어떤가?                      |
| Search grounding outcome | 내 연구 기준을 요청한 검색 중 실제 적용·degraded 비율은 얼마인가? |

검색 한 번이 provider를 여러 번 호출할 수 있으므로 두 수치를 같은 분모로 합치지
않는다. 사용자는 안전한 결과 품질만 보고 운영자는 내부 queue와 circuit 상태를 본다.
Telemetry 저장 실패는 검색을 실패시키면 안 된다.

현재 Episteme observation은 privacy-safe console log까지 연결됐지만 집계 소비자가
없어 `logging-only`다. 기존 LLM usage admin 패턴을 재사용하되 별도 원장과 좁은
append capability를 사용하는 운영 리포트는
[#422](https://github.com/corca-ai/lighthouse/issues/422)에서 추적한다.

DB 제공자와 애플리케이션의 관측 책임도 분리한다.

| Owner          | 수집할 사실                                                                |
| -------------- | -------------------------------------------------------------------------- |
| RDS·CloudWatch | CPU, memory, storage, connection, I/O, SQL latency, lock, DB log           |
| Lighthouse     | Gap attempt 시작, lease 인수, claim·CAS 거부, recovery 결과, 중복 LLM 실행 |

RDS는 SQL과 자원 상태를 알지만 그 SQL이 Runner 2의 recovery인지는 알지 못한다.
현재 Gap metadata에는 최신 `phase`, `attempt`, `leaseExpiresAt`,
`phaseDurationsMs`가 남는다. 상태 전이 history와 recovery 성공률을 계산할
append-only event와 운영 소비자는 없다.

RDS 기본 지표를 복제하지 않고 Lighthouse domain event만 추가하는 경계는
[#428](https://github.com/corca-ai/lighthouse/issues/428)에서 추적한다. Telemetry
저장 실패는 Gap build 결과를 바꾸면 안 된다.

## 증거와 완료 판정

리뷰 발견에는 다음 증거를 연결한다.

| 증거   | 확인할 내용                                          |
| ------ | ---------------------------------------------------- |
| 코드   | 입력, principal, 상태와 effect가 어디로 흐르는가?    |
| DB     | RLS, unique, CAS, lease가 잘못된 쓰기를 막는가?      |
| 테스트 | 정상 caller뿐 아니라 누락·충돌·중단도 실패시키는가?  |
| 운영   | p99, 5xx, pending age, 비용과 recovery를 관측하는가? |

Architecture Fitness는 승인한 좁은 구조 정책을 exact revision에서 검증한다.
`healthy`는 해당 case만 통과했다는 뜻이다. 전체 보안, 검색 관련성, production
fleet 부하와 운영 관측까지 자동으로 보장하지 않는다. 지원하지 않는 범위는
`unknown`으로 남긴다.

최신 적용 범위는
[`architecture-fitness/README.md`](https://github.com/corca-ai/lighthouse/blob/main/docs/architecture-fitness/README.md)에서
확인한다.

### 실제 DB에서 다시 확인하는 이유

코드 검토, mock 테스트, 실제 DB 테스트는 서로 다른 질문에 답한다.

| 증거                | 확인하는 것                                                                         |
| ------------------- | ----------------------------------------------------------------------------------- |
| 코드 검토           | CAS, owner filter, unique 충돌 복구의 의도가 맞는가?                                |
| Mock 테스트         | 애플리케이션이 예상한 성공·충돌 분기를 처리하는가?                                  |
| 실제 DB 경쟁 테스트 | PostgreSQL의 MVCC, lock, constraint, RLS와 driver 응답이 그 보장을 실제로 지키는가? |

전문가가 실제 DB 증거를 요구하는 이유는 여러 서버의 write가 결국 같은 DB
constraint와 transaction 규칙을 통과하기 때문이다. 애플리케이션 코드는 충돌
처리를 요청하지만 unique index, lock과 RLS가 실제로 어떤 write를 허용할지는
DB가 결정한다. Mock은 나쁜 증거가 아니지만 DB가 직접 수행하는 동작까지
증명하지는 못한다.

Lighthouse의 Gap report라면 운영과 같은 migration·DB role을 사용해 다음을
검증한다.

- 두 session이 같은 `expectedVersion`과 서로 다른 payload로 갱신하면 하나만
  성공하고 최종 version은 한 번만 증가하는가?
- 같은 canonical digest를 동시에 예약해도 artifact가 하나만 남는가?
- lease를 잃은 stale runner가 최신 결과를 덮어쓰지 못하는가?

여기서 CAS가 보장하는 것은 계산을 한 번만 한다는 뜻이 아니라 **최종 commit
하나만 인정한다**는 뜻이다. 실제 PostgreSQL 경쟁 테스트는
[#426](https://github.com/corca-ai/lighthouse/issues/426)에서 추적한다.

## 리뷰 체크리스트

- 사용자 행동과 보장 결과를 한 문장으로 적었는가?
- 핵심 필드와 상태 owner를 찾았는가?
- 정상·실패·중단을 모두 확인했는가?
- 정확성·보안·회복성·부하를 겹쳐 확인했는가?
- 공유 데이터와 개인 데이터를 구분했는가?
- Application filter와 DB 강제를 구분했는가?
- Process-local 보호와 fleet 전체 보장을 구분했는가?
- 코드, DB, 테스트, 운영 증거를 연결했는가?
- 발견을 영향도·가능성·노출로 우선순위화했는가?
- 지원하지 않는 범위를 `unknown`으로 남겼는가?

## 학습 퀴즈

별도
[`lighthouse-backend-review-quiz.html`](./lighthouse-backend-review-quiz.html)을
사용한다. 한 문제씩 Lighthouse의 실제 migration, route와 repository 코드를
판단한다. 답안과 복습 상태는 현재 브라우저에 저장된다.

[`lighthouse-backend-review-quiz`](./lighthouse-backend-review-quiz)는
텍스트로 학습 방법과 해설을 훑을 때 사용하는 참고본이다. 학습 진입점과 최신
실전 문항은 HTML 퀴즈다. 한 번에 전체 점수를 내지 않는다. 약한 영역을 확인하고
해당 단계만 다시 푼다.

## 참고 자료

- [Light House 제품 정체성](https://github.com/corca-ai/lighthouse/blob/main/docs/product-identity.md)
- [검색 runtime flow](https://github.com/corca-ai/lighthouse/blob/main/docs/runtime-flows/search-mechanism.md)
- [Gap report runtime flow](https://github.com/corca-ai/lighthouse/blob/main/docs/runtime-flows/gap-network-analysis.md)
- [운영 준비도](https://github.com/corca-ai/lighthouse/blob/main/docs/operational-readiness.md)
- [Lighthouse Architecture Fitness integration](https://github.com/corca-ai/lighthouse/blob/main/docs/architecture-fitness/README.md)
- [Architecture Fitness workload envelope](https://github.com/jaeyoung2026/architecture-fitness/blob/main/skills/architecture-fitness-review/references/workload-envelope.md)
- [Architecture Fitness critical path](https://github.com/jaeyoung2026/architecture-fitness/blob/main/skills/architecture-fitness-review/references/critical-path.md)
- [Amazon CloudWatch Database Insights](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Database-Insights.html)
- [Google SRE Book](https://sre.google/sre-book/table-of-contents/)
- [OWASP Least Privilege Principle](https://owasp.org/www-community/controls/Least_Privilege_Principle)
- [PostgreSQL Index Uniqueness Checks](https://www.postgresql.org/docs/current/index-unique-checks.html)
