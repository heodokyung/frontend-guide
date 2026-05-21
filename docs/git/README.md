# Git 가이드

> Git을 처음 쓰는 사람도, Fork 같은 GUI 도구를 쓰는 사람도, 이미 로컬 폴더를 만들어 둔 사람도 바로 따라 할 수 있도록 정리한 실전형 Git 시작 문서입니다.

이 문서는 Git 명령어를 단순히 외우기 위한 문서가 아닙니다. 핵심은 **지금 내가 어떤 상태인지 판단하고, 다음 명령을 정확히 선택하는 것**입니다.

---

## 목차

- [먼저 이것만 기억하세요](#먼저-이것만-기억하세요)
- [Git 문서 구성](#git-문서-구성)
- [Git과 GitHub는 다릅니다](#git과-github는-다릅니다)
- [작업 전 반드시 확인할 3개 명령어](#작업-전-반드시-확인할-3개-명령어)
- [상황별로 무엇을 해야 할까?](#상황별로-무엇을-해야-할까)
- [새 프로젝트를 GitHub에 처음 올리기](#새-프로젝트를-github에-처음-올리기)
- [이미 있는 GitHub 레포에 로컬 폴더 연결하기](#이미-있는-github-레포에-로컬-폴더-연결하기)
- [GitHub 저장소를 새로 내려받기](#github-저장소를-새로-내려받기)
- [매일 사용하는 기본 작업 흐름](#매일-사용하는-기본-작업-흐름)
- [자주 쓰는 명령어 치트시트](#자주-쓰는-명령어-치트시트)
- [Fork 앱 기준 명령어 대응표](#fork-앱-기준-명령어-대응표)
- [최소 `.gitignore` 예시](#최소-gitignore-예시)
- [위험한 명령어 주의표](#위험한-명령어-주의표)
- [실제 상황별 빠른 처방](#실제-상황별-빠른-처방)
- [커밋 메시지 추천 규칙](#커밋-메시지-추천-규칙)
- [핵심 결론](#핵심-결론)

## 먼저 이것만 기억하세요

Git 작업의 기본 흐름은 아래 네 단계입니다.

```txt
작업 폴더
  ↓ git add
Staging Area
  ↓ git commit
Local Repository
  ↓ git push
Remote Repository, 예: GitHub
```

| 단계 | 의미 | 명령어 | Fork 앱에서는 |
|---|---|---|---|
| 작업 | 파일을 수정한 상태 | - | Local Changes |
| 스테이징 | 커밋할 파일을 고른 상태 | `git add .` | Stage |
| 커밋 | 내 컴퓨터 Git에 기록 | `git commit -m "메시지"` | Commit |
| 푸시 | GitHub에 업로드 | `git push` | Push |

파일을 수정했다고 바로 GitHub에 올라가지 않습니다. 반드시 `add → commit → push` 순서를 거쳐야 합니다.

---

## Git 문서 구성

| 문서 | 언제 보면 좋은가 |
|---|---|
| [beginner.md](./beginner.md) | Git을 처음 시작하거나, `clone`과 `remote`가 헷갈릴 때 |
| [workflow.md](./workflow.md) | 브랜치, 커밋, Pull Request, merge/rebase 같은 실무 흐름이 필요할 때 |
| [troubleshooting.md](./troubleshooting.md) | push 오류, 충돌, remote 오류, 잘못된 커밋을 해결해야 할 때 |
| [repository-migration.md](./repository-migration.md) | 여러 학습용 레포를 하나로 모으거나 기존 레포를 정리할 때 |

---

## Git과 GitHub는 다릅니다

| 구분 | 역할 |
|---|---|
| Git | 내 컴퓨터에서 파일 변경 이력을 관리하는 도구 |
| GitHub | Git 저장소를 인터넷에 올려두는 서비스 |
| Fork 앱 | Git 명령어를 화면으로 조작하게 해주는 GUI 프로그램 |

GitHub에 올리지 않아도 Git은 사용할 수 있습니다. 다만 협업, 백업, 포트폴리오 공개를 하려면 GitHub 같은 원격 저장소가 필요합니다.

---

## 작업 전 반드시 확인할 3개 명령어

문제가 생겼을 때도, 작업을 시작할 때도 가장 먼저 아래 세 가지를 확인합니다.

```bash
git status
git branch
git remote -v
```

각 명령어의 의미는 다음과 같습니다.

| 명령어 | 확인하는 것 |
|---|---|
| `git status` | 현재 변경 파일, staged 여부, 커밋 가능 상태 |
| `git branch` | 현재 내가 어느 브랜치에 있는지 |
| `git remote -v` | GitHub 원격 저장소가 어디로 연결되어 있는지 |

---

## 상황별로 무엇을 해야 할까?

Git에서 가장 자주 헷갈리는 부분은 `clone`을 해야 하는지, 기존 폴더를 연결해야 하는지입니다.

| 상황 | 해야 할 일 | 사용하는 것 |
|---|---|---|
| GitHub에 있는 프로젝트를 내 PC로 새로 받고 싶다 | 새 폴더로 내려받기 | `git clone` |
| 이미 내 PC에 작업 폴더가 있다 | 그 폴더를 Git 저장소로 열기 | Fork: Open Repository |
| 이미 내 PC에 작업 폴더가 있고 GitHub 레포와 연결하고 싶다 | remote 연결 | `git remote add origin ...` |
| GitHub에 아직 레포가 없다 | GitHub에서 빈 레포 생성 후 연결 | `git init`, `git remote add origin ...` |

중요합니다.

> 이미 작업 중인 로컬 폴더가 있다면 보통 `clone`이 아닙니다.  
> `clone`은 GitHub 저장소를 새 폴더로 다시 내려받을 때 사용합니다.

---

## 새 프로젝트를 GitHub에 처음 올리기

GitHub에 아직 레포지토리가 없다면 먼저 GitHub에서 빈 레포를 만듭니다.

권장 설정은 다음과 같습니다.

```txt
Repository name: my-project
README 추가: 안 함
.gitignore 추가: 안 함
License 추가: 필요할 때만
```

이미 로컬에 파일이 있다면 GitHub에서 README를 만들지 않는 것이 충돌을 줄이는 방법입니다.

그다음 로컬 프로젝트 폴더에서 실행합니다.

```bash
cd C:\workspace\my-project

git init
git branch -M main
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/내계정/my-project.git
git push -u origin main
```

---

## 이미 있는 GitHub 레포에 로컬 폴더 연결하기

이미 로컬 작업 폴더가 있고 GitHub 레포도 만들어져 있다면 다음처럼 연결합니다.

```bash
cd C:\workspace\my-project

git remote add origin https://github.com/내계정/my-project.git
git remote -v
git push -u origin main
```

이미 `origin`이 있다고 나오면 주소를 교체합니다.

```bash
git remote set-url origin https://github.com/내계정/my-project.git
git remote -v
git push -u origin main
```

---

## GitHub 저장소를 새로 내려받기

GitHub에 있는 저장소를 내 컴퓨터에 새로 받을 때만 `clone`을 사용합니다.

```bash
git clone https://github.com/내계정/my-project.git
```

SSH를 사용한다면 다음과 같습니다.

```bash
git clone git@github.com:내계정/my-project.git
```

클론한 폴더에는 자동으로 `origin` remote가 등록됩니다.

확인:

```bash
git remote -v
```

---

## 매일 사용하는 기본 작업 흐름

가장 안전한 일상 루틴입니다.

```bash
# 1. 현재 상태 확인
git status

# 2. 원격 변경 사항 가져오기
git pull origin main

# 3. 작업 후 변경 파일 확인
git status

# 4. 커밋할 파일 추가
git add .

# 5. 커밋
git commit -m "작업 내용 요약"

# 6. GitHub에 업로드
git push
```

Fork 앱 기준으로는 다음과 같습니다.

```txt
Fetch 또는 Pull → 파일 수정 → Stage → Commit → Push
```

---

## 자주 쓰는 명령어 치트시트

### 상태 확인

```bash
git status
```

### 변경 내용 확인

```bash
git diff
```

스테이징된 변경 내용 확인:

```bash
git diff --staged
```

### 파일 추가

```bash
git add .
```

특정 파일만 추가:

```bash
git add src/App.vue
```

### 커밋

```bash
git commit -m "메시지"
```

### 커밋 로그 보기

```bash
git log --oneline --graph --decorate --all
```

### 원격 저장소 확인

```bash
git remote -v
```

### 원격 저장소 추가

```bash
git remote add origin https://github.com/내계정/my-project.git
```

### 원격 저장소 주소 변경

```bash
git remote set-url origin https://github.com/내계정/my-project.git
```

### 현재 브랜치 이름을 main으로 변경

```bash
git branch -M main
```

---

## Fork 앱 기준 명령어 대응표

| Fork 앱 버튼/메뉴 | Git 명령어 | 의미 |
|---|---|---|
| Open Repository | - | 기존 로컬 Git 폴더 열기 |
| Clone | `git clone` | GitHub 저장소를 새 폴더로 내려받기 |
| Fetch | `git fetch` | 원격 변경 사항 확인 |
| Pull | `git pull` | 원격 변경 사항 가져와 합치기 |
| Stage | `git add` | 커밋할 파일 선택 |
| Commit | `git commit` | 로컬 이력 기록 |
| Push | `git push` | GitHub에 업로드 |
| Stash | `git stash` | 작업 임시 보관 |
| Branch | `git branch`, `git switch` | 브랜치 생성/이동 |

Fork에서 특히 주의할 점은 두 가지입니다.

- 이미 로컬 작업 폴더가 있다면 `Clone`이 아니라 `Open Repository`입니다.
- 왼쪽 `Branches` 아래에 `https--github.com/...` 같은 항목이 있으면 원격이 아니라 잘못 만들어진 로컬 브랜치일 가능성이 높습니다.

---

## 최소 `.gitignore` 예시

Vue, React, 일반 프론트엔드 프로젝트에서 최소한 아래는 제외하는 것이 좋습니다.

```gitignore
node_modules/
dist/
build/
.env
.env.local
.DS_Store
*.log
npm-debug.log*
yarn-debug.log*
pnpm-debug.log*
.vscode/*
!.vscode/extensions.json
```

이미 Git에 올라간 파일은 `.gitignore`에 추가해도 자동으로 빠지지 않습니다.

추적에서만 제거하려면 다음처럼 처리합니다.

```bash
git rm --cached .env.local
git rm -r --cached node_modules

git add .gitignore
git commit -m "Update gitignore"
```

---

## 위험한 명령어 주의표

| 명령어 | 위험한 이유 | 대안/주의 |
|---|---|---|
| `git reset --hard` | 작업 내용이 사라질 수 있음 | 실행 전 `git status` 확인 |
| `git clean -fd` | 추적되지 않은 파일까지 삭제 | 먼저 `git clean -fdn`으로 미리보기 |
| `git push -f` | 원격 이력을 강제로 덮어씀 | `git push --force-with-lease` 사용 |
| `git add . -f` | ignore한 파일까지 강제 추가 가능 | 필요한 파일만 `git add -f 파일명` |
| `git rebase` | 이력을 다시 씀 | 공유 브랜치에서는 주의 |

---

## 실제 상황별 빠른 처방

### 내 로컬 폴더를 GitHub 새 레포에 처음 올리고 싶다

```bash
git init
git branch -M main
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/내계정/레포명.git
git push -u origin main
```

### remote 주소가 잘못됐다

```bash
git remote -v
git remote set-url origin https://github.com/내계정/레포명.git
git remote -v
```

### GitHub에 README를 만들어서 push가 막혔다

```bash
git pull origin main --allow-unrelated-histories
git push -u origin main
```

### 방금 커밋 메시지만 바꾸고 싶다

```bash
git commit --amend -m "새 메시지"
```

### 아직 커밋 안 한 작업을 버리고 싶다

```bash
git restore .
```

### 커밋은 취소하고 파일은 남기고 싶다

```bash
git reset --soft HEAD~1
```

### 충돌 해결 중인데 포기하고 싶다

```bash
git merge --abort
```

또는:

```bash
git rebase --abort
```

---

## 커밋 메시지 추천 규칙

작은 프로젝트라도 커밋 메시지를 정리하면 나중에 보기 좋습니다.

추천 형식:

```txt
타입: 작업 내용
```

예:

```txt
feat: 로그인 화면 추가
fix: 모바일 헤더 깨짐 수정
docs: Git 가이드 문서 보강
style: CSS 정렬 및 포맷 정리
refactor: 중복 함수 분리
chore: 패키지 설정 정리
```

처음부터 완벽할 필요는 없습니다. 다만 `수정`, `작업`, `테스트`만 반복하는 커밋은 나중에 추적하기 어렵습니다.

---

## 핵심 결론

Git은 명령어를 많이 아는 것보다 **상태 판단**이 중요합니다.

작업 전에 확인할 것은 세 가지입니다.

```bash
git status
git branch
git remote -v
```

일상 작업은 이 흐름으로 충분합니다.

```bash
git pull origin main
git add .
git commit -m "작업 내용"
git push
```

문제가 생기면 바로 강제 명령을 쓰지 말고, 먼저 상태를 확인하세요.

```bash
git status
git log --oneline --graph --decorate --all
git reflog
```
