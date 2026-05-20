# Git 실전 가이드

> 처음 Git을 시작하는 사람도, 이미 로컬 폴더를 만들어 둔 사람도, Fork 같은 GUI 도구를 쓰는 사람도 바로 따라 할 수 있도록 정리한 실전형 Git 가이드입니다.

---

## 0. 이 문서의 목적

Git 명령어를 단순히 외우는 것이 아니라, **지금 내가 어떤 상태인지 판단하고 다음 명령을 정확히 선택하는 것**이 목표입니다.

이 문서는 다음 두 종류의 자료를 통합해 다시 구성했습니다.

- Git의 개념과 흐름을 설명하는 입문형 튜토리얼
- 자주 쓰는 Git 명령어를 모아 둔 치트시트형 문서

기존 자료의 장점은 살리고, 실제 작업 중 자주 막히는 부분을 기준으로 다시 정리했습니다.

---

## 1. Git과 GitHub를 먼저 구분하기

### Git

Git은 내 컴퓨터 안에서 파일 변경 이력을 관리하는 도구입니다.

예를 들어 다음을 기록합니다.

- 누가 수정했는지
- 언제 수정했는지
- 어떤 파일이 바뀌었는지
- 왜 바꿨는지
- 예전 버전으로 돌아갈 수 있는지

### GitHub

GitHub는 Git 저장소를 인터넷에 올려두는 서비스입니다.

쉽게 말하면 다음처럼 구분하면 됩니다.

| 구분 | 역할 |
|---|---|
| Git | 내 컴퓨터에서 버전 관리 |
| GitHub | 온라인 저장소, 백업, 협업, 포트폴리오 공개 |
| Fork 앱 | Git 명령어를 화면으로 조작하게 해주는 GUI 프로그램 |

GitHub에 올리지 않아도 Git은 사용할 수 있습니다. 하지만 협업, 백업, 포트폴리오 공개를 하려면 GitHub 같은 원격 저장소가 필요합니다.

---

## 2. Git의 가장 중요한 4단계

Git은 아래 흐름만 이해하면 절반 이상은 끝입니다.

```txt
작업 폴더
  ↓ git add
Staging Area
  ↓ git commit
Local Repository
  ↓ git push
Remote Repository, 예: GitHub
```

| 단계 | 의미 | 대표 명령어 | Fork 앱에서는 |
|---|---|---|---|
| 작업 | 파일을 수정한 상태 | - | Local Changes |
| 스테이징 | 커밋할 파일을 고른 상태 | `git add .` | Stage |
| 커밋 | 내 컴퓨터 Git에 기록 | `git commit -m "메시지"` | Commit |
| 푸시 | GitHub에 업로드 | `git push` | Push |

핵심은 이것입니다.

> 파일을 수정했다고 바로 GitHub에 올라가는 것이 아닙니다.  
> `add → commit → push` 순서가 필요합니다.

---

## 3. 처음 한 번만 하는 기본 설정

새 컴퓨터에서 Git을 처음 쓴다면 사용자 이름과 이메일을 설정합니다.

```bash
git config --global user.name "내 이름"
git config --global user.email "내 GitHub 이메일"
```

설정 확인:

```bash
git config --global --list
```

---

## 4. 지금 내 상황부터 판단하기

Git에서 가장 많이 헷갈리는 부분은 `clone`을 해야 하는지, 기존 폴더를 연결해야 하는지입니다.

아래 기준으로 판단하세요.

| 상황 | 해야 할 일 | 쓰는 명령/기능 |
|---|---|---|
| GitHub에 있는 프로젝트를 내 PC로 새로 받고 싶다 | 새 폴더로 내려받기 | `git clone` |
| 이미 내 PC에 작업 폴더가 있다 | 그 폴더를 Git 저장소로 열기 | Fork: Open Repository |
| 이미 내 PC에 작업 폴더가 있고 GitHub 레포와 연결하고 싶다 | remote 연결 | `git remote add origin ...` |
| GitHub에 아직 레포가 없다 | GitHub에서 빈 레포 생성 후 연결 | `git remote add origin ...` |

중요합니다.

> 이미 작업 중인 로컬 폴더가 있다면 보통 `clone`이 아닙니다.  
> `clone`은 GitHub 저장소를 새 폴더로 다시 내려받을 때 사용합니다.

---

## 5. 새 프로젝트를 GitHub에 올리는 가장 기본 흐름

### 5-1. GitHub에 레포지토리가 아직 없는 경우

먼저 GitHub에서 새 저장소를 만듭니다.

권장 설정:

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

### 5-2. GitHub 레포지토리는 이미 있고, 로컬 폴더를 연결하려는 경우

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

### 5-3. Push가 `fetch first`로 거절되는 경우

GitHub 쪽에 이미 README나 기존 커밋이 있어서 생기는 상황입니다.

안전하게 합치려면:

```bash
git pull origin main --allow-unrelated-histories
git push -u origin main
```

GitHub에 있는 기존 내용이 필요 없고, 로컬 내용을 기준으로 덮어써도 된다면:

```bash
git push -u origin main --force-with-lease
```

단, `--force-with-lease`는 원격 저장소의 기존 이력을 바꿀 수 있으므로 혼자 쓰는 초기 레포에서만 조심해서 사용하세요.

---

## 6. GitHub 저장소를 새로 내려받는 경우

GitHub에 이미 있는 저장소를 내 컴퓨터에 새로 받을 때만 `clone`을 사용합니다.

```bash
git clone https://github.com/내계정/my-project.git
```

SSH를 사용한다면:

```bash
git clone git@github.com:내계정/my-project.git
```

클론한 폴더에는 자동으로 `origin` remote가 등록됩니다.

확인:

```bash
git remote -v
```

---

## 7. 매일 사용하는 기본 작업 흐름

가장 안전한 일상 루틴입니다.

```bash
# 1. 현재 상태 확인
git status

# 2. 원격 변경 사항 확인
git fetch origin

# 3. 최신 내용 반영
git pull origin main

# 4. 작업 후 변경 파일 확인
git status

# 5. 커밋할 파일 추가
git add .

# 6. 커밋
git commit -m "작업 내용 요약"

# 7. GitHub에 업로드
git push
```

Fork 앱 기준으로는 다음과 같습니다.

```txt
Fetch → Pull → 파일 수정 → Stage → Commit → Push
```

---

## 8. 자주 쓰는 명령어 치트시트

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

## 9. 브랜치 사용법

브랜치는 작업을 분리하기 위한 가지입니다.

예를 들어 `main`은 안정적인 기준 브랜치로 두고, 새로운 기능은 별도 브랜치에서 작업합니다.

### 브랜치 목록 보기

```bash
git branch
```

### 새 브랜치 만들고 이동

권장 명령어:

```bash
git switch -c feature/login
```

예전 방식:

```bash
git checkout -b feature/login
```

### 브랜치 이동

```bash
git switch main
```

### 브랜치 삭제

로컬 브랜치 삭제:

```bash
git branch -d feature/login
```

강제 삭제:

```bash
git branch -D feature/login
```

원격 브랜치 삭제:

```bash
git push origin --delete feature/login
```

---

## 10. 협업할 때 추천 흐름

혼자 작업할 때도 이 흐름을 쓰면 안전합니다.

```bash
# main 최신화
git switch main
git pull origin main

# 작업 브랜치 생성
git switch -c feature/header-ui

# 작업 후 커밋
git add .
git commit -m "헤더 UI 개선"

# 원격에 브랜치 올리기
git push -u origin feature/header-ui
```

그 후 GitHub에서 Pull Request를 만들고, 검토 후 `main`에 병합합니다.

작은 개인 프로젝트라면 바로 `main`에 커밋해도 되지만, 포트폴리오나 협업 프로젝트라면 브랜치를 나누는 습관이 좋습니다.

---

## 11. Pull과 Fetch 차이

| 명령어 | 의미 |
|---|---|
| `git fetch` | 원격 변경 사항을 가져오기만 함. 내 작업 파일은 건드리지 않음 |
| `git pull` | 원격 변경 사항을 가져오고 현재 브랜치에 합침 |

불안할 때는 먼저 fetch를 합니다.

```bash
git fetch origin
```

그다음 로그를 보고 판단할 수 있습니다.

```bash
git log --oneline --graph --decorate --all
```

---

## 12. Merge와 Rebase

### Merge

두 브랜치의 이력을 합칩니다.

```bash
git switch main
git merge feature/login
```

장점:

- 이력이 안전하게 남습니다.
- 협업 중인 브랜치에 적합합니다.

단점:

- merge commit이 생겨 이력이 복잡해질 수 있습니다.

### Rebase

내 브랜치의 시작점을 최신 main 뒤로 옮깁니다.

```bash
git switch feature/login
git rebase main
```

장점:

- 이력이 깔끔해집니다.

주의:

- 이미 다른 사람과 공유한 브랜치에서는 함부로 rebase하지 않는 것이 좋습니다.

기본 원칙:

> 혼자 쓰는 작업 브랜치는 rebase 가능.  
> 여러 사람이 같이 쓰는 브랜치는 merge가 더 안전합니다.

---

## 13. 충돌이 났을 때 해결하는 법

충돌은 같은 파일의 같은 부분을 서로 다르게 수정했을 때 발생합니다.

충돌 파일에는 이런 표시가 생깁니다.

```txt
<<<<<<< HEAD
내 현재 브랜치 내용
=======
상대 브랜치 내용
>>>>>>> feature/login
```

해결 순서:

```bash
# 1. 충돌 파일 확인
git status

# 2. 파일을 직접 열어서 남길 내용만 정리
# <<<<<<<, =======, >>>>>>> 표시 제거

# 3. 해결 완료 표시
git add .

# 4-A. merge 중이었다면
git commit

# 4-B. rebase 중이었다면
git rebase --continue
```

충돌 해결 중 되돌리고 싶다면:

```bash
# merge 취소
git merge --abort

# rebase 취소
git rebase --abort
```

---

## 14. 실수했을 때 복구 가이드

Git은 실수했을 때 어떤 단계인지에 따라 명령어가 달라집니다.

### 14-1. 아직 add 하지 않은 파일 변경을 취소하고 싶다

특정 파일 취소:

```bash
git restore src/App.vue
```

전체 취소:

```bash
git restore .
```

주의: 작업 내용이 사라집니다.

### 14-2. add 한 파일을 스테이징에서 내리고 싶다

```bash
git restore --staged src/App.vue
```

전체 내리기:

```bash
git restore --staged .
```

### 14-3. 방금 만든 커밋 메시지를 고치고 싶다

아직 push 전이면:

```bash
git commit --amend -m "새 커밋 메시지"
```

이미 push 했다면 이력이 바뀌므로:

```bash
git push --force-with-lease
```

단, 협업 브랜치에서는 주의해야 합니다.

### 14-4. 마지막 커밋을 취소하되 파일은 남기고 싶다

```bash
git reset --soft HEAD~1
```

커밋만 취소되고 변경 파일은 staged 상태로 남습니다.

### 14-5. 마지막 커밋을 취소하고 staging도 풀고 싶다

```bash
git reset --mixed HEAD~1
```

파일 내용은 남지만 staged 상태는 풀립니다.

### 14-6. 마지막 커밋과 작업 내용까지 모두 버리고 싶다

```bash
git reset --hard HEAD~1
```

주의: 작업 내용이 사라집니다.

### 14-7. 이미 push한 커밋을 안전하게 되돌리고 싶다

협업 중인 브랜치에서는 `reset`보다 `revert`가 안전합니다.

```bash
git revert HEAD
```

`revert`는 기존 이력을 지우지 않고, 되돌리는 새 커밋을 만듭니다.

---

## 15. Reflog: 잃어버린 커밋 찾기

실수로 reset을 했거나 브랜치를 잘못 움직였을 때는 `reflog`를 확인합니다.

```bash
git reflog
```

원하는 시점의 해시를 찾은 뒤:

```bash
git reset --hard 커밋해시
```

또는 안전하게 브랜치로 살릴 수 있습니다.

```bash
git switch -c rescue/backup 커밋해시
```

---

## 16. Stash: 작업 중 잠시 저장하기

아직 커밋하기 애매한 작업을 잠시 치워둘 때 사용합니다.

```bash
git stash
```

메시지를 붙이고 싶다면:

```bash
git stash push -m "헤더 수정 중"
```

목록 보기:

```bash
git stash list
```

다시 꺼내기:

```bash
git stash pop
```

꺼내되 stash 목록에 남기기:

```bash
git stash apply
```

---

## 17. Cherry-pick: 다른 브랜치의 특정 커밋만 가져오기

특정 커밋 하나만 현재 브랜치에 적용하고 싶을 때 사용합니다.

```bash
git cherry-pick 커밋해시
```

예시:

```bash
git switch main
git cherry-pick a1b2c3d
```

---

## 18. 커밋 정리: Squash와 Fixup

작업하다 보면 커밋이 너무 자잘해질 수 있습니다.

예:

```txt
로그인 UI 작업
오타 수정
다시 수정
버튼 색 수정
콘솔 삭제
```

이럴 때 커밋을 하나로 합칠 수 있습니다.

```bash
git rebase -i HEAD~5
```

편집 화면에서 기준 커밋은 `pick`, 합칠 커밋은 `squash` 또는 `fixup`으로 바꿉니다.

더 깔끔하게 fixup 커밋을 만들 수도 있습니다.

```bash
git commit --fixup 커밋해시
git rebase -i --autosquash 커밋해시^ 
```

원칙:

> push 전 커밋 정리는 좋습니다.  
> 이미 공유한 커밋을 정리할 때는 반드시 주의해야 합니다.

---

## 19. Fork 앱 기준 명령어 대응표

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

Fork에서 특히 주의할 점:

- 이미 로컬 작업 폴더가 있다면 `Clone`이 아니라 `Open Repository`입니다.
- 왼쪽 `Branches` 아래에 이상한 `https--github.com/...` 같은 항목이 있으면 원격이 아니라 잘못 만들어진 로컬 브랜치일 가능성이 높습니다.
- `Remotes > origin`이 진짜 GitHub 연결입니다.

---

## 20. .gitignore 기본 예시

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

추적에서만 제거하려면:

```bash
git rm --cached .env.local
```

폴더라면:

```bash
git rm -r --cached node_modules
```

그 후 커밋합니다.

```bash
git add .gitignore
git commit -m "Update gitignore"
```

---

## 21. 원격 저장소와 upstream

내가 다른 사람 저장소를 fork해서 작업할 때는 보통 remote가 두 개가 됩니다.

| 이름 | 의미 |
|---|---|
| origin | 내 GitHub 저장소 |
| upstream | 원본 저장소 |

upstream 추가:

```bash
git remote add upstream https://github.com/원본계정/원본저장소.git
```

확인:

```bash
git remote -v
```

원본 저장소 최신 내용 가져오기:

```bash
git fetch upstream
git switch main
git merge upstream/main
```

또는 rebase 방식:

```bash
git fetch upstream
git switch main
git rebase upstream/main
```

내 저장소에도 반영:

```bash
git push origin main
```

---

## 22. 자주 만나는 오류와 해결

### 22-1. `fatal: not a git repository`

현재 폴더가 Git 저장소가 아닙니다.

확인:

```bash
pwd
ls -a
```

Windows PowerShell:

```powershell
Get-Location
Get-ChildItem -Force
```

`.git` 폴더가 없다면 Git 저장소가 아닙니다.

### 22-2. `remote origin already exists`

이미 origin이 있습니다.

```bash
git remote -v
```

주소만 바꾸려면:

```bash
git remote set-url origin https://github.com/내계정/my-project.git
```

### 22-3. `rejected - fetch first`

원격 저장소에 내 로컬에 없는 커밋이 있습니다.

```bash
git pull origin main
```

서로 완전히 다른 이력이라면:

```bash
git pull origin main --allow-unrelated-histories
```

### 22-4. `non-fast-forward`

원격 이력과 로컬 이력이 맞지 않습니다.

먼저 원격 변경을 가져와 합치는 것이 기본입니다.

```bash
git pull --rebase origin main
```

그 후:

```bash
git push
```

### 22-5. push했는데 GitHub에 파일이 안 보인다

대부분 아래 중 하나입니다.

- `git add`를 안 했다.
- `git commit`을 안 했다.
- 다른 브랜치에 push했다.
- 다른 remote에 push했다.
- GitHub에서 보고 있는 브랜치가 다르다.

확인:

```bash
git status
git branch
git remote -v
git log --oneline -5
```

---

## 23. 위험한 명령어 주의표

| 명령어 | 위험한 이유 | 대안/주의 |
|---|---|---|
| `git reset --hard` | 작업 내용이 사라짐 | 실행 전 `git status` 확인 |
| `git clean -fd` | 추적되지 않은 파일 삭제 | 먼저 `git clean -fdn`으로 미리보기 |
| `git push -f` | 원격 이력 강제 덮어쓰기 | `git push --force-with-lease` 사용 |
| `git add . -f` | ignore한 파일까지 강제 추가 가능 | 필요한 파일만 `git add -f 파일명` |
| `git rebase` | 이력을 다시 씀 | 공유 브랜치에서는 주의 |

---

## 24. 실제 상황별 빠른 처방

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

## 25. 추천 커밋 메시지 규칙

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

처음부터 완벽할 필요는 없습니다. 다만 “수정”, “작업”, “테스트”만 반복하는 커밋은 나중에 추적하기 어렵습니다.

---

## 26. 이 가이드의 핵심 결론

Git은 명령어를 많이 아는 것보다 **상태 판단**이 중요합니다.

작업 전에 확인할 것:

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

문제가 생기면 바로 강제 명령을 쓰지 말고, 먼저 상태를 확인합니다.

```bash
git status
git log --oneline --graph --decorate --all
git reflog
```

Git을 잘 쓴다는 것은 모든 명령어를 외우는 것이 아니라, **지금 내 파일이 작업 중인지, staged인지, commit됐는지, GitHub에 올라갔는지 구분하는 것**입니다.

---

## 부록 A. 통합 가이드 레포 추천 구조

문서형 가이드를 하나로 관리하려면 다음 구조를 추천합니다.

```txt
guide/
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
│  └─ css/
│     ├─ convention.md
│     └─ sorting.md
├─ tools/
│  └─ css-aligner/
│     ├─ README.md
│     └─ src 또는 index.html
├─ assets/
│  └─ images/
├─ LICENSE
└─ NOTICE.md
```

### 운영 원칙

- 문서 성격의 자료는 `docs/` 아래로 모읍니다.
- 실제로 실행되는 작은 도구는 `tools/` 아래에 둡니다.
- 독립 배포가 필요한 앱 수준의 도구는 별도 레포로 유지합니다.
- 기존 레포는 삭제보다 archive 처리 후 새 가이드 레포로 이동 안내를 남깁니다.

### README 첫 화면 구성 추천

```md
# 개발 실무 가이드

프론트엔드 작업에서 반복적으로 확인하는 Git, Markdown, 마크업, CSS 컨벤션을 정리한 개인 가이드 저장소입니다.

## 문서

- Git 실전 가이드
- Markdown 작성 가이드
- 마크업 컨벤션
- CSS 정렬 및 작성 규칙

## 도구

- CSS 코드 정렬 도구
```

---

## 부록 B. 외부 자료를 통합할 때 라이선스 주의

외부 GitHub 자료를 내 저장소에 통합할 때는 반드시 라이선스를 확인해야 합니다.

권장 방식:

- 문장을 그대로 복사하기보다 내 말로 재작성합니다.
- 참고한 저장소의 이름, 원저자, 라이선스를 `NOTICE.md`에 남깁니다.
- 원본 LICENSE 파일이 요구하는 조건을 지킵니다.
- 이미지 링크나 외부 CDN이 오래되어 깨질 수 있으므로 가능하면 직접 만든 이미지로 대체합니다.

예시:

```md
# NOTICE

이 저장소의 Git 가이드는 다음 공개 자료를 참고하여 재구성했습니다.

- Minimal_Git_command: MIT License
- tutorial-git: 저장소 내 License 및 README의 라이선스 고지 확인 필요

본문은 원문을 그대로 복사하지 않고, 개인 학습용/실무용 문서로 재작성했습니다.
```
