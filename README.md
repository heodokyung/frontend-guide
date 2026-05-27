<div align="center">

# Frontend Guide

프론트엔드 작업 중 자주 다시 확인하게 되는 기준을 모아둔 저장소입니다.

Git, 문서화, HTML/CSS, SCSS, 접근성, UI 패턴, JavaScript, TypeScript처럼  
프로젝트를 만들고 유지보수할 때 반복해서 마주치는 주제를 정리합니다.

<sub>정리 · Heo Do Kyung</sub>

<br>

[![Git](https://img.shields.io/badge/Git-workflow-f05032?style=flat-square&logo=git&logoColor=white)](./docs/git/README.md)
[![Markdown](https://img.shields.io/badge/Markdown-docs-000000?style=flat-square&logo=markdown&logoColor=white)](./docs/markdown/README.md)
[![HTML CSS](https://img.shields.io/badge/HTML%20%2F%20CSS-convention-1572b6?style=flat-square&logo=css3&logoColor=white)](./docs/markup/README.md)
[![SCSS](https://img.shields.io/badge/SCSS-guide-c6538c?style=flat-square&logo=sass&logoColor=white)](./docs/scss/README.md)
[![Accessibility](https://img.shields.io/badge/Accessibility-WCAG%202.2-0f766e?style=flat-square)](./docs/accessibility/README.md)
[![TypeScript](https://img.shields.io/badge/TypeScript-guide-3178c6?style=flat-square&logo=typescript&logoColor=white)](./docs/typescript/README.md)

<br>

<a href="#why">Why</a> ·
<a href="#docs">Docs</a> ·
<a href="#code-align">Code Align</a> ·
<a href="#structure">Structure</a> ·
<a href="#rules">Rules</a>

</div>

---

## Why

프론트엔드 작업은 화면을 구현하는 일만으로 끝나지 않습니다.

저장소를 어떻게 관리할지,  
README를 어떻게 쓸지,  
HTML 구조와 CSS 기준을 어떻게 맞출지,  
접근성과 타입 안정성을 어디까지 챙길지 계속 판단해야 합니다.

작은 기준 차이는 처음에는 크게 보이지 않지만,  
프로젝트가 커질수록 유지보수성과 협업 속도에 직접 영향을 줍니다.

이 저장소는 그때마다 처음부터 다시 고민하지 않기 위해 만든 작업 기준입니다.

---

## Docs

필요한 문서를 빠르게 찾을 수 있도록 주제별로 나누었습니다.  
처음부터 순서대로 읽기보다, 지금 막힌 부분에 맞는 문서부터 보면 됩니다.

### Code Quality
| 문서 | 볼 때 | 내용 |
|---|---|---|
| [Clean Code 가이드](./docs/clean-code/README.md) | 코드 품질 기준을 잡고 싶을 때 | 이름 짓기, 함수 분리, 중복 제거, 유지보수 기준 |

### Git / Repository

| 문서 | 볼 때 | 내용 |
|---|---|---|
| [Git 입문 가이드](./docs/git/beginner.md) | Git을 거의 모를 때 | `init`, `clone`, `remote`, `push` 기본 흐름 |
| [Git 가이드](./docs/git/README.md) | Git 작업 흐름을 다시 잡고 싶을 때 | 브랜치, 커밋, push, pull 기본 기준 |
| [Git 실무 워크플로우](./docs/git/workflow.md) | 협업 흐름이 필요할 때 | 브랜치 전략, PR, merge/rebase 흐름 |
| [Git 문제 해결 가이드](./docs/git/troubleshooting.md) | push 거절, 충돌, remote 오류가 났을 때 | 자주 만나는 Git 오류와 해결 방법 |
| [레포지토리 통합 가이드](./docs/git/repository-migration.md) | 여러 저장소를 하나로 합칠 때 | 레포지토리 정리 기준과 이전 방법 |

### Documentation

| 문서 | 볼 때 | 내용 |
|---|---|---|
| [Markdown 가이드](./docs/markdown/README.md) | README나 문서를 정리할 때 | 제목, 표, 코드블록, 링크, 문서 구조 작성 기준 |

### Markup / Styling / UI

| 문서 | 볼 때 | 내용 |
|---|---|---|
| [Markup / CSS 가이드](./docs/markup/README.md) | HTML/CSS 기준이 필요할 때 | HTML 구조, 클래스 네이밍, CSS 작성 순서 |
| [SCSS 가이드](./docs/scss/README.md) | SCSS를 제대로 정리하고 싶을 때 | SCSS와 Sass 차이, 변수, 중첩, mixin, 파일 구조 |
| [UI 가이드](./docs/ui/README.md) | 반복 UI 기준이 필요할 때 | 버튼, 폼, 모달, 탭, 카드 패턴 |

### Accessibility

| 문서 | 볼 때 | 내용 |
|---|---|---|
| [웹 접근성 가이드](./docs/accessibility/README.md) | 접근성 점검이 필요할 때 | WCAG 2.2, KWCAG 2.2 기준의 화면 점검 |

### Script
| 문서 | 볼 때 | 내용 |
|---|---|---|
| [Clean Code 가이드](./docs/clean-code/README.md) | 코드 품질 기준을 잡고 싶을 때 | 이름 짓기, 함수 분리, 중복 제거, 유지보수 기준 |
| [TypeScript 가이드](./docs/typescript/README.md) | 타입 설계가 헷갈릴 때 | 타입을 안전하게 설계하고 사용하는 기준 |
| [jQuery → Vanilla JS 전환 가이드](./docs/javascript/README.md) | jQuery 코드를 걷어내고 싶을 때 | 선택자, 이벤트, Ajax, DOM 조작 전환 방법 |

### Deploy / Tools

| 문서 | 볼 때 | 내용 |
|---|---|---|
| [GitHub Pages 배포 가이드](./docs/deploy/github-pages.md) | 정적 페이지를 배포할 때 | GitHub Pages 설정, 배포 경로, 실행 주소 |
| [Code Align 문서](./code-align/README.md) | 코드 정리 도구 사용법이 필요할 때 | HTML, CSS, JavaScript 코드 정리 도구 사용법 |

---

## Code Align

`code-align`은 HTML, CSS, JavaScript 코드를 빠르게 정리해보기 위해 만든 작은 정적 도구입니다.

| 목적 | 링크 |
|---|---|
| 웹에서 실행 | [Code Align 실행](https://heodokyung.github.io/frontend-guide/code-align/) |
| 사용 방법 | [Code Align 문서](./code-align/README.md) |
| 소스 코드 | [code-align/index.html](./code-align/index.html) |

> [!TIP]
> GitHub에서 `index.html`을 클릭하면 실행 화면이 아니라 소스 코드가 열립니다.  
> 실제 도구는 GitHub Pages 주소에서 사용할 수 있습니다.

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
│  ├─ scss/
│  ├─ typescript/
│  └─ ui/
└─ .nojekyll
