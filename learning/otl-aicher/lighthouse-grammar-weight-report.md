---
layout: default
title: "문법의 무게 — Lighthouse 프로세스 체계 정량 조사와 Aicher/DSL 렌즈 리뷰"
---

# 문법의 무게 — Lighthouse 프로세스 체계 정량 조사와 Aicher/DSL 렌즈 리뷰

**작성일**: 2026-07-24
**방법**: Sonnet 서브에이전트 5개 — 웹 리서치 1개(문법 과중 해소 방안), 저장소 정량 조사 4개(Mission Control·Story Chain / Architecture Fitness / 게이트·스킬 / 런타임·제품 코드). 수집은 read-only, 판단은 본 리포트가 수행한다.
**전제**: [Aicher 픽토그램 리서치](./)와 [1차 리뷰](lighthouse-agentic-review)의 다섯 렌즈(문법, 그리드, 제약 속 자유, 저자의 소멸, 보편의 한계)를 그대로 사용한다.

## 요약

세 문장으로 줄인다. 첫째, "문법이 도메인보다 무겁다"는 1차 리뷰의 우려는 실측으로 확인됐다 — 프로세스·계약 체계의 물리량은 구현 코드의 1.7배다. 둘째, 그러나 문헌의 일치된 결론은 크기 자체가 아니라 회수(pay-as-you-go)를 보라는 것이고, Lighthouse는 이미 그 감사 습관을 부분적으로 갖고 있다. 셋째, 1차 리뷰의 판정 두 건은 이번 조사로 교정된다 — 층위 경계 검사기는 "없는" 것이 아니라 이미 21개 guard로 존재하며, 진짜 공백은 검사기가 아니라 문법의 불균일한 적용(auth의 repository 우회, domain-access 없는 개념)이다.

## 1. 정량 지형 — 실측 숫자

### 제품 대 프로세스

| 구분 | 파일 | 행 수 |
| --- | ---: | ---: |
| app/ 구현 코드(테스트 제외) | 348 | 56,586 |
| app/ 테스트 | 261 | 69,213 |
| Story Chain 계약 문서(promises 34 + aspects 22 + ledgers 107 + 기타) | 199 | 약 20,000 |
| Mission Control 스크립트(테스트 포함) | 49 | 11,128 |
| mission-control 스킬 + 정본 문서 | 17 | 2,235 |
| Architecture Fitness 정본(docs 10,573 + scripts 21,828 + 생성 사본 포함 시) | 86+ | 42,933 (사본 포함 62,671) |
| repo-authored 스킬 18개 | 18 | 3,331 |
| docs/ 최상위 13개 + contract-maps 10개 + runtime-flows 8개 | 31 | 6,212 |

프로세스·계약 계열 합계는 약 96,000행(AF 사본 제외 기준)으로, 구현 코드 56,586행의 약 1.7배다. 테스트를 제품 쪽에 넣어 125,799행으로 계산해도 프로세스 계열은 그 76%에 달한다. 1차 리뷰가 정성적으로 지적한 "문법이 도메인보다 무겁다"는 상태가 숫자로 확정된다.

### 검증기 밀도

- guard 21개, mc 11개, quality alias 8개. `quality:guards`는 guard 21개 전부를 직렬 실행한다.
- CI는 4개 workflow. `review-closeout` required check는 184행 스크립트가 exact content head와 정규식 레코드를 대조한다.
- AF protected run은 5개 job 파이프라인이며, 2026-07-17 감사 기준 45회 실행에 7.26시간, 확인된 false positive 0건이다.

### 온보딩 비용

새 에이전트의 무조건 필독은 472행(CLAUDE.md 1 + AGENTS.md 116 + product-identity 147 + project-knowledge README 208)이고, 작업 유형별 분기로 623~1,791행까지 늘어난다. Architecture Fitness review가 1,791행으로 가장 비싸다.

## 2. 리서치 — 무거운 문법을 다루는 검증된 접근

다섯 각도의 문헌 조사에서 나온 핵심만 요약한다. 출처는 부록에 있다.

**DSL 설계 문헌 (Fowler, Völter)**: 표현력 제한은 DSL의 결함이 아니라 설계 목표다. 실패는 문법이 아니라 메타 비용 — 문법을 유지하는 파서·에디터·diff 도구 — 이 도메인 가치를 앞지를 때 온다. 문법 확장은 비싸게, 어휘 확장은 싸게 유지하라.

**점진적 형식화 (Daniel Jackson, Amazon TLA+)**: 형식화는 실패 비용이 큰 좁은 스코프에만 적용하고 나머지는 느슨하게 둔다. 매 주기 "이 규약이 실제로 버그를 잡았는가"를 점검하는 pay-as-you-go 게이트를 두고, 회수가 없으면 폐기한다.

**프로세스 경량화 (Agile의 RUP 반작용, Shape Up)**: 무거운 방법론의 실패 패턴은 산출물 누적이다. Shape Up의 처방은 구조적이다 — 미채택 산출물을 이월하지 않고 버린다. 프로세스 품질을 문서·게이트의 존재가 아니라 실제로 막은 결함으로 측정한다.

**문서 구조론 (Diátaxis)**: 문서는 저작자의 조직이 아니라 독자의 인지 모드(학습/작업/조회/이해)로 4분류한다. 한 문서에 튜토리얼과 레퍼런스가 섞이는 것이 비대화의 주요 원인이다.

**AI 에이전트 규약의 실증 연구 (2026)**: 가장 반직관적인 결과다. 1,650세션 요인설계 실험(arXiv 2605.10039)에서 규약 파일의 크기·위치·구조·모순은 준수율에 유의미한 효과가 없었다. 유일하게 강한 효과는 세션 내 누적 작업량 — 생성 함수 1개당 준수 확률이 약 5.6%씩 떨어진다. 별도 연구(arXiv 2606.12231)는 규칙 개정의 77.78%가 "AI 오류 교정용 부정 제약 추가"로, 규칙이 리팩터링 없이 단조 증가하는 실태를 보였다.

## 3. Aicher/DSL 렌즈 리뷰 — 영역별

### Story Chain / Mission Control — 문법은 작고, 장부가 무겁다

개념 어휘는 놀랄 만큼 작다. concepts.md의 개념 9개, 정규 용어표 8개, Promise frontmatter 필드 약 10개. Aicher의 5요소에 견줄 만한 규모다. 무거운 것은 문법이 아니라 **장부**다 — evidence-ledgers가 13,685행으로 Story Chain 문서의 68%를 차지하고, 그중 reviews-archive만 4,686행이다. 이것은 문법 비대가 아니라 산출물 누적이며, Shape Up의 진단이 정확히 적용되는 지점이다. 이월 산출물(아카이브)의 보존 기한과 폐기 규칙이 없으면 장부는 단조 증가한다.

또 하나의 관찰: 1 Promise가 1 ledger로 닫히지 않고 8개 이상 ledger에 분산 참조되는 사례(inline-analysis-auto-run)가 있다. 낱말 하나의 정의가 사전 여덟 곳에 흩어진 상태로, 읽기 비용을 키우는 구조다.

### Architecture Fitness — 가장 정직한 검사기, 가장 무거운 문법

AF는 판정 어휘(healthy/degraded/unknown, included/unsupported/excluded, allow/block/defer-with-owner)가 코드에 정의되고(`common.py`, `merge-advisory.mjs`), 미지원 렌즈를 `unknown`으로 기계 보존하는 유일한 체계다. 거짓 보편을 거부하는 설계는 다섯 렌즈 중 5번(보편의 한계)을 가장 잘 내면화했다.

비용도 가장 크다. 사본 포함 62,671행, 온보딩 1,791행, protected run 45회에 7.26시간. 그러나 AF는 이 비용을 스스로 셈한다 — 2026-07-17 감사가 단계별 "고유한 출시 판단 가치"를 표로 판정했고, false positive 0건과 Q3의 코호트 결정 근거를 회수 증거로 기록했다. 문헌의 pay-as-you-go 원칙을 이미 실천하는 셈이다. 남은 문제는 이 감사가 AF에만 있고 다른 게이트·스킬 체계에는 없다는 비대칭이다.

### 게이트 — 1차 리뷰의 판정 교정 1: 층위 경계 검사기는 이미 있다

1차 리뷰와 후속 논의에서 "층위 경계에 검사기가 없다"고 판정했는데, 조사 결과 이는 틀렸다. `guard:repository-seam`, `guard:least-authority-boundaries`, `guard:state-boundaries`, `deps:boundaries`(dependency-cruiser 계열)가 이미 존재하고 `quality:guards`에 편입되어 있다. 경계 lint 이슈 등록은 불필요하다.

진짜 공백은 검사기의 부재가 아니라 **문법의 불균일한 적용**이다. 실측 두 건: (1) 인증 경로 4개 파일이 repository 층을 거치지 않고 Supabase 클라이언트를 직접 사용한다 — 의도된 예외라면 그 예외가 어디에도 선언되어 있지 않고, 아니라면 guard가 못 보는 사각이다. (2) route-ai-comment 개념은 domain-access 층 없이 agent 층에서 repository로 직행한다 — 층위 사슬이 모든 개념에 균일하게 적용되지 않는다. Aicher 용어로, 그리드는 있는데 일부 픽토그램이 그리드 밖에서 그려졌고 그 사실이 기록되지 않았다.

### 스킬·라우팅 — 사본 증식은 관리되고 있으나 회수 척도가 없다

repo-authored 스킬 18개 3,331행에 `.claude/skills`와 `.agents/skills` 사본 2벌이 있다. 문헌의 "단일 정본 + 참조" 전략과 어긋나 보이지만, `sync-agent-skills.py`와 `guard:skills`가 drift를 기계 검사하므로 절반은 해결된 상태다. 해결되지 않은 것은 스킬별 회수 척도다 — 각 스킬이 실제로 라우팅된 횟수, 막은 결함을 재는 지표가 없어서 통합·은퇴 판단이 감이 아닌 근거로 내려질 수 없다.

### 런타임 — 프로세스는 두껍고 AI 출력 문법은 얇다

흥미로운 비대칭이 발견됐다. structured generation gateway(`gateway.ts`)는 스키마를 바인딩하지 않는다 — `jsonMode`로 JSON 응답만 켜고 텍스트를 반환하며, 스키마 강제는 호출자마다 "프롬프트 문자열 지시 + JSON.parse + zod safeParse" 패턴으로 반복된다(zod 검증 호출자 9곳 확인). 프로세스 문서에는 6만 행을 쓰면서, 정작 AI 출력이라는 가장 비결정적인 경계의 문법은 프롬프트 속 자연어 지시에 의존한다. 반면 events.yaml은 2,042행에 이벤트 35개, storyRefs 실재 검증까지 갖춘 모범 DSL이다. 같은 저장소 안에 가장 좋은 문법과 가장 얇은 문법이 공존한다.

## 4. 처방 — 문헌 전략의 Lighthouse 매핑

우선순위 순서다. 실행은 모두 별도 process 세션 소관이다.

1. **게이트 회수 감사(pay-as-you-go)를 AF 밖으로 확장한다.** guard 21개·mc 11개 각각에 "최근 N개월간 실제로 막은 결함 수"를 기록하고, 회수 없는 게이트는 통합·폐기 후보로 올린다. AF의 2026-07-17 감사 형식을 재사용하면 새 문법이 필요 없다.
2. **장부 폐기 규칙을 만든다.** reviews-archive(4,686행)와 완결된 ledger review의 보존 기한을 정하고 이월을 멈춘다. Shape Up의 "bets, not backlogs"를 Evidence Ledger 아카이브에 적용하는 것이다.
3. **문법의 예외를 선언 가능하게 만든다.** auth의 repository 우회, domain-access 없는 개념처럼 그리드 밖에서 그려진 픽토그램을 "위반"이 아니라 "선언된 예외"로 기록하는 자리를 만든다. 선언되지 않은 예외만 guard가 잡게 하면, 문법의 균일성과 실용적 유연성이 같이 산다.
4. **gateway에 스키마 바인딩을 올린다.** 호출자 9곳에 반복되는 프롬프트 지시+zod 패턴을 gateway 층의 계약으로 끌어올리면, AI 출력 문법이 자연어 지시에서 기계 계약으로 바뀐다. 이것은 프로세스 문서 추가 없이 코드 층에서 문법을 강화하는, 비용 대비 회수가 가장 명확한 항목이다.
5. **온보딩 문서를 Diátaxis로 감사한다.** verification-gates.md(564행), agent-skills.md(413행)처럼 레퍼런스와 설명이 섞인 문서를 분리하면 필독 경로가 짧아진다.
6. **규약 다이어트보다 세션 관리를 우선한다.** 실증 연구는 규약 파일 크기가 아니라 세션 내 누적 작업량이 준수율을 결정한다고 말한다. AGENTS.md를 줄이는 것보다 작업 단위로 세션을 끊는 운영 규칙(이미 process 세션 분리로 부분 실천 중)이 더 효과적이다.
7. **규칙 리팩터링 주기를 명시한다.** 부정 제약의 단조 누적(77.78%)을 막으려면 skill-governance-steward의 주기 감사에 "이번 주기에 통합·삭제한 규칙 수"를 산출물로 요구한다.

## 5. 종합 — 다섯 렌즈 재판정

| 렌즈 | 1차 판정 | 이번 실측 후 |
| --- | --- | --- |
| 1 문법 | 건강 | 유지 — 개념 어휘 9개는 실제로 작다. 무거운 것은 문법이 아니라 장부다 |
| 2 그리드 | 게이트는 성공, 판정 절차는 산문 | 강화 — guard 21개는 예상보다 촘촘하다. 공백은 검사기가 아니라 선언되지 않은 예외다 |
| 3 제약 속 자유 | 작동 | 유지 |
| 4 저자의 소멸 | 건강 | 유지 |
| 5 보편의 한계 | 최대 긴장 | 구체화 — 학습 비용은 온보딩 472~1,791행으로 실측됐고, 처방은 다이어트가 아니라 회수 감사·폐기 규칙·Diátaxis 분리다 |

한 문장 결론: **Lighthouse의 문법은 크기가 아니라 회계가 문제다 — 무엇이 비용을 회수하는지 AF만 셈하고 있고, 나머지 체계는 아직 장부 없이 자란다.**

## 문답으로 재구성한 결론

리포트 작성 후 소크라테스식 문답으로 결론의 뼈대를 다시 세웠다. 여섯 개의 디딤돌로 정리한다.

1. **두께는 죄가 아니다.** 규정집의 판정 기준은 두께가 아니라 실효성이다. 지키든 안 지키든 결과가 같은 규정은 의미가 없다.
2. **실효성은 장부가 있어야 안다.** 비용 칸에는 규정에 들이는 시간을, 회수 칸에는 실제로 막은 사고 수와 헛경보 수를 적는다. Lighthouse에서 이 장부를 쓰는 체계는 Architecture Fitness 하나다.
3. **장부 없는 규정집은 늘기만 한다.** 추가는 사고 직후 즉시 일어나지만, 삭제는 "안 잡은 지 오래됐다"는 증거가 필요한데 그 증거를 아무도 모으지 않는다. 실증 연구에서 규칙 개정의 77.78%가 부정 제약 추가였다.
4. **규칙과 기록은 다르게 관리한다.** 규칙은 심의로만 늘고 심의로 줄인다. 기록은 일할 때마다 자동으로 쌓이므로 심의가 아니라 기한 규칙이 버린다. Lighthouse의 최대 덩어리는 규칙이 아니라 기한 없는 기록이었다.
5. **예외는 없애는 게 아니라 선언하게 한다.** 선언되지 않은 예외는 위반과 구별되지 않아서, 규칙의 침식이나 오작동 중 하나로 끝난다. 검사기의 임무는 예외를 잡는 것이 아니라 선언 안 된 예외만 잡는 것으로 바뀐다.
6. **규칙은 부탁이 아니라 길목에 심는다.** 아홉 호출자가 각자 부탁 문장에 형식을 적는 것은 "비슷한 느낌으로 그려주세요"다. 모두가 지나는 공용 창구에 형식을 두면 부탁 없이도 지켜지고 빼먹기가 불가능해진다.

### 세 층 분류 — 틀, 조문, 기록

문답에서 "법전"이라는 말이 규칙 전체와 그 안의 문법을 오가며 혼동을 일으켰다. 최종적으로 세 층으로 정리한다.

| 층 | 이름 | 법 비유 | Lighthouse | Aicher/DSL |
| --- | --- | --- | --- | --- |
| 1 | 틀 (메타 규칙) | 입법 형식 | 개념 9종 (Experience, Moment, Promise, Aspect…) | 그리드, 언어의 문법 |
| 2 | 조문 (내용 규칙) | 개별 법률 | Promise 34개, Aspect 22개, 예외 선언 | 픽토그램 하나하나, 그 언어로 쓴 문장 |
| 3 | 기록 | 집행·점검 서류 | evidence-ledgers 13,685행 | 언어가 아닌 사용 이력 |

층마다 성장의 건강 판정이 다르다. 틀이 늘면 경계한다 — 그리드는 얼린다. 조문이 느는 것은 정상이되 죽은 조문은 심의(retirement)로 폐지한다. 기록이 느는 것은 자동이므로 기한 규칙으로 폐기한다. 이 분류로 진단을 다시 읽으면 한 문장이 된다. Lighthouse는 틀을 작게 잘 얼려뒀고(9개), 조문은 건강하게 자라는 중이며, 문제는 3층 — 기한 규칙 없는 기록 — 에 몰려 있다.

## 부록 — 리서치 출처

- Martin Fowler & Rebecca Parsons, *Domain-Specific Languages*; Fowler의 language workbench 리뷰 (martinfowler.com/articles/mdaLanguageWorkbench.html)
- Berger/Völter, "Efficiency of Projectional Editing" (voelter.de/data/pub/fse2016-projEditing.pdf)
- Daniel Jackson, *Software Abstractions*; Jackson & Wing의 lightweight formal methods partiality 4차원 (arxiv.org/pdf/1807.01923)
- "A Systematic Literature Review on a Decade of Industrial TLA+ Practice" (arxiv.org/html/2411.13722)
- Ryan Singer, *Shape Up* — "Bets, Not Backlogs" (basecamp.com/shapeup/2.1-chapter-07)
- Diátaxis (diataxis.fr)
- "Instruction Adherence in Coding Agent Configuration Files" (arxiv.org/abs/2605.10039)
- "Rule Taxonomy and Evolution in AI IDEs" (arxiv.org/abs/2606.12231)
- 저장소 실측: docs/architecture-fitness/README.md 2026-07-17 감사, package.json, scripts/, docs/contracts/story-chain/ (2026-07-24 read-only 조사)
