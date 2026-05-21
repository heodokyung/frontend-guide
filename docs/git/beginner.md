# Git 입문 가이드

> Git을 처음 쓰는 사람이 `clone`, `init`, `remote`, `add`, `commit`, `push`를 헷갈리지 않도록 정리한 문서입니다.

이 문서의 목표는 Git의 모든 기능을 설명하는 것이 아닙니다. 처음 Git을 쓰는 사람이 **지금 무엇을 해야 하는지 판단하고, 실수 없이 첫 업로드까지 끝내는 것**이 목표입니다.

---

## 1. Git을 왜 사용할까?

Git은 파일 변경 이력을 관리합니다.

예를 들어 다음을 확인할 수 있습니다.

- 언제 수정했는지
- 어떤 파일이 바뀌었는지
- 왜 바꿨는지
- 이전 버전으로 돌아갈 수 있는지
- 여러 사람이 작업한 내용을 어떻게 합칠지

프론트엔드 프로젝트에서는 특히 다음 상황에서 Git이 필요합니다.

- 포트폴리오 프로젝트를 GitHub에 올릴 때
- Cloudflare Pages, Vercel, Netlify 같은 배포 서비스와 연결할 때
- 작업 전후 상태를 안전하게 남길 때
- 실수했을 때 이전 상태로 돌아갈 때
- 협업하거나 Pull Request를 만들 때

---

## 2. Git, GitHub, Fork 앱 구분하기

| 이름 | 역할 |
|---|---|
| Git | 내 컴퓨터에서 변경 이력을 관리하는 도구 |
| GitHub | Git 저장소를 인터넷에 올려두는 서비스 |
| Fork 앱 | Git 명령어를 버튼과 화면으로 조작할 수 있게 해주는 프로그램 |

쉽게 말하면 다음과 같습니다.

```txt
Git      = 내 컴퓨터의 버전 관리 도구
GitHub   = 인터넷에 있는 저장소
Fork 앱  = Git을 편하게 쓰게 해주는 화면 도구
```

---

## 3. Git의 가장 중요한 흐름

Git은 아래 흐름만 이해하면 입문 단계에서는 충분합니다.

```txt
파일 수정
  ↓
git add
  ↓
git commit
  ↓
git push
```

각 단계의 의미는 다음과 같습니다.

| 단계 | 의미 |
|---|---|
| 파일 수정 | 실제 프로젝트 파일을 수정한 상태 |
| `git add` | 이번 커밋에 넣을 파일을 고르는 단계 |
| `git commit` | 내 컴퓨터 Git에 기록하는 단계 |
| `git push` | GitHub에 업로드하는 단계 |

중요한 점은 이것입니다.

> 파일을 수정해도 GitHub에는 바로 올라가지 않습니다.  
> 반드시 `add → commit → push`를 해야 합니다.

---

## 4. 처음 한 번만 하는 기본 설정

새 컴퓨터에서 Git을 처음 쓴다면 사용자 정보를 설정합니다.

```bash
git config --global user.name "내 이름"
git config --global user.email "내 GitHub 이메일"
```

설정 확인:

```bash
git config --global --list
```

이 이메일은 GitHub 계정 이메일과 맞추는 것을 권장합니다.

---

## 5. 지금 내 상황부터 판단하기

Git 초보자가 가장 많이 헷갈리는 부분은 `clone`을 해야 하는지, 기존 폴더를 연결해야 하는지입니다.

아래 기준으로 판단하세요.

| 상황 | 해야 할 일 |
|---|---|
| GitHub에 있는 프로젝트를 내 PC로 새로 받고 싶다 | `git clone` |
| 이미 내 PC에 작업 폴더가 있다 | `git init` 또는 Fork의 Open Repository |
| 이미 Git 저장소인 로컬 폴더를 GitHub와 연결하고 싶다 | `git remote add origin ...` |
| GitHub에 레포가 아직 없다 | GitHub에서 빈 레포를 만든 뒤 연결 |

핵심은 이겁니다.

> 이미 내 PC에 작업 폴더가 있다면 보통 `clone`이 아닙니다.  
> `clone`은 원격 저장소를 새 폴더로 내려받을 때 사용합니다.

---

## 6. 내 폴더가 Git 저장소인지 확인하기

작업 폴더에서 확인합니다.

```bash
git status
```

정상적인 Git 저장소라면 현재 브랜치와 변경 파일 상태가 나옵니다.

Git 저장소가 아니면 이런 메시지가 나올 수 있습니다.

```txt
fatal: not a git repository
```

그때는 현재 폴더가 맞는지 확인합니다.

Windows PowerShell:

```powershell
Get-Location
Get-ChildItem -Force
```

macOS/Linux:

```bash
pwd
ls -a
```

`.git` 폴더가 있으면 Git 저장소입니다.

---

## 7. GitHub에 레포지토리가 아직 없는 경우

이미 로컬에 프로젝트 폴더가 있고, GitHub에는 아직 레포가 없다면 이 흐름을 사용합니다.

### 7-1. GitHub에서 빈 레포 생성

GitHub에서 새 레포지토리를 만들 때는 이렇게 하는 것을 추천합니다.

```txt
Repository name: my-project
README 추가: 안 함
.gitignore 추가: 안 함
License 추가: 필요할 때만
```

이미 로컬에 파일이 있으므로 GitHub에서 README를 만들지 않는 것이 충돌을 줄이는 방법입니다.

### 7-2. 로컬에서 Git 초기화 후 업로드

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

## 8. GitHub 레포는 이미 있고, 로컬 폴더만 연결하려는 경우

이미 GitHub에 레포가 만들어져 있다면 로컬 폴더에서 다음을 실행합니다.

```bash
cd C:\workspace\my-project

git remote add origin https://github.com/내계정/my-project.git
git remote -v
git push -u origin main
```

이미 `origin`이 있다고 나오면 주소를 바꿉니다.

```bash
git remote set-url origin https://github.com/내계정/my-project.git
git remote -v
git push -u origin main
```

`git remote -v` 결과는 보통 이렇게 보여야 합니다.

```txt
origin  https://github.com/내계정/my-project.git (fetch)
origin  https://github.com/내계정/my-project.git (push)
```

---

## 9. GitHub에 있는 프로젝트를 새로 내려받는 경우

이때만 `clone`을 사용합니다.

```bash
git clone https://github.com/내계정/my-project.git
```

SSH를 사용한다면 다음과 같습니다.

```bash
git clone git@github.com:내계정/my-project.git
```

클론하면 자동으로 `origin`이 등록됩니다.

```bash
git remote -v
```

---

## 10. HTTPS와 SSH 중 무엇을 쓸까?

GitHub 주소는 보통 두 가지 방식으로 사용합니다.

| 방식 | 예시 | 특징 |
|---|---|---|
| HTTPS | `https://github.com/user/repo.git` | 처음 쓰기 쉽지만 인증을 다시 요구할 수 있음 |
| SSH | `git@github.com:user/repo.git` | SSH 키 설정 후 편하게 사용 가능 |

초보자는 HTTPS로 시작해도 괜찮습니다. 다만 자주 push할 예정이라면 SSH 설정을 해두는 것이 편합니다.

remote 주소 변경은 다음처럼 할 수 있습니다.

```bash
git remote set-url origin git@github.com:내계정/my-project.git
```

---

## 11. 첫 커밋 만들기

현재 변경 상태를 확인합니다.

```bash
git status
```

모든 변경 파일을 커밋에 포함하려면:

```bash
git add .
git commit -m "Initial commit"
```

특정 파일만 포함하려면:

```bash
git add README.md package.json
git commit -m "Initial project setup"
```

---

## 12. GitHub에 올리기

처음 push할 때는 보통 `-u` 옵션을 붙입니다.

```bash
git push -u origin main
```

이 명령은 현재 로컬 `main` 브랜치를 GitHub의 `origin/main`과 연결합니다.

이후부터는 간단히 다음만 입력해도 됩니다.

```bash
git push
```

---

## 13. Fork 앱을 쓸 때 기준

Fork 앱에서는 상황별로 이렇게 선택하면 됩니다.

| 상황 | Fork에서 해야 할 일 |
|---|---|
| 이미 로컬에 있는 Git 저장소를 열고 싶다 | `File → Open Repository...` |
| GitHub 저장소를 새 폴더로 받고 싶다 | `File → Clone...` |
| 변경 파일을 커밋에 포함하고 싶다 | 파일 선택 후 `Stage` |
| 커밋하고 싶다 | 메시지 작성 후 `Commit` |
| GitHub에 올리고 싶다 | `Push` |
| GitHub 변경을 가져오고 싶다 | `Fetch` 또는 `Pull` |

주의:

> 이미 작업 중인 로컬 폴더를 GitHub에 연결하는 상황에서는 `Clone`이 아닙니다.  
> Fork에서는 `Open Repository`로 현재 폴더를 열어야 합니다.

---

## 14. `.gitignore`는 왜 필요할까?

`.gitignore`는 Git에 올리지 않을 파일을 정하는 파일입니다.

프론트엔드 프로젝트에서는 보통 아래 파일을 제외합니다.

```gitignore
node_modules/
dist/
build/
.env
.env.local
*.log
.DS_Store
```

특히 절대 올리면 안 되는 파일이 있습니다.

```txt
.env
.env.local
API 키
비밀번호
서비스 계정 키
keystore
개인 인증 파일
```

이미 올라간 파일은 `.gitignore`에 추가해도 자동으로 빠지지 않습니다. 추적에서만 제거하려면 다음처럼 처리합니다.

```bash
git rm --cached .env.local
git rm -r --cached node_modules

git add .gitignore
git commit -m "Update gitignore"
```

---

## 15. 입문자가 자주 하는 실수

### 실수 1. 이미 작업 폴더가 있는데 clone을 다시 한다

`clone`은 새 폴더로 내려받는 기능입니다. 기존 작업 폴더를 연결하려면 `remote add` 또는 Fork의 `Open Repository`를 사용합니다.

### 실수 2. 파일 수정 후 바로 push하려고 한다

push 전에 commit이 필요합니다.

```bash
git add .
git commit -m "작업 내용"
git push
```

### 실수 3. GitHub에 README를 만들어두고 첫 push를 한다

로컬 이력과 GitHub 이력이 달라져서 push가 거절될 수 있습니다.

```bash
git pull origin main --allow-unrelated-histories
git push -u origin main
```

GitHub의 기존 내용이 필요 없고 로컬을 기준으로 덮어써도 된다면 초기 레포에서만 조심스럽게 사용할 수 있습니다.

```bash
git push -u origin main --force-with-lease
```

### 실수 4. 잘못된 이름으로 브랜치를 만든다

예를 들어 `https--github.com/...` 같은 항목이 `Branches` 아래에 있다면 remote가 아니라 잘못 만든 로컬 브랜치일 수 있습니다.

확인:

```bash
git branch
```

삭제:

```bash
git branch -D "https--github.com/내계정/레포명.git"
```

---

## 16. 입문자용 체크리스트

작업 전:

```bash
git status
git branch
git remote -v
```

작업 후:

```bash
git add .
git commit -m "작업 내용"
git push
```

문제가 생겼을 때:

```bash
git status
git log --oneline --graph --decorate --all
git reflog
```

---

## 17. 핵심 결론

입문 단계에서는 Git 명령어를 많이 외울 필요가 없습니다.

먼저 아래 네 가지를 정확히 구분하세요.

```txt
clone  = GitHub 저장소를 새 폴더로 내려받기
init   = 현재 폴더를 Git 저장소로 만들기
remote = 현재 로컬 저장소와 GitHub 저장소를 연결하기
push   = 로컬 커밋을 GitHub에 올리기
```

그리고 매일 쓰는 흐름은 이것으로 충분합니다.

```bash
git status
git add .
git commit -m "작업 내용"
git push
```
