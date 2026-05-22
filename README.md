<div align="center">

# Frontend Guide

프론트엔드 작업 중 자주 다시 확인하는 기준을 모아둔 개인 가이드 저장소입니다.

Git, Markdown, Markup/CSS, 접근성, 클린 코드, TypeScript, Vanilla JS 전환처럼  
작업 중에 자주 헷갈리는 기준을 문서로 정리합니다.

<sub>정리 · Heo Do Kyung</sub>

<br>

[![Git](https://img.shields.io/badge/Git-workflow-f05032?style=flat-square&logo=git&logoColor=white)](./docs/git/README.md)
[![Markdown](https://img.shields.io/badge/Markdown-docs-000000?style=flat-square&logo=markdown&logoColor=white)](./docs/markdown/README.md)
[![Markup CSS](https://img.shields.io/badge/Markup%20%2F%20CSS-convention-1572b6?style=flat-square&logo=css3&logoColor=white)](./docs/markup/README.md)
[![Accessibility](https://img.shields.io/badge/Accessibility-WCAG%202.2-0f766e?style=flat-square)](./docs/accessibility/README.md)
[![TypeScript](https://img.shields.io/badge/TypeScript-guide-3178c6?style=flat-square&logo=typescript&logoColor=white)](./docs/typescript/README.md)

<br>

<a href="#quick-start">Quick Start</a> ·
<a href="#guide-map">Guide Map</a> ·
<a href="#code-align">Code Align</a> ·
<a href="#structure">Structure</a> ·
<a href="#rules">Rules</a>

</div>

---

## Overview

> [!NOTE]
> 이 저장소는 정답 모음집이 아니라, 실제 작업 중 반복해서 확인하기 위한 **프론트엔드 작업 기준 노트**입니다.  
> 프로젝트를 진행하면서 기준이 바뀌면 문서도 함께 수정합니다.

<table>
  <tr>
    <td width="33%"><strong>작업 기준</strong><br><sub>Git, 문서, 마크업, CSS, 접근성 기준을 빠르게 확인합니다.</sub></td>
    <td width="33%"><strong>문제 해결</strong><br><sub>Push 오류, 충돌, 배포, README 정리처럼 자주 막히는 상황을 정리합니다.</sub></td>
    <td width="33%"><strong>코드 정리</strong><br><sub>Clean Code, TypeScript, Vanilla JS 전환 기준을 남깁니다.</sub></td>
  </tr>
</table>

---

## Quick Start

처음부터 모든 문서를 볼 필요는 없습니다. 지금 필요한 상황에 맞는 문서부터 확인하면 됩니다.

| 상황 | 먼저 볼 문서 |
|---|---|
| GitHub에 프로젝트를 처음 올려야 한다 | [Git 입문 가이드](./docs/git/beginner.md) |
| Branch, Commit, Push 흐름이 헷갈린다 | [Git 가이드](./docs/git/README.md) |
| Push가 거절되거나 충돌이 났다 | [Git 문제 해결 가이드](./docs/git/troubleshooting.md) |
| 여러 저장소를 하나로 정리하고 싶다 | [레포지토리 통합 가이드](./docs/git/repository-migration.md) |
| README를 보기 좋게 정리하고 싶다 | [Markdown 가이드](./docs/markdown/README.md) |
| HTML/CSS 컨벤션을 맞추고 싶다 | [Markup / CSS 가이드](./docs/markup/README.md) |
| 접근성 기준을 빠르게 점검하고 싶다 | [웹 접근성 가이드](./docs/accessibility/README.md) |
| jQuery 코드를 순수 JavaScript로 바꾸고 싶다 | [jQuery → Vanilla JS 전환 가이드](./docs/javascript/README.md) |
| 코드가 길어져 정리 기준이 필요하다 | [Clean Code 가이드](./docs/clean-code/README.md) |
| TypeScript 타입 설계가 헷갈린다 | [TypeScript 가이드](./docs/typescript/README.md) |
| 정적 HTML 도구를 GitHub Pages로 배포하고 싶다 | [GitHub Pages 배포 가이드](./docs/deploy/github-pages.md) |

---

## Guide Map

아래 표는 이 저장소의 핵심 문서를 주제별로 묶은 문서 지도입니다.

| 분류 | 문서 | 다루는 내용 |
|---|---|---|
| Git | [Git 가이드](./docs/git/README.md) | Git 전체 흐름, 자주 쓰는 명령어, 기본 작업 기준 |
| Git | [Git 입문 가이드](./docs/git/beginner.md) | `init`, `clone`, `remote`, `push`가 헷갈릴 때 보는 문서 |
| Git | [Git 실무 워크플로우](./docs/git/workflow.md) | 브랜치, 커밋, Pull Request, merge/rebase 흐름 |
| Git | [Git 문제 해결 가이드](./docs/git/troubleshooting.md) | `fetch first`, 충돌, remote 오류, 브랜치 실수 해결 |
| Git | [레포지토리 통합 가이드](./docs/git/repository-migration.md) | 여러 학습용 레포를 하나로 모을 때의 기준과 명령어 |
| 문서 | [Markdown 가이드](./docs/markdown/README.md) | README, 문서, 이슈, PR 설명을 읽기 좋게 쓰는 기준 |
| 마크업 | [Markup / CSS 가이드](./docs/markup/README.md) | HTML 구조, 클래스 네이밍, CSS 작성 순서, 반응형 기준 |
| 접근성 | [웹 접근성 가이드](./docs/accessibility/README.md) | WCAG 2.2, KWCAG 2.2 기준의 화면 점검 |
| UI | [UI 가이드](./docs/ui/README.md) | 버튼, 폼, 모달, 탭, 카드처럼 반복되는 UI 패턴 |
| 코드 품질 | [Clean Code 가이드](./docs/clean-code/README.md) | 시간이 지나도 다시 읽고 고칠 수 있는 코드 기준 |
| TypeScript | [TypeScript 가이드](./docs/typescript/README.md) | 타입을 많이 쓰기보다 의도를 안전하게 남기는 기준 |
| JavaScript | [jQuery → Vanilla JS 전환 가이드](./docs/javascript/README.md) | 선택자, 이벤트, Ajax, DOM 조작을 순수 JS로 전환하는 방법 |
| 배포 | [GitHub Pages 배포 가이드](./docs/deploy/github-pages.md) | 정적 HTML 도구를 GitHub Pages로 실행하는 방법 |
| 도구 | [Code Align 문서](./code-align/README.md) | HTML, CSS, JavaScript 코드를 정리하는 작은 도구의 사용법 |

---

## Code Align

`code-align`은 이 저장소 안에 포함된 정적 HTML 도구입니다.  
README에서 `index.html`을 클릭하면 웹 도구가 실행되는 것이 아니라 소스 파일이 열리므로, 실제 사용은 GitHub Pages 주소로 접속해야 합니다.

<table>
  <tr>
    <td width="50%"><strong>웹에서 실행</strong><br><a href="https://heodokyung.github.io/frontend-guide/code-align/">Code Align 실행</a></td>
    <td width="50%"><strong>소스 확인</strong><br><a href="./code-align/index.html">code-align/index.html</a></td>
  </tr>
</table>

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

### 문서 작성 기준

- 처음 보는 사람도 현재 위치를 알 수 있게 문서의 목적을 먼저 적습니다.
- 설명은 길게 늘어놓기보다 실제 상황과 연결합니다.
- 예시는 복사해서 바로 써볼 수 있게 작성합니다.
- 오래된 방식은 가능하면 현재 기준에 맞게 다시 정리합니다.
- 개인적인 기준이더라도 왜 그렇게 판단했는지 함께 적습니다.
- 문서가 지나치게 딱딱해지지 않도록 실제 작업자의 말투를 유지합니다.

### 저장소 관리 기준

- 문서와 예시는 계속 수정될 수 있습니다.
- 더 나은 기준을 발견하면 기존 문서도 과감하게 고칩니다.
- 단, 기준이 바뀐 이유가 있다면 문서 안에 짧게 남깁니다.
- 개인 작업 기준이므로 프로젝트 상황에 맞게 조정해서 사용합니다.

---

## Related

| 저장소 | 역할 |
|---|---|
| [frontend-study](https://github.com/heodokyung/frontend-study) | 직접 만들어본 예제와 실험 코드를 모아둔 학습 저장소 |
| [frontend-guide](https://github.com/heodokyung/frontend-guide) | 작업하면서 다시 확인할 기준과 문서를 정리하는 가이드 저장소 |

---

## Note

이 저장소는 완성된 교과서가 아니라, 프론트엔드 작업을 하며 계속 업데이트하는 개인 가이드입니다.  
실제 프로젝트에서 반복해서 막혔던 부분을 중심으로 정리하고, 필요할 때마다 다시 고쳐갑니다.
