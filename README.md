<div align="center">

# Frontend Guide

프론트엔드 작업을 하면서 자주 다시 열어보는 기준을 모아둔 저장소입니다.

Git, Markdown, Markup/CSS, 접근성, 클린 코드, TypeScript, Vanilla JS 전환까지  
작업 중에 헷갈렸던 내용을 하나씩 정리하고 있습니다.

<sub>정리 · Heo Do Kyung</sub>

<br>

[![Git](https://img.shields.io/badge/Git-workflow-f05032?style=flat-square&logo=git&logoColor=white)](./docs/git/README.md)
[![Markdown](https://img.shields.io/badge/Markdown-docs-000000?style=flat-square&logo=markdown&logoColor=white)](./docs/markdown/README.md)
[![Markup CSS](https://img.shields.io/badge/Markup%20%2F%20CSS-convention-1572b6?style=flat-square&logo=css3&logoColor=white)](./docs/markup/README.md)
[![Accessibility](https://img.shields.io/badge/Accessibility-WCAG%202.2-0f766e?style=flat-square)](./docs/accessibility/README.md)
[![TypeScript](https://img.shields.io/badge/TypeScript-guide-3178c6?style=flat-square&logo=typescript&logoColor=white)](./docs/typescript/README.md)

</div>

---

## 목차

- [가이드가 필요한 이유](#가이드가-필요한-이유)
- [문서 바로가기](#문서-바로가기)
- [처음 보는 사람을 위한 추천 순서](#처음-보는-사람을-위한-추천-순서)
- [Code Align 실행하기](#code-align-실행하기)
- [저장소 구조](#저장소-구조)
- [문서 작성 기준](#문서-작성-기준)
- [사용 안내](#사용-안내)

---

## 가이드가 필요한 이유

프론트엔드 작업은 화면을 만드는 일에서 끝나지 않습니다.

로컬 폴더를 GitHub에 연결해야 하고, README를 읽기 좋게 정리해야 하고, HTML 구조와 CSS 규칙도 흔들리지 않아야 합니다. 접근성, 타입 안정성, 코드 정리 기준도 작업이 커질수록 중요해집니다.

그래서 이 저장소에는 제가 실제로 작업하면서 다시 확인하고 싶은 기준을 모았습니다.  
완성된 정답이라기보다, 프로젝트를 진행하면서 계속 다듬어 가는 작업 노트에 가깝습니다.

이런 상황에서 다시 열어보기 좋게 구성했습니다.

- GitHub 연결이나 Push 오류가 막힐 때
- README와 문서 구조를 정리해야 할 때
- HTML/CSS 컨벤션을 맞춰야 할 때
- 접근성 기준을 빠르게 점검해야 할 때
- jQuery 코드를 Vanilla JS로 옮겨야 할 때
- TypeScript 타입 설계가 애매할 때
- 코드가 길어져서 리팩터링 기준이 필요할 때

---

## 문서 바로가기

### Git

GitHub 연결, 브랜치, 커밋, Push 오류처럼 실제로 자주 막히는 부분을 중심으로 정리했습니다.

- [Git 가이드](./docs/git/README.md)  
  Git의 전체 흐름과 자주 쓰는 명령어를 한 번에 보는 문서입니다.
- [Git 입문 가이드](./docs/git/beginner.md)  
  `init`, `clone`, `remote`, `push`가 헷갈릴 때 먼저 보면 좋습니다.
- [Git 실무 워크플로우](./docs/git/workflow.md)  
  브랜치, 커밋, Pull Request, merge/rebase 흐름을 정리했습니다.
- [Git 문제 해결 가이드](./docs/git/troubleshooting.md)  
  `fetch first`, 충돌, remote 오류, 잘못 만든 브랜치 같은 문제를 다룹니다.
- [레포지토리 통합 가이드](./docs/git/repository-migration.md)  
  여러 학습용 레포를 하나의 저장소로 모을 때의 기준과 명령어를 정리했습니다.

### 문서 작성

- [Markdown 가이드](./docs/markdown/README.md)  
  README, 문서, 이슈, PR 설명을 읽기 좋게 작성하기 위한 기준입니다.

### 마크업 / 스타일 / 접근성

- [Markup / CSS 가이드](./docs/markup/README.md)  
  HTML 구조, 클래스 네이밍, CSS 작성 순서, 반응형 기준을 정리했습니다.
- [웹 접근성 가이드](./docs/accessibility/README.md)  
  WCAG 2.2와 KWCAG 2.2를 기준으로 화면을 점검하는 문서입니다.
- [UI 가이드](./docs/ui/README.md)  
  버튼, 폼, 모달, 탭, 카드처럼 반복되는 UI 패턴을 정리합니다.

### 코드 품질 / 언어

- [Clean Code 가이드](./docs/clean-code/README.md)  
  시간이 지나도 다시 읽고 고칠 수 있는 코드를 위한 기준입니다.
- [TypeScript 가이드](./docs/typescript/README.md)  
  타입을 많이 쓰기보다, 의도를 안전하게 남기는 방향으로 정리했습니다.
- [jQuery → Vanilla JS 전환 가이드](./docs/javascript/README.md)  
  jQuery로 작성하던 선택자, 이벤트, Ajax, DOM 조작을 순수 JavaScript로 옮기는 방법을 정리했습니다.

### 배포 / 도구

- [GitHub Pages 배포 가이드](./docs/deploy/github-pages.md)  
  저장소 안의 정적 HTML 도구를 GitHub Pages로 실행하는 방법을 정리했습니다.
- [Code Align 문서](./code-align/README.md)  
  HTML, CSS, JavaScript 코드를 정리하는 작은 도구의 사용 방법입니다.

---

## 처음 보는 사람을 위한 추천 순서

처음부터 모든 문서를 읽을 필요는 없습니다. 지금 필요한 것부터 보면 됩니다.

| 지금 필요한 일 | 먼저 볼 문서 |
|---|---|
| GitHub에 프로젝트를 처음 올려야 한다 | [Git 입문 가이드](./docs/git/beginner.md) |
| Fork 앱에서 Push, Pull, Branch가 헷갈린다 | [Git 가이드](./docs/git/README.md) |
| Push가 거절되거나 충돌이 났다 | [Git 문제 해결 가이드](./docs/git/troubleshooting.md) |
| 여러 학습용 레포를 하나로 모으고 싶다 | [Git 레포지토리 통합 가이드](./docs/git/repository-migration.md) |
| 내가 작업한 결과물을 링크로 확인하고 싶다 | [GitHub 배포 가이드](./docs/deploy/github-pages.md) |
| README를 보기 좋게 정리하고 싶다 | [Markdown 가이드](./docs/markdown/README.md) |
| HTML/CSS 컨벤션을 맞추고 싶다 | [Markup / CSS 가이드](./docs/markup/README.md) |
| 접근성 기준을 빠르게 확인하고 싶다 | [웹 접근성 가이드](./docs/accessibility/README.md) |
| jQuery 코드를 순수 JavaScript로 바꾸고 싶다 | [jQuery → Vanilla JS 전환 가이드](./docs/javascript/README.md) |
| 코드가 길어져서 정리 기준이 필요하다 | [Clean Code 가이드](./docs/clean-code/README.md) |
| TypeScript 타입 설계가 헷갈린다 | [TypeScript 가이드](./docs/typescript/README.md) |

---

## Code Align 실행하기

`code-align`은 이 저장소 안에 들어 있는 정적 HTML 도구입니다.

| 목적 | 링크 |
|---|---|
| 웹에서 바로 실행 | [Code Align 실행](https://heodokyung.github.io/frontend-guide/code-align/) |
| 소스 코드 보기 | [code-align/index.html](./code-align/index.html) |

GitHub README에서 `index.html`을 누르면 웹 도구가 실행되는 것이 아니라 소스 파일이 열립니다.  
실제 실행 주소는 GitHub Pages 주소를 사용해야 합니다.

---

## 저장소 구조

```txt
frontend-guide/
├─ README.md
├─ code-align/
│  ├─ README.md
│  └─ index.html
├─ docs/
│  ├─ accessibility/
│  ├─ clean-code/
│  ├─ deploy/
│  ├─ git/
│  ├─ javascript/
│  ├─ markdown/
│  ├─ markup/
│  ├─ typescript/
│  └─ ui/
└─ .nojekyll
```

---

## 문서 작성 기준

이 저장소의 문서는 아래 기준으로 작성합니다.

- 처음 보는 사람도 현재 위치를 알 수 있게 목차를 둡니다.
- 설명은 길게 늘어놓기보다, 실제 상황과 연결합니다.
- 예시는 복사해서 바로 써볼 수 있게 작성합니다.
- 오래된 방식은 가능하면 현재 기준에 맞게 정리합니다.
- 개인적인 기준이더라도, 왜 그렇게 판단했는지 함께 적습니다.
- 문서가 지나치게 딱딱해지지 않도록 실제 작업자의 말투를 유지합니다.

---

## 사용 안내

이 저장소는 제가 작업하면서 정리한 개인 가이드입니다.  
그대로 정답처럼 따르기보다, 프로젝트 상황에 맞게 조정해서 보는 쪽이 좋습니다.

문서와 예시는 계속 수정될 수 있습니다.  
더 나은 기준을 발견하면 기존 문서도 과감하게 고쳐갑니다.
