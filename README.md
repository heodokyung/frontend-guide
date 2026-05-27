<div align="center">

# Frontend Guide

프론트엔드 작업을 하면서 반복해서 확인하는 기준을 정리한 저장소입니다.

Git, Markdown, Markup/CSS, 접근성, UI 패턴, 클린 코드, TypeScript, JavaScript 전환까지  
프로젝트와 협업 과정에서 흔들리기 쉬운 기준을 문서로 모아두었습니다.

<sub>정리 · Heo Do Kyung</sub>

<br>

[![Git](https://img.shields.io/badge/Git-workflow-f05032?style=flat-square&logo=git&logoColor=white)](./docs/git/README.md)
[![Markdown](https://img.shields.io/badge/Markdown-docs-000000?style=flat-square&logo=markdown&logoColor=white)](./docs/markdown/README.md)
[![Markup CSS](https://img.shields.io/badge/Markup%20%2F%20CSS-convention-1572b6?style=flat-square&logo=css3&logoColor=white)](./docs/markup/README.md)
[![Accessibility](https://img.shields.io/badge/Accessibility-WCAG%202.2-0f766e?style=flat-square)](./docs/accessibility/README.md)
[![TypeScript](https://img.shields.io/badge/TypeScript-guide-3178c6?style=flat-square&logo=typescript&logoColor=white)](./docs/typescript/README.md)

<br>

<a href="#guide-start">Guide Start</a> ·
<a href="#document-index">Document Index</a> ·
<a href="#code-align">Code Align</a> ·
<a href="#structure">Structure</a> ·
<a href="#rules">Rules</a>

</div>

---

> [!NOTE]
> 이 저장소는 프로젝트를 진행하고 협업하는 과정에서 더 좋은 코드와 일관된 품질 기준을 유지하기 위해 정리한 프론트엔드 가이드입니다.

## Overview

프론트엔드 작업은 화면을 만드는 일에서 끝나지 않습니다.

프로젝트를 GitHub에 연결하고, README를 읽기 좋게 정리하고, HTML 구조와 CSS 규칙을 맞추고, 접근성과 타입 안정성까지 함께 챙겨야 합니다. 작업 규모가 커질수록 기준이 없으면 코드 스타일과 판단 방식이 쉽게 흔들립니다.

이 저장소는 그런 상황에서 다시 꺼내보기 위한 개인 작업 기준입니다. 완성된 정답이라기보다, 실제 작업을 하면서 계속 수정하고 보완하는 문서 저장소에 가깝습니다.

| 이 저장소에서 다루는 것 | 설명 |
|---|---|
| Git / GitHub | 저장소 연결, 브랜치, 커밋, Push 오류, 레포지토리 통합 |
| Markdown / 문서화 | README, 가이드 문서, 이슈와 PR 설명 작성 기준 |
| Markup / CSS / UI | HTML 구조, 클래스 네이밍, CSS 작성 순서, 반복 UI 패턴 |
| 접근성 | WCAG 2.2, KWCAG 2.2 기준의 화면 점검 |
| JavaScript / TypeScript | Vanilla JS 전환, 타입 설계, 코드 안정성 |
| 코드 품질 | 시간이 지나도 읽고 고칠 수 있는 코드 기준 |
| 배포 / 도구 | GitHub Pages 배포, Code Align 정적 도구 |

---

## Guide Start

처음부터 모든 문서를 읽을 필요는 없습니다. 지금 막힌 상황에 맞는 문서부터 확인하면 됩니다.

| 구분 | 지금 필요한 일 | 먼저 볼 문서 |
|---|---|---|
| Git | GitHub에 프로젝트를 처음 올려야 한다 | [Git 입문 가이드](./docs/git/beginner.md) |
| Git | Branch, Commit, Push 흐름이 헷갈린다 | [Git 가이드](./docs/git/README.md) |
| Git | Push가 거절되거나 충돌이 났다 | [Git 문제 해결 가이드](./docs/git/troubleshooting.md) |
| Git | 여러 저장소를 하나로 정리하고 싶다 | [레포지토리 통합 가이드](./docs/git/repository-migration.md) |
| 문서 | README를 보기 좋게 정리하고 싶다 | [Markdown 가이드](./docs/markdown/README.md) |
| 마크업 | HTML/CSS 컨벤션을 맞추고 싶다 | [Markup / CSS 가이드](./docs/markup/README.md) |
| CSS | SCSS를 좀 더 잘 이해하고 싶다 | [Markup / CSS 가이드](./docs/scss/README.md) |
| 접근성 | 접근성 기준을 빠르게 점검하고 싶다 | [웹 접근성 가이드](./docs/accessibility/README.md) |
| 코드 변환 | jQuery 코드를 순수 JavaScript로 바꾸고 싶다 | [jQuery → Vanilla JS 전환 가이드](./docs/javascript/README.md) |
| 타입 | TypeScript 타입 설계가 헷갈린다 | [TypeScript 가이드](./docs/typescript/README.md) |
| 코드 품질 | 좋은 코드란 무엇인지 기준을 잡고 싶다 | [Clean Code 가이드](./docs/clean-code/README.md) |
| 배포 | 정적 HTML 도구를 GitHub Pages로 배포하고 싶다 | [GitHub Pages 배포 가이드](./docs/deploy/github-pages.md) |

---

## Document Index

전체 문서는 주제별로 나누어 관리합니다. 자주 찾는 문서는 `Guide Start`에서 먼저 고르고, 전체 구조를 보고 싶을 때는 아래 목록을 확인합니다.

<details open>
<summary><strong>Git / Repository</strong> — 저장소 연결, 브랜치, 커밋, 오류 해결</summary>

| 문서 | 다루는 내용 |
|---|---|
| [Git 가이드](./docs/git/README.md) | Git 전체 흐름, 자주 쓰는 명령어, 기본 작업 기준 |
| [Git 입문 가이드](./docs/git/beginner.md) | `init`, `clone`, `remote`, `push`가 헷갈릴 때 보는 문서 |
| [Git 실무 워크플로우](./docs/git/workflow.md) | 브랜치, 커밋, Pull Request, merge/rebase 흐름 |
| [Git 문제 해결 가이드](./docs/git/troubleshooting.md) | `fetch first`, 충돌, remote 오류, 브랜치 실수 해결 |
| [레포지토리 통합 가이드](./docs/git/repository-migration.md) | 여러 학습용 레포를 하나로 모을 때의 기준과 명령어 |

</details>

<details open>
<summary><strong>Documentation</strong> — README와 문서 작성 기준</summary>

| 문서 | 다루는 내용 |
|---|---|
| [Markdown 가이드](./docs/markdown/README.md) | README, 문서, 이슈, PR 설명을 읽기 좋게 쓰는 기준 |

</details>

<details open>
<summary><strong>Markup / CSS / UI</strong> — 화면 구조와 반복 UI 패턴</summary>

| 문서 | 다루는 내용 |
|---|---|
| [Markup / CSS 가이드](./docs/markup/README.md) | HTML 구조, 클래스 네이밍, CSS 작성 순서, 반응형 기준 |
| [UI 가이드](./docs/ui/README.md) | 버튼, 폼, 모달, 탭, 카드처럼 반복되는 UI 패턴 |

</details>

<details open>
<summary><strong>Accessibility</strong> — 화면 접근성 점검</summary>

| 문서 | 다루는 내용 |
|---|---|
| [웹 접근성 가이드](./docs/accessibility/README.md) | WCAG 2.2, KWCAG 2.2 기준의 화면 점검 |

</details>

<details open>
<summary><strong>Code Quality / Language</strong> — 코드 품질과 언어별 기준</summary>

| 문서 | 다루는 내용 |
|---|---|
| [Clean Code 가이드](./docs/clean-code/README.md) | 시간이 지나도 다시 읽고 고칠 수 있는 코드 기준 |
| [TypeScript 가이드](./docs/typescript/README.md) | 타입을 많이 쓰기보다 의도를 안전하게 남기는 기준 |
| [jQuery → Vanilla JS 전환 가이드](./docs/javascript/README.md) | 선택자, 이벤트, Ajax, DOM 조작을 순수 JavaScript로 전환하는 방법 |

</details>

<details open>
<summary><strong>Deploy / Tools</strong> — 배포와 작업 보조 도구</summary>

| 문서 | 다루는 내용 |
|---|---|
| [GitHub Pages 배포 가이드](./docs/deploy/github-pages.md) | 정적 HTML 도구를 GitHub Pages로 실행하는 방법 |
| [Code Align 문서](./code-align/README.md) | HTML, CSS, JavaScript 코드를 정리하는 작은 도구의 사용법 |

</details>

---

## Code Align

`code-align`은 이 저장소 안에 포함된 정적 HTML 도구입니다. HTML, CSS, JavaScript 코드를 붙여넣고 간단히 정리하는 용도로 사용합니다.

| 목적 | 링크 |
|---|---|
| 웹에서 바로 실행 | [Code Align 실행](https://heodokyung.github.io/frontend-guide/code-align/) |
| 사용 방법 보기 | [Code Align 문서](./code-align/README.md) |
| 소스 코드 보기 | [code-align/index.html](./code-align/index.html) |

> [!TIP]
> GitHub에서 `index.html`을 클릭하면 웹 도구가 실행되는 것이 아니라 소스 파일이 열립니다. 실제 실행은 GitHub Pages 주소를 사용합니다.

---

## Structure

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

## Rules

이 저장소의 문서는 아래 기준으로 작성합니다.

| 기준 | 설명 |
|---|---|
| 실제 상황 중심 | 추상적인 설명보다 작업 중 마주치는 상황과 연결합니다. |
| 바로 적용 가능 | 명령어, 예시, 체크리스트는 복사해서 써볼 수 있게 작성합니다. |
| 판단 근거 기록 | 개인적인 기준이라도 왜 그렇게 판단했는지 함께 남깁니다. |
| 현재 기준 반영 | 오래된 방식은 그대로 두지 않고, 가능하면 현재 기준에 맞게 고칩니다. |
| 지나친 장식 지양 | 문서의 목적은 꾸미기가 아니라 빠르게 찾고 다시 적용하는 것입니다. |

---

## Related Repositories

| 저장소 | 역할 |
|---|---|
| [frontend-study](https://github.com/heodokyung/frontend-study) | 직접 만들어본 예제와 실험 코드를 모아두는 학습 저장소 |
| [frontend-guide](https://github.com/heodokyung/frontend-guide) | 작업하면서 정리한 기준과 문서를 모아두는 가이드 저장소 |

---

## Note

이 저장소는 정답 모음이 아니라 계속 수정되는 작업 기준입니다.  
프로젝트 상황에 따라 그대로 따르기보다 필요한 부분을 가져와 조정하는 것을 기준으로 합니다.
