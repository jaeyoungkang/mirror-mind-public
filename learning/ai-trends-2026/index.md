---
layout: default
title: 2026 에이전트 플랫폼 경쟁
---

# 2026 에이전트 플랫폼 경쟁: 축, 스택, 성숙도

> 작성일: 2026-06-08  
> 근거: `research/ai-trends/v2/` graph pilot  
> 검증: `python3 scripts/ai-trends.py v2-validate`, `python3 scripts/test-ai-trends.py`

## 범위

이 리포트는 Microsoft Build 2026, Google I/O 2026, GitHub Copilot app 관련 공식 자료를 바탕으로 Microsoft, Google, GitHub의 에이전트 플랫폼 전략을 비교한다.

현재 데이터 상태:

```text
v2 graph: 73 nodes, 8 axes, 13 stack layers, 28 source claims, 159 edges
seed records: 73 records
tests: ok 8 tests
```

## 요약

2026년 에이전트 플랫폼 경쟁은 모델 성능만의 경쟁이 아니다. 현재 graph가 보여주는 반복 축은 다음과 같다.

```text
execution-boundary
agent-harness
evaluation-observability
context-grounding
product surface
commercial-packaging
```

세 actor의 중심은 다르다.

```text
Microsoft: enterprise-governed production agent stack
Google: consumer/developer surface expansion with Gemini runtime/tooling
GitHub: coding-agent operations surface
```

가장 강한 cross-actor axis는 `execution-boundary`다.

```text
Microsoft: MXC, Foundry Hosted Agents, Agent 365 local governance
Google: Managed Agents persistent isolated environment
GitHub: Copilot app sessions in new worktree/local repository
```

두 번째로 강한 축은 `agent-harness`다.

```text
Microsoft: Microsoft Agent Framework
Google: Antigravity
GitHub: Copilot app focused agent sessions
```

## 1. 동향 축

### 1.1 Execution Boundary는 핵심 경쟁 단위다

근거 경로:

```text
Microsoft -> Microsoft Execution Containers -> Policy-driven agent containment -> execution-boundary
Google -> Managed Agents in the Gemini API -> Persistent isolated agent environment -> execution-boundary
GitHub -> GitHub Copilot app technical preview -> Copilot app sessions in new worktree/local repository -> execution-boundary
```

해석:

에이전트 플랫폼은 에이전트가 어디서 실행되는지, 무엇에 접근할 수 있는지, 상태를 어떻게 유지하는지, 작업 경계를 어떻게 통제하는지를 정의하려 한다. 이건 단순한 sandbox보다 큰 개념이다.

구현 방식은 서로 다르다.

```text
Microsoft: OS / enterprise security / Foundry runtime containment
Google: cloud-managed persistent Linux environment
GitHub: repository/worktree workspace isolation
```

### 1.2 Agent Harness는 플랫폼 계층이 되고 있다

근거 경로:

```text
Microsoft -> Microsoft Agent Framework v1.0 -> Agent harness with skills, memory, middleware, and orchestration -> agent-harness
Google -> Google Antigravity 2.0 -> Antigravity agent harness -> agent-harness
GitHub -> GitHub Copilot app technical preview -> GitHub Copilot app focused agent sessions -> agent-harness
```

해석:

agent harness는 더 이상 제품 내부 구현 디테일이 아니다. skills, subagents, middleware, memory, orchestration, sessions를 묶는 명시적 플랫폼 계층으로 올라오고 있다.

### 1.3 Evaluation / Observability는 존재하지만 성격이 다르다

근거 경로:

```text
Microsoft -> Foundry tracing, evaluation, optimizer, and Rubric -> evaluation-observability
Microsoft -> Agent 365 -> Entra / Defender / Intune / Purview mechanisms -> evaluation-observability
Google -> Chrome DevTools for agents -> Runtime visibility for coding agents -> evaluation-observability
```

해석:

Microsoft는 production governance와 policy/eval loop를 강조한다. Google은 Chrome DevTools for agents를 통해 developer-runtime visibility를 제공한다.

차이는 이렇게 요약된다.

```text
Microsoft: operate, govern, secure, evaluate
Google: inspect, debug, optimize, run audits
```

### 1.4 Google은 표면 확산이 가장 넓다

현재 pilot에서 Google은 8개 axis를 모두 커버한다.

```text
agent-harness
background-agent
commercial-packaging
context-grounding
evaluation-observability
execution-boundary
generative-ui
science-agent
```

해석:

Google은 Search, AI Mode, Antigravity, Managed Agents, Chrome DevTools, Gemini for Science, AI subscriptions를 통해 consumer, developer, science, runtime, commercial packaging 표면을 넓게 펼친다.

다만 이것이 enterprise governance가 강하다는 뜻은 아니다. 현재 stack projection에서는 Google의 `governance-identity`, `enterprise-surface`가 비어 있다.

## 2. 회사 전략

### 2.1 Microsoft: enterprise-governed production agent stack

Microsoft stack coverage:

```text
context-grounding
enterprise-surface
evaluation-observability
execution-boundary
governance-identity
harness
runtime
science-workflow
```

강한 계층:

```text
governance-identity: Agent 365, Entra, Defender, Intune, Purview, Scout
evaluation-observability: Foundry eval/optimizer/Rubric, Agent 365 controls
execution-boundary: MXC, Foundry Hosted Agents, Agent 365 local governance
context-grounding: Microsoft IQ / Web IQ / Scout
```

해석:

Microsoft는 에이전트 기능을 나열하는 것이 아니라 production agent를 위한 enterprise operating layer를 조립하고 있다. identity, containment, observability, evaluation, policy, runtime, context가 같은 방향으로 묶인다.

현재 약점 또는 데이터 결손:

```text
commercial-packaging
consumer-surface
data-backend
developer-surface
model
```

일부는 실제 전략 공백이 아니라 migration gap이다. 예를 들어 model/data-backend 관련 seed record는 있지만 아직 v2로 충분히 옮기지 않았다.

### 2.2 Google: surface-expansive Gemini agent stack

Google stack coverage:

```text
commercial-packaging
consumer-surface
context-grounding
developer-surface
evaluation-observability
execution-boundary
harness
runtime
science-workflow
```

강한 계층:

```text
consumer-surface: Search agents, AI Mode, generated UI
developer-surface: Antigravity, Chrome DevTools for agents
runtime/execution-boundary: Managed Agents
commercial-packaging: AI subscription updates
science-workflow: Gemini for Science
```

해석:

Google은 Search, AI Mode, Chrome, Antigravity, Gemini for Science 같은 고빈도 표면을 agent surface로 바꾸고 있다. Microsoft보다 enterprise governance는 약하게 드러나지만, consumer/developer surface 확산은 훨씬 넓다.

현재 약점 또는 데이터 결손:

```text
data-backend
enterprise-surface
governance-identity
model
```

model coverage는 migration gap이다. Gemini model record는 seed에 있으나 v2로 충분히 옮기지 않았다.

### 2.3 GitHub: coding-agent operations surface

GitHub stack coverage:

```text
developer-surface
execution-boundary
harness
```

해석:

GitHub는 범용 agent platform이라기보다 coding-agent operations surface로 보는 편이 정확하다.

핵심 구성:

```text
focused agent sessions
new worktree/local repository execution
Agent Merge
```

현재 결손:

```text
pricing
enterprise controls
review/merge workflow details
CI and validation integration
```

## 3. 성숙도와 시간 변화

주의: 아래 날짜는 시장 전체의 first appearance가 아니라 현재 수집 corpus 기준 first_seen이다.

```text
evaluation-observability: 2026-05-01
agent-harness: 2026-05-14
execution-boundary: 2026-05-14
background-agent: 2026-05-19
commercial-packaging: 2026-05-19
context-grounding: 2026-05-19
generative-ui: 2026-05-19
science-agent: 2026-05-19
```

가장 명확한 product transition은 Microsoft Agent 365다.

```text
Microsoft Agent 365
- 2026-05-01 [general_availability]
- 2026-06-02 [public_preview] local agent extension
```

전이:

```text
Microsoft Agent 365 generally available -> Agent 365 for local agents
scope: local agent extension
```

해석:

이건 단순한 preview → GA 진행이 아니다. 전체 control plane은 GA 상태지만 local agent extension은 public preview다. 따라서 에이전트 제품 성숙도는 단일 상태가 아니라 scope별 상태로 봐야 한다.

```text
product maturity != capability maturity
```

## 4. 결손

현재 axis gap:

```text
Google: none
Microsoft: commercial-packaging, generative-ui
GitHub: background-agent, commercial-packaging, context-grounding, evaluation-observability, generative-ui, science-agent
```

현재 stack-layer gap:

```text
Google: data-backend, enterprise-surface, governance-identity, model
Microsoft: commercial-packaging, consumer-surface, data-backend, developer-surface, model
GitHub: commercial-packaging, consumer-surface, context-grounding, data-backend, enterprise-surface, evaluation-observability, governance-identity, model, runtime, science-workflow
```

source claim gap:

```text
missing original_excerpt: 0
missing supports: 0
```

해석:

v2 pilot 내부의 source grounding은 충분히 안정적이다. 약점은 source grounding이 아니라 범위다.

```text
older event history missing
many seed records not migrated to v2
commercial packaging incomplete for Microsoft/GitHub
model and data-backend layers under-migrated
```

## 5. 신뢰도

높은 신뢰도:

```text
execution-boundary is a real cross-actor axis
Microsoft has stronger enterprise governance/eval/runtime profile
Google has broader consumer/developer surface spread
GitHub is a coding-agent operations surface
```

중간 신뢰도:

```text
Google fully covers evaluation/observability
Microsoft lacks commercial-packaging
May 2026 first_seen dates reflect current collection, not full market history
```

낮은 신뢰도:

```text
2025 -> 2026 evolution claims before older events are imported
pricing strategy comparison before commercial records are normalized
```

## 6. 다음 작업

### 데이터

1. v2로 migration할 seed record:
   - MAI model family
   - HorizonDB
   - Rayfin
   - Fabric GPU acceleration
2. Microsoft commercial/pricing/licensing:
   - Agent 365
   - Foundry Hosted Agents
   - Windows 365 for Agents
   - GitHub Copilot app / Copilot plans
3. GitHub workflow depth:
   - Agent Merge
   - review / diff / PR flow
   - enterprise controls
   - validation / CI path
4. older event records:
   - Agent 365 preview / Ignite 2025
   - GitHub Copilot Workspace
   - Google Project Mariner
   - OpenAI Codex
   - Anthropic Claude Code

### 그래프

1. `precedes` edge 추가
2. `availability_transition` edge 추가
3. product version node 추가
4. gap output에 `source_gap`, `strategy_gap`, `migration_gap` 라벨 추가

### 테스트

1. orphan product node 테스트
2. product timeline 테스트
3. axis별 source-backed path 테스트
4. `v2-gaps`, `v2-temporal --mode all` snapshot 테스트

## 7. 주요 원문 출처

이 리포트의 데이터 조각은 `research/ai-trends/v2/sources.jsonl`의 source id와 연결되어 있다. 공개 리포트에서 참조한 핵심 원문 출처는 다음과 같다.

- Microsoft, [Microsoft Build 2026: Be yourself at work](https://blogs.microsoft.com/blog/2026/06/02/microsoft-build-2026-be-yourself-at-work/), 2026-06-02.
- Microsoft Windows Developer Blog, [Build 2026: Furthering Windows as the trusted platform for development](https://blogs.windows.com/windowsdeveloper/2026/06/02/build-2026-furthering-windows-as-the-trusted-platform-for-development/), 2026-06-02.
- Microsoft News, [Microsoft Build Live](https://news.microsoft.com/build-2026-live-blog), 2026-06-02.
- Google Blog, [100 things we announced at I/O 2026](https://blog.google/innovation-and-ai/technology/ai/google-io-2026-all-our-announcements/), 2026-05-20.
- Google Blog, [Building the agentic future: Developer highlights from I/O 2026](https://blog.google/innovation-and-ai/technology/developers-tools/google-io-2026-developer-highlights/), 2026-05-19.
- Google Blog, [Google AI subscription updates from Google I/O 2026](https://blog.google/products-and-platforms/products/google-one/google-ai-subscriptions), 2026-05-19.
- Chrome for Developers, [Chrome DevTools for agents](https://developer.chrome.com/docs/devtools/agents).
- Chrome for Developers, [15 updates from Google I/O 2026: Powering the agentic web with new capabilities, tools, and features in Chrome](https://developer.chrome.com/blog/chrome-at-io26), 2026-05-19.
- Microsoft Security Blog, [Microsoft Agent 365, now generally available, expands capabilities and integrations](https://www.microsoft.com/en-us/security/blog/2026/05/01/microsoft-agent-365-now-generally-available-expands-capabilities-and-integrations/), 2026-05-01.
- Microsoft Learn, [Transition Microsoft Copilot Studio and Microsoft Foundry agent security capabilities to Microsoft Agent 365](https://learn.microsoft.com/en-us/defender-xdr/security-for-ai/transition-agent-security-to-agent-365), 2026-06-02.
- GitHub Docs, [Working with agent sessions in the GitHub Copilot app](https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions).
- GitHub Changelog, [GitHub Copilot app is now available in technical preview](https://github.blog/changelog/2026-05-14-github-copilot-app-is-now-available-in-technical-preview/), 2026-05-14.
- GitHub, [GitHub Copilot app](https://github.com/features/ai/github-app).
