# Git 문제 해결 가이드

> Git을 쓰다가 자주 만나는 오류와 실수를 상황별로 해결하는 문서입니다.

문제가 생겼을 때 가장 먼저 할 일은 강제 명령을 실행하는 것이 아니라, 현재 상태를 확인하는 것입니다.

```bash
git status
git branch
git remote -v
git log --oneline --graph --decorate --all
```

작업 이력을 잃어버린 것 같다면 다음도 확인합니다.

```bash
git reflog
```

---

## 1. `fatal: not a git repository`

### 의미

현재 폴더가 Git 저장소가 아닙니다.

### 확인

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

`.git` 폴더가 없다면 Git 저장소가 아닙니다.

### 해결

이미 Git 저장소인 다른 폴더가 있다면 그 폴더로 이동합니다.

```bash
cd C:\workspace\my-project
```

현재 폴더를 새 Git 저장소로 만들려면:

```bash
git init
git branch -M main
```

---

## 2. `git remote` 했는데 아무것도 안 나온다

### 의미

현재 폴더는 Git 저장소일 수 있지만, 아직 GitHub 원격 저장소와 연결되지 않았습니다.

### 해결

GitHub 레포 주소를 추가합니다.

```bash
git remote add origin https://github.com/내계정/레포명.git
git remote -v
```

정상 결과:

```txt
origin  https://github.com/내계정/레포명.git (fetch)
origin  https://github.com/내계정/레포명.git (push)
```

---

## 3. `remote origin already exists`

### 의미

이미 `origin`이라는 remote가 등록되어 있습니다.

### 확인

```bash
git remote -v
```

### 해결 1. 주소만 바꾸기

```bash
git remote set-url origin https://github.com/내계정/새레포명.git
git remote -v
```

### 해결 2. origin 삭제 후 다시 추가

```bash
git remote remove origin
git remote add origin https://github.com/내계정/새레포명.git
git remote -v
```

보통은 `set-url`이 더 안전하고 간단합니다.

---

## 4. remote 주소를 잘못 넣었다

예를 들어 `https--github.com/...`처럼 잘못 들어갔다면 주소를 바꿉니다.

```bash
git remote -v
git remote set-url origin https://github.com/내계정/레포명.git
git remote -v
```

정상 주소는 보통 아래 형태입니다.

```txt
https://github.com/내계정/레포명.git
```

또는 SSH 방식:

```txt
git@github.com:내계정/레포명.git
```

---

## 5. Fork 앱의 Branches 아래에 `https--github.com/...`가 생겼다

### 의미

원격 저장소가 아니라, 실수로 잘못 만든 로컬 브랜치일 가능성이 높습니다.

### 확인

```bash
git branch
```

예:

```txt
  https--github.com/heodokyung/vue-portfolio.git
* main
```

### 해결

현재 브랜치가 `main`인지 확인한 뒤 잘못된 브랜치를 삭제합니다.

```bash
git branch -D "https--github.com/heodokyung/vue-portfolio.git"
```

주의:

> `Branches` 아래의 항목은 로컬 브랜치입니다.  
> `Remotes > origin`이 실제 GitHub 원격 저장소 연결입니다.

---

## 6. `rejected - fetch first`

### 의미

GitHub 원격 저장소에 내 로컬에 없는 커밋이 있습니다. 예를 들어 GitHub에서 README를 먼저 만들었을 때 자주 발생합니다.

### 해결 1. 원격 내용을 가져와 합치기

```bash
git pull origin main
```

만약 서로 완전히 다른 이력이라면 다음을 사용합니다.

```bash
git pull origin main --allow-unrelated-histories
```

그 후 push합니다.

```bash
git push -u origin main
```

### 해결 2. 로컬 내용을 기준으로 덮어쓰기

GitHub의 기존 내용이 필요 없고, 혼자 쓰는 초기 레포라면 다음을 사용할 수 있습니다.

```bash
git push -u origin main --force-with-lease
```

주의:

> 강제 push는 원격 이력을 바꿀 수 있습니다.  
> 협업 중인 저장소에서는 신중하게 사용해야 합니다.

---

## 7. `non-fast-forward`

### 의미

원격 브랜치와 로컬 브랜치의 이력이 맞지 않아 바로 push할 수 없습니다.

### 해결

먼저 원격 변경을 가져와 합칩니다.

```bash
git pull --rebase origin main
```

충돌이 없다면 push합니다.

```bash
git push
```

충돌이 나면 파일을 정리한 뒤:

```bash
git add .
git rebase --continue
git push
```

rebase를 포기하려면:

```bash
git rebase --abort
```

---

## 8. 충돌이 발생했다

### 의미

같은 파일의 같은 부분을 서로 다르게 수정했습니다.

충돌 파일에는 이런 표시가 생깁니다.

```txt
<<<<<<< HEAD
내 현재 브랜치 내용
=======
상대 브랜치 내용
>>>>>>> feature/login
```

### 해결 순서

```bash
# 1. 충돌 파일 확인
git status

# 2. 파일을 열어서 남길 내용만 정리
# <<<<<<<, =======, >>>>>>> 표시 제거

# 3. 해결 완료 표시
git add .
```

merge 중이었다면:

```bash
git commit
```

rebase 중이었다면:

```bash
git rebase --continue
```

### 충돌 해결을 포기하고 싶다면

merge 취소:

```bash
git merge --abort
```

rebase 취소:

```bash
git rebase --abort
```

---

## 9. push했는데 GitHub에 파일이 안 보인다

### 가능한 원인

- `git add`를 안 했다.
- `git commit`을 안 했다.
- 다른 브랜치에 push했다.
- 다른 remote에 push했다.
- GitHub에서 보고 있는 브랜치가 다르다.

### 확인

```bash
git status
git branch
git remote -v
git log --oneline -5
```

### 해결

현재 브랜치가 맞는지 확인합니다.

```bash
git branch
```

커밋이 있는지 확인합니다.

```bash
git log --oneline -5
```

원격 주소가 맞는지 확인합니다.

```bash
git remote -v
```

필요하면 올바른 브랜치로 push합니다.

```bash
git push -u origin main
```

---

## 10. 아직 add 하지 않은 변경을 취소하고 싶다

특정 파일 취소:

```bash
git restore src/App.vue
```

전체 취소:

```bash
git restore .
```

주의:

> 작업 내용이 사라집니다. 실행 전 정말 버려도 되는지 확인하세요.

---

## 11. add 한 파일을 staging에서 내리고 싶다

특정 파일만 내리기:

```bash
git restore --staged src/App.vue
```

전체 내리기:

```bash
git restore --staged .
```

파일 내용은 그대로 남고, 커밋 대상에서만 제외됩니다.

---

## 12. 방금 만든 커밋 메시지를 고치고 싶다

아직 push 전이면:

```bash
git commit --amend -m "새 커밋 메시지"
```

이미 push했다면 원격과 이력이 달라졌으므로 다음이 필요할 수 있습니다.

```bash
git push --force-with-lease
```

주의:

> 협업 브랜치에서 이미 push한 커밋을 amend하면 다른 사람에게 영향을 줄 수 있습니다.

---

## 13. 마지막 커밋을 취소하고 싶다

### 커밋만 취소하고 파일은 staged 상태로 남기기

```bash
git reset --soft HEAD~1
```

### 커밋 취소 + staging도 풀기

```bash
git reset --mixed HEAD~1
```

### 커밋과 작업 내용까지 모두 버리기

```bash
git reset --hard HEAD~1
```

주의:

> `reset --hard`는 작업 내용이 사라질 수 있습니다. 실행 전 `git status`를 확인하세요.

---

## 14. 이미 push한 커밋을 안전하게 되돌리고 싶다

협업 중인 브랜치에서는 `reset`보다 `revert`가 안전합니다.

```bash
git revert HEAD
```

`revert`는 기존 이력을 지우지 않고, 되돌리는 새 커밋을 만듭니다.

특정 커밋을 되돌리려면:

```bash
git revert 커밋해시
```

---

## 15. 실수로 reset했거나 커밋을 잃어버린 것 같다

`reflog`를 확인합니다.

```bash
git reflog
```

원하는 시점의 해시를 찾은 뒤 브랜치로 살릴 수 있습니다.

```bash
git switch -c rescue/backup 커밋해시
```

또는 해당 시점으로 되돌릴 수 있습니다.

```bash
git reset --hard 커밋해시
```

주의:

> 바로 `reset --hard`를 하기보다 먼저 rescue 브랜치를 만드는 것이 더 안전합니다.

---

## 16. `.gitignore`에 추가했는데 계속 Git에 잡힌다

### 의미

이미 Git이 추적 중인 파일은 `.gitignore`에 추가해도 자동으로 제외되지 않습니다.

### 해결

추적에서만 제거합니다. 파일 자체는 로컬에 남습니다.

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

## 17. `node_modules`, `dist`, `.env`를 실수로 올렸다

### 해결

`.gitignore`에 제외 규칙을 추가합니다.

```gitignore
node_modules/
dist/
build/
.env
.env.local
```

Git 추적에서 제거합니다.

```bash
git rm -r --cached node_modules
git rm -r --cached dist
git rm --cached .env .env.local
```

커밋합니다.

```bash
git add .gitignore
git commit -m "Remove ignored files from repository"
git push
```

주의:

> 이미 공개 저장소에 비밀 키가 올라갔다면 파일 삭제만으로 충분하지 않습니다. 해당 키를 폐기하고 새로 발급해야 합니다.

---

## 18. 현재 작업 중인데 다른 브랜치로 이동이 안 된다

### 의미

현재 변경 파일 때문에 브랜치 이동 시 덮어쓰기 위험이 있습니다.

### 해결 1. 커밋하기

```bash
git add .
git commit -m "작업 내용 임시 저장"
git switch 다른브랜치
```

### 해결 2. stash 사용

```bash
git stash push -m "작업 임시 저장"
git switch 다른브랜치
```

다시 꺼내기:

```bash
git stash pop
```

---

## 19. 강제로 삭제될 파일을 미리 보고 싶다

추적되지 않은 파일을 삭제하는 명령은 위험합니다.

실제 삭제 전에 미리보기:

```bash
git clean -fdn
```

정말 삭제:

```bash
git clean -fd
```

주의:

> `git clean -fd`는 Git이 추적하지 않는 파일을 삭제합니다.  
> 복구가 어려울 수 있으므로 반드시 `-n`으로 먼저 확인하세요.

---

## 20. 다른 사람 저장소를 fork한 뒤 원본을 따라가고 싶다

### upstream 추가

```bash
git remote add upstream https://github.com/원본계정/원본저장소.git
git remote -v
```

### 원본 최신 내용 가져오기

```bash
git fetch upstream
git switch main
git merge upstream/main
```

내 fork 저장소에도 반영:

```bash
git push origin main
```

---

## 21. GitHub 인증 오류가 난다

### 가능한 원인

- HTTPS 인증 정보가 만료됨
- 비밀번호 대신 토큰이 필요한 상황
- SSH 키가 등록되지 않음
- remote 주소가 HTTPS/SSH 중 원하는 방식과 다름

### 확인

```bash
git remote -v
```

HTTPS에서 SSH로 바꾸려면:

```bash
git remote set-url origin git@github.com:내계정/레포명.git
```

SSH 연결 확인:

```bash
ssh -T git@github.com
```

---

## 22. Windows에서 줄바꿈 때문에 파일이 계속 바뀐 것처럼 보인다

Windows와 macOS/Linux는 줄바꿈 방식이 다를 수 있습니다.

프로젝트에 `.gitattributes`를 두면 안정적입니다.

```gitattributes
* text=auto
*.sh text eol=lf
*.bat text eol=crlf
```

설정 후 전체 파일 정규화가 필요할 수 있습니다.

```bash
git add --renormalize .
git commit -m "Normalize line endings"
```

---

## 23. 파일 이름 대소문자만 바꿨는데 Git이 인식하지 못한다

Windows에서는 대소문자 변경을 Git이 제대로 감지하지 못할 때가 있습니다.

중간 이름을 거쳐 변경합니다.

```bash
git mv component.vue temp-component.vue
git mv temp-component.vue Component.vue
git commit -m "Rename component file"
```

---

## 24. 문제 해결 기본 순서

어떤 오류든 먼저 아래 순서로 접근합니다.

```txt
1. git status로 현재 상태 확인
2. git branch로 현재 브랜치 확인
3. git remote -v로 원격 주소 확인
4. git log --oneline --graph --decorate --all로 이력 확인
5. 오류 메시지를 그대로 읽고 원인 분류
6. 삭제/강제 명령은 마지막에 사용
```

---

## 25. 위험한 명령어 다시 보기

| 명령어 | 위험한 이유 | 먼저 할 일 |
|---|---|---|
| `git reset --hard` | 작업 내용 삭제 가능 | `git status`, 필요하면 브랜치 백업 |
| `git clean -fd` | 추적되지 않은 파일 삭제 | `git clean -fdn`으로 미리보기 |
| `git push -f` | 원격 이력 덮어쓰기 | `git push --force-with-lease` 사용 |
| `git rebase` | 이력 재작성 | 공유 브랜치인지 확인 |
| `git add . -f` | ignore 파일까지 강제 추가 가능 | 필요한 파일만 선택 |

---

## 26. 최종 결론

Git 문제 해결은 명령어 암기가 아니라 상태 판단입니다.

문제가 생기면 먼저 아래 명령어를 실행하세요.

```bash
git status
git branch
git remote -v
git log --oneline --graph --decorate --all
```

그리고 복구가 필요하면 바로 삭제하거나 덮어쓰지 말고 먼저 백업 브랜치를 만듭니다.

```bash
git switch -c backup/before-fix
```

Git에서 가장 위험한 순간은 명령어를 모를 때가 아니라, **현재 상태를 확인하지 않고 강제 명령을 실행할 때**입니다.
