---
layout: default
title: "Engelbart의 Augmentation 접근 vs 자동화 사조"
---

# Engelbart의 Augmentation 접근 vs 자동화(Automation) 사조

## 들어가며 — 왜 지금 다시 Engelbart인가

Douglas C. Engelbart(1925–2013)는 마우스와 하이퍼텍스트의 발명자로 회자되지만, 그의 본업은 도구가 아니라 명제였다. 그는 "기계가 사람을 대신할 것인가, 아니면 사람을 더 똑똑하게 만들 것인가"라는 1950년대의 분기점에서 후자를 택했고, 그 선택은 현재 LLM 시대에 다시 살아 있는 질문으로 돌아왔다. 이 노트는 그 분기의 사상사적 맥락을 살피되, 평가가 아니라 맥락을 따라가는 방식으로 쓴다.

## 1. 1950–60년대의 분기 — Dartmouth와 Menlo Park

1956년 다트머스 회의(Dartmouth Workshop)에서 John McCarthy가 "artificial intelligence"라는 용어를 정착시킨 시점은, 동시에 "사람을 대체하는 기계"라는 사조의 출발점이기도 했다. McCarthy, Marvin Minsky, Allen Newell, Herbert Simon으로 이어지는 이른바 GOFAI(Good Old-Fashioned AI) 계열은 인간 지능을 기호 조작(symbol manipulation) 시스템으로 모형화하고, 그 시스템을 기계 안에 재현하는 것을 목표로 삼았다. 이들의 암묵적 명제는 "인간 인지의 본질이 기계 안에 옮겨질 수 있다"였다.

거의 같은 시기, 정확히는 1960년에 J.C.R. Licklider는 "Man-Computer Symbiosis"를 발표한다. Licklider는 AI의 장기적 가능성을 부정하지 않으면서도, 그것과 명시적으로 다른 길을 제안했다.

> "The hope is that, in not too many years, human brains and computing machines will be coupled together very tightly, and that the resulting partnership will think as no human brain has ever thought."
> (오래지 않은 미래에 인간의 뇌와 계산 기계가 매우 긴밀하게 결합되고, 그 결합체가 어떤 인간의 뇌도 사고해 본 적이 없는 방식으로 사고하기를 희망한다.)

Licklider는 당시 자신과 다른 진영을 의식한 듯 명시적으로 거리 두기를 한다.

> "It seems worthwhile to avoid argument with (other) enthusiasts for artificial intelligence by conceding dominance in the distant future of cerebration to machines alone."
> (먼 미래의 사고 영역이 기계 단독에게 넘어가리라는 점은 양보하더라도, 그와 별개로 지금은 다른 길이 가치 있다.)

흥미로운 사실은, 이 두 사조가 같은 자금원의 다른 줄기였다는 점이다. Licklider 자신이 1962년부터 ARPA의 IPTO(Information Processing Techniques Office)를 이끌었고, 그가 Engelbart의 SRI 그룹과 McCarthy의 SAIL(Stanford AI Lab) 양쪽 모두에 자금을 흘려보냈다. 한 부처가 두 적대적 비전을 동시에 부양한 셈이다. John Markoff는 *What the Dormouse Said*(2005)에서 "Engelbart의 비전은 컴퓨팅의 주류와 정면으로 어긋났고, 컴퓨터로 인간 지능을 증강한다는 그의 발상은 당시에는 시대착오적이고 평범한 것으로 치부됐다"고 적었다.

Engelbart는 Licklider의 논문이 나온 지 2년 뒤인 1962년, SRI 보고서 *Augmenting Human Intellect: A Conceptual Framework*를 발표한다. 이 문서가 그의 사상의 SSOT다.

## 2. Engelbart의 핵심 명제 — Augmentation은 효율화가 아니다

Engelbart는 자신의 목표를 다음과 같이 정의한다.

> "By 'augmenting human intellect' we mean increasing the capability of a man to approach a complex problem situation, to gain comprehension to suit his particular needs, and to derive solutions to problems."
> ('인간 지능 증강'이란, 사람이 복잡한 문제 상황에 접근해 자신의 필요에 맞는 이해를 얻고 해를 도출하는 능력을 키운다는 뜻이다.)

여기서 그가 단호히 끊는 지점이 있다. 증강은 사람을 더 빨리 일하게 만드는 일이 아니다. 그가 다루려는 문제는 "복잡성과 긴급성이 동시에 가속되는 세계"이고, 그 안에서 인간의 *복잡성 처리 능력 자체*를 끌어올리는 것이 과제다.

> "Man's population and gross product are increasing at a considerable rate, but the *complexity* of his problems grows still faster, and the *urgency* with which solutions must be found becomes steadily greater."

Engelbart의 작업 단위는 개별 도구가 아니라 "H-LAM/T 시스템"이다. **H**uman using **L**anguage, **A**rtifacts, **M**ethodology, in which he is **T**rained. 사람·언어·도구·방법·훈련이 하나의 통합 시스템으로 작동한다는 것. 따라서 마우스나 NLS는 "도구"가 아니라 시스템 안의 한 자리(Artifact)에 불과하고, 그 자리의 변경은 반드시 다른 자리(Language·Methodology·Training)의 변경과 함께 가야 한다. 그가 거듭 강조한 명제는 다음과 같다.

> "A direct new innovation in one particular capability can have far-reaching effects throughout the rest of your capability hierarchy."

이 사고에서 자연스럽게 흘러나오는 개념이 **bootstrapping(자기부양)** — 시스템이 자기 자신을 개선하기 위해 자기 자신을 도구로 쓴다는 것 — 그리고 인간과 도구가 함께 진화한다는 **co-evolution**이다. 1968년 12월 9일 샌프란시스코의 Fall Joint Computer Conference에서 행해진 "A Research Center for Augmenting Human Intellect" 시연(흔히 Mother of All Demos로 불리는)은 마우스·하이퍼텍스트·실시간 협업·화상회의를 보여 준 사건으로 기억되지만, Engelbart 자신의 프레이밍은 한결같이 H-LAM/T의 구체화였다.

요컨대 Engelbart의 분기는 다음과 같이 정리할 수 있다.

- **자동화**: 사람이 하던 일을 기계가 한다. 사람의 자리는 줄어든다.
- **증강**: 사람이 더 어려운 일을 할 수 있게 된다. 사람의 자리는 *복잡해진다*.

두 흐름은 효율의 정도가 아니라 *주어*가 다르다.

## 3. McCarthy 라인과의 사상사적 대립

McCarthy와 Engelbart 사이에 직접 충돌의 기록은 많지 않다. 두 사람이 인격적으로 부딪쳤다기보다, 같은 자금과 같은 캠퍼스 인근에서 서로 다른 명제를 운영했다는 편이 정확하다. Markoff의 정리를 다시 빌리면, "philosophical divide developed between Engelbart and McCarthy — the two men were not in personal conflict, but they had very different goals."

McCarthy 라인의 명제는 단순했다. *지능 자체가 연구 대상이고, 그것을 기계로 구현하는 것이 목표다.* Newell·Simon의 General Problem Solver, Minsky의 Society of Mind, McCarthy의 LISP은 모두 "사람의 자리를 비우고 그 안에 기계를 앉힐 수 있다"는 가정 위에서 작동했다. 이 라인에서 인간은 *모형의 대상*이지, *시스템의 일부*가 아니다.

Engelbart 라인은 거꾸로다. 인간을 모형화 대상에서 빼지 않고, 시스템 안에 둔 채로 시스템 전체의 능력을 높인다. 그래서 Engelbart의 글에는 "인지 모형"이 없다. 대신 "역량 위계(capability hierarchy)"가 있다. 무엇이 사람의 머릿속에서 일어나는지를 묻지 않고, 사람과 도구의 결합이 *밖에서* 무엇을 할 수 있는지를 묻는다.

이 차이는 후속 연구의 흐름에도 길게 남는다. Bret Victor는 *The Humane Representation of Thought*(2014)에서 자신을 명시적으로 Engelbart의 후예로 위치시키며, "인간의 사고 능력 자체를 매체가 어떻게 확장할 수 있는가"라는 질문을 이어받는다. Victor의 Dynamicland는 NLS의 정신적 후속작에 가깝다. 반대편 라인은 deep learning의 대성공을 거치면서 "사람이 하던 일을 기계가 한다"는 명제를 자율 에이전트(autonomous agent)라는 형태로 다시 들고 나왔다.

## 4. LLM 시대의 재연 — Replace vs Augment

2020년대 후반, 같은 분기가 다시 표면에 올라왔다. 이번에는 GOFAI가 아니라 LLM이 무대 위에 있다.

Andrej Karpathy는 2025년 Y Combinator 강연 *Software Is Changing (Again)*에서 LLM 시대를 "Software 3.0"이라 부르며 두 가지 비유를 강조했다. 하나는 **Iron Man suit** — "사람을 비우지 말고, 사람 주변에 능력을 입혀라". 다른 하나는 **autonomy slider** — 자율성은 0/1이 아니라 슬라이더이고, 좋은 도구는 사용자가 그 위치를 선택할 수 있게 한다는 것이다. Karpathy의 표현을 직접 빌리면, "we will move the autonomy slider from left to right over time, which is probably a decade-long transition."

이 프레이밍은 사실상 Engelbart의 H-LAM/T를 21세기 어휘로 다시 쓴 것이다. "사람을 어디에 둘 것인가"가 여전히 1차 변수이고, 자동화의 정도는 그다음에 결정되는 2차 변수다.

제품 진영에서도 같은 분기선이 보인다. Anthropic은 명시적으로 "augment"와 "human oversight"의 어휘를 전면에 내세우고, "staircase of autonomy"라는 표현으로 자율성을 단계적으로 올리는 모델을 선언한다. OpenAI는 "the most capable model, backed by the largest consumer platform"이라는 문장으로 알 수 있듯, 모델의 일반 역량과 플랫폼 통합을 1차 변수로 둔다. 두 회사가 같은 LLM을 다루지만, "사람의 자리"를 다루는 비중이 다르다. 이 차이는 Engelbart-McCarthy 분기의 현대적 잔향이다.

다만 Engelbart의 시대와 다른 새 사실이 하나 있다. 그가 말한 Artifact는 *지시받는 도구*였지만, LLM은 지시 없이도 행동을 시작할 수 있다. 이 새 사실 때문에 "도구"라는 어휘가 충분치 않다는 감각이 곳곳에서 생기고 있다.

## 5. 현재 작업 접점 (mirror-mind 4대 원칙 관점)

mirror-mind의 4대 원칙은 사용자(인간)와 AI를 "독립된 행위 주체(Co-actor)"로 규정한다. 이 어휘는 Engelbart의 어휘와 부분적으로 닿고, 부분적으로 갈라진다.

**닿는 지점.** mirror-mind도 Engelbart도, 시스템의 1차 변수를 "사람의 자리"로 둔다. 효율을 먼저 묻지 않고, 사람의 복잡성 처리 능력이 시스템 전체로 어떻게 길어지는지를 먼저 묻는다. lighthouse를 비롯한 하위 프로젝트가 "결과를 자동으로 내주는 기계"가 아니라 "재영의 사고를 펼치게 만드는 무대"로 설계되는 점, 기억 시스템·내러티브·의사결정 기록을 분리해 사람-도구 결합이 *함께* 진화하도록 짜는 점은 H-LAM/T의 직접 후예다. bootstrapping("도구로 도구를 만든다")의 정신도 mirror-mind 운영 방식 — 자기 자신을 codex/Claude로 다듬는 — 안에 내재해 있다.

**갈라지는 지점.** Engelbart는 끝까지 "Artifact"라는 어휘를 썼다. 그에게 컴퓨터는 사람과 결합하는 한 자리였지, 별도의 행위 주체는 아니었다. mirror-mind는 "독립된 행위 주체(Co-actor)"라는 어휘를 택한다. 이 차이는 단순한 용어 선택이 아니라 LLM 등장 이후의 새 사실 — *지시 없이 행동을 시작할 수 있는 비결정적 동료* — 에서 온다고 보는 편이 정직하다. Engelbart의 Artifact는 "내가 누르면 작동한다"는 신뢰 모델 위에 있었고, LLM은 "내가 시키지 않은 일도 시도한다"는 비결정성 위에 있다. 후자에 대해서는 "도구"라는 어휘가 모자라고, "동료" 또는 "행위 주체"라는 어휘가 더 정확하다.

**그렇지만 분기는 같다.** 새 어휘를 쓰더라도 mirror-mind가 향하는 분기는 Engelbart의 분기다. 사람을 비우지 않고, 사람의 자리를 *더 복잡하게* 만든다. Co-actor는 "사람을 대신하는 자율 에이전트"가 아니라 "사람과 함께 더 어려운 문제로 들어가는 동료"다. 이 점에서 mirror-mind는 Karpathy의 Iron Man suit 은유보다 한 걸음 더 나아간다 — 슈트는 입는 사람이 단수지만, Co-actor는 두 행위 주체가 *대칭적으로* 마주 선다. 그러나 이 대칭성조차 Engelbart의 명제에서 어긋나지는 않는다. 그가 H-LAM/T를 "사람과 시스템의 분리"가 아니라 "결합체로서의 능력"으로 정의했을 때, 그 결합체 안의 비대칭이 시간이 지나면서 좁혀질 가능성은 이미 열려 있었다.

요약하면, mirror-mind는 Engelbart가 1962년에 그은 분기선의 같은 쪽에 서 있다. 다만 그가 Artifact라고 부른 자리에 *비결정적 동료*가 들어왔기 때문에, 동일한 분기를 새 어휘로 다시 쓰고 있다. "Co-actor"는 "Augmentation"의 부정이 아니라, LLM 시대에 맞게 갱신된 Augmentation의 다른 이름이다.

---

## 출처

- Engelbart, Douglas C. *Augmenting Human Intellect: A Conceptual Framework*. SRI Summary Report AFOSR-3223, 1962. https://www.dougengelbart.org/content/view/138/
- Licklider, J.C.R. "Man-Computer Symbiosis." *IRE Transactions on Human Factors in Electronics*, vol. HFE-1, March 1960, 4–11. https://groups.csail.mit.edu/medg/people/psz/Licklider.html
- Engelbart, Douglas C. "A Research Center for Augmenting Human Intellect" (1968 demo, Fall Joint Computer Conference). https://en.wikipedia.org/wiki/The_Mother_of_All_Demos
- Markoff, John. *What the Dormouse Said: How the Sixties Counterculture Shaped the Personal Computer Industry*. Viking, 2005.
- Wikipedia. "Intelligence amplification." https://en.wikipedia.org/wiki/Intelligence_amplification
- Ashby, W. Ross. *An Introduction to Cybernetics*. Chapman & Hall, 1956.
- Victor, Bret. "The Humane Representation of Thought." SPLASH 2014 keynote. https://worrydream.com/
- Karpathy, Andrej. "Software Is Changing (Again)" / Software 3.0. Y Combinator AI Startup School, 2025. https://www.latent.space/p/s3
- Anthropic. "Building Effective Agents." https://www.anthropic.com/research/building-effective-agents
- Anthropic. "Measuring AI Agent Autonomy in Practice." https://www.anthropic.com/research/measuring-agent-autonomy
