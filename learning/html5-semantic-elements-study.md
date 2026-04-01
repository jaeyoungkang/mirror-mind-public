---
layout: default
title: "HTML5 시맨틱 요소 비교학습"
---

# HTML5 시맨틱 요소 비교학습

> 2026-03-31 세션112. HTML5가 선택한 요소들을 "혼동하기 쉬운 쌍" 단위로 비교한다.
> 핵심 질문: "이것이 무엇인가"를 HTML이 스스로 말할 수 있는가.
> 체크 기준: CSS 끄면 구조가 읽히는가.
>
> **학습 방법: 각 그룹마다 퀴즈를 먼저 풀고, 해설을 읽는다. 먼저 틀려보고, 왜 틀렸는지 읽는 게 체화가 빠르다.**

---

## 배경: HTML의 변천사와 HTML5의 철학

### 왜 이 교재가 필요한가

이 교재에서 다루는 모든 비교 — `div` vs `section`, `strong` vs `b`, `a` vs `button` — 는 결국 하나의 질문으로 수렴한다: **"이 마크업이 무엇인가를 말하는가, 아니면 어떻게 보이는가만 말하는가?"** 이 질문이 HTML 30년 역사의 핵심 긴장이었고, HTML5는 그 긴장에 대한 답이다.

### 1단계: 문서로 출발 (1989~1995)

팀 버너스리가 CERN에서 만든 최초의 HTML은 **과학 문서를 의미적으로 기술하는 언어**였다. 제목(`h1`), 문단(`p`), 링크(`a`), 목록(`ul/ol`) — 전부 "이것이 무엇인가"를 말하는 요소들이다. "어떻게 보이는가"는 브라우저가 알아서 했다.

```
[의미] h1 = "이것은 1레벨 제목이다"
[표현] 브라우저가 크고 굵게 그린다 (하지만 그건 브라우저의 판단)
```

HTML 2.0 (1995, RFC 1866)이 이 구조를 공식화했다. 이때까지 HTML은 순수한 **의미 기술 언어**였다.

### 2단계: 표현과 의미가 뒤섞임 (1996~2003)

웹이 대중화되면서 사람들은 "문서를 기술"하는 게 아니라 **"화면을 꾸미고"** 싶어했다. 브라우저 전쟁(넷스케이프 vs IE)이 터지면서:

- `<font color="red" size="5">` — 의미가 아니라 생김새를 직접 지정
- `<table>` 레이아웃 — 표가 아닌데 표로 화면을 짜는 해킹
- `<b>`, `<i>` — 원래 의미 없이 "굵게", "기울임"만 뜻함
- `<div>` 남용 — 의미 없는 상자로 모든 걸 감쌈
- 브라우저별 독자 태그 — `<marquee>`, `<blink>`

**결과:** HTML이 "이것이 무엇인가"를 잃고 "이것이 어떻게 보이는가"만 남았다. CSS가 꺼지면 아무것도 안 읽히는 페이지들이 넘쳐났다.

이 시기에 W3C는 XHTML 방향으로 갔다. "HTML을 XML처럼 엄격하게 만들자." 이론적으로는 깔끔했지만, 현실의 웹은 이미 깨진 마크업으로 가득 차 있었고, XHTML 2.0은 기존 웹과의 호환성을 포기하려 했다.

### 3단계: 현실에서 의미를 되찾다 — HTML5 (2004~현재)

2004년, 브라우저 제작사들(Apple, Mozilla, Opera)이 WHATWG를 만들고 선언했다: **"현실의 웹에서 출발하자."**

WHATWG의 접근은 두 가지였다:

**첫째, 깨진 마크업도 살려서 읽는다.**
XML처럼 "에러면 중단"이 아니라 "가능한 한 복구해서 보여준다." 이건 느슨함이 아니라, 웹이 전문가만의 매체가 아닌 **누구나 올리고 누구나 읽는 공공 공간**이기 때문에 생긴 선택이었다. HTML 표준은 파싱 에러 상황을 수백 가지 세밀하게 정의한다 — "에러를 무시"가 아니라 "에러를 일관되게 복구"하는 것이다.

**둘째, 현실의 저작 관행을 관찰해서 의미를 다시 제도화했다.**
사람들이 이미 `<div class="header">`, `<div class="nav">`, `<div class="article">`를 쓰고 있었다. HTML5는 이 패턴을 흡수해서 **진짜 요소로 격상**시켰다:

| 사람들이 이미 쓰던 패턴 | HTML5가 만든 요소 |
|----------------------|-----------------|
| `<div class="header">` | `<header>` |
| `<div class="nav">` | `<nav>` |
| `<div class="article">` | `<article>` |
| `<div class="section">` | `<section>` |
| `<div class="footer">` | `<footer>` |
| `<div class="main">` | `<main>` |
| `<div class="sidebar">` | `<aside>` |

이게 이 교재 그룹 1의 모든 비교가 존재하는 이유다. `div.header`와 `<header>`는 화면에서 똑같이 보인다. 하지만 `<header>`는 **기계가 "이것은 머리 영역이다"를 안다.** 스크린리더가 건너뛸 수 있고, 검색 엔진이 구조를 파악하고, CSS가 꺼져도 문서로 읽힌다.

### HTML5가 동시에 고친 것들

HTML5는 문서 뼈대만 고친 게 아니다. 교재의 나머지 그룹들도 같은 흐름의 산물이다:

**그룹 2 (텍스트 의미) — `<b>`와 `<i>`를 죽이지 않고 재정의했다.**
HTML 2단계에서 `<b>`는 "굵게", `<i>`는 "기울임"이었다 — 순수 표현. HTML5는 이걸 버리지 않고 의미를 재부여했다: `<b>` = "시각적으로 구분되는 텍스트", `<i>` = "다른 목소리/톤". 동시에 `<strong>` = "중요함", `<em>` = "강세"를 명확히 분리했다. 표현이 같아도 의미가 다른 것을 구별할 수 있게 된 것이다.

**그룹 3 (인터랙션) — 브라우저 기본 동작을 복권했다.**
`<details/summary>`, `<dialog>` 같은 요소는 JS 없이 접기/펼치기, 모달이 작동한다. 이건 HTML5의 "**점진적 향상(Progressive Enhancement)**" 철학이다: HTML만으로 핵심 기능이 돌아가고, CSS가 꾸미고, JS가 확장한다. JS가 실패해도 기본 동작은 남는다.

**그룹 4 (미디어) — 플러그인 의존을 끊었다.**
`<video>`, `<audio>`가 Flash를 대체했다. `<figure/figcaption>`이 이미지와 설명의 관계를 선언하게 했다. 전부 "외부 도구 없이 브라우저가 직접 이해하고 처리한다"는 원칙.

**그룹 5 (폼) — 브라우저에 내장된 검증.**
`<input type="email/url/tel/date">`는 JS 없이 키보드가 바뀌고 형식이 검증된다. `<label>`과 `<fieldset/legend>`는 폼의 의미를 기계가 읽을 수 있게 한다. 이것도 점진적 향상 — JS 검증이 추가되더라도 HTML 수준의 검증이 기본층으로 남는다.

**그룹 6 (시간·데이터) — 사람과 기계의 이중 읽기.**
`<time datetime="2017-06-12">어제</time>` — 사람은 "어제"를 읽고, 기계는 "2017-06-12"를 읽는다. `<data value="187">cited 187</data>` — 같은 원리. HTML5는 사람과 기계가 같은 문서에서 각자에게 맞는 정보를 읽을 수 있는 구조를 만들었다.

### HTML5의 핵심 철학 — 한 줄 요약

> **의미를 포기하지 않되, 현실을 버리지 않는다.**

- 순수한 이상(XHTML 2.0)은 현실을 무시했다 → 실패
- 현실만 따라가면(div + CSS 남용) 의미를 잃는다 → 접근성, SEO, 복원력 붕괴
- HTML5는 **현실의 패턴을 관찰해서 의미를 재제도화**했다

이 교재의 모든 "잘못된 예 → 올바른 예" 비교는 결국 이 한 줄의 구체적 적용이다.

### Living Standard — 끝나지 않는 진화

HTML5는 고정된 판본이 아니다. WHATWG의 **Living Standard** 체계에서 HTML은 브라우저 구현과 함께 계속 갱신된다. `<dialog>`, `<details>`, `<search>`(최근 추가) 같은 요소들이 계속 늘어난다. "HTML 6"는 없다 — HTML은 이제 살아 있는 문서다.

이게 중요한 이유: **지금 div로 쓰고 있는 패턴이 내일 시맨틱 요소가 될 수 있다.** `<div class="search">`를 쓰고 있다면, 그건 이미 `<search>` 요소가 되어 있을 수 있다.

### 교재 구조와 HTML 역사의 대응

| 교재 그룹 | HTML5가 한 일 | 역사적 맥락 |
|----------|-------------|-----------|
| 1. 문서 뼈대 | `div` 패턴을 시맨틱 요소로 격상 | 2단계에서 잃어버린 문서 구조를 되찾음 |
| 2. 텍스트 의미 | `b`/`i`를 죽이지 않고 의미 재부여 | 표현과 의미의 분리를 완성 |
| 3. 인터랙션 | 브라우저 기본 동작 복권 | 점진적 향상 — JS 없이도 핵심이 작동 |
| 4. 미디어 | 플러그인 없이 브라우저가 직접 처리 | Flash/Silverlight 의존 종식 |
| 5. 폼 | 브라우저 내장 검증 + 시맨틱 그룹 | 점진적 향상의 폼 적용 |
| 6. 시간·데이터 | 사람/기계 이중 읽기 구조 | 웹을 기계 판독 가능한 매체로 |

---

## 그룹 1: 문서 뼈대 — 어디서 끊는가

### 퀴즈 1: 먼저 풀어보라

**Q1-1. 이 HTML의 문제를 모두 찾아라 (힌트: 7개)**

```html
<div class="header">
  <div class="logo">Light House</div>
  <div class="nav">
    <a href="/">홈</a>
    <a href="/search">검색</a>
  </div>
</div>
<div class="main">
  <div class="post">
    <div class="title">Attention Is All You Need 리뷰</div>
    <div class="body">
      <div class="section-title">배경</div>
      <div class="text">기존 seq2seq 모델은 장거리 의존성에 취약했다.</div>
    </div>
  </div>
</div>
```

**Q1-2. section인가, article인가, div인가?**

| # | 상황 | 내 답 |
|---|------|------|
| a | 뉴스 사이트의 기사 하나 | |
| b | 블로그 글의 "방법론" 챕터 | |
| c | 2컬럼 레이아웃을 위한 감싸기 | |
| d | 블로그 댓글 하나 | |
| e | 대시보드의 "최근 활동" 위젯 | |

**Q1-3. 링크 목록이 있다. 다음 중 `nav`로 감싸야 하는 것은?**

| # | 상황 | nav인가? |
|---|------|---------|
| a | 사이트 상단 GNB (홈, 검색, 소개) | |
| b | 논문 본문 안의 참고문헌 링크 목록 | |
| c | 페이지 하단 사이트맵 링크 | |

---

### 해설 1: 정답과 근거

#### Q1-1 정답

<details>
<summary>정답 보기</summary>

| # | 현재 | 올바른 요소 | 이유 |
|---|------|-----------|------|
| 1 | `div.header` | `header` | 사이트 머리 영역 → 랜드마크 |
| 2 | `div.nav` | `nav > ul > li > a` | 사이트 탐색 링크 → nav. 링크 나열은 목록 |
| 3 | `div.main` | `main` | 페이지 고유 콘텐츠 → "본문으로 건너뛰기" 랜드마크 |
| 4 | `div.post` | `article` | 떼어내도 혼자 의미 있는 글 |
| 5 | `div.title` | `h1` | 글의 제목. CSS 끄면 크기 위계가 안 보임 |
| 6 | `div.body` | `section` | 글의 챕터 → 더 큰 글의 파트 |
| 7 | `div.section-title` | `h2` | 챕터 제목 |

</details>

#### Q1-2 정답

<details>
<summary>정답 보기</summary>

| # | 상황 | 답 | 이유 |
|---|------|-----|------|
| a | 뉴스 기사 | `article` | RSS로 보내도 혼자 의미 있다 |
| b | 블로그 "방법론" 챕터 | `section` | 더 큰 글의 일부. 혼자 떼어내면 맥락 부족 |
| c | 2컬럼 레이아웃 감싸기 | `div` | 순수 레이아웃. 의미 없음 |
| d | 블로그 댓글 하나 | `article` | 댓글도 독립 콘텐츠. article 안에 article 중첩의 전형 |
| e | 대시보드 위젯 | `section` | 대시보드의 한 영역. 독립 콘텐츠라기보다 페이지 구성 파트 |

</details>

#### Q1-3 정답

<details>
<summary>정답 보기</summary>

| # | 상황 | nav인가? | 이유 |
|---|------|---------|------|
| a | 사이트 GNB | **Yes** | 사이트 탐색 목적 |
| b | 참고문헌 링크 | **No** | 탐색이 아니라 참조 |
| c | 사이트맵 | **Yes** | 사이트 탐색 목적 (footer에 있어도 nav 가능) |

</details>

---

### 해설 1: 상세 설명

#### `section` vs `article`

둘 다 "콘텐츠 덩어리". 차이는 **독립성**.

```html
<!-- 잘못: div로 구분 -->
<div class="blog-post">
  <div class="title">논문 리뷰: Attention Is All You Need</div>
  <div class="chapter">배경</div>
  <div class="text">기존 seq2seq 모델은...</div>
</div>

<!-- 올바름 -->
<article>
  <h1>논문 리뷰: Attention Is All You Need</h1>
  <section>
    <h2>배경</h2>
    <p>기존 seq2seq 모델은...</p>
  </section>
</article>
```

| 질문 | article | section |
|------|---------|---------|
| 떼어내서 RSS/카드/다른 페이지에 놓아도 혼자 의미 있는가? | **Yes** — 블로그 글, 뉴스, 논문, 댓글 | No |
| 더 큰 글의 **챕터/파트**인가? | No | **Yes** — 배경, 방법론, 결론 |
| 중첩 가능? | article 안에 article (댓글 등) | section 안에 section (하위 챕터) |

**판별법:** "이걸 트위터에 공유하면 혼자 말이 되는가?" → Yes면 article, No면 section.

#### `header` vs `h1`~`h6`

`h1`~`h6`은 **제목 텍스트**, `header`는 **제목을 포함하는 머리 영역**.

```html
<!-- h1 = 제목 그 자체 -->
<h1>Light House</h1>

<!-- header = 제목 + 부가 정보를 묶는 영역 -->
<header>
  <h1>Light House</h1>
  <p>AI 연구 동료</p>
  <nav>...</nav>
</header>
```

| | `h1`~`h6` | `header` |
|---|-----------|----------|
| 정체 | 제목 텍스트 | 영역(컨테이너) |
| 혼자 쓸 수 있나 | Yes | 안에 뭐가 있어야 의미 있음 |
| 여러 개 가능? | h1은 페이지당 1개 권장 | article마다, section마다 각각 가능 |

**흔한 실수:** header를 페이지 맨 위에만 쓰는 것. 실제로는 article이나 section마다 자기 header를 가질 수 있다.

```html
<article>
  <header>
    <h2>Attention Is All You Need</h2>
    <time datetime="2017-06-12">2017</time>
    <p>Vaswani et al.</p>
  </header>
  <p>본문...</p>
</article>
```

#### `main` vs `body`

```html
<body>
  <header>사이트 로고 + 네비게이션</header>
  <aside>사이드바</aside>
  <main>
    <!-- 이 페이지의 고유한 핵심 콘텐츠 -->
    <article>...</article>
  </main>
  <footer>저작권, 링크</footer>
</body>
```

| | `body` | `main` |
|---|--------|--------|
| 범위 | 페이지 전체 (nav, footer 포함) | **이 페이지만의 고유 콘텐츠** |
| 반복되는가 | 매 페이지마다 있음 | 안의 내용이 페이지마다 다름 |
| 스크린리더 | — | "본문으로 건너뛰기" 랜드마크 |

**핵심:** main = "모든 페이지에서 반복되는 것(nav, sidebar, footer)을 제외한 나머지".

#### `div` — 의미가 없을 때만

| 상황 | 쓸 것 | div를 쓰면? |
|------|-------|------------|
| 블로그 글 하나 | `article` | 기계가 "글"인 줄 모름 |
| 글의 챕터 | `section` | 구조가 안 보임 |
| 페이지 상단 영역 | `header` | 랜드마크 소실 |
| 사이트 탐색 링크 | `nav` | 스크린리더가 건너뛰기 불가 |
| 핵심 콘텐츠 영역 | `main` | "본문으로 가기" 불가 |
| **순수 CSS 레이아웃 목적** | **`div`** | ← 이때만 맞다 |

---

## 그룹 2: 텍스트 의미 — 보이는 건 같은데 뜻이 다르다

### 퀴즈 2: 먼저 풀어보라

**Q2-1. strong vs b, em vs i — 어떤 요소를 쓸까?**

| # | 문장 | 내 답 |
|---|------|------|
| a | "이 약물은 **임산부에게 투여 금지**이다." | |
| b | 레시피에서 "**밀가루** 200g, **설탕** 50g" 재료명을 굵게 | |
| c | "*그건 네가 한 게 아니잖아*" — 강세 위치가 의미를 바꿈 | |
| d | 논문에서 라틴어 학명 *Homo sapiens* | |

**Q2-2. del인가, s인가?**

| # | 상황 | 내 답 |
|---|------|------|
| a | 쇼핑몰 가격 변경: ~~50,000원~~ → 35,000원 | |
| b | 할인 이벤트 종료: ~~정가 50,000원~~ (이 가격은 더 이상 유효하지 않음) | |
| c | 위키피디아 편집 이력에서 삭제된 문장 | |

**Q2-3. 검색 결과에서 사용자가 입력한 키워드를 노랗게 표시하고 싶다. `<span style="background:yellow">` vs `<mark>` — 어떤 걸 써야 하는가?**

---

### 해설 2: 정답과 근거

#### Q2-1 정답

<details>
<summary>정답 보기</summary>

| # | 문장 | 답 | 이유 |
|---|------|-----|------|
| a | 임산부 투여 금지 | `strong` | 빼면 의미가 달라지는 중요한 경고 |
| b | 밀가루/설탕 재료명 | `b` | 시각적 구분. 밀가루가 설탕보다 "중요"한 건 아니다 |
| c | 강세가 의미를 바꿈 | `em` | "네가"에 두면 "다른 사람이 했다", "한"에 두면 "하지 않았다" |
| d | 라틴어 학명 | `i` | 다른 언어/전문 용어. 강세가 아니라 톤이 다름 |

</details>

#### Q2-2 정답

<details>
<summary>정답 보기</summary>

| # | 상황 | 답 | 이유 |
|---|------|-----|------|
| a | 가격 변경 | `del` + `ins` | 문서 편집 이력 — 삭제된 가격과 새 가격 |
| b | 이벤트 종료 | `s` | "더 이상 정확하지 않은" 정보. 편집 이력이 아니라 현재 시점의 무효화 |
| c | 위키 편집 이력 | `del` | 말 그대로 문서에서 삭제된 내용 |

</details>

#### Q2-3 정답

<details>
<summary>정답 보기</summary>

`mark`. "참조 맥락에서 관련 있는 부분"을 표시하는 게 mark의 정확한 용도. 검색 결과 하이라이트가 가장 전형적인 사례. CSS 배경색은 의미가 없다.

</details>

---

### 해설 2: 상세 설명

#### `strong` vs `b`

둘 다 화면에서 **굵게** 보인다. 차이는 의미.

```html
<!-- strong = "이 부분이 중요하다" -->
<p>이 실험의 <strong>핵심 한계</strong>는 샘플 크기다.</p>

<!-- b = "시각적으로 구분할 뿐, 중요도 차이 없음" -->
<p>검색 결과에서 <b>키워드</b>를 강조 표시했습니다.</p>
```

| | `strong` | `b` |
|---|----------|-----|
| 의미 | **중요하다** (importance) | 시각적 구분 (stylistic offset) |
| 스크린리더 | 강세를 넣어 읽는다 | 차이 없이 읽는다 |
| 쓸 때 | 경고, 핵심 결론, 주의 사항 | 키워드 하이라이트, 제품명, 리드 문장 |

**판별법:** "이걸 빼면 의미가 달라지는가?" → Yes면 strong, No면 b.

#### `em` vs `i`

둘 다 화면에서 *기울임*으로 보인다.

```html
<!-- em = "강세를 준다" — 읽는 톤이 달라짐 -->
<p>그건 <em>내가</em> 한 게 아니다.</p>   <!-- "내가"에 힘 -->
<p>그건 내가 <em>한</em> 게 아니다.</p>    <!-- "한"에 힘 — 의미가 바뀜 -->

<!-- i = "다른 목소리, 다른 언어, 전문 용어" -->
<p>이 현상을 <i lang="la">in vitro</i>에서 재현했다.</p>
<p>그는 속으로 <i>이건 아닌데</i>라고 생각했다.</p>
```

**핵심:** em의 위치를 바꾸면 문장 의미가 바뀐다. i는 바꿔도 의미가 안 바뀐다.

#### `del` vs `s`

```html
<!-- del = "삭제된 내용" (문서 편집 이력) -->
<p>가격: <del>50,000원</del> <ins>35,000원</ins></p>

<!-- s = "더 이상 정확하지 않은" (현재 관점에서 무효) -->
<p><s>재고 있음</s> 품절</p>
```

| | `del` | `s` |
|---|-------|-----|
| 의미 | 문서에서 **삭제됨** | 더 이상 **정확하지 않음** |
| 짝꿍 | `ins` (삽입)과 쌍 | 없음 |
| 쓸 때 | 가격 변경, 편집 이력, diff | 품절, 마감, 철회된 정보 |

#### `mark` vs CSS 배경색

```html
<!-- mark = "참조 맥락에서 관련 있는 부분" -->
<p>검색 결과: "이 연구는 <mark>장기 기억 통합</mark>에 초점을 맞춘다"</p>

<!-- CSS 배경색 = 순수 시각 강조 -->
<p>검색 결과: "이 연구는 <span style="background:#ff0">장기 기억 통합</span>에 초점을 맞춘다"</p>
```

---

## 그룹 3: 인터랙션 — 링크인가, 버튼인가

### 퀴즈 3: 먼저 풀어보라

**Q3-1. `a`인가, `button`인가, 둘 다 아닌가?**

| # | 상황 | 내 답 |
|---|------|------|
| a | "다크 모드 전환"을 클릭. URL은 안 바뀜 | |
| b | "검색 페이지로" 클릭. /search로 이동 | |
| c | `<div class="btn" onclick="save()">저장</div>` — 이건 괜찮은가? | |
| d | `<a href="#" onclick="doSomething()">저장</a>` — 이건? | |

**Q3-2. FAQ 접기/펼치기를 만들고 싶다. 복잡한 애니메이션은 필요 없다. JS로 구현해야 하는가?**

**Q3-3. 확인/취소 모달을 만든다. `<div class="modal">`로 만들면 빠지는 기능 3가지는?**

---

### 해설 3: 정답과 근거

#### Q3-1 정답

<details>
<summary>정답 보기</summary>

| # | 상황 | 답 | 이유 |
|---|------|-----|------|
| a | 다크 모드 전환 | `button` | 행동(상태 변경)이지 탐색이 아니다 |
| b | 검색 페이지 이동 | `a` | URL이 바뀌는 탐색 |
| c | div onclick | **잘못** | 키보드 접근 불가, 스크린리더 인식 못함. `button`이어야 함 |
| d | a href="#" onclick | **잘못** | 어디로도 안 가는데 href="#"? 탐색이 아니라 행동이면 `button` |

</details>

#### Q3-2 정답

<details>
<summary>정답 보기</summary>

**No.** `<details>/<summary>`를 쓰면 JS 없이 브라우저 기본 동작으로 접기/펼치기가 된다. 접근성(aria-expanded)도 자동.

```html
<details>
  <summary>자주 묻는 질문 1</summary>
  <p>답변 내용...</p>
</details>
```

</details>

#### Q3-3 정답

<details>
<summary>정답 보기</summary>

`<dialog>` 대신 div 모달을 쓰면 빠지는 것:
1. **ESC로 닫기** — 직접 구현해야 함
2. **포커스 트랩** — 모달 밖으로 탭 못 가게 직접 구현
3. **스크린리더 인식** — role="dialog"를 직접 추가해야 함

`<dialog>`는 이 셋이 공짜다.

</details>

---

### 해설 3: 상세 설명

#### `a` vs `button`

```html
<!-- a = "누르면 어딘가로 간다" (탐색) -->
<a href="/search">검색 페이지로</a>

<!-- button = "누르면 무언가를 실행한다" (행동) -->
<button onclick="submitForm()">제출</button>
```

| | `a` | `button` |
|---|-----|----------|
| 본질 | **탐색** — URL이 바뀐다 | **행동** — 상태가 바뀐다 |
| href 필수? | Yes. href 없는 a는 의미 없음 | href 없음 |
| 키보드 | Enter로 작동 | Enter + Space로 작동 |
| 스크린리더 | "링크"라고 읽음 | "버튼"이라고 읽음 |

**판별법:** "누르면 URL이 바뀌는가?" → Yes면 `a`, No면 `button`. `div`는 답이 아니다.

#### `details/summary` vs JS 아코디언

| | `details/summary` | JS 아코디언 |
|---|-------------------|------------|
| JS 필요? | **No** — 브라우저 기본 동작 | Yes |
| 접근성 | 기본 제공 (aria-expanded 자동) | 직접 구현해야 함 |
| 한계 | 애니메이션이 제한적 | 자유로움 |

#### `dialog` vs 모달 div

| | `dialog` | div 모달 |
|---|----------|---------|
| ESC로 닫기 | 자동 | 직접 구현 |
| 배경 클릭 차단 | `::backdrop` 자동 | 직접 구현 |
| 포커스 트랩 | 자동 (모달 밖으로 탭 못 감) | 직접 구현 |
| 스크린리더 | "대화상자"로 인식 | role="dialog" 직접 추가 |

---

## 그룹 4: 미디어와 캡션

### 퀴즈 4: 먼저 풀어보라

**Q4-1. 이미지 아래에 "Figure 1. 트랜스포머 아키텍처" 캡션을 달고 싶다. 어떻게 마크업하는가?**

```html
<!-- A안 -->
<img src="arch.png" alt="트랜스포머">
<p>Figure 1. 트랜스포머 아키텍처</p>

<!-- B안 -->
<figure>
  <img src="arch.png" alt="트랜스포머">
  <figcaption>Figure 1. 트랜스포머 아키텍처</figcaption>
</figure>
```

**Q4-2. `figure`는 이미지 전용 요소인가?**

**Q4-3. 모바일에서는 작은 이미지, 데스크톱에서는 큰 이미지를 보여주고 싶다. `<img>`만으로 충분한가?**

---

### 해설 4: 정답과 근거

#### Q4-1 정답

<details>
<summary>정답 보기</summary>

**B안.** A안은 이미지와 캡션이 "우연히 옆에 있을 뿐" 연결이 없다. figure로 감싸면 "이 설명은 이 이미지에 속한다"는 관계가 선언된다. figure를 사이드바로 옮겨도 의미가 유지된다.

</details>

#### Q4-2 정답

<details>
<summary>정답 보기</summary>

**아니다.** figure는 "본문에서 참조하는 독립 콘텐츠"면 다 쓴다. 코드 블록, 표, 인용문도 가능:

```html
<figure>
  <pre><code>const x = 42;</code></pre>
  <figcaption>변수 초기화 예시</figcaption>
</figure>
```

</details>

#### Q4-3 정답

<details>
<summary>정답 보기</summary>

**아니다.** `<picture>` 요소로 조건별 다른 이미지를 제공:

```html
<picture>
  <source media="(max-width: 600px)" srcset="hero-mobile.webp">
  <source media="(min-width: 601px)" srcset="hero-desktop.webp">
  <img src="hero.jpg" alt="히어로 이미지">  <!-- fallback -->
</picture>
```

</details>

---

### 해설 4: 상세 설명

#### `figure/figcaption` vs `img` + `p`

| | `figure` + `figcaption` | `img` + `p` |
|---|------------------------|-------------|
| 관계 | **이 설명은 이 이미지에 속한다** | 연결 없음 |
| 위치 이동 | figure를 사이드바로 옮겨도 의미 유지 | p를 옮기면 연결 끊김 |

#### `picture` vs `img`

| | `img` | `picture` |
|---|-------|-----------|
| 이미지 수 | 1개 | 조건별 여러 개 |
| 쓸 때 | 대부분의 경우 | 모바일/데스크톱 다른 이미지, WebP/AVIF 포맷 분기 |

#### `video/audio` — 플러그인을 죽인 요소

HTML5 이전에는 Flash, Silverlight 같은 플러그인이 필요했다. `<video>`와 `<audio>`가 이걸 대체했다.

```html
<video controls width="640">
  <source src="demo.mp4" type="video/mp4">
  <source src="demo.webm" type="video/webm">
  <p>브라우저가 비디오를 지원하지 않습니다. <a href="demo.mp4">다운로드</a></p>
</video>
```

---

## 그룹 5: 폼 — 의미가 접근성이다

### 퀴즈 5: 먼저 풀어보라

**Q5-1. 이 입력칸의 문제는?**

```html
<input type="email" placeholder="이메일 주소">
```

**Q5-2. 라디오 버튼 3개를 "결제 방법"이라는 그룹으로 묶으려 한다. `<div>` + `<p>결제 방법</p>`로 감쌌다. 스크린리더 사용자에게 무슨 문제가 생기는가?**

**Q5-3. 이메일 입력칸에 `<input type="text">`를 쓰고 있다. `type="email"`로 바꾸면 뭐가 달라지는가?**

---

### 해설 5: 정답과 근거

#### Q5-1 정답

<details>
<summary>정답 보기</summary>

**label이 없다.** placeholder는 힌트이지 레이블이 아니다. 입력을 시작하면 사라지고, 스크린리더는 이 칸의 목적을 모른다.

```html
<!-- 올바름 -->
<label for="email">이메일 주소</label>
<input type="email" id="email" placeholder="example@mail.com">
```

</details>

#### Q5-2 정답

<details>
<summary>정답 보기</summary>

스크린리더가 **그룹을 인식하지 못한다.** "결제 방법"이라는 텍스트와 라디오 버튼들 사이에 의미적 연결이 없다. `fieldset/legend`를 써야 한다:

```html
<fieldset>
  <legend>결제 방법</legend>
  <input type="radio" name="pay" id="card"> <label for="card">카드</label>
  <input type="radio" name="pay" id="bank"> <label for="bank">계좌이체</label>
</fieldset>
```

스크린리더: "결제 방법 그룹, 라디오 버튼 2개"

</details>

#### Q5-3 정답

<details>
<summary>정답 보기</summary>

두 가지가 달라진다:
1. **모바일 키보드**가 @ 포함 키보드로 바뀐다
2. **브라우저가 JS 없이** 이메일 형식을 자동 검증한다

</details>

---

### 해설 5: 상세 설명

#### `label` + `input` vs placeholder만

| | `label` + `input` | placeholder만 |
|---|-------------------|---------------|
| 스크린리더 | "이메일 주소, 입력칸" | 목적을 모름 |
| 클릭 영역 | label 클릭해도 focus | input만 |
| 입력 중 | label은 계속 보임 | placeholder 사라짐 |

#### input type 별 차이

| type | 모바일 키보드 | 브라우저 검증 |
|------|-------------|-------------|
| `text` | 일반 | 없음 |
| `email` | @ 포함 키보드 | 이메일 형식 자동 체크 |
| `url` | / . 포함 키보드 | URL 형식 자동 체크 |
| `tel` | 숫자 키패드 | 없음 (나라마다 형식 다름) |
| `number` | 숫자 키패드 | 범위 체크 (min/max) |
| `date` | 날짜 선택기 | 날짜 형식 체크 |

---

## 그룹 6: 시간과 데이터 — 기계가 읽을 수 있는가

### 퀴즈 6: 먼저 풀어보라

**Q6-1. `<p>발표일: 2017년 6월 12일</p>` — 기계(검색 엔진, 캘린더)가 이 날짜를 자동으로 인식할 수 있는가? 없다면 어떻게 고치는가?**

**Q6-2. 논문 카드에 "cited 187"이라고 표시한다. 사람은 "187회 인용"을 읽지만, 기계가 187이라는 숫자를 파싱하게 하려면?**

**Q6-3. 계산기 앱에서 합계를 `<span>`으로 표시 중이다. 스크린리더 사용자가 값이 바뀔 때 알림을 못 받는다. 어떤 요소로 바꿔야 하는가?**

---

### 해설 6: 정답과 근거

#### Q6-1 정답

<details>
<summary>정답 보기</summary>

**인식할 수 없다.** `time` 요소를 써야 한다:

```html
<p>발표일: <time datetime="2017-06-12">2017년 6월 12일</time></p>
```

사람은 "2017년 6월 12일"을, 기계는 `datetime="2017-06-12"`를 읽는다. "어제", "지난주" 같은 상대 표현도 datetime으로 정확한 값을 줄 수 있다:

```html
<time datetime="2026-03-31">오늘</time>
<time datetime="PT2H30M">2시간 30분</time>  <!-- 기간 -->
```

</details>

#### Q6-2 정답

<details>
<summary>정답 보기</summary>

`data` 요소:

```html
<data value="187">cited 187</data>
```

사람은 "cited 187"을, 기계는 `value="187"`을 읽는다.

</details>

#### Q6-3 정답

<details>
<summary>정답 보기</summary>

`output` 요소:

```html
<output name="total" for="a b">35000</output>
```

- `output`은 스크린리더에게 **live region** — 값이 바뀌면 자동으로 알린다
- `for` 속성으로 어떤 입력에서 나온 결과인지 연결할 수 있다
- `span`은 값이 바뀌어도 스크린리더가 알림을 주지 않는다

</details>

---

## 종합 실전 퀴즈

배경 + 6개 그룹을 모두 학습한 뒤 푸는 종합 문제.

### Q-종합. lighthouse 랜딩 페이지 리팩토링

아래는 g-combined.html의 CTA 영역이다. 시맨틱 요소로 고쳐라.

```html
<div class="cta">
  <a href="#">시작하기</a>
  <div class="note">이메일 하나면 됩니다</div>
</div>
```

<details>
<summary>정답 보기</summary>

```html
<section class="cta">
  <a href="/signup">시작하기</a>
  <p class="note">이메일 하나면 됩니다</p>
</section>
```

**3가지 변경:**
1. `div.cta` → `section` — 의미 있는 콘텐츠 덩어리 (그룹 1)
2. `div.note` → `p` — 설명 문장은 문단 (그룹 1)
3. `href="#"` → 실제 URL — href="#"는 "어디로도 안 감". 실제 목적지가 있어야 `a`가 의미 있다 (그룹 3)

</details>

---

## 체크리스트: CSS 끄기 테스트

모든 그룹의 요소를 제대로 썼으면, CSS를 전부 꺼도:

- [ ] 제목의 크기 위계가 보인다 (h1 > h2 > h3)
- [ ] 글의 덩어리가 구분된다 (article 사이 간격)
- [ ] 순서 목록은 번호가 붙는다 (ol > li)
- [ ] 링크는 파란 밑줄로 보인다
- [ ] 버튼은 클릭 가능한 버튼으로 보인다
- [ ] 폼 입력칸에 레이블이 보인다
- [ ] 취소선은 del/s에 자동 적용
- [ ] details는 접기/펼치기가 작동한다
- [ ] 이미지 아래에 캡션이 붙어 있다

div만으로 쌓은 페이지에서는 위의 어느 것도 자동으로 작동하지 않는다.

---

## 부록 A: React / Next.js는 HTML5 철학을 준수하는가

프레임워크 자체는 금지하지도 강제하지도 않는다. 문제는 사용 문화와 기본 구조에 있다.

### React — 철학과의 긴장

**맞는 곳:** JSX에서 `<article>`, `<section>`, `<nav>` 전부 쓸 수 있다. 개발자가 원하면 완벽한 시맨틱 HTML을 출력할 수 있다.

**어긋나는 곳 3가지:**

**1. 점진적 향상의 근본적 위반 (가장 큰 문제)**

```
HTML5 철학: HTML → CSS → JS (각 층이 실패해도 아래 층은 남는다)
React SPA:  JS → HTML (JS가 실패하면 빈 페이지)
```

```html
<!-- React SPA의 실제 HTML 소스 -->
<body>
  <div id="root"></div>
  <script src="bundle.js"></script>
</body>
```

JS 로드 전에 검색 엔진, 스크린리더, 느린 네트워크 사용자가 보는 것: **빈 페이지**.

**2. div soup 문화**

React가 div를 강제하지는 않지만 생태계가 기울어져 있다:

```jsx
// 흔한 코드
<div className="header">
  <div className="nav">
    <div className="nav-item" onClick={() => navigate('/')}>홈</div>
  </div>
</div>

// HTML5 철학에 맞는 코드 (가능하지만 덜 흔함)
<header>
  <nav>
    <ul><li><a href="/">홈</a></li></ul>
  </nav>
</header>
```

원인: 컴포넌트 추상화가 시맨틱을 가림 (`<Card />`가 div인지 article인지 모름), UI 라이브러리 내부 div 남용, `<div onClick>` 패턴 만연.

**3. 브라우저 기본 동작을 JS로 재구현**

| 브라우저가 공짜로 주는 것 | React 생태계가 하는 것 |
|----------------------|---------------------|
| `<details/summary>` | Accordion 컴포넌트 (JS) |
| `<dialog>` | Modal 컴포넌트 (JS) |
| `<input type="date">` | DatePicker 라이브러리 (JS) |
| `<a href>` 네비게이션 | React Router + onClick |
| `<form>` submit | e.preventDefault() + 커스텀 핸들러 |

### Next.js — 긴장을 상당히 해소한다

React의 가장 큰 문제(빈 페이지)를 고친다:

```
React SPA:  JS → HTML (서버에서 빈 div만 내려옴)
Next.js:    HTML → JS (서버에서 완성된 HTML이 먼저 내려옴)
```

| Next.js 기능 | HTML5 철학과의 관계 |
|-------------|------------------|
| SSR/SSG | 서버에서 HTML 렌더링 → JS 로드 전에도 콘텐츠 보임 |
| Server Components | JS를 클라이언트에 안 보내는 컴포넌트 → HTML-first |
| Streaming | HTML을 점진적으로 보냄 → 부분적으로라도 먼저 보임 |
| `<Link>` | 내부적으로 `<a>` 렌더링 → 시맨틱 유지 |
| `<Image>` | 내부적으로 `<img>` + 최적화 → 시맨틱 유지 |

**그래도 남는 문제:** 개발자가 div를 쓰면 div가 나온다 (자동 변환 없음), hydration 전까지 "보이는데 안 눌리는" 순간 존재, UI 라이브러리 시맨틱 수준에 의존.

### 스펙트럼

```
HTML5 철학에 가까움 ←────────────────────→ 멀어짐

정적 HTML    Next.js       Next.js      React SPA
(순수)       Server        Client       (CSR only)
             Components    Components
             + SSG/SSR     + Hydration
```

**결론:** 프레임워크가 시맨틱을 대신해주지 않는다. 이 교재에서 배운 판단 기준은 React/Next.js에서도 그대로 적용해야 한다.
