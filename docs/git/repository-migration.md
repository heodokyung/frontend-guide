# Repository Migration Guide

> 흩어진 학습용 저장소를 `frontend-study`처럼 하나의 저장소로 모을 때 참고하는 문서입니다.

정리: Heo Do Kyung

---

## 목차

- [먼저 결정할 것](#먼저-결정할-것)
- [추천 결론](#추천-결론)
- [방법 1. 단순 복사로 통합하기](#방법-1-단순-복사로-통합하기)
- [방법 2. 기존 커밋 이력까지 가져오기](#방법-2-기존-커밋-이력까지-가져오기)
- [방법 3. 기존 레포 이름을 바꾸기](#방법-3-기존-레포-이름을-바꾸기)
- [기존 레포는 어떻게 처리할까](#기존-레포는-어떻게-처리할까)
- [GitHub Pages를 함께 쓸 때](#github-pages를-함께-쓸-때)
- [체크리스트](#체크리스트)

---

## 먼저 결정할 것

기존 레포를 하나로 모을 때는 먼저 두 가지를 정해야 합니다.

1. 커밋 이력이 꼭 필요한가?
2. 기존 레포 URL을 계속 살려야 하는가?

학습용 예제나 정리 문서는 보통 커밋 이력보다 현재 구조가 더 중요합니다.  
그래서 대부분은 새 저장소를 만들고, 필요한 파일만 폴더별로 옮기는 방식이 가장 깔끔합니다.

---

## 추천 결론

`frontend-study`는 아래처럼 운영하는 것을 추천합니다.

```txt
frontend-study/
├─ README.md
├─ javascript/
├─ typescript/
├─ vue/
├─ react/
├─ html-css/
├─ animation/
├─ examples/
└─ assets/
```

기존 레포는 바로 삭제하지 말고, README 상단에 새 위치를 남긴 뒤 Archive 처리하는 편이 안전합니다.

---

## 방법 1. 단순 복사로 통합하기

가장 쉽고 실수도 적은 방식입니다.

1. GitHub에 `frontend-study` 레포를 새로 만듭니다.
2. 로컬에 clone합니다.

```bash
git clone https://github.com/heodokyung/frontend-study.git
cd frontend-study
```

3. 기존 레포에서 필요한 파일만 주제별 폴더로 복사합니다.

```txt
기존 study-list/      → frontend-study/javascript/
기존 react-coin-list/ → frontend-study/react/coin-list/
기존 svelte-todo/     → frontend-study/svelte/todo/
```

4. 커밋합니다.

```bash
git add .
git commit -m "docs: organize frontend study notes"
git push
```

이 방식은 기존 커밋 이력은 가져오지 않습니다. 대신 구조가 단순하고 관리가 쉽습니다.

---

## 방법 2. 기존 커밋 이력까지 가져오기

기존 레포의 커밋 이력도 보존하고 싶다면 `git subtree`를 사용할 수 있습니다.

```bash
git remote add study-list https://github.com/heodokyung/study-list.git
git fetch study-list
git subtree add --prefix=javascript/study-list study-list main
```

다른 레포도 같은 방식으로 추가할 수 있습니다.

```bash
git remote add react-coin-list https://github.com/heodokyung/react-coin-list.git
git fetch react-coin-list
git subtree add --prefix=react/coin-list react-coin-list main
```

주의할 점은 있습니다.

- 명령어가 단순 복사보다 어렵습니다.
- 레포마다 기본 브랜치가 `main`이 아닐 수 있습니다.
- 충돌이 나면 해결해야 합니다.
- 학습용 레포라면 이력 보존보다 현재 구조 정리가 더 중요할 수 있습니다.

---

## 방법 3. 기존 레포 이름을 바꾸기

기존 레포 하나를 기준으로 삼고 싶다면, 그 레포의 이름을 `frontend-study`로 바꿀 수도 있습니다.

예를 들어 `study-list`를 `frontend-study`로 바꾸는 방식입니다.

```txt
GitHub 레포 접속
→ Settings
→ Repository name 변경
→ Rename
```

이 방식은 기존 이슈, 스타, 커밋 이력이 그대로 이어집니다.  
다만 여러 레포를 하나로 합치는 것은 아니기 때문에, 다른 레포의 파일은 다시 옮겨야 합니다.

---

## 기존 레포는 어떻게 처리할까

삭제는 마지막에 생각해도 됩니다. 처음에는 아래 순서가 안전합니다.

1. 기존 레포 README 상단에 이동 안내를 추가합니다.
2. 새 `frontend-study` 링크를 남깁니다.
3. 더 이상 수정하지 않을 레포는 Archive 처리합니다.
4. 충분히 시간이 지난 뒤 삭제 여부를 결정합니다.

README 예시:

```md
# 안내

이 저장소의 내용은 아래 저장소로 옮겨 정리하고 있습니다.

https://github.com/heodokyung/frontend-study
```

Archive 처리하면 코드는 남아 있지만 수정은 막히기 때문에, “기록은 보존하고 관리 대상에서는 제외”하기 좋습니다.

---

## GitHub Pages를 함께 쓸 때

`frontend-study` 안에 여러 예제 페이지를 넣는다면 각 폴더에 `index.html`을 두는 방식이 좋습니다.

```txt
frontend-study/
├─ css-animation/
│  └─ index.html
├─ vanilla-slider/
│  └─ index.html
└─ react-example/
```

GitHub Pages를 `main / root`로 설정했다면 실행 주소는 이런 식이 됩니다.

```txt
https://heodokyung.github.io/frontend-study/css-animation/
https://heodokyung.github.io/frontend-study/vanilla-slider/
```

React/Vue처럼 빌드가 필요한 프로젝트는 폴더별로 바로 배포하기가 까다로울 수 있습니다.  
그 경우에는 예제 단위로 정적 결과물을 만들거나, 별도 배포 전략을 잡는 편이 좋습니다.

---

## 체크리스트

- [ ] `frontend-study` 레포를 새로 만들었는가?
- [ ] 주제별 폴더 구조를 먼저 정했는가?
- [ ] 기존 레포를 바로 삭제하지 않고 백업했는가?
- [ ] README에 이동 안내를 남겼는가?
- [ ] GitHub Pages로 실행할 예제는 각 폴더에 `index.html`을 두었는가?
- [ ] 기존 레포를 Archive 처리할지 결정했는가?
