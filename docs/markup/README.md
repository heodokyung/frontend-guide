# Markup / CSS Guide (Heo do kyung)

> HTML은 의미 있게, CSS는 예측 가능하게 작성하기 위한 프론트엔드 마크업/CSS 컨벤션입니다.

이 문서는 기존 마크업 가이드의 장점을 유지하되, 현재 프론트엔드 작업에서 더 중요해진 접근성, 시맨틱 HTML, 반응형, 컴포넌트 기반 CSS 기준을 보강한 문서입니다.

---

## 먼저 결론

마크업과 CSS의 핵심은 “같은 화면을 누가 작업해도 비슷한 구조와 예측 가능한 코드가 나오게 하는 것”입니다.

좋은 마크업/CSS는 아래 기준을 만족합니다.

1. HTML은 의미에 맞는 태그를 사용한다.
2. 스타일 제어는 `id`보다 `class`를 기준으로 한다.
3. 클래스 이름은 역할과 구조가 예측 가능해야 한다.
4. CSS는 일정한 선언 순서와 상태 규칙을 가진다.
5. 접근성은 나중에 추가하는 것이 아니라 처음부터 함께 작성한다.
6. 불필요한 래퍼와 깊은 중첩을 줄인다.

---

## 기본 환경 규칙

| 항목 | 기준 |
|---|---|
| 인코딩 | UTF-8 |
| 들여쓰기 | 공백 2칸 |
| 줄 끝 공백 | 저장 시 제거 |
| 파일명 | 소문자와 하이픈 권장 |
| HTML 속성 값 | 큰따옴표 사용 |
| CSS 단위 | 0에는 단위 생략 가능 |

```html
<!-- Good -->
<button class="button" type="button">저장</button>
```

```css
/* Good */
.button {
  margin: 0;
  padding: 12px 16px;
}
```

---

## HTML 기본 구조

```html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>페이지 제목</title>
  </head>
  <body>
    <main>
      <h1>페이지 제목</h1>
    </main>
  </body>
</html>
```

### 현대 기준으로 정리한 점

과거에는 `X-UA-Compatible`, `maximum-scale`, `user-scalable=no` 같은 속성을 자주 넣었습니다. 현재 일반적인 신규 프로젝트에서는 아래 기준을 권장합니다.

- `<!DOCTYPE html>`을 사용합니다.
- `html`에는 실제 문서 언어에 맞는 `lang`을 넣습니다.
- `viewport`는 기본적으로 `width=device-width, initial-scale=1`을 사용합니다.
- 사용자의 확대를 막는 `user-scalable=no`, `maximum-scale=1`은 접근성 측면에서 신중히 사용합니다.
- IE 전용 `X-UA-Compatible`은 레거시 지원이 필요한 프로젝트가 아니라면 생략합니다.

---

## 시맨틱 HTML

HTML 태그는 모양이 아니라 의미로 선택합니다.

| 목적 | 권장 태그 |
|---|---|
| 페이지의 핵심 콘텐츠 | `main` |
| 독립적인 콘텐츠 묶음 | `section`, `article` |
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

---

## 접근성 기본 규칙

접근성은 특별한 사용자를 위한 추가 기능이 아니라, 더 견고한 UI를 만드는 기본 조건입니다.

### 반드시 지킬 것

- 이미지에는 의미 있는 `alt`를 작성합니다.
- 장식 이미지는 빈 `alt=""`를 사용합니다.
- 폼 입력에는 `label`을 연결합니다.
- 버튼은 `button` 요소를 사용합니다.
- 링크는 이동 목적이 있을 때 사용합니다.
- 키보드로 조작할 수 있어야 합니다.
- 색상만으로 상태를 전달하지 않습니다.
- 모달, 탭, 아코디언처럼 동적 UI는 `aria-*`를 신중히 사용합니다.

```html
<!-- Good -->
<label class="form-label" for="user-email">이메일</label>
<input class="form-input" id="user-email" type="email" name="email">
```

```html
<!-- 장식 이미지 -->
<img src="/decorative-line.svg" alt="">

<!-- 의미 있는 이미지 -->
<img src="/profile.jpg" alt="허도경 프로필 사진">
```

### ARIA 사용 기준

ARIA는 의미 없는 태그를 억지로 의미 있게 만들기 위한 만능 도구가 아닙니다. 가능한 한 먼저 올바른 HTML 태그를 사용합니다.

```html
<!-- Bad -->
<div role="button" tabindex="0">저장</div>

<!-- Good -->
<button type="button">저장</button>
```

---

## ID / Class 규칙

### 원칙

- 스타일 제어는 `class`를 기준으로 합니다.
- `id`는 CSS 선택자로 사용하지 않습니다.
- `id`는 `label for`, 앵커 이동, ARIA 연결처럼 고유 식별이 필요한 경우에만 사용합니다.

```html
<!-- Bad -->
<div id="header"></div>

<!-- Good -->
<header class="site-header"></header>
```

---

## 클래스 네이밍

이 저장소에서는 BEM을 기본 기준으로 삼습니다.

```txt
block
block__element
block--modifier
is-state
```

```html
<article class="profile-card profile-card--featured">
  <img class="profile-card__image" src="..." alt="...">
  <div class="profile-card__body">
    <h2 class="profile-card__title">도경</h2>
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

### 상태 클래스

상태는 `is-`, `has-` 접두사를 사용합니다.

```css
.is-active {}
.is-disabled {}
.is-loading {}
.is-expanded {}
.has-error {}
.has-value {}
```

---

## 속성 작성 순서

HTML 속성은 아래 순서를 권장합니다.

1. `class`
2. `id`
3. `type`, `name`, `value`, `href`, `src`
4. `data-*`
5. `aria-*`, `role`
6. `title`, `alt`
7. `style`는 예외 상황에서만 마지막에 사용

```html
<input
  class="form-input"
  id="user-name"
  type="text"
  name="userName"
  aria-describedby="user-name-help"
>
```

단, 팀 컨벤션이나 프레임워크 자동 포매터가 있다면 그 기준을 우선합니다.

---

## Boolean 속성

HTML의 Boolean 속성은 값 없이 작성할 수 있습니다.

```html
<input type="checkbox" checked>
<button type="button" disabled>저장</button>
```

Vue/React 같은 프레임워크에서는 바인딩 문법과 충돌하지 않도록 프로젝트 규칙을 따릅니다.

---

## 이미지 규칙

이미지는 콘텐츠인지 장식인지 먼저 판단합니다.

```html
<!-- 콘텐츠 이미지 -->
<img class="product-card__image" src="/product.jpg" alt="검은색 가죽 지갑">

<!-- 장식 이미지 -->
<img class="section-line" src="/line.svg" alt="">
```

권장:

- `alt`는 파일명이 아니라 이미지의 의미를 적습니다.
- lazy loading이 필요한 경우 `loading="lazy"`를 고려합니다.
- 레이아웃 밀림을 줄이기 위해 가능하면 `width`, `height`를 지정합니다.

---

## 폼 규칙

폼은 접근성과 사용성 문제가 가장 많이 생기는 영역입니다.

```html
<div class="form-field">
  <label class="form-field__label" for="password">비밀번호</label>
  <input class="form-field__input" id="password" type="password" name="password" autocomplete="current-password">
  <p class="form-field__help" id="password-help">8자 이상 입력하세요.</p>
</div>
```

권장:

- `label`과 `input`을 연결합니다.
- 입력 목적에 맞는 `type`을 사용합니다.
- `autocomplete`를 적절히 사용합니다.
- 에러 메시지는 입력 필드와 연결합니다.
- placeholder를 label 대체로 사용하지 않습니다.

---

## 테이블 규칙

표 형태의 데이터에는 `table`을 사용합니다. 레이아웃을 만들기 위해 `table`을 사용하지 않습니다.

```html
<table class="data-table">
  <caption>월별 매출 현황</caption>
  <thead>
    <tr>
      <th scope="col">월</th>
      <th scope="col">매출</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">1월</th>
      <td>1,000,000원</td>
    </tr>
  </tbody>
</table>
```

---

## CSS 기본 문법

```css
.card {
  display: block;
  width: 100%;
  padding: 16px;
  border-radius: 12px;
  background-color: #fff;
}
```

권장:

- 선택자와 중괄호 사이에 공백을 둡니다.
- 선언 뒤에는 세미콜론을 붙입니다.
- 색상, 간격, 폰트는 가능하면 토큰화합니다.
- `!important`는 예외 상황에서만 사용합니다.

---

## CSS 선언 순서

속성 순서는 팀마다 다를 수 있지만, 한 프로젝트 안에서는 반드시 일관되어야 합니다.

이 저장소에서는 아래 순서를 권장합니다.

1. 표시/흐름: `display`, `visibility`, `overflow`
2. 위치: `position`, `top`, `right`, `bottom`, `left`, `z-index`
3. 박스 모델: `width`, `height`, `margin`, `padding`, `border`
4. 레이아웃: `flex`, `grid`, `gap`, `align-*`, `justify-*`
5. 타이포그래피: `font`, `line-height`, `letter-spacing`, `text-*`
6. 배경/색상: `color`, `background`, `box-shadow`
7. 변형/애니메이션: `transform`, `transition`, `animation`
8. 기타: `cursor`, `pointer-events`, `user-select`

```css
.card {
  display: flex;
  position: relative;
  width: 100%;
  min-height: 120px;
  margin: 0;
  padding: 20px;
  align-items: center;
  justify-content: space-between;
  font-size: 16px;
  line-height: 1.5;
  color: #222;
  background-color: #fff;
  border-radius: 16px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.08);
  transition: transform 0.2s ease;
  cursor: pointer;
}
```

---

## 선택자 규칙

### 권장

```css
.card {}
.card__title {}
.card__button {}
.card.is-active {}
```

### 피해야 할 것

```css
/* 너무 구체적 */
body .wrap .container .card .title {}

/* id 선택자에 스타일 의존 */
#cardTitle {}

/* 태그 구조에 과도하게 의존 */
ul li div span {}
```

선택자가 깊어질수록 수정이 어려워지고, 덮어쓰기를 위해 더 강한 선택자를 만들게 됩니다.

---

## 컴포넌트 CSS 규칙

컴포넌트는 외부 환경에 덜 의존해야 합니다.

```html
<article class="product-card">
  <img class="product-card__image" src="..." alt="...">
  <div class="product-card__content">
    <h2 class="product-card__title">상품명</h2>
    <p class="product-card__price">10,000원</p>
  </div>
</article>
```

```css
.product-card {}
.product-card__image {}
.product-card__content {}
.product-card__title {}
.product-card__price {}
```

권장:

- 컴포넌트 루트 클래스가 있어야 합니다.
- 내부 요소는 루트 클래스 기준으로 이름을 짓습니다.
- 다른 컴포넌트의 내부 클래스에 직접 의존하지 않습니다.
- 페이지별 예외는 modifier 또는 별도 wrapper에서 처리합니다.

---

## 반응형 규칙

모바일 우선 또는 데스크톱 우선 중 하나를 정하고 일관되게 사용합니다. 신규 프로젝트는 모바일 우선을 권장합니다.

```css
.product-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 16px;
}

@media (min-width: 768px) {
  .product-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .product-grid {
    grid-template-columns: repeat(4, 1fr);
  }
}
```

권장:

- 브레이크포인트는 프로젝트 토큰으로 관리합니다.
- 컴포넌트와 가까운 위치에 관련 미디어 쿼리를 둡니다.
- 뷰포트 기준만으로 해결하기 어렵다면 컨테이너 쿼리도 검토합니다.

---

## 주석 규칙

주석은 “무엇을 하는지”보다 “왜 이렇게 했는지”를 설명합니다.

```css
/* Bad: 버튼 색상 */
.button {
  color: #fff;
}

/* Good: 브랜드 캠페인 기간 동안 CTA 대비를 높이기 위한 예외 색상 */
.button--campaign {
  color: #fff;
}
```

권장:

- 임시 코드는 날짜와 제거 조건을 남깁니다.
- 브라우저 버그 대응, 레거시 대응은 이유를 적습니다.
- 누구나 코드만 보고 알 수 있는 내용은 주석으로 반복하지 않습니다.

---

## 인라인 스타일 사용 기준

기존 가이드에는 너비가 유동적인 입력 필드에 인라인 스타일을 사용할 수 있다고 되어 있었지만, 최신 기준에서는 더 신중히 사용하는 편이 좋습니다.

인라인 스타일은 아래 경우에만 예외적으로 허용합니다.

- 서버/사용자 입력값 기반으로 동적으로 계산되는 값
- 컴포넌트 props로 전달되는 CSS 변수
- 이메일 템플릿처럼 인라인 스타일이 필요한 환경

```html
<!-- Prefer -->
<input class="form-input form-input--sm" type="text">
<input class="form-input form-input--md" type="text">

<!-- Exception -->
<div class="progress" style="--progress-value: 72%"></div>
```

---

## 마크업/CSS 체크리스트

- [ ] `html`에 올바른 `lang`이 있다.
- [ ] 페이지에 의미 있는 `h1`이 있다.
- [ ] 클릭 동작은 `button`, 이동은 `a`를 사용했다.
- [ ] 이미지 `alt`가 의미에 맞게 작성되어 있다.
- [ ] 폼 입력에 `label`이 연결되어 있다.
- [ ] 스타일은 `id`가 아니라 `class` 기준이다.
- [ ] 클래스 이름이 BEM 또는 프로젝트 규칙에 맞다.
- [ ] 선택자가 불필요하게 깊지 않다.
- [ ] 상태 클래스가 예측 가능하다.
- [ ] 모바일/PC 반응형 기준이 일관되어 있다.
- [ ] `!important`가 남용되지 않았다.
- [ ] 인라인 스타일은 예외 상황에서만 사용했다.

---

## 참고 자료

- Google HTML/CSS Style Guide: https://google.github.io/styleguide/htmlcssguide
- MDN - HTML accessibility: https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Accessibility/HTML
- MDN - CSS media queries: https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_media_queries
- Code Guide by @mdo: https://codeguide.co/
