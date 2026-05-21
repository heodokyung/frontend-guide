<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0f766e,100:2563eb&height=180&section=header&text=Frontend%20Guide&fontSize=46&fontColor=ffffff&desc=Heo%20Do%20Kyung%27s%20practical%20frontend%20notes&descAlignY=68" alt="Frontend Guide banner">
</p>

<h1 align="center">Frontend Guide</h1>

<p align="center">
  <strong>허도경이 실제 작업하며 정리한 프론트엔드 실무 가이드</strong><br>
  Git, Markdown, Markup/CSS, Accessibility, Clean Code, TypeScript, Vanilla JS, UI 구현 기준을 한곳에 모았습니다.
</p>

<p align="center">
  <a href="./docs/git/README.md"><img src="https://img.shields.io/badge/Git-workflow-f05032?style=flat-square&logo=git&logoColor=white" alt="Git workflow"></a>
  <a href="./docs/markdown/README.md"><img src="https://img.shields.io/badge/Markdown-docs-000000?style=flat-square&logo=markdown&logoColor=white" alt="Markdown docs"></a>
  <a href="./docs/markup/README.md"><img src="https://img.shields.io/badge/Markup%20%2F%20CSS-convention-1572b6?style=flat-square&logo=css3&logoColor=white" alt="Markup CSS convention"></a>
  <a href="./docs/accessibility/README.md"><img src="https://img.shields.io/badge/Accessibility-WCAG%202.2-0f766e?style=flat-square" alt="Accessibility WCAG 2.2"></a>
  <a href="./docs/typescript/README.md"><img src="https://img.shields.io/badge/TypeScript-guide-3178c6?style=flat-square&logo=typescript&logoColor=white" alt="TypeScript guide"></a>
</p>

---

## 목차

- [이 저장소는 왜 만들었나](#이-저장소는-왜-만들었나)
- [문서 지도](#문서-지도)
- [처음 보는 사람을 위한 추천 순서](#처음-보는-사람을-위한-추천-순서)
- [Code Align 도구 바로가기](#code-align-도구-바로가기)
- [저장소 구조](#저장소-구조)
- [문서 작성 기준](#문서-작성-기준)
- [저작권과 사용 안내](#저작권과-사용-안내)

---

## 이 저장소는 왜 만들었나

프론트엔드 작업은 화면만 예쁘게 만드는 일이 아니었습니다.

작업을 하다 보면 매번 비슷한 순간에서 멈춥니다. GitHub에 처음 올릴 때, README를 다듬을 때, 마크업 구조를 잡을 때, CSS 순서가 흐트러질 때, 접근성을 놓쳤을 때, TypeScript 타입이 애매할 때. 그때마다 검색해서 넘기기보다, 내가 실제로 쓰는 기준을 한곳에 모아두고 싶었습니다.

`frontend-guide`는 그런 이유로 만든 저장소입니다.

이곳의 문서는 책처럼 한 번 읽고 끝내는 글이 아니라, 작업 중에 다시 열어보는 기준표에 가깝습니다. 내용은 계속 고쳐질 수 있고, 프로젝트를 진행하면서 더 나은 방식이 생기면 그 기준도 함께 바꿉니다.

> 이 가이드는 허도경(Heo Do Kyung)이 개인 프로젝트와 실무형 포트폴리오를 정리하며 만든 프론트엔드 작업 기준입니다.

---

## 문서 지도

### Git

로컬 폴더와 GitHub를 연결하거나, Fork 앱에서 Push가 막히거나, 브랜치와 커밋 흐름이 헷갈릴 때 봅니다.

| 문서 | 볼 때 |
|---|---|
| [Git 가이드 시작하기](./docs/git/README.md) | Git 흐름을 한 번에 정리하고 싶을 때 |
| [Git 입문 가이드](./docs/git/beginner.md) | `clone`, `init`, `remote`, `push`가 헷갈릴 때 |
| [Git 실무 워크플로우](./docs/git/workflow.md) | 브랜치, 커밋, PR, merge/rebase 흐름을 잡을 때 |
| [Git 문제 해결 가이드](./docs/git/troubleshooting.md) | `rejected`, 충돌, remote 오류, 잘못된 커밋을 해결할 때 |

### 문서 작성

README와 문서형 저장소를 읽기 좋게 정리하기 위한 기준입니다.

| 문서 | 볼 때 |
|---|---|
| [Markdown 가이드](./docs/markdown/README.md) | README, 표, 목차, 코드블록, 접기/펼치기 문법을 정리할 때 |

### 마크업 / 스타일 / 접근성

화면 구조를 의미 있게 만들고, CSS를 예측 가능하게 유지하기 위한 기준입니다.

| 문서 | 볼 때 |
|---|---|
| [Markup / CSS 가이드](./docs/markup/README.md) | HTML 구조, 클래스 네이밍, CSS 작성 순서를 정할 때 |
| [웹 접근성 가이드](./docs/accessibility/README.md) | WCAG 2.2 / KWCAG 2.2 기준으로 화면을 점검할 때 |
| [UI 가이드](./docs/ui/README.md) | 버튼, 폼, 모달, 탭 같은 반복 UI 기준을 잡을 때 |

### 코드 품질 / 언어

오래 유지되는 코드를 만들기 위한 기준입니다.

| 문서 | 볼 때 |
|---|---|
| [Clean Code 가이드](./docs/clean-code/README.md) | 네이밍, 함수 분리, 주석, 리팩터링 기준이 필요할 때 |
| [TypeScript 가이드](./docs/typescript/README.md) | 타입을 안전하게 설계하고 `any`를 줄이고 싶을 때 |
| [jQuery → Vanilla JS 전환 가이드](./docs/javascript/README.md) | jQuery 코드를 순수 JavaScript로 바꾸고 싶을 때 |

---

## 처음 보는 사람을 위한 추천 순서

| 지금 상황 | 먼저 볼 문서 |
|---|---|
| GitHub 레포를 만들고 로컬 폴더와 연결해야 한다 | [Git 입문 가이드](./docs/git/beginner.md) |
| Fork 앱에서 Push, Pull, Branch가 헷갈린다 | [Git 가이드 시작하기](./docs/git/README.md) |
| `fetch first`, `non-fast-forward`, 충돌 오류가 났다 | [Git 문제 해결 가이드](./docs/git/troubleshooting.md) |
| README를 보기 좋게 정리하고 싶다 | [Markdown 가이드](./docs/markdown/README.md) |
| HTML/CSS 컨벤션을 정하고 싶다 | [Markup / CSS 가이드](./docs/markup/README.md) |
| 접근성 검사 전에 무엇을 봐야 할지 모르겠다 | [웹 접근성 가이드](./docs/accessibility/README.md) |
| 코드가 점점 길어지고 읽기 어려워진다 | [Clean Code 가이드](./docs/clean-code/README.md) |
| JavaScript 프로젝트를 TypeScript로 정리하고 싶다 | [TypeScript 가이드](./docs/typescript/README.md) |
| jQuery 없이 DOM과 이벤트를 처리하고 싶다 | [jQuery → Vanilla JS 전환 가이드](./docs/javascript/README.md) |

---

## Code Align 도구 바로가기

작은 코드 정렬 도구는 이 저장소 안의 `code-align/` 폴더에 두었습니다.

| 구분 | 링크 |
|---|---|
| GitHub에서 코드 보기 | [code-align/index.html](./code-align/index.html) |
| GitHub Pages에서 실행 | `https://heodokyung.github.io/frontend-guide/code-align/` |
| 배포 설정 확인 | [GitHub Pages 배포 가이드](./docs/deploy/github-pages.md) |

GitHub README 안에서 `./code-align/index.html`을 누르면 보통 “소스 파일”이 열립니다. 실제 도구처럼 실행하려면 GitHub Pages 주소를 써야 합니다.

GitHub Pages를 `main` 브랜치의 `/root`로 배포하고 있다면 `code-align/index.html`은 아래 주소로 접근하는 것이 정상입니다.

```txt
https://heodokyung.github.io/frontend-guide/code-align/
```

---

## 저장소 구조

```txt
frontend-guide/
├─ README.md
├─ .nojekyll
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
│  ├─ accessibility/
│  │  └─ README.md
│  ├─ clean-code/
│  │  └─ README.md
│  ├─ typescript/
│  │  └─ README.md
│  ├─ javascript/
│  │  └─ README.md
│  ├─ ui/
│  │  └─ README.md
│  └─ deploy/
│     └─ github-pages.md
└─ code-align/
   ├─ README.md
   └─ index.html
```

---

## 문서 작성 기준

이 저장소의 문서는 아래 기준을 따릅니다.

| 기준 | 설명 |
|---|---|
| 결론부터 쓴다 | 길게 읽기 전에 방향을 잡을 수 있어야 합니다. |
| 상황으로 나눈다 | “처음 시작”, “실무 적용”, “문제 해결”처럼 실제 사용 장면이 보여야 합니다. |
| 예시를 넣는다 | 좋은 예와 나쁜 예를 함께 두어야 바로 적용할 수 있습니다. |
| 위험한 작업은 표시한다 | `reset`, `force push`, `rebase`처럼 이력에 영향을 주는 작업은 조심스럽게 다룹니다. |
| 내 기준을 숨기지 않는다 | 공개 자료를 참고하되, 최종 문서는 내가 실제로 쓰는 방식으로 정리합니다. |

---

## 저작권과 사용 안내

별도 `LICENSE` 파일은 두지 않았습니다.

그래서 이 저장소의 글과 예제는 기본적으로 작성자인 Heo Do Kyung에게 권리가 있습니다. 개인 학습이나 참고는 자유롭게 봐도 되지만, 문서를 그대로 복사해서 다른 공개 자료로 배포하는 것은 권장하지 않습니다.

누구나 재사용해도 되는 공개 가이드로 운영하고 싶다면 나중에 아래 중 하나를 선택하면 됩니다.

| 목적 | 추천 라이선스 |
|---|---|
| 문서 공유와 출처 표기를 원한다 | Creative Commons BY 4.0 |
| 코드까지 자유롭게 재사용하게 하고 싶다 | MIT License |
| 당장은 개인 포트폴리오 성격을 유지하고 싶다 | 라이선스 없음 |

현재 방향은 세 번째, 즉 “개인 기준 문서이지만 공개적으로 읽을 수 있는 저장소”에 가깝습니다.

---

## 참고한 주요 공개 자료

이 저장소는 아래 자료를 참고하되, 문장을 그대로 옮기지 않고 프론트엔드 실무 기준에 맞게 다시 정리했습니다.

- Google HTML/CSS Style Guide
- MDN Web Docs
- GitHub Docs
- CommonMark
- W3C WCAG 2.2
- 한국형 웹 콘텐츠 접근성 지침 2.2(KWCAG 2.2)
- TypeScript Handbook
- Conventional Commits
- Code Guide by @mdo

---

<p align="center">
  <strong>좋은 가이드는 많은 내용을 담는 문서가 아니라, 다시 열어봤을 때 바로 쓸 수 있는 문서라고 생각합니다.</strong><br>
  <sub>Written and maintained by Heo Do Kyung.</sub>
</p>
