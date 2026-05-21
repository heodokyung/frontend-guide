# Code Align

> HTML, CSS, JavaScript 코드를 빠르게 정리해 보기 위한 작은 웹 도구입니다.

정리: Heo Do Kyung

---

## 목차

- [실행 링크](#실행-링크)
- [기능](#기능)
- [CSS 정렬 기준](#css-정렬-기준)
- [배포 구조](#배포-구조)
- [주의할 점](#주의할-점)

---

## 실행 링크

| 구분 | 링크 |
|---|---|
| GitHub에서 코드 보기 | [index.html](./index.html) |
| GitHub Pages에서 실행 | `https://heodokyung.github.io/frontend-guide/code-align/` |

GitHub README에서 `index.html`을 누르면 웹 도구가 실행되는 것이 아니라 소스 파일이 열립니다. 실제로 사용하려면 GitHub Pages 주소로 들어가야 합니다.

---

## 기능

- CSS 코드 정렬
- JavaScript 코드 정렬
- HTML 코드 정렬
- 입력/결과 복사
- 파일 저장
- Prettier CDN 로드 실패 시 CSS 자체 포매터로 동작

---

## CSS 정렬 기준

CSS는 화면에 미치는 영향이 큰 속성부터 정렬합니다.

1. 표시와 위치
2. Flex/Grid
3. 크기
4. 여백
5. 테두리
6. 배경
7. 글자
8. overflow와 시각 효과
9. transform, transition, animation

단축 속성과 개별 속성의 순서에 따라 결과가 달라질 수 있는 경우에는 원본 순서를 보호합니다.

```css
.box {
  margin: 0;
  margin-top: 12px;
}
```

---

## 배포 구조

현재 도구는 별도 빌드 없이 `code-align/index.html` 하나로 실행됩니다.

```txt
frontend-guide/
└─ code-align/
   ├─ README.md
   └─ index.html
```

GitHub Pages를 `main / root`로 설정하면 아래 주소에서 열립니다.

```txt
https://heodokyung.github.io/frontend-guide/code-align/
```

자세한 설정은 [GitHub Pages 배포 가이드](../docs/deploy/github-pages.md)를 참고합니다.

---

## 주의할 점

- 자동 정렬 결과가 항상 의도와 같다고 믿지 않습니다.
- 단축 속성과 개별 속성이 섞인 CSS는 결과를 확인합니다.
- 프리픽스는 가능한 한 Autoprefixer 같은 표준 도구를 우선합니다.
- 팀 프로젝트에서는 정렬 규칙을 먼저 합의합니다.
