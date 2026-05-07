---
layout: default
title: "한계·비판·실패한 이유"
---

# 한계·비판·실패한 이유 — Engelbart 비전이 왜 좁아졌고 왜 다시 살아나는가

1968년 12월 9일의 "Mother of All Demos"는 마우스, 하이퍼텍스트, 화상회의, 실시간 공동 편집, 윈도잉을 한 시간 반 동안 한꺼번에 보여줬다. 그러나 그 데모를 만든 사상은 산업으로 흡수되지 못했다. 표면(마우스, GUI, 윈도)은 PARC를 거쳐 Apple로 흘러갔고, 핵심(co-evolution, Bootstrap, B/C activity, chord keyset)은 거의 전부 잘려나갔다. 이 글은 그 잘려나간 자리에서 무엇이 남았고 무엇이 사라졌는지, 그 비판이 어디까지 정당한지를 사료에 따라 정리한다.

## 1. NLS의 흡수 손실 — PARC로 가며 깎인 것

ARC에서 PARC로의 인력 이동은 단발 사건이 아니라 1970–1973년에 걸친 흐름이었다. Bill English가 1971년 PARC로 옮겨 마우스와 디스플레이 시스템을 그대로 옮겨 심었고, Charles Irby, Jeff Rulifson, Larry Tesler, William Duvall이 뒤따랐다. John Markoff는 *What the Dormouse Said* (2005)에서 이를 두고 "Engelbart's poor management skills doomed the project, and his best team members leaked over to Xerox PARC"라 표현한다 ("엥겔바트의 부족한 관리 능력이 프로젝트를 좌초시켰고, 그의 최고 팀원들은 제록스 PARC로 새어 나갔다"). Markoff의 평가는 다소 가혹하지만, 이동의 사실관계 자체는 다른 사료들과 일치한다.

PARC로 흘러간 것은 "마우스 + 비트맵 디스플레이 + 객체 지향 텍스트 모델"이지, NLS의 핵심 구조가 아니었다. 떠난 것은 다음과 같다.

- **chord keyset** — 왼손 5건반 코드 키보드. NLS에서 마우스(오른손)와 한 쌍으로 작동했다. PARC는 키셋을 빼고 마우스+QWERTY 조합으로 단순화했다.
- **viewspecs** — 같은 문서에 다른 "뷰 지정자"를 적용해 outline 깊이, 라벨, 정렬을 즉시 바꾸는 메커니즘. PARC의 WYSIWYG는 이를 "한 가지 뷰가 곧 문서"로 환원했다.
- **B/C activity** — A는 본업, B는 본업을 개선하는 활동, C는 "개선을 개선하는" 메타 개선. PARC는 A에 집중하는 사용자 모델만 가져갔다.
- **Bootstrap 자기개선 회로** — 도구를 만드는 팀이 그 도구로 자기 자신을 개선하며, 그 결과를 외부 조직으로 확산시키는 코-에볼루션 루프. PARC의 모델은 "연구실이 만들고, 사용자는 쓴다"였다.

Alan Kay 본인은 NLS 데모를 "one of the greatest experiences in my life"라 회고했다. 그러나 PARC가 만든 것은 NLS의 후속이 아니라 다른 계열의 시스템 — Smalltalk + Alto — 이었다. Kay는 후일 이를 두고 "Engelbart, for better or for worse, was trying to make a violin, but most people don't want to learn the violin" ("엥겔바트는 좋게 봐주든 나쁘게 봐주든 바이올린을 만들고 있었다. 그러나 대부분의 사람은 바이올린을 배우고 싶어 하지 않는다") 이라 정리했다. 이 한 문장이 PARC가 NLS에서 무엇을 떼어냈는지를 압축한다. 그것은 "전문가용 악기"라는 사상 자체였다.

이 단순화가 실용적 필요였는지 사상적 후퇴였는지는 사료에 따라 갈린다. Bardini *Bootstrapping* (2000)은 사상적 후퇴 쪽으로 무게를 싣는다. Bardini의 진단은 두 층이다. 첫째, NLS는 모달 인터페이스였고 PARC는 모드리스였는데, "modeless" 선택은 단순히 기술적 진보가 아니라 "사용자가 이미 도구를 알고 있다고 가정하지 않는다"는 사용자 모델의 교체였다. 둘째, Engelbart의 설계는 "사용자를 발명한다(invents the kind of people they expect to use their innovations)" — 즉 도구가 사람을 끌어올린다는 전제 위에 서 있는데, PARC는 "현재 있는 사람"을 받아들였다. 이 둘은 같은 기술을 다른 인류학 위에 올린 것이다.

## 2. 학습곡선 논쟁 — chord keyset은 정말 실패했는가

chord keyset 비판은 가장 자주 인용되는 실패 서사다. Bardini는 "Engelbart's notion of returning to the five-chord keyset failed because it did not accommodate the way people actually work" ("다섯 건반 코드 키셋으로 돌아가자는 엥겔바트의 구상은 실제 사람들이 일하는 방식에 맞지 않았기 때문에 실패했다") 고 결론지었다. 이는 정량적 효율성 논의가 아니다. 그가 가리키는 것은 "타이핑 학습은 하면서 키셋 학습은 거부한다"는 비대칭이 사회적으로 이미 굳어 있었다는 사실이다.

Engelbart 본인의 반박은 두 갈래로 읽어야 한다.

첫째, 학습 비용/능력 거래의 비대칭. Engelbart는 *Augmenting Human Intellect* (1962)에서 도구의 가치를 "도구가 풀어주는 능력"으로 평가해야지 "도구의 진입 비용"만으로 평가해선 안 된다고 주장했다. 그의 코어 가설은 Whorf적이다 — "Both the language used by a culture, and the capability for effective intellectual activity are directly affected during their evolution by the means by which individuals control the external manipulation of symbols" ("문화가 사용하는 언어와 효과적 지적 활동의 능력은, 개인이 외부 기호 조작을 통제하는 수단에 의해 진화 중에 직접 영향받는다"). 도구가 언어를 바꾸고, 언어가 사고를 바꾼다면, 학습 곡선은 비용이 아니라 입장료다.

둘째, 받쳐줄 인프라의 부재. Engelbart는 후기 작업에서 chord keyset 자체보다 그것을 사회가 학습하도록 받쳐줄 B/C activity의 부재를 더 자주 지적했다. 바이올린은 어렵지만 음악원, 강사, 악보 시스템, 평가 체계가 학습을 받친다. 컴퓨팅에는 그 인프라가 없었다. 그래서 키셋을 "도구 단독의 실패"로 읽는 것은 그가 보기엔 단계 오류다.

비판자의 정당한 부분은 분명히 있다. 모달 인터페이스, 정해진 학습 경로, 단일 작업 환경 가정은 1970년대 사무실의 워크플로우와 충돌했다. 그러나 비판이 과잉 일반화되는 지점도 분명하다. "사람들이 학습을 거부했다"는 명제는 "사회가 그 학습을 받칠 인프라를 만들지 않기로 했다"와 다르고, 후자는 정책·자본·문화의 선택이지 사용자의 본성이 아니다. Bardini는 이 둘을 구분해 다루며, Engelbart의 잘못은 "악기를 만든 것"이 아니라 "악기와 동시에 음악원을 만들지 못한 것"이라 본다.

## 3. ARC 해체와 Bootstrap Institute의 영향력 한계

ARC의 자금 기반은 1969년 Mansfield Amendment를 기점으로 흔들리기 시작했다. 비군사 연구에 대한 군 자금 사용을 제한한 이 개정안과 베트남전 종결, Apollo 프로그램 종료가 겹치며 ARC의 ARPA·NASA 자금은 1970년대 초 동안 점진적으로 줄었다. 1976년 SRI 경영진은 Engelbart의 운영 방식에 동의하지 않았고, AI 연구자 Bertram Raphael을 통해 ARC를 Tymshare로 매각하는 협상을 마쳤다. 1977년 기술과 인력 20명이 Tymshare로 이전했고, 시스템 이름은 "Augment"가 되어 Office Automation Division의 상용 서비스로 제공됐다. Engelbart 본인은 Tymshare 내부에서 점차 주변화되었다고 사료들은 일관되게 기록한다.

이후 Engelbart는 1989년 딸 Christina와 함께 Bootstrap Institute(나중의 Doug Engelbart Institute)를 세웠다. 그러나 1990–2000년대 그의 후기 활동은 산업 임팩트가 거의 없었다. 그 이유는 단일 요인이 아니다.

- **자금 구조의 변화** — ARPA가 받쳐주던 "장기·탐색·기초" 연구 모델이 사라지고, "단기·결과 지향·즉시 적용" 모델이 그 자리를 차지했다. Bret Victor도 *The Future of Programming* (DBX 2013) 강연 레퍼런스에서 이 전환을 지적한다.
- **소통 양식의 미스매치** — Engelbart는 "Collective IQ", "CoDIAK"(Concurrent Development, Integration and Application of Knowledge), "ABC activity" 같은 자기 어휘를 끝까지 고수했다. 이 어휘는 그의 사상적 정합성을 지키는 데는 도움이 됐지만, 1990년대 GUI·웹 시대의 산업 어휘로는 번역되지 않았다.
- **방법론의 모듈화 실패** — Bootstrap의 핵심은 "도구를 만드는 팀이 그 도구로 자기를 개선한다"는 회로다. 이것은 단일 컴포넌트로 떼어 팔 수 없다. 컨설팅 상품으로 만들기에는 너무 통합적이었고, 오픈소스 프로젝트로 만들기에는 시기가 맞지 않았다.

이 결과 Bootstrap Institute는 Engelbart 사상의 보존소로는 기능했지만, 그 사상을 산업에 다시 주입하는 펌프로는 기능하지 못했다.

## 4. Victor·Kay 계보의 평가 — 무엇을 잇고 무엇을 비판하는가

Bret Victor는 Engelbart의 가장 충실한 계승자 중 하나이지만, 이어받는 방식이 특이하다. *The Future of Programming* (DBX 2013) 강연에서 Victor는 1973년 IBM 시스템 엔지니어 복장으로 무대에 올라 오버헤드 프로젝터를 쓰며 "1973년 시점에서 본 미래"를 발표했다. 의도된 시간 역전은 단순한 연출이 아니라 비판이다. 그가 NLS, GRAIL, Smalltalk, Sutherland의 Sketchpad를 같은 줄에 놓고 "spatial representations of information"이라 묶을 때, 그 묶음이 1970년대 이후 거의 진척되지 않았다는 사실이 비판의 본체다. Victor가 인용하는 Engelbart는 "마우스의 발명자"가 아니라 "텍스트 덤프를 공간 표현으로 바꾸려 한 사람"이다.

Alan Kay의 위치는 더 양가적이다. Kay는 NLS 데모를 자신의 인생에서 가장 위대한 경험 중 하나로 회고하면서, 동시에 Engelbart의 모델을 "literacy" 관점에서 재구성한다. Kay에게 컴퓨터 리터러시는 "읽기와 쓰기 모두에서 동등한 유창성"을 요구한다 — "in print writing, the tools you generate are rhetorical, while in computer writing, the tools you generate are processes" ("인쇄물 쓰기에서 만드는 도구는 수사적이지만, 컴퓨터 쓰기에서 만드는 도구는 프로세스다"). 이 정의는 Engelbart의 "도구 만드는 도구" 개념과 거의 같다. 그러나 Kay는 Engelbart의 "co-evolution"을 "literacy"로 이름을 바꾸면서 사회적 단위를 한 단계 내렸다. Engelbart가 "조직의 Collective IQ"를 보았다면 Kay는 "개인의 인지 도구"를 보았다.

동시에 Kay는 Engelbart에게 가장 가혹한 평가도 남긴 사람이다. "violin" 비유는 변호처럼 들리지만 실제로는 "산업이 그를 받지 않은 데에는 이유가 있었다"는 진단이다. Kay 본인은 PARC에서 Dynabook을 통해 "어린이도 다룰 수 있는 강력한 표현 매체"를 추구했고, 이것은 Engelbart의 "전문가 양성" 노선과 명백히 다른 길이었다. Kay의 후기 인터뷰들에서 반복되는 자기 평가 — "we still don't have a Dynabook" — 는 Engelbart가 못 간 자리에 자기도 못 갔다는 자백이기도 하다.

## 5. LLM 시대의 재해석 — 학습 곡선이 사라지면 회로도 사라지는가

LLM 등장 이후 Engelbart 비전이 다시 진지하게 읽히는 이유는 두 갈래의 주장이 동시에 가능해졌기 때문이다.

**낙관적 독해.** chord keyset이나 viewspecs 같은 "전문가 도구"의 진입장벽이 자연어 인터페이스로 우회된다. 사용자는 코드를 모르고도 시스템을 조작하고, 데이터 변환을 지시하고, 워크플로우를 구성한다. 이 독해에서 Engelbart의 "악기"는 LLM이 대신 연주해주는 셈이고, 그가 평생 풀지 못한 "도구가 너무 어렵다"는 문제는 모델 능력에 흡수된다.

**비관적 독해.** LLM이 답을 즉시 주는 구조는 Bootstrap의 자기개선 회로를 끊는다. B activity(본업을 개선하는 활동)는 사용자가 자기 작업을 명시적으로 관찰·구조화·재설계할 때 발생한다. C activity(개선을 개선하는 활동)는 그 관찰을 다시 관찰할 때 발생한다. LLM이 "결과만 주는" 방식으로 쓰이면 A activity의 산출은 늘지만 B/C activity의 회로는 짧아지거나 끊긴다. 이 독해에서 LLM은 Engelbart 비전의 동맹이 아니라 그 정반대 — Licklider 노선의 "automation/replacement"의 가장 강력한 형태 — 다.

두 독해 사이에 균형점이 있다. LLM은 학습 곡선을 평탄화할 수도 있고 회로를 끊을 수도 있다. 차이는 도구의 능력이 아니라 도구를 둘러싼 B/C activity가 함께 설계되었는가다. Engelbart의 1962년 가설을 LLM 시대 어휘로 옮기면 다음과 같다 — 사용자가 LLM의 출력을 "수용" 모드로 받으면 augmentation은 일어나지 않고, "관찰·재구성·재지시" 모드로 받으면 일어난다. 이 차이는 모델 안에 있지 않고 하네스(harness) 안에 있다.

## 6. 현재 작업 접점 — mirror-mind·lighthouse 설계 관점

Engelbart 비판사를 mirror-mind와 lighthouse 설계에 비추면 세 가지 시사점이 남는다.

첫째, **표면과 회로의 분리.** PARC가 NLS의 표면(마우스, GUI)만 가져가고 회로(B/C activity, Bootstrap)를 버린 패턴은 LLM 제품에서 반복되기 쉽다. lighthouse의 propose 카드, 취소 FSM, NarrativeState 같은 구조는 표면 UX가 아니라 "사용자의 작업을 관찰·재구성하는 회로"의 자리다. 이 회로가 표면에 흡수되어 사라지지 않도록 책임 분리가 필요하다.

둘째, **학습 곡선의 사회적 인프라.** Engelbart의 chord keyset 실패는 "도구 단독 실패"가 아니라 "도구를 받칠 사회 인프라의 부재"였다. mirror-mind 안의 AGENTS.md, operations.md, 기억 시스템, 주간 플랜은 그 인프라에 해당한다. 도구(에이전트)의 학습 곡선이 정당화되려면 그것을 받칠 운영 양식이 같이 자라야 한다는 원칙이 여기서 도출된다.

셋째, **augmentation의 모드 차이.** LLM을 "수용 모드"로 쓰면 자기개선 회로가 끊긴다는 비관적 독해는 P0(적은 시간 × 더 좋은 결과 + 남는 시간 사고 활동)와 직접 연결된다. 속도가 아닌 통제력을 기준으로 두는 작업 방식은 Engelbart 어휘로 옮기면 "B/C activity의 비중을 의식적으로 유지한다"가 된다. 이 관점에서 lighthouse는 사용자의 A activity를 빠르게 해주는 도구가 아니라, B activity를 가능하게 하는 도구로 정의되어야 한다.

Engelbart의 비전이 좁아진 이유는 단일 사건이 아니다. 자금 모델의 전환, 산업의 단순화 압력, 사상의 모듈화 실패, 후기 소통의 어휘 미스매치가 겹쳤다. 그러나 그 비전이 다시 살아나는 이유는 분명하다. 도구가 강해질수록 "도구로 자기 자신을 개선한다"는 회로가 다시 가능해지고, 동시에 그 회로가 끊길 위험도 같이 커지기 때문이다. Bardini가 2000년에, Victor가 2013년에, 지금 LLM 시대의 우리가 다시 같은 자료를 펴는 것은 이 회로 문제가 아직 풀리지 않았다는 사실의 증거다.

---

**주요 출처**

- Thierry Bardini, *Bootstrapping: Douglas Engelbart, Coevolution, and the Origins of Personal Computing*, Stanford University Press, 2000
- John Markoff, *What the Dormouse Said: How the Sixties Counterculture Shaped the Personal Computer Industry*, Viking, 2005
- Douglas C. Engelbart, *Augmenting Human Intellect: A Conceptual Framework*, SRI Summary Report AFOSR-3223, 1962
- Bret Victor, *The Future of Programming*, DBX Conference, 2013-07-30, references at worrydream.com/dbx
- Alan Kay, *User Interface: A Personal View*, 1989
- Doug Engelbart Institute archive (dougengelbart.org) — Bootstrapping methodology, ABC activity, CoDIAK
- Augmentation Research Center 관련 항목 (Wikipedia, Computer History Museum SRI ARC Journal finding aid)
- Stanislav Datskovskiy, "Engelbart's Violin", loper-os.org, 2012
- "Explaining the Neglect of Doug Engelbart's Vision: The Economic Irrelevance of Human Intelligence Augmentation", macroresilience.com, 2013
