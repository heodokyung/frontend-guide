# Markup / CSS Guide

> 제가 HTML과 CSS를 작성할 때 흔들리지 않기 위해 정리한 컨벤션입니다.

마크업은 화면의 뼈대이고, CSS는 그 뼈대에 질서를 붙이는 방식입니다.

화면이 예쁘게 보이는 것도 중요하지만, 구조가 흐트러지면 수정할 때마다 비용이 커집니다. 이 문서는 HTML과 CSS를 작성할 때 제가 기본값으로 삼는 기준을 정리한 것입니다.

---

## 목차

- [기본 원칙](#기본-원칙)
- [파일과 작성 환경](#파일과-작성-환경)
- [HTML 기본 구조](#html-기본-구조)
- [시맨틱 HTML](#시맨틱-html)
- [접근성 기본](#접근성-기본)
- [ID와 Class 사용 기준](#id와-class-사용-기준)
- [클래스 네이밍](#클래스-네이밍)
- [CSS 작성 순서](#css-작성-순서)
- [반응형 작성 기준](#반응형-작성-기준)
- [상태와 컴포넌트 스타일](#상태와-컴포넌트-스타일)
- [금지하거나 줄일 패턴](#금지하거나-줄일-패턴)
- [마크업 리뷰 체크리스트](#마크업-리뷰-체크리스트)

---

## 기본 원칙

마크업과 CSS는 화려하게 쓰는 것보다, 다음 사람이 같은 흐름으로 이어갈 수 있게 쓰는 것이 중요합니다.

1. HTML은 모양이 아니라 의미로 선택합니다.
2. CSS는 예측 가능한 순서로 씁니다.
3. 스타일 제어는 `id`보다 `class`를 기준으로 합니다.
4. 접근성은 마지막 점검 항목이 아니라 작성 단계의 기본값입니다.
5. 불필요한 래퍼와 깊은 중첩을 줄입니다.
6. 컴포넌트 단위로 재사용 가능한 이름을 붙입니다.
7. 수정 범위가 넓어지는 전역 스타일은 조심스럽게 다룹니다.

---

## 파일과 작성 환경

| 항목 | 기준 |
|---|---|
| 인코딩 | UTF-8 |
| 들여쓰기 | 공백 2칸 |
| 파일명 | 소문자와 하이픈 사용: `profile-card.html` |
| HTML 속성 값 | 큰따옴표 사용 |
| CSS 단위 | `0`에는 단위 생략 |
| 색상 | 가능하면 디자인 토큰 또는 CSS 변수 사용 |
| 주석 | 왜 필요한지 설명할 때만 사용 |

```html
<button class="button" type="button">저장</button>
```

```css
.button {
  margin: 0;
  padding: 12px 16px;
}
```

---

## HTML 기본 구조

신규 페이지의 기본 구조는 단순하게 시작합니다.

```html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>페이지 제목</title>
  </head>
  <body>
    <header class="site-header"></header>

    <main class="site-main">
      <h1>페이지 제목</h1>
    </main>

    <footer class="site-footer"></footer>
  </body>
</html>
```

권장 기준은 다음과 같습니다.

- `<!DOCTYPE html>`을 사용합니다.
- `html`에는 실제 문서 언어에 맞는 `lang`을 넣습니다.
- `viewport`는 기본적으로 `width=device-width, initial-scale=1`을 사용합니다.
- 사용자의 확대를 막는 `user-scalable=no`, `maximum-scale=1`은 피합니다.
- IE 전용 `X-UA-Compatible`은 레거시 프로젝트가 아니라면 생략합니다.

---

## 시맨틱 HTML

태그는 “어떻게 보이는가”가 아니라 “무슨 역할인가”로 선택합니다.

| 목적 | 권장 태그 |
|---|---|
| 페이지의 핵심 콘텐츠 | `main` |
| 독립적인 콘텐츠 | `article` |
| 주제별 구역 | `section` |
| 보조 정보 | `aside` |
| 상단 영역 | `header` |
| 하단 영역 | `footer` |
| 내비게이션 | `nav` |
| 클릭 동작 | `button` |
| 페이지 이동 | `a` |
| 목록 | `ul`, `ol`, `li` |

```html
<!-- Bad -->
<div class="button" onclick="save()">저장</div>

<!-- Good -->
<button class="button" type="button">저장</button>
```

```html
<!-- Bad -->
<div class="list">
  <div class="item">공지 1</div>
  <div class="item">공지 2</div>
</div>

<!-- Good -->
<ul class="notice-list">
  <li class="notice-list__item">공지 1</li>
  <li class="notice-list__item">공지 2</li>
</ul>
```

제목은 시각 크기가 아니라 문서 구조입니다.

```html
<main>
  <h1>포트폴리오</h1>

  <section aria-labelledby="project-title">
    <h2 id="project-title">대표 프로젝트</h2>
  </section>
</main>
```

---

## 접근성 기본

접근성은 따로 붙이는 기능이 아닙니다. 제대로 된 HTML을 쓰는 순간 절반은 해결됩니다.

반드시 지킬 기준은 다음과 같습니다.

- 이미지에는 의미 있는 `alt`를 작성합니다.
- 장식 이미지는 `alt=""`로 둡니다.
- 폼 입력에는 `label`을 연결합니다.
- 클릭 동작은 `button`, 이동은 `a`를 사용합니다.
- 키보드만으로 모든 기능을 사용할 수 있어야 합니다.
- 포커스가 보이지 않으면 안 됩니다.
- 색상만으로 상태를 전달하지 않습니다.
- 모달, 탭, 아코디언은 열림/선택 상태를 보조기술에 전달해야 합니다.

```html
<label class="form-label" for="user-email">이메일</label>
<input class="form-input" id="user-email" type="email" name="email" autocomplete="email">
```

```html
<img src="/line.svg" alt="">
<img src="/profile.jpg" alt="허도경 프로필 사진">
```

ARIA는 먼저 쓰는 것이 아니라, 네이티브 HTML만으로 부족할 때 보완하는 도구입니다.

```html
<!-- Bad -->
<div role="button" tabindex="0">저장</div>

<!-- Good -->
<button type="button">저장</button>
```

접근성의 세부 기준은 [웹 접근성 가이드](../accessibility/README.md)에서 따로 관리합니다.

---

## ID와 Class 사용 기준

`id`와 `class`의 역할을 섞지 않습니다.

| 구분 | 사용 목적 |
|---|---|
| `id` | 문서 안에서 유일해야 하는 연결 지점 |
| `class` | 스타일, 상태, 컴포넌트 구조 |

`id`는 아래 경우에 사용합니다.

- `label`과 입력 요소 연결
- `aria-labelledby`, `aria-describedby` 연결
- 앵커 이동
- 특정 스크립트 연결 지점

CSS 선택자로는 가능하면 `id`를 쓰지 않습니다.

```html
<!-- Bad -->
<div id="header"></div>

<!-- Good -->
<header class="site-header"></header>
```

---

## 클래스 네이밍

기본은 BEM을 사용합니다.

```txt
block
block__element
block--modifier
is-state
has-state
```

```html
<article class="profile-card profile-card--featured">
  <img class="profile-card__image" src="..." alt="...">
  <div class="profile-card__body">
    <h2 class="profile-card__title">Heo Do Kyung</h2>
  </div>
</article>
```

```css
.profile-card {}
.profile-card__image {}
.profile-card__body {}
.profile-card__title {}
.profile-card--featured {}
.profile-card.is-active {}
```

상태 클래스는 의미가 보이도록 작성합니다.

```css
.is-active {}
.is-disabled {}
.is-loading {}
.is-expanded {}
.has-error {}
.has-value {}
```

자바스크립트 연결이 필요한 클래스는 스타일 클래스와 분리합니다.

```html
<button class="button js-submit-button" type="button">저장</button>
```

```css
.button {}
/* .js-submit-button에는 스타일을 주지 않습니다. */
```

---

## CSS 작성 순서

CSS 속성 순서는 팀마다 다를 수 있습니다. 이 저장소에서는 “레이아웃에서 장식으로” 내려가는 방식을 기본으로 합니다.

1. 생성/표시: `content`, `box-sizing`, `display`
2. 위치: `position`, `inset`, `top`, `right`, `bottom`, `left`, `z-index`
3. Flex/Grid: `flex`, `grid`, `justify-content`, `align-items`, `gap`
4. 크기: `width`, `height`, `min-*`, `max-*`, `aspect-ratio`
5. 여백: `margin`, `padding`
6. 테두리: `border`, `border-radius`, `outline`
7. 배경: `background`, `background-color`, `background-image`
8. 글자: `color`, `font`, `line-height`, `text-align`, `white-space`
9. 넘침/시각 효과: `overflow`, `opacity`, `box-shadow`, `filter`
10. 움직임/상호작용: `transform`, `transition`, `animation`, `cursor`, `user-select`

```css
.card {
  display: flex;
  align-items: center;
  gap: 12px;
  width: 100%;
  padding: 16px;
  border: 1px solid var(--color-border);
  border-radius: 12px;
  background: var(--color-surface);
  color: var(--color-text);
  font-size: 14px;
  line-height: 1.5;
  box-shadow: var(--shadow-sm);
}
```

단축 속성과 개별 속성을 함께 쓸 때는 순서에 따라 결과가 달라질 수 있습니다. 자동 정렬 도구를 사용할 때도 이 부분은 반드시 확인합니다.

```css
/* 의도: 전체 margin을 0으로 초기화한 뒤 위쪽만 12px */
.box {
  margin: 0;
  margin-top: 12px;
}
```

---

## 반응형 작성 기준

반응형은 “모바일을 억지로 줄이는 작업”이 아닙니다. 작은 화면에서 먼저 읽히게 만들고, 큰 화면에서 여유를 더하는 방식이 안전합니다.

```css
.product-grid {
  display: grid;
  gap: 16px;
}

@media (min-width: 768px) {
  .product-grid {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}

@media (min-width: 1024px) {
  .product-grid {
    grid-template-columns: repeat(3, minmax(0, 1fr));
  }
}
```

권장 기준:

- 모바일 기본 스타일을 먼저 작성합니다.
- `min-width` 기반으로 확장합니다.
- 터치 영역은 충분히 확보합니다.
- 텍스트가 줄어들 때 깨지지 않는지 확인합니다.
- 모션은 `prefers-reduced-motion`을 고려합니다.

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    scroll-behavior: auto !important;
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## 상태와 컴포넌트 스타일

상태는 클래스 이름만 봐도 의미가 보이게 작성합니다.

```html
<button class="button is-loading" type="button" disabled>
  저장 중
</button>
```

```css
.button {}
.button:hover {}
.button:focus-visible {}
.button:disabled,
.button.is-disabled {}
.button.is-loading {}
```

컴포넌트 스타일은 가능한 한 컴포넌트 안에서 닫히게 작성합니다.

```css
.modal {}
.modal__header {}
.modal__body {}
.modal__footer {}
.modal--fullscreen {}
.modal.is-open {}
```

전역 유틸리티는 적게, 명확하게 둡니다.

```css
.sr-only {}
.text-muted {}
.hide-mobile {}
```

---

## 금지하거나 줄일 패턴

아래 패턴은 당장 편해 보이지만, 프로젝트가 커질수록 수정 비용을 키웁니다.

```css
/* 너무 강한 선택자 */
#app .page .section .card .title {}

/* 의미가 흐린 이름 */
.box {}
.wrap {}
.item {}

/* 불필요한 !important */
.button {
  color: red !important;
}
```

줄여야 할 것:

- 과한 중첩 선택자
- 의미 없는 `div` 래퍼
- 전역에 뿌려진 `!important`
- 스타일 목적의 `id` 선택자
- 색상, 크기, 여백의 하드코딩 남발
- 접근성을 무시한 커스텀 버튼/셀렉트

---

## 마크업 리뷰 체크리스트

- [ ] 페이지에 `h1`이 있고 제목 구조가 자연스러운가?
- [ ] 클릭은 `button`, 이동은 `a`로 구분했는가?
- [ ] 이미지의 `alt`가 의미에 맞는가?
- [ ] 폼 입력에 `label`이 연결되어 있는가?
- [ ] 키보드만으로 사용할 수 있는가?
- [ ] 포커스가 시각적으로 보이는가?
- [ ] 색상만으로 상태를 전달하지 않는가?
- [ ] 클래스 이름만 봐도 컴포넌트와 역할이 보이는가?
- [ ] CSS 속성 순서가 일정한가?
- [ ] 모바일, 태블릿, PC에서 레이아웃이 자연스러운가?

---

## 참고

- Google HTML/CSS Style Guide
- MDN Web Docs: HTML, CSS, Accessibility
- Code Guide by @mdo
- W3C WCAG 2.2
- KWCAG 2.2
