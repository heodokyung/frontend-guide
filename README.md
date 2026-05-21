# Frontend Guide

> 프론트엔드 개발자가 실무에서 반복적으로 확인하는 Git, Markdown, 마크업, CSS, UI 구현 규칙을 한곳에 정리한 가이드 저장소입니다.

이 저장소는 단순한 명령어 모음이 아니라, **작업을 시작하기 전 어떤 상태인지 판단하고, 어떤 순서로 처리해야 하는지 바로 결정할 수 있게 만드는 실전형 문서 모음**을 목표로 합니다.

---

## 이 저장소가 필요한 이유

프론트엔드 작업은 코드만 잘 작성한다고 끝나지 않습니다.

- Git으로 변경 이력을 안전하게 관리해야 하고
- README와 Markdown 문서를 읽기 쉽게 정리해야 하며
- HTML/마크업 구조와 CSS 작성 규칙을 일관되게 유지해야 하고
- UI 컴포넌트와 화면 구현 기준을 팀이나 개인 프로젝트 안에서 계속 재사용할 수 있어야 합니다.

`frontend-guide`는 이 흐름을 하나의 기준으로 정리하기 위한 저장소입니다.

---

## 문서 바로가기

| 분류 | 문서 | 설명 |
|---|---|---|
| Git | [Git 가이드](./docs/git/README.md) | Git의 기본 개념, 일상 작업 흐름, 문제 해결을 한눈에 보는 시작 문서 |
| Git | [입문 가이드](./docs/git/beginner.md) | Git을 처음 쓰는 사람이 꼭 알아야 할 개념과 첫 업로드 흐름 |
| Git | [실무 워크플로우](./docs/git/workflow.md) | 브랜치, 커밋, Pull Request, merge/rebase, stash, squash 등 실무 흐름 |
| Git | [문제 해결 가이드](./docs/git/troubleshooting.md) | push 거절, 충돌, remote 오류, 잘못된 커밋 등 자주 만나는 문제 해결 |
| Markdown | `docs/markdown/` | README, 문서 구조, 제목/목차/표 작성 규칙 정리 예정 |
| Markup | `docs/markup/` | HTML 구조, 접근성, 클래스 네이밍, 시맨틱 마크업 규칙 정리 예정 |
| CSS | `docs/css/` | CSS 작성 순서, 속성 정렬, 반응형/상태 스타일 규칙 정리 예정 |
| UI | `docs/ui/` | 버튼, 폼, 모달, 탭, 카드 등 UI 패턴 규칙 정리 예정 |
| Tools | `tools/` | CSS 정렬/변환 같은 작은 실무 도구 관리 영역 |

---

## 추천 학습 순서

Git을 처음 접한다면 아래 순서로 읽는 것을 추천합니다.

```txt
1. docs/git/beginner.md
2. docs/git/README.md
3. docs/git/workflow.md
4. docs/git/troubleshooting.md
```

이미 Git을 쓰고 있다면 `docs/git/README.md`에서 상황별 명령어를 먼저 확인하고, 문제가 생겼을 때 `troubleshooting.md`를 보면 됩니다.

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
│  ├─ markup/
│  ├─ css/
│  └─ ui/
├─ tools/
├─ assets/
│  └─ images/
├─ NOTICE.md
└─ LICENSE
```

---

## 운영 원칙

### 1. 문서는 `docs/` 아래에서 관리합니다

문서 성격의 자료는 모두 `docs/` 아래로 모읍니다.

예를 들어 Git, Markdown, 마크업, CSS, UI 컨벤션은 각각 독립된 폴더를 갖습니다.

### 2. 실행 가능한 작은 도구는 `tools/`에 둡니다

CSS 속성 정렬기, 코드 변환기처럼 간단한 도구는 `tools/` 아래에 둡니다.

단, 독립적으로 배포해야 하는 앱 수준의 도구라면 별도 레포지토리로 분리하는 것이 좋습니다.

### 3. 문서는 실무 상황 중심으로 작성합니다

이 저장소의 문서는 사전처럼 모든 개념을 나열하는 것이 아니라, 실제 작업 중 자주 만나는 상황을 기준으로 작성합니다.

좋은 문서의 기준은 다음과 같습니다.

- 지금 어떤 상황인지 판단할 수 있다.
- 바로 실행할 명령어가 있다.
- 위험한 명령어는 주의사항이 함께 있다.
- Fork 같은 GUI 도구를 쓰는 사람도 이해할 수 있다.
- 초보자도 따라 할 수 있지만, 실무자에게도 도움이 된다.

---

## Git 문서 요약

Git 문서는 네 개로 나누어 관리합니다.

### `docs/git/README.md`

Git 문서의 시작점입니다. Git과 GitHub의 차이, 기본 흐름, 자주 쓰는 명령어, 상황별 빠른 처방을 정리합니다.

### `docs/git/beginner.md`

입문자를 위한 문서입니다. `clone`과 `remote add`의 차이, 처음 GitHub에 올리는 흐름, `.gitignore`, SSH/HTTPS, Fork 앱 기준을 설명합니다.

### `docs/git/workflow.md`

실무 작업 흐름 문서입니다. 브랜치 전략, 커밋 메시지, Pull Request, merge/rebase, stash, cherry-pick, squash/fixup, upstream 관리까지 다룹니다.

### `docs/git/troubleshooting.md`

문제 해결 문서입니다. `fetch first`, `non-fast-forward`, 충돌, remote 오류, 잘못 만든 브랜치, 커밋 수정, reset/revert, GitHub에 파일이 안 보이는 문제를 다룹니다.

---

## 이 저장소를 사용하는 방식

개인 프로젝트에서는 작업 전에 이 저장소를 체크리스트처럼 사용합니다.

```txt
작업 전
- git status
- git branch
- git remote -v

작업 중
- 변경 파일 확인
- 필요한 파일만 stage
- 의미 있는 커밋 메시지 작성

작업 후
- push 확인
- GitHub에서 브랜치와 파일 확인
```

팀 프로젝트에서는 프로젝트 README나 Wiki에서 이 저장소의 관련 문서를 링크해 공통 기준으로 사용할 수 있습니다.

---

## 문서 작성 규칙

이 저장소의 문서는 아래 형식을 권장합니다.

```md
# 문서 제목

> 이 문서가 해결하는 문제를 한 문장으로 설명합니다.

## 먼저 결론

가장 중요한 판단 기준을 먼저 적습니다.

## 상황별 가이드

실제 사용자가 만나는 상황을 기준으로 설명합니다.

## 명령어

바로 복사해서 사용할 수 있는 명령어를 제공합니다.

## 주의사항

작업 내용 삭제, 이력 변경, 강제 push 등 위험한 부분을 명확히 표시합니다.
```

---

## 기존 개별 레포지토리 정리 기준

기존에 따로 관리하던 문서형 레포지토리는 이 저장소로 통합하는 것을 권장합니다.

| 기존 자료 성격 | 추천 처리 |
|---|---|
| Git 튜토리얼 | `docs/git/`로 통합 |
| Markdown 가이드 | `docs/markdown/`로 통합 |
| 마크업 컨벤션 | `docs/markup/`로 통합 |
| CSS 정렬/작성 규칙 | `docs/css/`로 통합 |
| 작은 CSS 변환 도구 | `tools/`로 통합 가능 |
| 독립 배포가 필요한 웹앱 | 별도 레포 유지 |

기존 레포지토리는 바로 삭제하기보다 README 상단에 이동 안내를 남긴 뒤, GitHub에서 Archive 처리하는 방식을 추천합니다.

```md
# 안내

이 문서는 아래 저장소로 이동되었습니다.

https://github.com/heodokyung/frontend-guide
```

---

## 라이선스와 출처

외부 자료를 참고해 문서를 재구성한 경우, 원문을 그대로 복사하지 않고 직접 다시 작성합니다. 참고한 자료와 라이선스 정보는 [NOTICE.md](./NOTICE.md)에 남깁니다.

---

## 핵심 결론

`frontend-guide`는 단순한 개인 메모 저장소가 아니라, **프론트엔드 실무를 위한 기준 문서 저장소**입니다.

이 저장소의 목표는 하나입니다.

> 매번 헷갈리는 개발 작업 기준을 한곳에서 빠르게 확인하고, 실수 없이 적용할 수 있게 만드는 것.
