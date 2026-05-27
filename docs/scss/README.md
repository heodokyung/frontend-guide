# SCSS 제대로 사용하기

## 들어가며

CSS는 웹 화면의 모양을 만드는 가장 기본적인 언어입니다.
하지만 프로젝트가 커지면 단순 CSS만으로는 다음과 같은 문제가 생깁니다.

* 같은 색상, 여백, 폰트 크기를 여러 곳에 반복해서 작성하게 된다.
* 버튼, 카드, 모달 같은 UI 패턴이 많아질수록 코드가 길어진다.
* 반응형, 다크모드, 상태별 스타일을 관리하기 어려워진다.
* 파일이 커지면 “어디에 어떤 스타일이 있는지” 찾기 힘들어진다.
* 작은 수정이 다른 화면에 예상치 못한 영향을 줄 수 있다.

SCSS는 이런 문제를 줄이기 위해 사용하는 **CSS 확장 문법**입니다.
Sass 공식 문서에서도 Sass를 “CSS로 컴파일되는 스타일시트 언어”라고 설명하며, 변수, 중첩, 믹스인, 함수 등을 통해 큰 스타일시트를 더 잘 정리할 수 있다고 설명합니다. ([Sass][1])

---

# 1. SCSS와 Sass의 차이점

## 1-1. 가장 먼저 정리해야 할 개념

많은 사람이 `Sass`와 `SCSS`를 혼동합니다.
정확히 말하면 다음과 같습니다.

```text
Sass = 스타일시트 언어 전체의 이름
SCSS = Sass를 작성하는 문법 방식 중 하나
.sass = 들여쓰기 기반의 오래된 Sass 문법
.scss = CSS와 거의 같은 형태로 작성하는 Sass 문법
```

즉, **SCSS는 Sass의 한 문법 형식**입니다.
Sass에는 크게 두 가지 문법이 있습니다.

| 구분           | 확장자     | 특징                                    |
| ------------ | ------- | ------------------------------------- |
| SCSS 문법      | `.scss` | CSS와 거의 동일한 문법. 중괄호 `{}`와 세미콜론 `;` 사용 |
| Sass 들여쓰기 문법 | `.sass` | 중괄호와 세미콜론 없이 들여쓰기로 구조 표현              |

Sass 공식 문서에 따르면 `.sass` 문법은 Sass의 원래 문법이며, 들여쓰기를 사용하고 중괄호와 세미콜론을 쓰지 않습니다. 반면 `.scss`는 CSS와 유사한 문법을 사용합니다. ([Sass][2])

---

## 1-2. SCSS 예시

```scss
.card {
  padding: 20px;
  border-radius: 12px;

  .card-title {
    font-size: 20px;
    font-weight: 700;
  }
}
```

SCSS는 CSS처럼 `{}`와 `;`를 사용합니다.
그래서 기존 CSS를 알고 있다면 비교적 쉽게 배울 수 있습니다.

---

## 1-3. Sass 들여쓰기 문법 예시

```sass
.card
  padding: 20px
  border-radius: 12px

  .card-title
    font-size: 20px
    font-weight: 700
```

`.sass` 문법은 짧고 간결하지만, 들여쓰기에 매우 민감합니다.
팀 프로젝트나 초보자 학습용으로는 보통 `.scss`가 더 직관적입니다.

---

## 1-4. 실무에서는 무엇을 쓰는 게 좋을까?

대부분의 프론트엔드 프로젝트에서는 **SCSS 문법을 추천**합니다.

이유는 단순합니다.

```text
CSS와 생김새가 거의 같다.
기존 CSS 코드를 옮기기 쉽다.
초보자가 이해하기 쉽다.
Vue, React, Vite, Webpack 등과 함께 쓰기 쉽다.
팀원 간 코드 리뷰가 편하다.
```

따라서 이 문서에서는 `.scss` 기준으로 설명합니다.

---

# 2. SCSS에서 기본적으로 알아야 하는 문법

## 2-1. 변수

SCSS에서 변수는 `$` 기호로 선언합니다.

```scss
$primary-color: #256f8f;
$text-color: #222;
$border-radius: 12px;
$spacing-md: 16px;

.button {
  color: #fff;
  background-color: $primary-color;
  border-radius: $border-radius;
  padding: $spacing-md;
}
```

CSS로 컴파일되면 변수는 실제 값으로 바뀝니다.

```css
.button {
  color: #fff;
  background-color: #256f8f;
  border-radius: 12px;
  padding: 16px;
}
```

SCSS 변수는 반복되는 값을 관리할 때 유용합니다.

예를 들어 프로젝트 전체에서 사용하는 대표 색상이 있다고 가정해 봅니다.

```scss
$brand-color: #256f8f;
```

이 색상을 버튼, 링크, 배지, 탭 메뉴에 모두 사용하고 있다면, 나중에 브랜드 색상을 바꿀 때 변수 하나만 수정하면 됩니다.

---

## 2-2. 변수 이름 짓기

좋은 변수 이름은 “값”보다 “역할”을 설명해야 합니다.

나쁜 예시입니다.

```scss
$blue: #256f8f;
$red: #e03131;
$big-size: 32px;
```

좋은 예시입니다.

```scss
$color-primary: #256f8f;
$color-danger: #e03131;
$font-size-title: 32px;
```

더 좋은 예시입니다.

```scss
$color-brand-primary: #256f8f;
$color-text-main: #222;
$color-text-muted: #777;
$color-border-default: #ddd;
$radius-card: 16px;
$radius-button: 10px;
```

색상 이름을 단순히 `$blue`라고 지으면, 나중에 브랜드 컬러가 초록색으로 바뀌었을 때 이름과 값이 맞지 않게 됩니다.
그래서 실무에서는 색상 그 자체보다 **용도 중심 이름**을 추천합니다.

---

## 2-3. 중첩

SCSS의 대표 기능 중 하나가 중첩입니다.

일반 CSS에서는 이렇게 작성합니다.

```css
.card {
  padding: 20px;
}

.card .card-title {
  font-size: 20px;
}

.card .card-description {
  color: #666;
}
```

SCSS에서는 이렇게 작성할 수 있습니다.

```scss
.card {
  padding: 20px;

  .card-title {
    font-size: 20px;
  }

  .card-description {
    color: #666;
  }
}
```

이렇게 하면 `.card` 안에 있는 요소라는 구조가 더 잘 보입니다.

하지만 중첩은 너무 많이 사용하면 오히려 문제가 됩니다.

---

## 2-4. 나쁜 중첩 예시

```scss
.page {
  .section {
    .container {
      .card {
        .header {
          .title {
            span {
              color: red;
            }
          }
        }
      }
    }
  }
}
```

이 코드는 CSS로 컴파일되면 다음처럼 매우 긴 선택자가 됩니다.

```css
.page .section .container .card .header .title span {
  color: red;
}
```

이런 코드는 다음 문제가 생깁니다.

```text
선택자 우선순위가 불필요하게 높아진다.
재사용하기 어렵다.
다른 곳에서 덮어쓰기 힘들다.
HTML 구조가 조금만 바뀌어도 스타일이 깨진다.
```

---

## 2-5. 좋은 중첩 기준

실무에서는 보통 **2단계에서 3단계 정도까지만 중첩**하는 것이 좋습니다.

좋은 예시입니다.

```scss
.card {
  padding: 20px;
  border-radius: 16px;

  &__title {
    font-size: 20px;
    font-weight: 700;
  }

  &__description {
    margin-top: 8px;
    color: #666;
  }
}
```

여기서 `&`는 현재 부모 선택자를 의미합니다.

```scss
.card {
  &__title {
    font-size: 20px;
  }
}
```

위 코드는 다음 CSS로 컴파일됩니다.

```css
.card__title {
  font-size: 20px;
}
```

---

## 2-6. `&` 선택자

`&`는 SCSS에서 매우 자주 사용됩니다.
현재 선택자 자신을 가리킵니다.

```scss
.button {
  background-color: #256f8f;

  &:hover {
    background-color: #1d5a75;
  }

  &:disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }

  &.is-active {
    border: 2px solid #256f8f;
  }
}
```

컴파일 결과는 다음과 같습니다.

```css
.button {
  background-color: #256f8f;
}

.button:hover {
  background-color: #1d5a75;
}

.button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.button.is-active {
  border: 2px solid #256f8f;
}
```

`&`는 BEM 방식과도 잘 어울립니다.

```scss
.modal {
  &__header {}
  &__body {}
  &__footer {}

  &--small {}
  &--large {}

  &.is-open {}
}
```

---

## 2-7. 주석

SCSS에서는 두 가지 주석을 사용할 수 있습니다.

```scss
// 한 줄 주석
// 컴파일된 CSS에는 남지 않습니다.

/*
  여러 줄 주석
  일반적으로 컴파일된 CSS에 남을 수 있습니다.
*/
```

실무에서는 보통 설명용 주석은 `//`를 많이 사용합니다.

```scss
// 카드 내부 여백은 모바일 기준을 먼저 잡는다.
.card {
  padding: 16px;
}
```

라이브러리나 공통 믹스인을 문서화할 때는 여러 줄 주석을 사용할 수 있습니다. Sass 공식 문서는 SassDoc 같은 도구가 변수, 믹스인, 함수 등을 문서화하기 위해 주석을 활용할 수 있다고 설명합니다. ([Sass][3])

---

## 2-8. 파일 분리와 partial

SCSS는 파일을 여러 개로 나눠 관리할 수 있습니다.

보통 공통 변수, 믹스인, 기본 스타일, 컴포넌트 스타일을 나눕니다.

```text
styles/
  abstracts/
    _variables.scss
    _mixins.scss
    _functions.scss
  base/
    _reset.scss
    _typography.scss
  components/
    _button.scss
    _card.scss
    _modal.scss
  pages/
    _home.scss
    _login.scss
  main.scss
```

파일명 앞에 `_`가 붙은 SCSS 파일을 보통 **partial**이라고 부릅니다.

```text
_variables.scss
_mixins.scss
_button.scss
```

partial 파일은 단독으로 CSS 파일을 만들기 위한 파일이 아니라, 다른 SCSS 파일에서 불러와 사용하기 위한 조각 파일입니다.

---

## 2-9. `@use`

과거에는 SCSS 파일을 불러올 때 `@import`를 많이 사용했습니다.

```scss
@import 'variables';
@import 'mixins';
@import 'button';
```

하지만 현재 Sass에서는 `@use`와 `@forward`를 사용하는 방식이 권장됩니다. 공식 문서에 따르면 `@use`는 다른 Sass 스타일시트의 변수, 믹스인, 함수를 로드하고 CSS를 함께 결합합니다. ([Sass][4])

예시입니다.

```scss
@use './variables';

.button {
  background-color: variables.$color-primary;
}
```

`@use`를 사용하면 불러온 파일의 변수나 믹스인을 네임스페이스를 통해 접근합니다.

```scss
variables.$color-primary
```

이 방식은 코드가 조금 길어 보일 수 있지만, 장점이 있습니다.

```text
이 변수가 어디에서 왔는지 알기 쉽다.
다른 파일의 변수명과 충돌할 가능성이 줄어든다.
프로젝트 규모가 커져도 관리하기 쉽다.
```

---

## 2-10. `@import`는 왜 피해야 할까?

Sass 공식 문서에 따르면 `@import`는 전역 네임스페이스 문제, 중복 로드, 변수와 믹스인의 출처 파악 어려움 등의 문제가 있어 deprecated 상태입니다. Dart Sass 1.80.0부터 Sass `@import`와 전역 내장 함수 사용 시 deprecation warning이 발생합니다. ([Sass][5])

즉, 새 프로젝트에서는 다음 방식보다

```scss
@import 'variables';
```

다음 방식을 추천합니다.

```scss
@use './variables';
```

---

## 2-11. `@forward`

`@forward`는 여러 SCSS 파일을 하나의 진입점으로 모아줄 때 사용합니다. Sass 공식 문서에 따르면 `@forward`는 Sass 파일의 변수, 믹스인, 함수를 다른 파일에서 `@use`로 사용할 수 있도록 전달하는 역할을 합니다. ([Sass][6])

예를 들어 다음과 같은 구조가 있다고 가정합니다.

```text
styles/
  abstracts/
    _colors.scss
    _spacing.scss
    _mixins.scss
    _index.scss
```

`_index.scss`에서 여러 파일을 모읍니다.

```scss
@forward './colors';
@forward './spacing';
@forward './mixins';
```

그리고 실제 사용하는 파일에서는 하나만 불러옵니다.

```scss
@use '@/styles/abstracts' as *;

.button {
  padding: $spacing-md;
  background-color: $color-primary;
}
```

다만 `as *`는 모든 변수와 믹스인을 현재 파일에 직접 풀어놓는 방식입니다.
작은 프로젝트에서는 편리하지만, 큰 프로젝트에서는 출처가 불분명해질 수 있습니다.

명확성을 더 중요하게 본다면 다음처럼 네임스페이스를 유지하는 방식이 좋습니다.

```scss
@use '@/styles/abstracts' as a;

.button {
  padding: a.$spacing-md;
  background-color: a.$color-primary;
}
```

---

# 3. SCSS의 사용성을 높여주는 코드 — 고급

## 3-1. Mixin

Mixin은 반복되는 스타일 묶음을 재사용할 수 있게 해주는 기능입니다. Sass 공식 문서에 따르면 믹스인은 `@mixin`으로 정의하고, `@include`로 현재 위치에 포함합니다. ([Sass][7])

기본 예시입니다.

```scss
@mixin flex-center {
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal {
  @include flex-center;
}
```

컴파일 결과입니다.

```css
.modal {
  display: flex;
  align-items: center;
  justify-content: center;
}
```

---

## 3-2. 인자를 받는 Mixin

Mixin은 함수처럼 값을 받을 수 있습니다.

```scss
@mixin box($padding, $radius) {
  padding: $padding;
  border-radius: $radius;
}

.card {
  @include box(20px, 16px);
}

.button {
  @include box(12px 16px, 8px);
}
```

결과는 다음과 같습니다.

```css
.card {
  padding: 20px;
  border-radius: 16px;
}

.button {
  padding: 12px 16px;
  border-radius: 8px;
}
```

---

## 3-3. 기본값이 있는 Mixin

인자에 기본값을 줄 수도 있습니다.

```scss
@mixin card($padding: 20px, $radius: 16px, $shadow: true) {
  padding: $padding;
  border-radius: $radius;
  background-color: #fff;

  @if $shadow {
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.08);
  }
}

.card {
  @include card;
}

.card-compact {
  @include card(12px, 10px, false);
}
```

이렇게 하면 자주 쓰는 스타일은 간단히 사용하고, 필요한 경우만 값을 바꿀 수 있습니다.

---

## 3-4. 반응형 Mixin

SCSS에서 가장 실용적인 믹스인 중 하나는 반응형 믹스인입니다.

```scss
$breakpoint-mobile: 480px;
$breakpoint-tablet: 768px;
$breakpoint-desktop: 1024px;

@mixin mobile {
  @media (max-width: $breakpoint-mobile) {
    @content;
  }
}

@mixin tablet {
  @media (max-width: $breakpoint-tablet) {
    @content;
  }
}

@mixin desktop {
  @media (min-width: $breakpoint-desktop) {
    @content;
  }
}
```

사용 예시입니다.

```scss
.card-list {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;

  @include tablet {
    grid-template-columns: repeat(2, 1fr);
  }

  @include mobile {
    grid-template-columns: 1fr;
    gap: 16px;
  }
}
```

이렇게 작성하면 반응형 코드가 훨씬 읽기 쉬워집니다.

---

## 3-5. `@content`

위 반응형 믹스인에서 사용한 `@content`는 믹스인을 호출한 위치의 내용을 믹스인 내부로 넣어주는 기능입니다.

```scss
@mixin hover-supported {
  @media (hover: hover) and (pointer: fine) {
    &:hover {
      @content;
    }
  }
}

.button {
  background-color: #256f8f;

  @include hover-supported {
    background-color: #1d5a75;
  }
}
```

이 코드는 마우스 hover가 가능한 환경에서만 hover 스타일을 적용합니다.

---

## 3-6. 접근성용 Mixin

실무에서 자주 쓰는 접근성 믹스인입니다.

```scss
@mixin visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  padding: 0;
  overflow: hidden;
  white-space: nowrap;
  border: 0;
  clip: rect(0 0 0 0);
}

.blind {
  @include visually-hidden;
}
```

이런 코드는 화면에는 보이지 않지만 스크린 리더에는 읽히게 만들 때 사용합니다.

예를 들어 아이콘 버튼에 숨김 텍스트를 넣을 수 있습니다.

```html
<button class="icon-button">
  <span class="blind">메뉴 열기</span>
</button>
```

---

## 3-7. 말줄임 Mixin

한 줄 말줄임입니다.

```scss
@mixin ellipsis {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.title {
  @include ellipsis;
}
```

여러 줄 말줄임입니다.

```scss
@mixin line-clamp($line: 2) {
  display: -webkit-box;
  overflow: hidden;
  -webkit-line-clamp: $line;
  -webkit-box-orient: vertical;
}

.description {
  @include line-clamp(3);
}
```

---

## 3-8. Position Mixin

반복되는 absolute center 패턴을 믹스인으로 만들 수 있습니다.

```scss
@mixin absolute-center {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.loading-spinner {
  @include absolute-center;
}
```

상하좌우 전체 채우기도 자주 씁니다.

```scss
@mixin full-cover {
  position: absolute;
  inset: 0;
}

.dimmed {
  @include full-cover;
  background: rgba(0, 0, 0, 0.5);
}
```

---

## 3-9. Safe Area Mixin

모바일 앱, PWA, iOS, Android WebView 등을 고려하면 safe area 처리가 필요할 수 있습니다.

```scss
@mixin safe-bottom($extra: 0px) {
  padding-bottom: calc(env(safe-area-inset-bottom, 0px) + #{$extra});
}

.modal-footer {
  @include safe-bottom(16px);
}
```

하단 버튼이 시스템 내비게이션 영역이나 홈 인디케이터에 가려지는 것을 줄일 때 유용합니다.

---

## 3-10. Theme Mixin

다크모드를 지원할 때 사용할 수 있는 방식입니다.

```scss
@mixin dark-mode {
  [data-theme='dark'] & {
    @content;
  }
}

.card {
  background-color: #fff;
  color: #222;

  @include dark-mode {
    background-color: #1f2933;
    color: #f5f5f5;
  }
}
```

결과적으로 다음과 같은 CSS 구조가 만들어집니다.

```css
.card {
  background-color: #fff;
  color: #222;
}

[data-theme='dark'] .card {
  background-color: #1f2933;
  color: #f5f5f5;
}
```

---

## 3-11. Function

Mixin이 스타일 묶음을 재사용하는 기능이라면, Function은 값을 계산해서 반환하는 기능입니다.

```scss
@function rem($px, $base: 16px) {
  @return calc($px / $base) * 1rem;
}

.title {
  font-size: rem(24px);
}
```

다만 최신 Sass에서는 수학 연산을 더 명확히 하기 위해 `sass:math` 모듈을 사용하는 방식을 권장합니다. Sass 공식 문서에서는 `sass:`로 시작하는 내장 모듈들을 `@use`로 불러와 사용할 수 있다고 설명합니다. ([Sass][8])

```scss
@use 'sass:math';

@function rem($px, $base: 16px) {
  @return math.div($px, $base) * 1rem;
}

.title {
  font-size: rem(24px);
}
```

---

## 3-12. Map

Map은 여러 값을 하나의 객체처럼 관리할 때 사용합니다.

```scss
$colors: (
  primary: #256f8f,
  danger: #e03131,
  success: #2f9e44,
  warning: #f08c00
);
```

사용 예시입니다.

```scss
@use 'sass:map';

$colors: (
  primary: #256f8f,
  danger: #e03131,
  success: #2f9e44,
  warning: #f08c00
);

.button {
  background-color: map.get($colors, primary);
}
```

Map은 디자인 토큰을 관리할 때 유용합니다.

```scss
$spacing: (
  xs: 4px,
  sm: 8px,
  md: 16px,
  lg: 24px,
  xl: 32px
);
```

---

## 3-13. 반복문 `@each`

Map과 `@each`를 조합하면 반복 클래스를 만들 수 있습니다.

```scss
$colors: (
  primary: #256f8f,
  danger: #e03131,
  success: #2f9e44
);

@each $name, $value in $colors {
  .text-#{$name} {
    color: $value;
  }

  .bg-#{$name} {
    background-color: $value;
  }
}
```

컴파일 결과입니다.

```css
.text-primary {
  color: #256f8f;
}

.bg-primary {
  background-color: #256f8f;
}

.text-danger {
  color: #e03131;
}

.bg-danger {
  background-color: #e03131;
}

.text-success {
  color: #2f9e44;
}

.bg-success {
  background-color: #2f9e44;
}
```

여기서 `#{$name}`은 보간법입니다.
변수 값을 문자열이나 선택자 안에 끼워 넣을 때 사용합니다.

---

## 3-14. Placeholder와 `@extend`

SCSS에는 `%placeholder`와 `@extend`가 있습니다.

```scss
%button-base {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border: 0;
  cursor: pointer;
}

.button-primary {
  @extend %button-base;
  background-color: #256f8f;
  color: #fff;
}

.button-secondary {
  @extend %button-base;
  background-color: #eee;
  color: #222;
}
```

Sass 공식 문서는 `@extend`가 하나의 선택자가 다른 선택자의 스타일을 상속하도록 하는 기능이라고 설명합니다. ([Sass][9])

하지만 실무에서는 `@extend`를 조심해서 사용해야 합니다.
이유는 컴파일 결과가 예상보다 복잡해질 수 있기 때문입니다.

초보자에게는 보통 다음 우선순위를 추천합니다.

```text
1순위: 공통 클래스 사용
2순위: mixin 사용
3순위: placeholder + @extend는 제한적으로 사용
```

예를 들어 버튼 스타일은 `@extend`보다 mixin이 더 예측하기 쉽습니다.

```scss
@mixin button-base {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border: 0;
  cursor: pointer;
}

.button-primary {
  @include button-base;
  background-color: #256f8f;
  color: #fff;
}
```

---

# 4. SCSS 전문가로 되기 — 심화

## 4-1. SCSS를 잘 쓴다는 것은 무엇일까?

SCSS를 잘 쓴다는 것은 문법을 많이 아는 것이 아닙니다.

진짜 중요한 것은 다음입니다.

```text
CSS로 컴파일된 결과를 예측할 수 있는가?
중복을 줄이되 과하게 추상화하지 않는가?
변수, 믹스인, 함수의 역할을 명확히 나누는가?
팀원이 읽어도 이해하기 쉬운 구조인가?
디자인 변경에 강한 구조인가?
```

SCSS는 CSS를 더 편하게 작성하기 위한 도구입니다.
SCSS 자체가 목적이 되면 안 됩니다.

---

## 4-2. SCSS 변수와 CSS 변수의 차이

SCSS 변수와 CSS 변수는 다릅니다.

SCSS 변수입니다.

```scss
$primary-color: #256f8f;

.button {
  background-color: $primary-color;
}
```

컴파일 후에는 실제 값으로 바뀝니다.

```css
.button {
  background-color: #256f8f;
}
```

즉, SCSS 변수는 **빌드 시점에 사라집니다.**

반면 CSS 변수는 브라우저에 남습니다.

```css
:root {
  --primary-color: #256f8f;
}

.button {
  background-color: var(--primary-color);
}
```

CSS 변수는 런타임에 값을 바꿀 수 있습니다.

```css
[data-theme='dark'] {
  --primary-color: #7cc7e8;
}
```

따라서 기준은 다음처럼 잡으면 좋습니다.

| 상황                       | 추천      |
| ------------------------ | ------- |
| 빌드 시점에 고정되는 값            | SCSS 변수 |
| 다크모드, 테마 변경처럼 런타임에 바뀌는 값 | CSS 변수  |
| 계산용, 믹스인 내부 값            | SCSS 변수 |
| 사용자 설정에 따라 바뀌는 색상        | CSS 변수  |

---

## 4-3. 디자인 토큰 구조 만들기

프로젝트가 커지면 색상, 여백, 폰트 크기, radius, z-index 등을 토큰화하는 것이 좋습니다.

```scss
// _tokens.scss

$color-brand-primary: #256f8f;
$color-brand-secondary: #67a6c2;

$color-text-main: #1f2933;
$color-text-muted: #6b7280;
$color-border-default: #e5e7eb;
$color-surface-default: #ffffff;
$color-surface-muted: #f6f7f9;

$font-size-xs: 12px;
$font-size-sm: 14px;
$font-size-md: 16px;
$font-size-lg: 20px;
$font-size-xl: 28px;

$spacing-xs: 4px;
$spacing-sm: 8px;
$spacing-md: 16px;
$spacing-lg: 24px;
$spacing-xl: 32px;

$radius-sm: 6px;
$radius-md: 10px;
$radius-lg: 16px;
$radius-xl: 24px;

$z-index-dropdown: 100;
$z-index-sticky: 200;
$z-index-modal: 1000;
$z-index-toast: 1100;
```

토큰 이름은 다음 원칙을 따르는 것이 좋습니다.

```text
색상 자체보다 역할을 기준으로 이름 짓는다.
크기는 xs, sm, md, lg, xl처럼 일관성 있게 정한다.
z-index는 숫자를 직접 쓰지 말고 변수로 관리한다.
border-radius, spacing, font-size도 공통 기준을 둔다.
```

---

## 4-4. 컴포넌트 단위 스타일 설계

버튼 컴포넌트를 예로 들어보겠습니다.

```scss
.button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-height: 44px;
  padding: 0 16px;
  border: 0;
  border-radius: 10px;
  font-size: 15px;
  font-weight: 700;
  cursor: pointer;
  transition:
    background-color 0.2s ease,
    color 0.2s ease,
    opacity 0.2s ease;

  &:disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }

  &--primary {
    background-color: #256f8f;
    color: #fff;
  }

  &--secondary {
    background-color: #eef2f5;
    color: #1f2933;
  }

  &--danger {
    background-color: #e03131;
    color: #fff;
  }

  &--full {
    width: 100%;
  }

  &--small {
    min-height: 36px;
    padding: 0 12px;
    font-size: 14px;
  }
}
```

HTML에서는 이렇게 사용합니다.

```html
<button class="button button--primary">저장</button>
<button class="button button--secondary">취소</button>
<button class="button button--danger">삭제</button>
<button class="button button--primary button--full">전체 저장</button>
```

이 구조의 장점은 명확합니다.

```text
.button은 기본 구조를 담당한다.
.button--primary는 색상 변형만 담당한다.
.button--full은 너비 변형만 담당한다.
.button--small은 크기 변형만 담당한다.
```

역할이 나뉘면 스타일 유지보수가 쉬워집니다.

---

## 4-5. 나쁜 SCSS 추상화

SCSS를 배우면 모든 것을 mixin, function, map으로 만들고 싶어질 수 있습니다.
하지만 과한 추상화는 오히려 코드를 어렵게 만듭니다.

나쁜 예시입니다.

```scss
@mixin make-component($type, $color, $size, $rounded, $shadow, $border, $state) {
  // 너무 많은 책임을 가진 mixin
}
```

이런 코드는 처음 만든 사람만 이해할 가능성이 큽니다.

좋은 mixin은 역할이 작고 명확해야 합니다.

```scss
@mixin flex-center {
  display: flex;
  align-items: center;
  justify-content: center;
}

@mixin ellipsis {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

@mixin safe-bottom($extra: 0px) {
  padding-bottom: calc(env(safe-area-inset-bottom, 0px) + #{$extra});
}
```

Mixin 하나가 너무 많은 일을 하면 안 됩니다.

---

## 4-6. 좋은 SCSS 파일 구조

초보 프로젝트라면 너무 복잡한 구조보다 다음 정도가 좋습니다.

```text
src/
  styles/
    abstracts/
      _tokens.scss
      _mixins.scss
      _functions.scss
      _index.scss

    base/
      _reset.scss
      _global.scss
      _typography.scss

    components/
      _button.scss
      _card.scss
      _modal.scss
      _form.scss

    layouts/
      _app-shell.scss
      _header.scss
      _bottom-nav.scss

    pages/
      _home.scss
      _settings.scss

    main.scss
```

`main.scss`는 전체 스타일의 진입점입니다.

```scss
@use './base/reset';
@use './base/global';
@use './base/typography';

@use './components/button';
@use './components/card';
@use './components/modal';
@use './components/form';

@use './layouts/app-shell';
@use './layouts/header';
@use './layouts/bottom-nav';

@use './pages/home';
@use './pages/settings';
```

공통 변수와 믹스인은 `abstracts`에서 관리합니다.

```scss
// abstracts/_index.scss

@forward './tokens';
@forward './mixins';
@forward './functions';
```

사용할 때는 다음처럼 씁니다.

```scss
@use '@/styles/abstracts' as a;

.card {
  padding: a.$spacing-md;
  border-radius: a.$radius-lg;
}
```

---

## 4-7. Vue에서 SCSS 사용 예시

Vue 컴포넌트에서는 다음처럼 사용할 수 있습니다.

```vue
<template>
  <section class="profile-card">
    <h2 class="profile-card__title">사용자 정보</h2>
    <p class="profile-card__description">SCSS 예시 컴포넌트입니다.</p>
  </section>
</template>

<style lang="scss" scoped>
.profile-card {
  padding: 20px;
  border-radius: 16px;
  background-color: #fff;

  &__title {
    font-size: 20px;
    font-weight: 700;
  }

  &__description {
    margin-top: 8px;
    color: #666;
  }
}
</style>
```

Vue에서 `scoped`를 사용하면 해당 컴포넌트에만 스타일이 적용됩니다.
다만 모든 스타일을 컴포넌트 안에만 넣으면 공통 버튼, 공통 모달, 공통 폼 스타일이 중복될 수 있습니다.

기준은 다음이 좋습니다.

| 스타일 종류               | 위치                  |
| -------------------- | ------------------- |
| 전역 reset, typography | `styles/base`       |
| 공통 버튼, 카드, 모달        | `styles/components` |
| 특정 화면에서만 쓰는 스타일      | 해당 Vue 컴포넌트         |
| 디자인 토큰, 믹스인          | `styles/abstracts`  |

---

## 4-8. SCSS에서 피해야 할 습관

### 1. 너무 깊은 중첩

```scss
.page {
  .content {
    .box {
      .item {
        .title {
          color: red;
        }
      }
    }
  }
}
```

대신 다음처럼 작성합니다.

```scss
.item-title {
  color: red;
}
```

또는 BEM 방식으로 작성합니다.

```scss
.item {
  &__title {
    color: red;
  }
}
```

---

### 2. 색상값을 아무 곳에나 직접 쓰기

나쁜 예시입니다.

```scss
.button {
  background-color: #256f8f;
}

.link {
  color: #256f8f;
}

.badge {
  border-color: #256f8f;
}
```

좋은 예시입니다.

```scss
$color-primary: #256f8f;

.button {
  background-color: $color-primary;
}

.link {
  color: $color-primary;
}

.badge {
  border-color: $color-primary;
}
```

---

### 3. `!important` 남발

나쁜 예시입니다.

```scss
.title {
  color: red !important;
}
```

`!important`가 많아지면 나중에 스타일을 수정하기 어려워집니다.

대부분의 경우 문제는 다음 중 하나입니다.

```text
선택자가 너무 복잡하다.
전역 스타일이 너무 강하다.
컴포넌트 구조가 명확하지 않다.
CSS 로딩 순서가 꼬여 있다.
```

`!important`를 쓰기 전에 구조를 먼저 확인해야 합니다.

---

### 4. 모든 것을 mixin으로 만들기

나쁜 예시입니다.

```scss
@mixin title-style {
  font-size: 20px;
  font-weight: 700;
  color: #222;
}

.card-title {
  @include title-style;
}
```

이 정도는 그냥 클래스로 작성하는 편이 더 명확할 수 있습니다.

```scss
.card-title {
  font-size: 20px;
  font-weight: 700;
  color: #222;
}
```

Mixin은 “반복되는 패턴”이 명확할 때 사용하는 것이 좋습니다.

---

### 5. `@import` 계속 사용하기

새 프로젝트에서는 `@import`보다 `@use`, `@forward`를 기준으로 잡는 것이 좋습니다. Sass 공식 문서에서도 `@import`와 전역 내장 함수는 deprecated 상태라고 안내하고 있습니다. ([Sass][5])

나쁜 예시입니다.

```scss
@import './variables';
@import './mixins';
```

좋은 예시입니다.

```scss
@use './variables';
@use './mixins';
```

또는

```scss
@use '@/styles/abstracts' as a;
```

---

# 5. 실무에서 바로 쓸 수 있는 SCSS 기본 세트

## 5-1. `_tokens.scss`

```scss
$color-primary: #256f8f;
$color-primary-dark: #1d5a75;

$color-danger: #e03131;
$color-success: #2f9e44;
$color-warning: #f08c00;

$color-text-main: #1f2933;
$color-text-sub: #4b5563;
$color-text-muted: #9ca3af;

$color-border: #e5e7eb;
$color-surface: #ffffff;
$color-surface-muted: #f6f7f9;

$font-size-xs: 12px;
$font-size-sm: 14px;
$font-size-md: 16px;
$font-size-lg: 20px;
$font-size-xl: 28px;

$spacing-xs: 4px;
$spacing-sm: 8px;
$spacing-md: 16px;
$spacing-lg: 24px;
$spacing-xl: 32px;

$radius-sm: 6px;
$radius-md: 10px;
$radius-lg: 16px;
$radius-xl: 24px;

$z-index-dropdown: 100;
$z-index-sticky: 200;
$z-index-modal: 1000;
$z-index-toast: 1100;
```

---

## 5-2. `_mixins.scss`

```scss
@mixin flex-center {
  display: flex;
  align-items: center;
  justify-content: center;
}

@mixin inline-flex-center {
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

@mixin ellipsis {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

@mixin line-clamp($line: 2) {
  display: -webkit-box;
  overflow: hidden;
  -webkit-line-clamp: $line;
  -webkit-box-orient: vertical;
}

@mixin visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  padding: 0;
  overflow: hidden;
  white-space: nowrap;
  border: 0;
  clip: rect(0 0 0 0);
}

@mixin full-cover {
  position: absolute;
  inset: 0;
}

@mixin safe-bottom($extra: 0px) {
  padding-bottom: calc(env(safe-area-inset-bottom, 0px) + #{$extra});
}

@mixin mobile {
  @media (max-width: 480px) {
    @content;
  }
}

@mixin tablet {
  @media (max-width: 768px) {
    @content;
  }
}

@mixin desktop {
  @media (min-width: 1024px) {
    @content;
  }
}

@mixin dark-mode {
  [data-theme='dark'] & {
    @content;
  }
}
```

---

## 5-3. `_functions.scss`

```scss
@use 'sass:math';

@function rem($px, $base: 16px) {
  @return math.div($px, $base) * 1rem;
}
```

---

## 5-4. `_index.scss`

```scss
@forward './tokens';
@forward './mixins';
@forward './functions';
```

---

## 5-5. 사용 예시

```scss
@use '@/styles/abstracts' as a;

.card {
  padding: a.$spacing-lg;
  border-radius: a.$radius-lg;
  background-color: a.$color-surface;
  color: a.$color-text-main;

  @include a.tablet {
    padding: a.$spacing-md;
  }

  @include a.dark-mode {
    background-color: #1f2933;
    color: #f5f5f5;
  }

  &__title {
    font-size: a.rem(24px);
    font-weight: 700;

    @include a.ellipsis;
  }

  &__description {
    margin-top: a.$spacing-sm;
    color: a.$color-text-sub;

    @include a.line-clamp(2);
  }
}
```

---

# 6. SCSS 학습 순서

초보자라면 다음 순서로 학습하는 것이 좋습니다.

```text
1단계: CSS 기본기
선택자, 박스 모델, display, position, flex, grid, media query

2단계: SCSS 기본 문법
변수, 중첩, &, partial, @use

3단계: 재사용 문법
mixin, @include, @content, function

4단계: 구조화
tokens, abstracts, components, layouts, pages

5단계: 실무 설계
디자인 시스템, 다크모드, 반응형 전략, 접근성, 유지보수

6단계: 컴파일 결과 이해
작성한 SCSS가 어떤 CSS로 바뀌는지 확인
```

SCSS를 잘하려면 결국 CSS를 잘 알아야 합니다.
SCSS는 CSS의 대체제가 아니라 CSS를 더 체계적으로 작성하게 도와주는 도구입니다.

---

# 7. 최종 정리

SCSS를 제대로 사용하려면 다음 원칙을 기억하면 됩니다.

```text
SCSS는 Sass의 CSS 친화적인 문법이다.
새 프로젝트에서는 .scss 문법을 사용하는 것이 가장 무난하다.
반복되는 값은 변수로 관리한다.
반복되는 스타일 패턴은 mixin으로 관리한다.
파일은 역할별로 나눈다.
@import보다 @use, @forward를 사용한다.
중첩은 2~3단계까지만 제한한다.
CSS 변수와 SCSS 변수의 차이를 이해한다.
mixin과 function을 남발하지 않는다.
컴파일된 CSS 결과를 항상 의식한다.
```

가장 중요한 결론은 이것입니다.

> SCSS를 잘 쓰는 사람은 화려한 문법을 많이 쓰는 사람이 아니라,
> 나중에 수정하기 쉬운 CSS 구조를 만드는 사람입니다.

SCSS는 프로젝트가 커질수록 빛을 발합니다.
처음에는 변수와 중첩만 써도 충분합니다.
그다음 반복되는 패턴이 보이면 mixin을 만들고, 파일이 커지면 구조를 나누고, 디자인 기준이 생기면 토큰을 정리하면 됩니다.

처음부터 완벽한 구조를 만들려고 하기보다,
**반복을 발견하고, 이름을 붙이고, 역할별로 분리하는 습관**을 들이는 것이 SCSS 실력의 핵심입니다.

[1]: https://sass-lang.com/documentation/?utm_source=chatgpt.com "Sass: Documentation"
[2]: https://sass-lang.com/documentation/syntax/?utm_source=chatgpt.com "Syntax"
[3]: https://sass-lang.com/documentation/syntax/comments/?utm_source=chatgpt.com "Comments"
[4]: https://sass-lang.com/documentation/at-rules/use/?utm_source=chatgpt.com "Sass: @use"
[5]: https://sass-lang.com/documentation/breaking-changes/import/?utm_source=chatgpt.com "Breaking Change: @import and global built-in functions"
[6]: https://sass-lang.com/documentation/at-rules/forward/?utm_source=chatgpt.com "Sass: @forward"
[7]: https://sass-lang.com/documentation/at-rules/mixin/?utm_source=chatgpt.com "mixin and @include"
[8]: https://sass-lang.com/documentation/modules/?utm_source=chatgpt.com "Built-In Modules"
[9]: https://sass-lang.com/documentation/at-rules/extend/?utm_source=chatgpt.com "extend"
