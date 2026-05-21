# Frontend Guide

> 프론트엔드 작업에서 반복해서 헷갈리는 **Git, Markdown, Markup/CSS, Clean Code, TypeScript, UI 구현 기준**을 한곳에 모은 실무형 가이드입니다.

`frontend-guide`는 단순한 문서 모음이 아닙니다.  
작업 중 문제가 생겼을 때 “지금 어떤 상태인지 → 무엇을 확인해야 하는지 → 어떤 순서로 해결해야 하는지”를 빠르게 판단하기 위한 기준 문서 저장소입니다.

---

## 이 저장소의 방향

프론트엔드 개발은 화면을 만드는 일처럼 보이지만, 실제 작업은 훨씬 넓습니다.

- Git으로 변경 이력을 안전하게 관리하고
- README와 Markdown 문서를 읽기 좋게 정리하고
- HTML은 의미 있게, CSS는 예측 가능하게 작성하고
- JavaScript/TypeScript 코드는 오래 유지될 수 있게 다듬고
- 버튼, 폼, 모달, 탭 같은 UI 패턴을 일관되게 구현해야 합니다.

이 저장소는 그 기준을 흩어진 메모가 아니라 **다시 찾아보기 쉬운 실무 가이드**로 정리합니다.

---

## 빠른 바로가기

### Git

Git을 처음 연결하거나, Fork 앱에서 Push가 막히거나, 브랜치/커밋이 헷갈릴 때 봅니다.

- [Git 가이드 시작하기](./docs/git/README.md)
- [Git 입문 가이드](./docs/git/beginner.md)
- [Git 실무 워크플로우](./docs/git/workflow.md)
- [Git 문제 해결 가이드](./docs/git/troubleshooting.md)

### Markdown

README, 문서 목차, 표, 코드블록, 체크리스트, GitHub 문서 작성 규칙을 정리합니다.

- [Markdown 가이드](./docs/markdown/README.md)

### Markup / CSS

HTML 구조, 접근성, 클래스 네이밍, BEM, CSS 작성 순서, 반응형, 컴포넌트 스타일 규칙을 정리합니다.

- [Markup / CSS 가이드](./docs/markup/README.md)

### Clean Code

좋은 코드란 무엇인지, 네이밍/함수/주석/구조/리팩터링 기준을 정리합니다.

- [Clean Code 가이드](./docs/clean-code/README.md)

### TypeScript

타입스크립트의 기본 개념부터 프론트엔드 실무에서 안전하게 쓰는 기준까지 정리합니다.

- [TypeScript 가이드](./docs/typescript/README.md)

### Code-align

CSS, HTML, Js등을 컨벤션 규칙이 맞게 정렬합니다.

- [코드 정렬 바로가기](./code-align/index.html)

---

## 처음 보는 사람을 위한 추천 순서

처음부터 모든 문서를 읽을 필요는 없습니다. 지금 필요한 상황에 맞게 보면 됩니다.

| 상황 | 먼저 볼 문서 |
|---|---|
| GitHub 레포를 만들고 로컬 폴더와 연결해야 한다 | [Git 입문 가이드](./docs/git/beginner.md) |
| Fork 앱에서 Push, Pull, Branch가 헷갈린다 | [Git 가이드 시작하기](./docs/git/README.md) |
| `rejected`, `fetch first`, 충돌 오류가 났다 | [Git 문제 해결 가이드](./docs/git/troubleshooting.md) |
| README를 보기 좋게 만들고 싶다 | [Markdown 가이드](./docs/markdown/README.md) |
| HTML/CSS 컨벤션을 정하고 싶다 | [Markup / CSS 가이드](./docs/markup/README.md) |
| 코드가 점점 복잡해지고 읽기 어려워진다 | [Clean Code 가이드](./docs/clean-code/README.md) |
| JavaScript 프로젝트를 TypeScript로 정리하고 싶다 | [TypeScript 가이드](./docs/typescript/README.md) |

---

## 저장소 구조

```txt
frontend-guide/
├─ README.md
├─ docs/
│  ├─ git/
│  │  ├─ README.md
│  │  ├─ beginner.md
│  │  ├─ workflow.md
│  │  └─ troubleshooting.md
│  ├─ markdown/
│  │  └─ README.md
│  ├─ markup/
│  │  └─ README.md
│  ├─ clean-code/
│  │  └─ README.md
│  └─ typescript/
│     └─ README.md
├─ code-align/
└─ LICENSE
```

---

## 문서 작성 원칙

이 저장소의 문서는 “개념 설명”보다 “실제 적용”에 무게를 둡니다.

좋은 문서는 아래 기준을 만족해야 합니다.

| 기준 | 설명 |
|---|---|
| 결론이 먼저 보인다 | 글을 끝까지 읽지 않아도 방향을 알 수 있어야 합니다. |
| 상황별로 찾을 수 있다 | `처음 시작`, `문제 발생`, `실무 적용`처럼 사용 맥락이 보여야 합니다. |
| 예시가 있다 | 좋은 예와 나쁜 예가 함께 있어야 실제 코드에 적용할 수 있습니다. |
| 위험한 작업을 표시한다 | `reset`, `force push`, `rebase`처럼 이력에 영향을 주는 작업은 주의가 필요합니다. |
| 오래 유지될 수 있다 | 개인 취향보다 범용 컨벤션과 팀 협업 기준을 우선합니다. |

---

## 통합 관리 기준

기존에 따로 관리하던 문서형 레포지토리는 이 저장소로 통합하는 것을 권장합니다.

| 기존 자료 성격 | 추천 위치 |
|---|---|
| Git 튜토리얼, Git 명령어 모음 | `docs/git/` |
| Markdown 작성법 | `docs/markdown/` |
| 마크업/CSS 컨벤션 | `docs/markup/` |
| 클린 코드 글 | `docs/clean-code/` |
| TypeScript 학습 정리 | `docs/typescript/` |
| CSS 정렬/변환 같은 작은 도구 | `code-align/` |

문서형 자료는 하나의 저장소에서 관리하는 편이 찾기 쉽고, 포트폴리오 관점에서도 더 전문적으로 보입니다. 반대로 실제 배포가 필요한 웹앱이나 독립적인 도구는 별도 레포로 유지하는 편이 좋습니다.

---

## 기존 레포지토리 정리 방법

기존 문서 레포는 바로 삭제하기보다 아래 방식으로 정리하는 것을 추천합니다.

1. 기존 레포 README 상단에 이동 안내 추가
2. 새 문서 위치 링크 연결
3. GitHub에서 Archive 처리
4. 새 수정은 `frontend-guide`에서만 진행

예시:

```md
# 안내

이 문서는 아래 저장소로 이동되었습니다.

https://github.com/heodokyung/frontend-guide
```

---

## 참고한 주요 공개 자료

- Google HTML/CSS Style Guide: https://google.github.io/styleguide/htmlcssguide
- MDN Web Docs - HTML accessibility: https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Accessibility/HTML
- MDN Web Docs - CSS media queries: https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_media_queries
- GitHub Docs - Writing on GitHub: https://docs.github.com/en/get-started/writing-on-github
- CommonMark: https://commonmark.org/
- TypeScript Handbook: https://www.typescriptlang.org/docs/handbook/intro.html
- Conventional Commits: https://www.conventionalcommits.org/ko/v1.0.0/
- Code Guide by @mdo: https://codeguide.co/

---

## 한 줄 결론

> `frontend-guide`는 프론트엔드 작업을 할 때 매번 다시 검색하던 기준을 한곳에 모아, 실수 없이 빠르게 적용하기 위한 개인/실무 겸용 개발 가이드입니다.
