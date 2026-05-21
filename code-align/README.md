# Code alignment
코드를 가독성 높고 밀집도(Compactness) 있게 최적화하는 고급 정렬 포맷터입니다. AST(추상 구문 트리) 파싱을 통해 데이터 유실과 구문 파괴를 완벽하게 방지합니다.

## 1. 코드 포맷팅 타입
세로형 나열 방식이 아닌, **가로형(1줄) 정렬**을 강제하여 코드 라인 수를 획기적으로 단축하고 유지보수성을 확보합니다.

### 시각적 정렬 규칙
- **선언부 밀집화:** 속성과 값 사이의 공백은 제거하고, 각 선언 사이에는 단일 공백만 유지합니다. 중괄호(`{ }`) 내부의 불필요한 공백도 모두 제거합니다.
  - *예시:* `selector {display:block; margin-top:10px;}`
- **주석 여백 제어:** 블록 주석(`/* */`)의 바로 윗줄에는 한 줄의 공백(`\n\n`)을 두어 시각적으로 분리하고, 주석 바로 아랫줄은 공백 없이 코드가 즉시 시작되도록 하여 주석과 대상 코드의 결합도를 높입니다.

## 2. 기능적 정렬 규칙

### 2.1 정렬 순서 (Concentric CSS 기반)
레이아웃에 미치는 영향력이 가장 큰 범위에서 작은 범위 순으로, 그리고 축약형(Shorthand)에서 상세형(Longhand) 순으로 자동 정렬됩니다.

1. **Layout & Box Model:** `box-sizing`, `display`, `position`, `inset` (top/right/bottom/left), `z-index`, `float`
2. **Flex / Grid:** `flex`, `flex-direction`, `justify-content`, `align-items`, `gap`, `grid`, `grid-template`
3. **Size:** `width`, `height`, `min/max` sizes, `aspect-ratio`
4. **Margin:** `margin`, `margin-top/right/bottom/left`
5. **Padding:** `padding`, `padding-top/right/bottom/left`
6. **Border & Outline:** `border`, `border-width/style/color`, 방향별 border, `border-radius`, `outline`
7. **Background:** `background`, `background-color/image/position/size/repeat`, `backdrop-filter`
8. **Typography:** `color`, `font`, `font-family/size/weight`, `line-height`, `text-align`, `white-space`
9. **Visual & Interaction:** `overflow`, `opacity`, `box-shadow`, `transform`, `transition`, `animation`, `user-select`

### 2.2 종속성(Cascade) 보호 예외 규칙 [중요]
원래 작성된 코드의 순서가 뒤바뀌면 UI 렌더링 결과가 달라질 수 있는 **순서 민감 속성(Order-Sensitive Properties)**은 강제 정렬하지 않고 사용자가 작성한 원본 순서를 절대 유지합니다.
- *대상 속성:* `margin`, `padding`, `border`, `background`, `font`, `animation`, `transition` 등 단축/개별 속성 혼용 시 우선순위가 발생하는 그룹.
- *예시:* `margin-top: 10px; margin: 0;` 으로 작성된 코드는, 정렬 규칙(Margin 단축형 우선)에 의해 `margin: 0; margin-top: 10px;` 로 임의 변경되지 않고 원본을 보존합니다.

### 2.3 벤더 프리픽스(Vendor Prefix) 자동 생성
최신 웹 표준 및 크로스 브라우징을 위해 필수적인 속성 누락 시, `-webkit-` 프리픽스를 원본 속성 직전에 자동으로 삽입합니다.
- *지원 속성:* `user-select`, `backdrop-filter`, `appearance`, `clip-path`, `background-clip: text` 등.
