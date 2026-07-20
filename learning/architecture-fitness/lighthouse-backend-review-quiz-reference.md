---
layout: default
title: Lighthouse 백엔드 리뷰 퀴즈 해설
---

# Lighthouse 사례로 배우는 백엔드 리뷰 퀴즈

이 문서는 Lighthouse 코드를 검토하면서 백엔드 판단력을 단계적으로 훈련한다.
용어를 외우는 데서 끝나지 않는다. 코드를 읽고 실패를 예측하며, 제한된 정보에서
결정을 내리고 필요한 증거를 요청하는 수준까지 올라가는 것이 목표다.

정본은
[`lighthouse-backend-review-guide`](./lighthouse-backend-review-guide)다.
문제를 먼저 풀고 같은 단계의 해설을 확인한다.

브라우저에서 한 문제씩 풀고 진도를 저장하려면
[`lighthouse-backend-review-quiz.html`](./lighthouse-backend-review-quiz.html)을
연다. 외부 서버 없이 동작하며 답안은 현재 브라우저에만 저장된다.

## 학습 방법

네 단계를 순서대로 진행한다.

| 단계 | 훈련할 역량                  | 통과 기준                                               |
| ---- | ---------------------------- | ------------------------------------------------------- |
| 1    | 기술 용어를 동작으로 설명    | 용어 없이도 무엇을 막는지 설명한다.                     |
| 2    | 코드에서 경계와 실패 발견    | 코드 줄과 발생 가능한 실패를 연결한다.                  |
| 3    | 좋은 구현과 부족한 구현 비교 | 장점, 남은 위험과 과도한 설계를 함께 말한다.            |
| 4    | 시니어 의사결정              | 보장, 위험, 대안, 결정과 검증 증거를 순서대로 제시한다. |

정답 문장을 그대로 외우지 않는다. 다음 네 항목이 들어가면 표현이 달라도 맞다.

```text
관찰한 사실
→ 깨질 수 있는 보장
→ 선택한 대응과 범위
→ 완료를 확인할 증거
```

총점으로 약한 영역을 가리지 않는다. 코드 문제는 실행하지 않아도 되지만 실제
구현을 열어 근거를 확인하는 습관을 권장한다.

문항 수보다 예상 풀이시간을 기준으로 세션을 끊는다.

| 세션 | 문항         | 권장 시간 | 초점                                  |
| ---- | ------------ | --------- | ------------------------------------- |
| A    | 1–6          | 15분      | API 입구와 작업 중복                  |
| B    | 7–12         | 15분      | 동시성, 권한, 실행 범위와 상태        |
| C    | 13–17A       | 20분      | API 코드의 거부 순서                  |
| D    | 17B–21       | 20분      | 비용 테스트, dedupe와 partial failure |
| E    | 22–27 중 3개 | 20분      | 구현 비교와 증거의 한계               |
| F    | 28–31 중 1개 | 20분      | 리뷰 우선순위와 입력 정책             |
| G    | 32–35 중 1개 | 20분      | 재시도, 권한, 운영과 공통 mechanism   |
| H    | 36–40        | 20분      | 실제 DB identity와 오류 계약          |
| I    | 41–46        | 20분      | Transaction, version과 저장 경계      |
| J    | 47–50        | 20분      | LLM fan-out, admission과 부하 증거    |
| K    | 51–54        | 20분      | 배포 topology와 상태 수명             |

### 역량별 평가

각 축을 0~3으로 따로 기록한다. 네 점수를 평균내서 통과시키지 않는다. 단계마다
평가할 축이 다르다.

| 축        | 0                      | 1                     | 2                                   | 3                                        |
| --------- | ---------------------- | --------------------- | ----------------------------------- | ---------------------------------------- |
| 용어      | 개념을 혼동한다.       | 정의를 기억한다.      | Lighthouse 사례로 설명한다.         | 비슷한 개념의 경계를 설명한다.           |
| 코드      | 실행 흐름을 못 찾는다. | 위험 줄을 지목한다.   | 안전한 순서나 수정을 제시한다.      | 실패 테스트로 보장을 고정한다.           |
| 제품 보장 | 코드 모양만 본다.      | 발생할 증상을 말한다. | 깨지는 사용자·데이터 보장을 잇는다. | 정상·실패·중단과 운영 영향까지 확장한다. |
| 의사결정  | 취향을 말한다.         | 해결책 하나를 고른다. | 대안과 trade-off를 비교한다.        | 증거, 재검토 조건과 owner를 명시한다.    |

단계별 문항의 약 70%를 자신의 말로 설명하고, 아래 대상 축이 모두 2 이상이면 다음
단계로 이동한다.

| 단계 | 평가할 축                       |
| ---- | ------------------------------- |
| 1    | 용어, 제품 보장                 |
| 2    | 용어, 코드, 제품 보장           |
| 3    | 코드, 제품 보장, 의사결정       |
| 4    | 용어, 코드, 제품 보장, 의사결정 |

### 현재 상태와 권장안

코드 문제의 축약 snippet은 학습용이다. 실제 구현과 다를 수 있으므로 연결한
Lighthouse 파일에서 확인한다. 해설은 다음 표현을 구분한다.

- **현재**: 지금 코드와 테스트에서 확인한 사실이다.
- **권장**: 이번 리뷰에서 제안한 개선 방향이다.
- **미확인**: 배포 플랫폼, production 지표나 승인된 정책 증거가 부족하다.

---

# 1단계: 기술 용어를 동작으로 이해한다

## 세션 A 용어 카드

| 용어                    | 한국어 뜻                        | Lighthouse 사례                                 |
| ----------------------- | -------------------------------- | ----------------------------------------------- |
| Zod                     | JSON 안의 필드 형식과 값 검사    | `query`가 비어 있지 않은 문자열인지 검사한다.   |
| Bounded body            | 읽을 요청 byte에 상한을 둠       | Gap route가 1MB를 넘으면 읽기를 중단한다.       |
| 인증·권한               | 누구인지 확인·무엇을 할지 허용   | A의 로그인과 reaction 수정 허용은 다르다.       |
| Rate limit              | 일정 시간의 요청 수를 제한       | 서로 다른 query 폭주를 `429`로 거부한다.        |
| In-flight deduplication | 진행 중인 같은 일을 하나로 합침  | 권장안에서는 동일 spelling 요청을 합칠 수 있다. |
| Idempotency             | 반복 요청을 같은 효과로 수렴시킴 | 같은 Gap artifact 예약이 하나로 수렴한다.       |

## 문제

### 1. Zod와 bounded body

다음 두 장치의 책임을 각각 한 문장으로 설명하라.

```ts
await readBoundedJsonBody(req, { maxBytes: 1_000_000 });
schema.safeParse(body);
```

둘 중 하나만 사용했을 때 남는 위험도 적어라.

### 2. HTTP 상태 코드

다음 상황을 `400`, `401`, `403`, `413`, `429`와 연결하라.

1. 로그인하지 않았다.
2. JSON의 `query`가 숫자다.
3. 1MB 제한 route에 2MB body를 보냈다.
4. 로그인했지만 허용되지 않은 운영자 API를 호출한다.
5. 사용자별 동시 Gap build 한 개를 이미 실행 중이다.

### 3. 인증과 권한

인증과 권한 확인의 차이를 Lighthouse reaction으로 설명하라. 현재 API가
사용자 A에게 사용자 B의 principal을 지정할 수 있게 하는지도 확인하라.

### 4. Rate limit과 in-flight deduplication

다음 두 상황에 각각 어떤 장치를 적용할지 결정하라.

- 같은 사용자가 동일한 query와 metadata로 1초 안에 세 번 요청했다.
- 같은 사용자가 서로 다른 query 100개를 1초 안에 요청했다.

### 5. Idempotency

사용자가 네트워크 오류 때문에 Gap 생성 버튼을 다시 눌렀다. 같은 입력의 artifact
예약이 하나로 수렴하는 성질을 무엇이라 하는가? Lighthouse에서는 어떤 값과 DB
장치가 이 성질을 돕는가? Gap POST의 모든 effect가 항상 같다고 말할 수 있는지도
답하라.

### 6. Lease

`leaseExpiresAt = now + 70초`가 저장됐다. 70초 뒤 서버가 자동으로 Runner 2를
실행하는가? Lease가 허용하는 것과 직접 실행하지 않는 것을 나누어 설명하라.

## 세션 B 용어 카드

| 용어                     | 한국어 뜻                                 | Lighthouse 사례                                      |
| ------------------------ | ----------------------------------------- | ---------------------------------------------------- |
| Lease                    | 제한된 시간 동안 작업 소유권을 빌림       | 만료 뒤 새 Runner가 Gap attempt를 인수할 수 있다.    |
| CAS                      | 읽은 version이 그대로일 때만 갱신         | 오래된 Runner의 최종 저장을 거부한다.                |
| RLS·service role         | DB row 접근 정책·그 정책을 우회하는 권한  | Service role에서는 owner filter 누락이 더 위험하다.  |
| Process-local·fleet-wide | 한 process 범위·모든 instance를 합친 범위 | Episteme queue 4개가 fleet 전체 4개를 뜻하지 않는다. |
| Partial failure          | 일부 결과는 유효하고 일부 단계만 실패     | Gap core는 ready이고 enrichment만 failed일 수 있다.  |
| p95·p99                  | 느린 요청 경계를 보는 응답시간 백분위     | 느린 5%와 1%가 어디까지 지연되는지 본다.             |
| Canonical identity       | 같은 작업으로 볼 입력 차이를 정하는 기준  | Gap digest에 참여하는 필드를 결정한다.               |

### 7. CAS

CAS가 비교하는 값은 무엇이며 무엇을 막는가? CAS가 같은 계산을 절대로 두 번
실행하지 않게 만드는지도 답하라.

### 8. RLS와 service role

Repository가 `.eq("owner_principal_id", userId)`를 사용한다. DB client가
service role이라면 사용자 격리가 충분한가? Application filter와 DB 강제의
차이를 설명하라.

### 9. Process-local과 fleet-wide

Episteme queue가 process마다 동시 실행을 4개로 제한한다. 고정 서버 instance
10개라면 provider에는 이론상 최대 몇 개가 동시에 갈 수 있는가?

현재 Lighthouse의 Vercel Fluid에서는 같은 계산으로 fleet 상한을 확정할 수
있는지도 설명하라.

### 10. Partial failure

Gap core는 준비됐지만 enrichment가 실패했다. 전체 실패로 처리하지 않는 이유와
사용자에게 남겨야 할 상태를 설명하라.

### 11. p95와 p99

평균 응답시간이 500ms라는 사실만으로 느린 사용자가 없다고 말할 수 없는 이유를
설명하라. Provider queue 운영에서 p95나 p99가 답하는 질문은 무엇인가?

### 12. Canonical identity

같은 Gap 입력을 판단하는 canonical digest에 결과를 바꾸는 필드 하나가 빠졌다.
어떤 문제가 생기는가? Canonical identity를 단순한 ID 생성 방식이라고만 보면
안 되는 이유를 설명하라.

## 해설

### 1. Zod와 bounded body

`readBoundedJsonBody`는 body를 제한된 크기까지만 읽고 초과하면 `413`으로
거부한다. Zod는 허용된 크기의 JSON 안에서 필드 형식과 값을 검사하고 잘못되면
`400`으로 거부한다.

Zod만 사용하면 큰 body를 이미 메모리에 올리고 parse한 뒤 거부할 수 있다.
크기 제한만 사용하면 작지만 잘못된 형식이나 위험한 값을 통과시킬 수 있다.

### 2. HTTP 상태 코드

순서대로 `401`, `400`, `413`, `403`, `429`다. 네 번째는 일반적인 권한 거부
사례다. 상태 코드는 서버 내부 분류가
아니다. 호출자가 로그인, 입력 수정, 크기 축소, 권한 변경, 대기 중 무엇을 해야
하는지 알려주는 계약이다.

### 3. 인증과 권한

인증은 요청한 주체가 A임을 확인한다. 권한 확인은 A가 해당 reaction을 읽거나
바꿀 수 있는지 판단한다. 현재 Lighthouse reaction API는 target principal을
caller에게 받지 않고 인증된 principal을 서버에서 넣는다. A가 B를 지정하는 표현
자체를 제거한 구조다. `403`을 반환하는 것보다 더 앞에서 권한 범위를 좁혔다.

### 4. Rate limit과 in-flight deduplication

동일한 진행 중 요청 세 개는 하나로 합치고 같은 결과를 돌려줄 수 있다. 서로
다른 요청 100개는 합칠 수 없으므로 사용자별 rate·concurrency limit을 적용하고
초과분을 `429`로 거부한다. 두 장치는 서로 대체하지 않는다.

### 5. Idempotency

같은 의도의 반복 요청이 같은 효과로 수렴하는 성질을 idempotency라고 한다.
Lighthouse Gap 생성에서는 canonical digest와 DB unique constraint가 같은 입력의
artifact 예약을 하나로 수렴시킨다. 범위는 artifact identity다. Failed artifact에
대한 다음 POST는 pending 전환과 retry를 시작할 수 있으므로 POST 전체의 모든
effect가 항상 같다고 확장하면 안 된다.

### 6. Lease

Lease 만료는 새 Runner가 작업 소유권을 획득할 수 있게 한다. 만료 시각 자체는
timer나 worker가 아니므로 아무 작업도 자동으로 시작하지 않는다. 현재는 다음
조회나 recovery 요청이 만료를 관찰해야 Runner 2를 시작할 수 있다.

### 7. CAS

CAS는 저장된 version과 caller가 읽었던 `expectedVersion`이 같은지 비교한 뒤
갱신한다. 오래된 Runner가 최신 결과를 덮어쓰는 일을 막는다. 계산이 잠시
중복되는 것은 막지 않으며 최종 commit 하나만 인정한다.

### 8. RLS와 service role

충분하지 않다. Application filter가 빠지면 service role은 RLS를 우회해 다른
사용자의 row에 접근할 수 있다. Filter는 올바른 코드 작성에 의존한다. DB 정책은
실수한 코드도 데이터 경계에서 거부한다.

### 9. Process-local과 fleet-wide

모든 instance가 같은 provider를 향하고 각 process에 queue가 하나라면 이론상
40개다. Vercel Fluid에서는 Function instance가 동적으로 추가·재사용·폐기되고
route와 region별로 module state 사본이 달라질 수 있다. 따라서 고정된 10개라는
전제가 없다. Function별 active work와 같은 시간창에 겹친 instance를 측정해야
한다. Process-local 상한을 fleet 전체 상한으로 보고하면 안 된다.

### 10. Partial failure

사용 가능한 core를 버리면 사용자는 이미 완성된 결과를 잃고 재시도 비용도
증가한다. Lifecycle은 terminal이어도 결과 품질은 degraded일 수 있다. Core
결과, enrichment 실패 상태와 명시적인 재시도 가능 여부를 함께 남겨야 한다.

### 11. p95와 p99

평균은 빠른 다수의 요청이 매우 느린 일부 요청을 가린다. p95는 95%의 요청이
어느 시간 안에 끝나는지, p99는 가장 느린 1% 경계가 어디인지 보여준다. Queue
대기와 provider timeout이 일부 사용자에게 집중되는지 판단할 때 필요하다.

### 12. Canonical identity

의미가 다른 두 입력이 같은 artifact로 합쳐져 잘못된 결과를 재사용할 수 있다.
Canonical identity는 문자열을 만드는 기법이 아니다. 어떤 차이를 같은 작업으로
볼지 결정하는 제품·데이터 계약이다.

---

# 2단계: 코드에서 실패를 찾는다

코드는 학습을 위해 핵심 부분만 줄였다. 실제 현재 상태는 각 링크에서 확인한다.

## 문제

### 13. 늦은 크기 검증

```ts
const body = await req.json();
const parsed = schema.safeParse(body);
```

이 코드는 잘못된 JSON 형식을 거부한다. 그래도 ingress 보호가 충분하지 않은
이유와 최소 수정 방향을 적어라.

### 14. 인증 순서

Lighthouse term discovery의 축약 코드다.

```ts
const body = await req.json();
const parsed = requestSchema.safeParse(body);
if (!parsed.success) return badRequest();

const { db, user } = await requireOwnerPrincipalAuth();
return runLlmWork({ db, user, input: parsed.data });
```

공격자가 로그인하지 않고 큰 body를 반복해서 보낸다면 어떤 비용이 먼저
발생하는가? 인증된 사용자만 쓰는 route라는 정책을 유지할 때 순서를 다시 써라.

### 15. 좋은 ingress 순서

Lighthouse Gap route의 축약 코드다.

```ts
const { db, user } = await requireOwnerPrincipalAuth();
const body = await readBoundedJsonBody(req, { maxBytes });
const collectionIssues = listCollectionLimitIssues(body);
const parsed = gapNetworkPostSchema.safeParse(body);
```

각 줄이 막는 실패를 설명하라. `listCollectionLimitIssues`가 Zod보다 먼저 있는
이유도 추론하라.

### 16. 이름이 주는 오해

```ts
export function withRouteGuard(handler) {
  try {
    return await handler();
  } catch (error) {
    if (error instanceof UnauthenticatedError) return response(401);
    if (error instanceof ForbiddenError) return response(403);
    throw error;
  }
}
```

이 wrapper가 자동으로 제공하지 않는 보호 세 가지를 적어라. 코드 리뷰에서
이름만 보고 “guard가 있으니 안전하다”고 결론 내리지 않으려면 무엇을 확인해야
하는가?

### 17A. Spelling correction 위험 찾기

```ts
const schema = z.object({
  query: z.string().trim().min(1),
  metadata: searchMetadataSchema,
});

const body = await req.json();
const parsed = schema.safeParse(body);
if (!parsed.success) return badRequest();
const corrected = await resolveSearchSpellingCorrection(parsed.data.query);
```

최소 네 가지 위험 또는 미결정 정책을 찾아 우선순위를 정하라. 단순히 “검증을
더한다”고 답하지 말고 각 검사가 무엇을 보호하는지 적어라.

### 17B. 비용이 발생하지 않았다는 테스트

인증되지 않은 요청이 `401`을 받는 것뿐 아니라 LLM 비용도 발생시키지 않았음을
검증하는 assertion을 작성하라. 응답 코드 검사만으로 충분한지도 설명하라.

### 18. 중복 실행 key

현재 spelling correction에는 in-flight dedupe가 없다. #430 보강에서 이를
도입한다면 다음 중 key로 가장 적절한 것을 고르고 이유를 설명하라.

1. `query`
2. `userId + normalizedQuery`
3. `userId + normalizedQuery + 결과에 영향을 주는 metadata projection`
4. `Date.now()`

Metadata 전체를 그대로 key로 사용할 때 생길 수 있는 문제도 적어라.

### 19. CAS 갱신

두 Runner가 version 3을 읽었다. 다음 조건으로 동시에 update한다.

```sql
UPDATE gap_reports
SET metadata = :metadata, version = version + 1
WHERE id = :id AND version = 3;
```

Runner 1이 먼저 성공한 뒤 Runner 2의 affected row 수는 몇 개인가? 애플리케이션은
0을 오류, 재시도 또는 stale result 거부 중 무엇으로 해석해야 하는가?

### 20. Partial failure를 지우는 코드

```ts
try {
  const core = await buildCore();
  const enrichment = await enrich(core);
  await saveReady({ core, enrichment });
} catch {
  await saveFailed();
}
```

Enrichment만 실패했을 때 어떤 유효한 결과가 사라지는가? 상태와 저장 순서를
어떻게 나눌지 의사코드로 작성하라.

### 21. 조회가 작업을 시작한다

```ts
export async function GET(id) {
  const report = await findReport(id);
  if (report.enrichmentStatus === "failed") {
    void retryEnrichment(report);
  }
  return report;
}
```

이 코드가 재방문과 polling에서 만들 수 있는 문제를 설명하라. Lighthouse에서
제품 요구사항으로 승인했지만 아직 구현하지 않은 명시적 재시도 계약에 맞는 API
경계를 제안하라.

## 해설

### 13. 늦은 크기 검증

`req.json()`이 body 전체를 읽고 JSON parse를 끝낸 뒤 Zod가 실행된다. 따라서
메모리와 parse 비용을 제한하지 못한다. Stream 또는 `Content-Length`를 신뢰
가능한 범위에서 확인하고, 실제 읽은 byte를 누적해 상한을 넘으면 중단하는
bounded reader를 schema 검증 앞에 둔다.

### 14. 인증 순서

현재 순서에서는 body 수신, JSON parse와 Zod 검증 비용이 인증보다 먼저 든다.
정책이 authenticated-only라면 먼저 principal을 확인하고, bounded body와 schema를
거친 뒤 LLM을 호출한다.

```ts
const { db, user } = await requireOwnerPrincipalAuth();
const body = await readBoundedJsonBody(req, { maxBytes });
const parsed = requestSchema.safeParse(body);
if (!parsed.success) return badRequest();
return runLlmWork({ db, user, input: parsed.data });
```

인증 전에 body를 읽어야 하는 framework 제약이 있다면 상위 proxy나 platform에서
더 싼 admission과 byte ceiling을 강제해야 한다.

### 15. 좋은 ingress 순서

첫 줄은 인증되지 않은 요청을 비싼 입력 처리 전에 거부한다. 둘째 줄은 body
byte를 제한한다. 셋째 줄은 큰 배열이나 중첩 collection을 상세 parse 전에
빠르게 거부한다. 마지막 줄은 허용된 입력의 필드 형식과 관계를 검증한다.

Precheck가 필요한지는 schema 비용과 구현 복잡도를 측정해 결정한다. 모든 route에
무조건 복사하면 안 된다.

### 16. 이름이 주는 오해

이 wrapper는 인증을 수행하지 않고 body 크기나 호출량도 제한하지 않는다. 발생한
인증·권한 오류를 HTTP 상태로 바꿀 뿐이다. Reviewer는 handler 안의 인증 호출,
bounded reader, schema, rate·concurrency control과 effect 호출 순서를 직접
추적해야 한다.

### 17A. Spelling correction 위험 찾기

우선순위가 높은 후보는 다음과 같다.

1. Route 공개성·인증 정책을 정한다. 현재 route 안에는 명시적 principal 확인이
   없으므로 누구의 비용인지 귀속할 수 없다.
2. Body byte와 `query` 최대 길이를 제한한다. 메모리·prompt 크기와 LLM 비용을
   통제한다.
3. 사용자별 rate·concurrency budget을 정한다. 인증된 UI 버그나 반복 호출도
   비용 폭주를 만들 수 있다.
4. 동일한 진행 중 입력을 dedupe하고 짧은 cache 정책을 검토한다.
5. Metadata에서 결과에 영향을 주는 필드와 cardinality 상한을 정한다.

정확한 숫자는 코드에서 추정하지 않는다. 제품 사용량과 provider allowance를
근거로 승인해야 한다.

### 17B. 비용이 발생하지 않았다는 테스트

응답 코드만 확인하면 route 뒤의 effect가 실행됐는지 알 수 없다. 비용 경계는 다음
negative assertion으로 잠근다.

```ts
expect(response.status).toBe(401);
expect(resolveSearchSpellingCorrection).not.toHaveBeenCalled();
```

### 18. 중복 실행 key

현재는 dedupe가 없다. 도입한다면 LLM 결과에 전달되는 입력은 query뿐이므로
2번이 맞다. 이는 route 인증과 principal 귀속을 추가한 뒤의 권장 설계다. Principal을
포함해 사용자 사이의 진행 상태와 비용 귀속을 섞지 않는다. 향후 metadata가
prompt나 결과에 참여한다면 3번으로 확장하되 결과 의미에 참여하는 필드만
canonical projection으로 만든다. Metadata 전체를 직렬화하면 결과와 무관한
timestamp나 필드 순서 차이로 dedupe가 깨지고 key가 과도하게 커질 수 있다.

### 19. CAS 갱신

Runner 1이 version을 4로 올렸으므로 Runner 2의 affected row는 0이다. 이는 DB
오류가 아니라 “내가 읽은 version은 더 이상 최신이 아니다”라는 정상적인 경쟁
결과다. 오래된 결과를 버리고 최신 row를 읽는다. 자동 재시도는 새 결과가 여전히
유효하고 비용상 허용될 때만 별도 정책으로 결정한다.

### 20. Partial failure를 지우는 코드

문제에 제시된 나쁜 코드는 이미 완성된 core를 저장하지 못한다. Core와
enrichment의 milestone을 독립적으로 저장해야 한다.

```ts
const core = await buildCore();
await saveCoreReady(core);

try {
  const enrichment = await enrich(core);
  await saveEnrichmentReady(enrichment);
} catch (error) {
  await saveEnrichmentFailed(error);
}
```

Core 자체가 실패했을 때만 report 전체를 실패로 닫는다.

현재 Lighthouse는 core를 먼저 저장한 뒤 enrichment를 실행하고, enrichment 실패를
별도 상태로 닫는다. 이 문제의 좋은 대조 사례다.

### 21. 조회가 작업을 시작한다

Polling과 새로고침이 LLM 재시도를 반복하고 비용·동시성·상태 전이를 숨긴다.
현재 Lighthouse 조회는 저장된 상태만 반환한다. 명시적 재시도 제품 요구사항은
승인됐지만 아직 구현되지 않았다. 권장안은 별도
`POST /api/gap-reports/:id/enrichment-retries` 같은 command route가 인증,
현재 상태, CAS, lease와 admission을 검사한 뒤 재시도를 시작해야 한다.

---

# 3단계: 좋은 사례와 부족한 사례를 비교한다

## 문제

### 22. 모든 route에 같은 middleware

팀이 모든 API에 `1MB`, 분당 10회, 사용자별 동시 실행 1개를 공통 middleware로
적용하려 한다. 일관성은 좋아 보인다. 그대로 채택할지, route별 정책으로 나눌지
결정하라.

### 23. 공개 Magic link

Magic link는 로그인 전 호출하므로 사용자 인증을 요구할 수 없다. 다음 대안을
비교하고 Lighthouse에 필요한 조합을 제안하라.

- 이메일 allowlist만 검사한다.
- IP/source rate limit을 둔다.
- 이메일 주소별 cooldown을 둔다.
- CAPTCHA를 항상 요구한다.
- Supabase provider 제한에만 의존한다.

### 24. Provider 실패와 빈 결과

Episteme가 timeout일 때 빈 배열과 `200`을 반환하는 구현과, provider 실패 상태를
별도로 반환하는 구현을 비교하라. 두 번째 구현에서도 화면을 계속 사용할 수
있는 방법을 설명하라.

### 25. Reaction write와 spelling correction

Reaction write는 DB write이고 spelling correction은 LLM 호출이다. 두 route의
스크리닝을 비용 순서 하나로만 비교하면 무엇을 놓치는가? 각각 가장 중요한
보장을 두 개씩 선정하라.

### 26. Process-local queue

Episteme queue의 unit test가 통과했고 process당 동시 실행 상한도 지켜졌다. 이를
production provider 보호 완료로 판정할 수 있는가? 추가로 필요한 증거를 세
가지 적어라. 장기 실행 고정 서버와 Vercel Fluid에서 증거가 어떻게 달라지는지도
포함하라.

### 27. Mock과 실제 PostgreSQL

CAS repository mock test에서 두 번째 update가 0 row를 반환하는 분기가 통과했다.
실제 DB 경쟁 테스트를 생략해도 되는가? 생략할 수 있는 조건과 반드시 해야 하는
조건을 나누어 설명하라.

## 해설

### 22. 모든 route에 같은 middleware

공통 기계 장치는 재사용할 수 있지만 정책 숫자까지 같을 필요는 없다. 조회,
DB write, telemetry, provider와 LLM route는 payload와 비용이 다르다. Route
inventory에서 공개성, effect, body envelope, rate, concurrency와 deadline을
선언하고 공통 helper가 그 정책을 실행하게 한다.

작은 내부 조회에 과한 제한을 두면 UX를 해친다. 고비용 LLM route에 느슨한 공통
제한을 두면 비용을 막지 못한다.

### 23. 공개 Magic link

Allowlist는 누가 가입 가능한지 제한하지만 허용 이메일에 대한 반복 발송을 막지
않는다. Source rate limit과 이메일별 cooldown을 함께 두고 provider의 실제 제한을
보조 방어로 사용한다. CAPTCHA는 공격 증거와 UX 비용을 보고 단계적으로 도입한다.

Process-local source limit만 있다면 autoscaling 뒤 전체 상한이 늘어난다. Platform
또는 shared store가 fleet 책임을 맡는지 명시해야 한다.

### 24. Provider 실패와 빈 결과

빈 배열과 `200`은 “관련 논문이 없음”과 “검색하지 못함”을 같은 의미로 만든다.
Provider 실패 상태를 분리하면 사용자가 결과의 신뢰 범위를 알 수 있다. 이전
snapshot이나 이미 받은 결과를 유지하고 degraded 안내와 제한된 재시도를 제공하면
화면 전체를 실패시키지 않아도 된다.

### 25. Reaction write와 spelling correction

Spelling correction은 비용, latency와 호출량이 중요하다. Reaction은 다른
사용자의 개인 상태를 바꾸지 않는 격리, 중복 클릭과 경쟁 쓰기에서의 일관성이
중요하다. 비용이 더 높은 route가 모든 보안 축에서도 더 위험한 것은 아니다.

### 26. Process-local queue

판정할 수 없다. 현재 instance·process 수, autoscaling peak, provider account
allowance, 요청당 fan-out, production queue wait·timeout·5xx가 필요하다. 단위
테스트는 한 process의 알고리즘만 증명한다. 고정 서버에서는 배포 replica 수를
곱해 상한 후보를 계산할 수 있다. Vercel Fluid에서는 route·region별 Function
instance와 같은 시간창의 overlapping active work를 관측해야 한다.

### 27. Mock과 실제 PostgreSQL

순수한 분기 처리만 검증할 때 mock으로 충분할 수 있다. 그러나 MVCC, lock,
unique constraint, RLS, driver affected-row semantics가 보장의 최종 판정자라면
실제 migration과 role을 사용한 경쟁 테스트가 필요하다.

---

# 4단계: 시니어의 의사결정을 연습한다

각 답은 다음 형식으로 작성한다.

```text
보장:
관찰:
위험:
결정:
대안과 기각 이유:
검증:
재검토 조건:
```

## 문제

### 28. 첫 리뷰 우선순위

다음 세 발견 중 무엇부터 조사할지 순서를 정하라.

1. `search-execution.ts`가 600줄이다.
2. Spelling correction route에 명시적 인증과 비용 상한이 없다.
3. Gap report 변수 이름이 일관되지 않다.

영향도, 발생 가능성, 발견 난이도와 사용자 보장을 근거로 답하라.

### 29. 사용자별 Gap build 한 개

Gap build 총수가 아직 적다. 사용자별 active build를 한 개로 제한하자는 제안이
나왔다. 지금 구현할지 미룰지 결정하라. 조회와 status polling까지 막을지도
판단하라.

### 30. 동일 query 세 번

같은 사용자가 같은 query를 1초 안에 세 번 요청했다. 모두 실행, 두 개 `429`,
하나만 실행하고 결과 공유 중 하나를 선택하라. 서로 다른 query 100개가 들어왔을
때 결정이 어떻게 달라지는지도 설명하라.

### 31. 잘못된 year

URL의 `year=garbage`가 provider 요청에서는 빠졌지만 화면에는 필터처럼 남는다.
조용히 기본 검색으로 복구, `400` 거부, 경고 후 canonical URL로 정리 중 하나를
선택하라. 과거에 저장한 필터가 잘못 적용된 상황과 사용자가 직접 오타를 낸
상황을 구분할 필요가 있는지도 판단하라.

### 32. Enrichment 재시도

Gap core는 ready이고 enrichment만 failed다. 페이지를 열 때 자동 재시도, 제한된
서버 자동 재시도, 사용자의 “분석 다시 시도” command 중 하나를 선택하라.
중복 클릭과 stale Runner를 어떻게 처리할지도 포함하라.

### 33. Service role 제거

일반 사용자 request가 service-role DB client를 감싼 repository를 사용한다.
모든 repository에 owner filter 테스트가 있다. 그대로 유지할지, session-bound
client와 RLS로 옮길지 결정하라. Shared Gap artifact와 운영 telemetry writer를
같은 권한으로 처리해도 되는가?

### 34. 운영 장애

Production에서 검색 p99가 증가했다. Episteme console log에는 queue wait가
남지만 사용자별 grounding 결과와 instance 수는 집계되지 않는다. 원인을
단정하지 말고 조사 순서, 필요한 지표와 임시 완화책을 제안하라.

### 35. 공통 route 정책 도입

GitHub #430을 구현하면서 팀이 하나의 `secureRoute()` wrapper에 인증, 1MB body,
Zod, 분당 10회와 30초 deadline을 모두 넣으려 한다. 유지할 공통 mechanism과
route가 소유할 policy를 나누어 설계하라. Wrapper 이름과 테스트 전략도 포함하라.

## 판단 기준

### 28. 첫 리뷰 우선순위

2번을 먼저 본다. 비용이 실제 발생하는 공개 가능 경계이며 인증·호출량 정책
공백은 운영 사고로 이어질 수 있다. 1번은 변경 비용의 신호지만 길이만으로
사용자 보장이 깨졌다고 말할 수 없다. 3번은 의미 혼동이 실제 결함을 만들 때
우선순위를 올린다.

좋은 답은 순위만 제시하지 않는다. 먼저 현재 공개성, caller, provider effect와
운영 호출량을 확인한 뒤 심각도를 확정한다고 쓴다.

### 29. 사용자별 Gap build 한 개

현재 총수가 적다면 작은 admission rule로 시작할 수 있다. DB에서 principal과
active lease/state를 기준으로 원자적으로 한 개만 허용해야 여러 instance에서도
같은 정책을 지킨다. 추가 build command는 `429`나 기존 작업 안내로 거부하지만
조회와 status는 상태 관찰이므로 막지 않는다.

실제 사용량이 계속 낮고 구현 복잡도가 크다면 관측부터 시작할 수 있다. 재검토
조건으로 동시 build 수, token 비용과 queue wait를 명시해야 한다.

### 30. 동일 query 세 번

동일한 결과 의미를 가진 요청이면 하나만 실행하고 세 caller가 결과를 공유한다.
서로 다른 query 100개는 dedupe할 수 없으므로 rate·concurrency limit으로
초과분을 거부한다. 동일성을 판단할 canonical key와 사용자 격리를 함께 정해야
한다.

### 31. 잘못된 year

중요한 보장은 화면 조건과 실제 provider 조건이 같아야 한다는 것이다. 정책은
제품 결정이지만 raw `garbage`를 계속 필터처럼 표시하는 현재 불일치는 허용하면
안 된다.

좋은 답은 입력 출처를 고려한다. 직접 오타는 경고와 canonical no-year 복구가
자연스러울 수 있다. 저장된 필터나 시스템 migration 오류라면 조용히 지우지
말고 사용자와 운영자에게 상태를 알려야 한다. Lighthouse의 현재 정책 공백은
[#408](https://github.com/corca-ai/lighthouse/issues/408)이 추적한다.

### 32. Enrichment 재시도

Lighthouse는 사용자의 명시적 command를 제품 요구사항으로 채택했지만 아직
구현하지 않았다. 현재 Read와 polling은 저장 상태만 읽는다. 권장 Retry route는
인증, 현재 `core=ready`, `enrichment=failed`, 사용자별 admission을 확인한다.
CAS와 lease로 중복 요청을 하나의 유효한 attempt에 수렴시키고 core는 다시
계산하지 않는다. 구현 작업은
[#414](https://github.com/corca-ai/lighthouse/issues/414)가 추적한다.

### 33. Service role 제거

일반 request는 session-bound client와 DB-enforced isolation으로 옮기는 편이
안전하다. Repository filter 테스트는 보조 증거이며 누락 시 피해를 제한하지
못한다. Shared artifact, viewer-private reaction, telemetry append와 admin read는
권한 목적이 다르므로 하나의 broad role로 합치지 않는다.

### 34. 운영 장애

먼저 route p99를 parse, auth, DB, queue와 provider 구간으로 나눈다. Instance 수와
process당 queue, provider 요청 수·timeout·5xx, grounding outcome과 affected
principal 수를 같은 시간축으로 비교한다. Console log가 있다는 이유만으로
provider를 원인으로 단정하지 않는다.

임시 완화는 증거에 맞춘다. Queue가 포화됐다면 admission이나 concurrency를
낮추고 degraded keyword-only 결과를 보존할 수 있다. DB pool이 원인이면 provider
상한 조정은 효과가 없다.

### 35. 공통 route 정책 도입

Bounded reader, error mapping, policy 실행기와 계측은 공통 mechanism으로 만들 수
있다. 공개성, 인증 방식, body 크기, schema, rate·concurrency 숫자와 deadline은
route 위험에 맞춘 선언이어야 한다.

`secureRoute`라는 이름은 모든 보안을 해결한다고 오해하게 한다. `withErrorMapping`,
`readBoundedJsonBody`, `applyIngressBudget`처럼 책임이 드러나는 작은 이름이
낫다. 테스트는 helper 단위 테스트 외에 실제 route별 `400/401/403/413/429`,
인증-before-effect와 provider·LLM 미호출 negative case를 포함해야 한다.

---

# 실전 보충: Lighthouse DB와 오류 계약을 확인한다

## 문제

### 36. 공유 report와 개인 preference

실제 migration은 다음 복합 primary key를 사용한다.

```sql
primary key (gap_report_id, viewer_principal_id)
```

`(report-1, user-A)`와 `(report-1, user-B)`는 함께 저장할 수 있는가? 같은
`(report-1, user-A)` row 두 개는 어떤가? 이 key가 report 소유권을 뜻하는지도
답하라.

### 37. 아직 commit되지 않은 같은 key

서버 1과 서버 2가 동시에 `(report-1, user-A)`를 INSERT한다. 첫 transaction은
아직 commit되지 않았다. PostgreSQL이 두 row를 모두 성공시키지 않는 과정을
일반 `SELECT` visibility와 unique index 검사로 나누어 설명하라.

### 38. `23505`를 받은 repository

Lighthouse 실제 코드는 다음 충돌을 처리한다.

```ts
if (inserted.error?.code === "23505") return null;
```

이 오류가 나타나는 실제 상황과 `null`을 받은 상위 계층의 다음 행동을 설명하라.

### 39. `400`과 LLM 일시 실패

Search enrichment route가 `400 invalid payload`를 반환했다. Client가 같은
payload를 잠시 뒤 최대 세 번 재시도하는 것이 적절한가? `400`이 route의 어느
단계에서 발생하는지도 답하라.

### 40. 정책과 구조 검증

팀이 다음 정책을 승인했다.

```text
400 → 동일 payload 재시도 금지
409 → 최신 상태를 읽고 command 재구성
429 → server backoff 뒤 제한 재시도
```

제품 정책, #433 구현과 #401 Architecture Fitness가 각각 맡을 일을 나누어라.

### 41. Reaction 세 필드의 transaction

Reaction preference 갱신은 다음 값을 한 `UPDATE`에 담는다.

```text
reaction
reaction_history
reaction_version
```

`reaction`만 저장되고 같은 SQL의 history와 version 저장이 실패할 수 있는가?
명시적인 `BEGIN`이 없어도 SQL 한 문장이 어떻게 실행되는지 설명하라.

### 42. 두 화면이 version 3을 읽었다

노트북과 휴대폰이 같은 preference의 `reaction_version = 3`을 읽었다. 노트북이
먼저 version 4로 저장했다. 휴대폰이 다음 조건으로 저장하면 affected row는
몇 개인가? Version 조건이 없을 때 깨지는 보장도 설명하라.

```sql
WHERE gap_report_id = :id
  AND viewer_principal_id = :viewer
  AND reaction_version = 3
```

### 43. 세 version의 의미

다음 필드가 무엇을 구분하는지 실제 write와 소비 기준으로 설명하라.

1. `gap_reports.version`
2. `gap_report_reactions.reaction_version`
3. `paper_inline_analysis_cache.version`

### 44. 모든 변경 row의 version

Reaction preference, `reviewed_papers`, append-only analytics event에 모두 동시
수정용 version을 추가하자는 제안을 검토하라. 각 데이터에 version,
`UNIQUE + upsert`, append 중 무엇이 맞는지 설명하라.

### 45. Gap build의 transaction 경계

다음 전체를 하나의 긴 DB transaction으로 묶을지 판단하라.

```text
pending 저장
→ core build와 저장
→ LLM enrichment
→ enrichment 저장
```

Enrichment 실패 때 core를 남기는 현재 제품 계약과 DB 연결·잠금 관점도 포함하라.

### 46. Lighthouse의 DB 역할

“Lighthouse는 검색 서비스이므로 논문 검색과 결과를 모두 자체 DB에서 처리하고
저장한다”는 설명을 검토하라. Episteme가 맡는 일과 Lighthouse DB가 맡는 상태를
나누고, DB 학습 사례로 Gap report를 깊게 본 이유를 설명하라.

### 47. 검색 20개의 LLM 호출량

모든 기능이 실행되는 검색 1건이 inline-analysis batch, AI comment,
research-term discovery, spelling correction를 각각 한 번 호출한다. 검색
20건의 정상 호출 시도 수를 계산하라.

Inline-analysis batch가 실패한 뒤 같은 provider에 논문별 5회를 추가 호출하는
현재 fallback이 모든 검색에서 발생하면 총 시도 수가 얼마까지 늘어나는지도
계산하라. 총 시도 수와 동시 실행 수가 같은지도 설명하라.

### 48. 전체 cap과 기능별 pool

다음 초기 제안을 현재 Lighthouse의 Vercel Fluid topology에서 다시 검토하라.

```text
process total = 200
Gemini Flash inline analysis = 100
Gemini Lite other features = 100
OpenAI secondary = 50
```

Module-level semaphore가 제한하는 정확한 범위와 fleet hard cap으로 사용할 수
없는 이유를 설명하라. 이 숫자를 계속 승인 상태로 둘지도 판단하라.

### 49. 포화 시 작업 우선순위

LLM 실행 자리가 가득 찼다. 다음 작업을 모두 같은 queue에 넣어 먼저 온 순서로
처리할지 판단하라.

1. 사용자가 화면에서 기다리는 AI comment
2. Inline analysis
3. Background research-term discovery
4. Best-effort spelling correction

사용자 보장과 장애 범위를 기준으로 지연하거나 생략할 작업을 결정하라.

### 50. 설정 상수가 있으면 검증이 끝나는가

공통 gateway에 `MAX_ACTIVE_LLM = 200`이 추가되고 unit test가 통과했다. 다음
주장을 검토하라.

> Lighthouse는 20개 동시 검색을 안전하게 처리한다.

현재 코드, 부하 테스트, Function·region과 fleet 범위, provider 실패를 나누어
필요한 증거를 적어라. 구현 전 Architecture Fitness 판정도 제시하라.

### 51. 같은 module global의 세 배포

다음 module global cache가 있다.

```ts
const cache = new Map<string, Result>();
```

장기 실행 단일 서버, Vercel Fluid, durable worker 세 환경에서 어느 실행끼리
cache를 공유하는지 설명하라. 어느 환경에서도 이 cache만으로 durable 결과
저장을 보장할 수 있는지도 답하라.

### 52. `after()`와 durable queue

Gap route가 `202 pending`을 반환하고 `after(runGapNetworkBuildJob())`를
등록했다. 다음 주장을 검토하라.

> 응답과 job이 분리됐으므로 Function이 종료돼도 job은 반드시 재개된다.

현재 Vercel 구조와 durable queue worker 구조의 차이를 설명하라.

### 53. Circuit breaker의 범위

`gateway.ts`의 module global circuit breaker가 Gemini 장애를 감지해 `open`이
됐다. `iad1`의 다른 Function instance와 `icn1`도 즉시 `open`인가?

Process-local과 shared breaker의 장단점도 설명하라.

### 54. 배포 형태가 바뀔 때 유지되는 보장

Lighthouse가 Vercel Fluid에서 고정된 container 서버나 durable worker로
이전한다고 가정하라. 다음 중 그대로 유지되는 보장과 다시 검토할 보장을
나누어라.

- DB unique constraint
- Lease와 version CAS
- Module in-flight dedupe
- `maxDuration`
- User-visible partial failure contract
- Process-local queue

## 해설

### 36. 공유 report와 개인 preference

A와 B의 row는 함께 저장할 수 있다. 같은 report와 A의 row 두 개는 primary
key가 거부한다. Gap report는 공유 artifact다. 복합 key는 report 소유권이 아니라
어느 report에서 어느 viewer가 저장한 preference인지 식별한다.

### 37. 아직 commit되지 않은 같은 key

첫 INSERT는 일반 `SELECT`에서 아직 보이지 않을 수 있다. Unique index 검사는
진행 중인 동일 key 충돌을 확인한다. 두 번째 INSERT는 첫 transaction의 종료를
기다린다. 첫 transaction이 commit하면 `23505 unique_violation`으로 실패하고,
rollback하면 계속 진행한다.

### 38. `23505`를 받은 repository

다른 요청이 같은 report와 viewer preference를 먼저 저장한 경쟁 상황이다.
Repository는 이를 알 수 없는 서버 장애 대신 충돌 신호 `null`로 바꾼다. 상위
계층은 최신 row와 version을 다시 읽고 제한된 횟수 안에서 수렴하거나 `409`로
닫는다. 같은 INSERT를 무제한 반복하면 안 된다.

### 39. `400`과 LLM 일시 실패

자동 재시도하면 안 된다. `400`은 Zod가 provider나 LLM 작업 전에 payload를
거부했다는 뜻이다. 같은 payload는 기다려도 유효해지지 않는다. 일시 실패는
`429`, `5xx`, timeout 또는 명시적인 degraded success로 구분한다. 현재
status별 client 행동의 불일치는
[#433](https://github.com/corca-ai/lighthouse/issues/433)이 추적한다.

### 40. 정책과 구조 검증

사람이 오류 의미와 재시도 정책을 승인한다. #433은 stable error identity를
server response, transport와 client action까지 연결하고 negative test를 둔다.
#401은 승인된 연결이 구조 변경 뒤에도 끊기지 않는지 검증한다. 정책이나 결정적
증거가 없으면 `authority-missing` 또는 `unknown`으로 남긴다.

### 41. Reaction 세 필드의 transaction

PostgreSQL은 SQL 한 문장도 하나의 transaction으로 실행한다. 한 `UPDATE`에 들어간
세 column은 함께 성공하거나 함께 취소된다. 여러 SQL 문장을 같은 성공·취소
단위로 묶어야 할 때 명시적 transaction을 추가한다.

### 42. 두 화면이 version 3을 읽었다

Affected row는 0이다. 노트북 저장 뒤 현재 version은 4이므로 휴대폰이 기대한
version 3과 맞지 않는다. 조건이 없으면 늦은 휴대폰 요청이 최신 선택을 덮는
갱신 유실이 발생한다. 이 조건부 변경을 CAS 또는 낙관적 동시성 제어라고 부른다.

### 43. 세 version의 의미

`gap_reports.version`은 오래된 Runner의 report 갱신을 막는다.
`reaction_version`은 한 viewer preference의 갱신 순서를 조정한다.
Inline-analysis cache의 `version`은 어느 분석 계약으로 만든 결과인지 구분한다.
같은 이름만 보고 모두 concurrency 장치라고 판단하면 안 된다.

### 44. 모든 변경 row의 version

Reaction preference는 오래된 선택을 막아야 하므로 version이 적절하다. 검토 완료
표시는 반복해도 같은 상태로 수렴하므로 `UNIQUE + upsert`가 단순하다. Analytics
event는 기존 row를 수정하지 않고 append하므로 동시 수정용 version이 필요하지
않다.

### 45. Gap build의 transaction 경계

하나의 긴 transaction으로 묶지 않는다. LLM을 기다리는 동안 DB 연결과 잠금을
오래 점유하고, enrichment 실패가 먼저 완성한 core까지 rollback하기 때문이다.
Pending, core, enrichment terminal을 짧게 저장하고 version 조건으로 오래된
Runner를 거부한다. Core만으로 사용자 가치를 제공할지는 제품 정책이 먼저
결정한다.

### 46. Lighthouse의 DB 역할

설명은 틀렸다. Query 검색과 논문 corpus는 Episteme provider가 담당한다.
Lighthouse DB는 reviewed papers, Gap artifact와 reaction, inline-analysis cache,
LLM usage와 운영 기록처럼 지속되어야 하는 상태를 맡는다. Gap report는 평균적인
route라서가 아니라 identity, lease, CAS, 중단 복구와 partial failure가 가장
밀집된 DB 사례라서 깊게 검토했다.

### 47. 검색 20개의 LLM 호출량

정상 경로는 검색당 4회이므로 총 80회다. Batch 실패 뒤 개별 호출 5회가
추가되면 검색당 최대 9회, 20건은 최대 180회다. 180회는 cohort 전체에서 발생할
수 있는 총 시도 수다. 첫 batch의 실패 뒤 개별 호출이 시작되므로 모두 같은
순간에 실행된다는 뜻은 아니다. 동시 실행 수는 실제 timing, queue와 cap을
측정해야 알 수 있다.

### 48. 전체 cap과 기능별 pool

Module-level semaphore는 그 module 사본이 올라간 Function instance만 제한한다.
같은 instance 안에서는 전체 200과 하위 pool의 관계가 성립할 수 있다. 그러나
다른 route, `iad1`, `icn1`과 scale-out instance는 별도 counter를 가질 수 있다.
따라서 service hard cap으로 승인하면 안 된다. 기존 숫자는 철회하고
`per_function_instance` soft guard 후보로만 남긴다. 실제 숫자는 production
overlap evidence 뒤 결정한다.

### 49. 포화 시 작업 우선순위

모두 같은 FIFO queue에 넣으면 background 작업이 사용자가 기다리는 응답을
막을 수 있다. 초기 승인 순서는 AI comment, inline analysis, research-term,
spelling correction다. 사용자-visible 작업은 bounded wait 뒤 명시적인
degraded/failure로 닫는다. Background와 best-effort 작업은 먼저 지연하거나
생략한다. 우선순위만 정하고 queue 대기 시간에 상한을 두지 않으면 요청 수명과
메모리 사용이 다시 무제한이 될 수 있다.

### 50. 설정 상수가 있으면 검증이 끝나는가

주장은 아직 증명되지 않았다. 모든 structured generation이 공통 gateway를
통과하는지 정적 경로를 확인해야 한다. 20개 검색 fixture로 정상 약 80회와
batch 실패 fan-out 제거를 측정해야 한다. Active, queued, wait time, timeout,
429, latency와 token을 Function·region·runtime identity와 함께 관측해야 한다.
서로 다른 identity 수만 세지 말고 같은 시간창에 겹친 active work를 확인한다.
Process-local 200은 fleet 전체 200이나 provider account를 보장하지 않는다.
구현과 행동 증거 전 Architecture Fitness 판정은 `unknown`이다.

### 51. 같은 module global의 세 배포

단일 서버에서는 같은 process의 요청이 cache를 공유한다. Vercel Fluid에서는
같은 Function instance에 배치된 invocation만 공유할 수 있다. 다른 route bundle,
region과 scale-out instance에는 별도 cache가 생긴다. Durable worker도 worker
process마다 별도 cache를 가진다. 어느 환경에서도 process memory는 재시작을
넘는 durable 결과 저장소가 아니다.

### 52. `after()`와 durable queue

주장은 틀렸다. `after()`는 응답 뒤에도 같은 Vercel Function invocation의 실행을
이어가지만 Function duration과 platform 수명 안에 있다. 종료 뒤 다른 worker가
job을 자동 인수한다고 보장하지 않는다. Durable queue는 job을 공유 저장소에
기록하고 visibility timeout, ack와 retry로 다른 worker의 인수를 조정한다. 현재
Gap은 DB pending·lease·CAS와 사용자의 recovery 요청으로 중단을 복구한다.

### 53. Circuit breaker의 범위

즉시 `open`이라고 보장할 수 없다. Module global breaker는 해당 Function
instance에서만 상태를 공유한다. Process-local breaker는 한 instance의 네트워크
이상을 fleet 장애로 확대하지 않는 장점이 있다. Shared breaker는 provider 전체
장애에 빠르게 반응하지만 한 instance의 오판을 전체에 전파할 수 있다. 관측된
장애 범위와 승격 정책이 필요하다.

### 54. 배포 형태가 바뀔 때 유지되는 보장

같은 DB를 사용한다면 unique constraint, lease와 version CAS는 유지된다.
User-visible partial failure contract도 제품 계약이므로 유지해야 한다. Module
dedupe와 process-local queue는 새 process·worker topology에 맞춰 범위를 다시
검토한다. `maxDuration`은 Vercel Function 설정이므로 container나 worker에서는
다른 실행 deadline과 shutdown 계약으로 바꿔야 한다.

---

# 복습 계획

오답을 개수로만 세지 않는다.

| 약한 영역                      | 다시 볼 문제 | 다음 실습                                      |
| ------------------------------ | ------------ | ---------------------------------------------- |
| 용어가 동작으로 연결되지 않음  | 1–12         | 코드에서 해당 장치 한 곳을 직접 찾는다.        |
| 코드는 읽지만 위험을 못 찾음   | 13–21        | effect까지 호출 순서를 화살표로 그린다.        |
| 보호장치를 만능으로 해석함     | 22–27        | 장치가 막는 것과 못 막는 것을 두 열로 쓴다.    |
| 결정을 바로 단정함             | 28–35        | 대안, 필요한 증거와 재검토 조건을 추가한다.    |
| DB 저장 경계가 약함            | 36–46        | identity, 원자성, 동시성과 수명을 나눈다.      |
| 내부 호출량을 과소평가함       | 47–50        | 정상 fan-out과 실패 증폭을 따로 계산한다.      |
| 실행 환경을 고정 서버로 가정함 | 51–54        | 상태마다 request·instance·fleet 범위를 적는다. |

## Lighthouse 코드 근거

- [Gap report route](https://github.com/corca-ai/lighthouse/blob/main/app/api/gap-reports/route.ts)
- [Inline analysis route](https://github.com/corca-ai/lighthouse/blob/main/app/api/papers/analyze-inline/route.ts)
- [Search term discovery route](https://github.com/corca-ai/lighthouse/blob/main/app/api/search/term-discovery/route.ts)
- [Search spelling correction route](https://github.com/corca-ai/lighthouse/blob/main/app/api/search/spelling-correction/route.ts)
- [Route guard](https://github.com/corca-ai/lighthouse/blob/main/app/server/guards/route-guard.ts)
- [Gap report repository](https://github.com/corca-ai/lighthouse/blob/main/app/server/repository/gap-reports.ts)
- [Shared Gap artifact migration](https://github.com/corca-ai/lighthouse/blob/main/supabase/migrations/00019_shared_gap_report_artifacts.sql)
- [Gap runtime flow](https://github.com/corca-ai/lighthouse/blob/main/docs/runtime-flows/gap-network-analysis.md)
- [Search runtime flow](https://github.com/corca-ai/lighthouse/blob/main/docs/runtime-flows/search-mechanism.md)
- [Operational readiness](https://github.com/corca-ai/lighthouse/blob/main/docs/operational-readiness.md)
- [Structured-generation gateway](https://github.com/corca-ai/lighthouse/blob/main/app/server/ai-generation/gateway.ts)
- [Inline analysis service](https://github.com/corca-ai/lighthouse/blob/main/app/server/services/inline-analysis-service.ts)
- [Route AI comment generation](https://github.com/corca-ai/lighthouse/blob/main/app/server/agent/route-ai-comment-generation.ts)
- [Research-term discovery](https://github.com/corca-ai/lighthouse/blob/main/app/server/services/search-term-discovery.ts)
- [Spelling correction](https://github.com/corca-ai/lighthouse/blob/main/app/server/services/search-spelling-correction-service.ts)
- [Vercel topology 추적 이슈 #442](https://github.com/corca-ai/lighthouse/issues/442)
- [Vercel Fluid Compute](https://vercel.com/docs/fluid-compute)
- [Vercel Function region](https://vercel.com/docs/functions/configuring-functions/region)
- [Vercel Function duration](https://vercel.com/docs/functions/configuring-functions/duration)

## 지식 레퍼런스

- [OWASP Input Validation Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html)
- [OWASP REST Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/REST_Security_Cheat_Sheet.html)
- [PostgreSQL Transaction Isolation](https://www.postgresql.org/docs/current/transaction-iso.html)
- [Google SRE Book](https://sre.google/sre-book/table-of-contents/)
