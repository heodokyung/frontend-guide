# Git 실무 워크플로우

> 실제 프론트엔드 작업에서 Git을 어떻게 쓰면 안전하고 깔끔한지 정리한 문서입니다.

이 문서는 Git의 개념 설명보다 **일상 작업 루틴, 브랜치 전략, 커밋 관리, 협업 흐름, 커밋 정리**에 초점을 둡니다.

---

## 1. 기본 원칙

실무에서 Git을 쓸 때 가장 중요한 원칙은 세 가지입니다.

```txt
1. 작업 전 현재 상태를 확인한다.
2. 하나의 커밋에는 하나의 의미 있는 변경만 담는다.
3. 원격 이력을 강제로 바꾸는 명령은 신중하게 사용한다.
```

작업 전 기본 확인:

```bash
git status
git branch
git remote -v
```

---

## 2. 가장 안전한 일상 루틴

혼자 작업할 때도 아래 흐름을 습관화하면 실수가 줄어듭니다.

```bash
# 1. main으로 이동
git switch main

# 2. 원격 최신 내용 반영
git pull origin main

# 3. 작업 브랜치 생성
git switch -c feature/header-ui

# 4. 파일 수정 후 상태 확인
git status

# 5. 필요한 파일 스테이징
git add .

# 6. 커밋
git commit -m "feat: 헤더 UI 개선"

# 7. 원격 브랜치로 push
git push -u origin feature/header-ui
```

작은 개인 프로젝트라면 `main`에 바로 커밋해도 됩니다. 하지만 포트폴리오나 공개 프로젝트라면 브랜치를 나누는 습관이 좋습니다.

---

## 3. 브랜치 전략

### 3-1. 간단한 개인 프로젝트

개인 프로젝트 초기에는 단순하게 가도 됩니다.

```txt
main
```

단, 작업 규모가 커지면 기능별 브랜치를 사용합니다.

```txt
main
feature/header-ui
feature/project-detail
fix/mobile-layout
```

### 3-2. 추천 브랜치 이름

| 목적 | 예시 |
|---|---|
| 기능 추가 | `feature/login`, `feature/header-ui` |
| 버그 수정 | `fix/mobile-header`, `fix/build-error` |
| 문서 수정 | `docs/git-guide`, `docs/readme-update` |
| 리팩토링 | `refactor/button-component` |
| 설정/잡무 | `chore/eslint-config` |

브랜치 이름은 짧고 명확하게 작성합니다.

---

## 4. 브랜치 명령어

### 브랜치 목록 보기

```bash
git branch
```

원격 브랜치까지 보기:

```bash
git branch -a
```

### 새 브랜치 만들고 이동

```bash
git switch -c feature/login
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

## 5. 커밋 메시지 규칙

커밋 메시지는 나중에 작업 이력을 이해하기 위한 기록입니다.

추천 형식:

```txt
타입: 작업 내용
```

예:

```txt
feat: 프로젝트 상세 페이지 추가
fix: 모바일 탭 메뉴 정렬 오류 수정
docs: Git 입문 가이드 보강
style: CSS 속성 순서 정리
refactor: 공통 버튼 컴포넌트 분리
chore: Vite 설정 정리
```

### 자주 쓰는 타입

| 타입 | 의미 |
|---|---|
| `feat` | 기능 추가 |
| `fix` | 버그 수정 |
| `docs` | 문서 수정 |
| `style` | 포맷, CSS 정리, 코드 의미 변화 없는 스타일 수정 |
| `refactor` | 기능 변화 없는 구조 개선 |
| `chore` | 설정, 패키지, 빌드 관련 작업 |
| `test` | 테스트 추가/수정 |
| `perf` | 성능 개선 |

피해야 할 메시지:

```txt
수정
작업
테스트
최종
진짜최종
다시수정
```

---

## 6. 좋은 커밋 단위

좋은 커밋은 하나의 목적을 가집니다.

좋은 예:

```txt
feat: 프로젝트 카드 컴포넌트 추가
fix: 모바일에서 카드 이미지 비율 깨짐 수정
docs: README 배포 방법 추가
```

아쉬운 예:

```txt
feat: 프로젝트 카드 추가 및 README 수정 및 빌드 설정 변경 및 CSS 정리
```

하나의 커밋에 너무 많은 변경이 들어가면 나중에 되돌리거나 원인을 찾기 어렵습니다.

---

## 7. Pull과 Fetch 차이

| 명령어 | 의미 |
|---|---|
| `git fetch` | 원격 변경 사항을 가져오기만 함. 내 작업 파일은 건드리지 않음 |
| `git pull` | 원격 변경 사항을 가져오고 현재 브랜치에 합침 |

불안할 때는 먼저 fetch를 합니다.

```bash
git fetch origin
```

전체 이력을 보고 판단합니다.

```bash
git log --oneline --graph --decorate --all
```

일반적인 개인 프로젝트에서는 다음으로 충분합니다.

```bash
git pull origin main
```

---

## 8. Merge와 Rebase

### 8-1. Merge

두 브랜치의 이력을 합칩니다.

```bash
git switch main
git merge feature/login
```

장점:

- 안전합니다.
- 이력이 명확히 남습니다.
- 협업 브랜치에 적합합니다.

단점:

- merge commit이 생겨 이력이 복잡해질 수 있습니다.

### 8-2. Rebase

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

```txt
혼자 쓰는 작업 브랜치: rebase 가능
여러 사람이 같이 쓰는 브랜치: merge 권장
```

---

## 9. Pull Request 흐름

GitHub에서 Pull Request를 사용하면 작업 내용을 main에 바로 넣지 않고 검토할 수 있습니다.

추천 흐름:

```bash
git switch main
git pull origin main
git switch -c feature/project-detail

# 작업
git add .
git commit -m "feat: 프로젝트 상세 페이지 개선"
git push -u origin feature/project-detail
```

그 후 GitHub에서 Pull Request를 만들고, 확인 후 main에 병합합니다.

개인 프로젝트에서도 Pull Request를 사용하면 포트폴리오 관점에서 작업 흐름이 더 전문적으로 보입니다.

---

## 10. Stash: 작업 중 잠시 저장하기

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

특정 stash 삭제:

```bash
git stash drop stash@{0}
```

stash는 임시 보관함입니다. 오래 보관할 작업은 브랜치를 만들어 커밋하는 것이 더 안전합니다.

---

## 11. Cherry-pick: 특정 커밋만 가져오기

다른 브랜치의 특정 커밋 하나만 현재 브랜치에 적용하고 싶을 때 사용합니다.

```bash
git cherry-pick 커밋해시
```

예:

```bash
git switch main
git cherry-pick a1b2c3d
```

주의:

- 같은 변경이 이미 들어와 있으면 충돌이 날 수 있습니다.
- 여러 커밋을 cherry-pick하기보다 브랜치 병합이 더 적절한 경우도 많습니다.

---

## 12. 커밋 정리: Squash와 Fixup

작업하다 보면 커밋이 너무 자잘해질 수 있습니다.

예:

```txt
프로젝트 상세 페이지 작업
오타 수정
다시 수정
버튼 간격 수정
콘솔 삭제
```

이런 커밋은 Pull Request 전에 하나 또는 몇 개의 의미 있는 커밋으로 정리할 수 있습니다.

```bash
git rebase -i HEAD~5
```

편집 화면에서 기준 커밋은 `pick`, 합칠 커밋은 `squash` 또는 `fixup`으로 바꿉니다.

```txt
pick a1b2c3d 프로젝트 상세 페이지 작업
fixup b2c3d4e 오타 수정
fixup c3d4e5f 다시 수정
fixup d4e5f6g 버튼 간격 수정
fixup e5f6g7h 콘솔 삭제
```

원칙:

```txt
push 전 커밋 정리: 좋음
이미 공유한 커밋 정리: 주의 필요
협업 브랜치 rebase: 신중하게 처리
```

---

## 13. Amend: 방금 커밋 수정하기

마지막 커밋 메시지를 고치고 싶다면:

```bash
git commit --amend -m "새 커밋 메시지"
```

마지막 커밋에 파일을 추가하고 싶다면:

```bash
git add src/App.vue
git commit --amend --no-edit
```

이미 push한 커밋을 amend했다면 원격과 이력이 달라집니다.

```bash
git push --force-with-lease
```

혼자 쓰는 브랜치라면 괜찮지만, 협업 브랜치에서는 주의해야 합니다.

---

## 14. 원격 저장소와 upstream

다른 사람의 저장소를 fork해서 작업할 때는 보통 remote가 두 개가 됩니다.

| 이름 | 의미 |
|---|---|
| `origin` | 내 GitHub 저장소 |
| `upstream` | 원본 저장소 |

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

## 15. 태그와 릴리스

버전을 남기고 싶을 때 태그를 사용할 수 있습니다.

```bash
git tag v1.0.0
git push origin v1.0.0
```

메시지가 있는 태그:

```bash
git tag -a v1.0.0 -m "첫 번째 안정 버전"
git push origin v1.0.0
```

GitHub Releases와 연결하면 포트폴리오 프로젝트에서 배포 이력을 보여주기 좋습니다.

---

## 16. Fork 앱으로 작업할 때 추천 흐름

Fork 기준 일상 루틴:

```txt
1. Open Repository로 프로젝트 열기
2. Fetch로 원격 상태 확인
3. Pull로 최신화
4. 작업
5. Local Changes에서 변경 파일 확인
6. 필요한 파일만 Stage
7. Commit 메시지 작성
8. Push
```

주의할 점:

- `Clone`은 새 폴더로 내려받을 때만 사용합니다.
- 이미 로컬에 있는 프로젝트는 `Open Repository`로 엽니다.
- `Branches` 아래의 항목과 `Remotes` 아래의 항목을 구분해야 합니다.
- `Remotes > origin`이 실제 GitHub 연결입니다.

---

## 17. 작업 전후 체크리스트

작업 전:

```bash
git status
git branch
git remote -v
git pull origin main
```

작업 후:

```bash
git status
git diff
git add .
git diff --staged
git commit -m "타입: 작업 내용"
git push
```

문제 발생 시:

```bash
git status
git log --oneline --graph --decorate --all
git reflog
```

---

## 18. 추천 워크플로우 결론

개인 프로젝트에서는 아래 흐름을 기본으로 삼으면 충분합니다.

```bash
git switch main
git pull origin main
git switch -c feature/작업명

# 작업 후
git add .
git commit -m "feat: 작업 내용"
git push -u origin feature/작업명
```

작업이 작고 혼자만 관리하는 레포라면 main에 바로 커밋해도 됩니다.

```bash
git pull origin main
git add .
git commit -m "docs: Git 가이드 수정"
git push
```

중요한 것은 거창한 전략이 아니라, **상태 확인 → 의미 있는 커밋 → 안전한 push**를 반복하는 것입니다.
