# GitHub Pages Deploy Guide

> `frontend-guide` 안의 정적 HTML 도구를 GitHub Pages에서 실행하는 방법을 정리합니다.

작성: Heo Do Kyung

---

## 목차

- [핵심 결론](#핵심-결론)
- [README 링크와 Pages 링크의 차이](#readme-링크와-pages-링크의-차이)
- [code-align 배포 주소](#code-align-배포-주소)
- [GitHub Pages 설정](#github-pages-설정)
- [폴더 안 index.html이 안 열릴 때](#폴더-안-indexhtml이-안-열릴-때)
- [체크리스트](#체크리스트)

---

## 핵심 결론

`code-align/index.html`처럼 폴더 안에 있는 정적 HTML은 GitHub Pages에서 실행할 수 있습니다.

다만 GitHub README의 상대 링크와 GitHub Pages의 실행 링크는 다릅니다.

```txt
GitHub 소스 보기:
https://github.com/heodokyung/frontend-guide/blob/main/code-align/index.html

GitHub Pages 실행:
https://heodokyung.github.io/frontend-guide/code-align/
```

---

## README 링크와 Pages 링크의 차이

README에서 아래처럼 쓰면 GitHub 저장소 안의 파일로 이동합니다.

```md
[코드 보기](./code-align/index.html)
```

실제 웹 도구처럼 실행하려면 Pages 주소를 써야 합니다.

```md
[도구 실행](https://heodokyung.github.io/frontend-guide/code-align/)
```

그래서 README에는 가능하면 두 링크를 나눠 둡니다.

| 목적 | 링크 |
|---|---|
| 코드를 보고 싶을 때 | `./code-align/index.html` |
| 웹에서 실행하고 싶을 때 | `https://heodokyung.github.io/frontend-guide/code-align/` |

---

## code-align 배포 주소

레포 이름이 `frontend-guide`이고 GitHub 계정이 `heodokyung`이면 실행 주소는 아래 형태입니다.

```txt
https://heodokyung.github.io/frontend-guide/code-align/
```

폴더 안에 `index.html`이 있으면 `/code-align/`까지만 입력해도 `index.html`을 자동으로 찾습니다.

---

## GitHub Pages 설정

GitHub 저장소에서 다음 순서로 확인합니다.

```txt
Settings
→ Pages
→ Build and deployment
→ Source: Deploy from a branch
→ Branch: main
→ Folder: /root
→ Save
```

이 방식이면 `main` 브랜치 루트의 파일이 그대로 배포됩니다.

---

## 폴더 안 index.html이 안 열릴 때

아래를 확인합니다.

### 1. Pages가 `/root`를 보고 있는가

`/docs`로 설정되어 있으면 루트의 `code-align/`은 배포되지 않을 수 있습니다.

### 2. 배포가 완료되었는가

커밋 직후에는 바로 반영되지 않을 수 있습니다. Actions 또는 Pages 배포 상태가 초록색인지 확인합니다.

### 3. 파일명이 정확한가

```txt
code-align/index.html
```

대소문자도 확인합니다.

### 4. Jekyll 처리 문제를 피하고 싶은가

루트에 `.nojekyll` 파일을 두면 GitHub Pages가 Jekyll 처리를 건너뜁니다. 이 저장소에는 `.nojekyll`을 두는 것을 권장합니다.

### 5. GitHub Actions로 배포 중인가

GitHub Actions를 사용한다면 워크플로우가 전체 저장소를 업로드하는지 확인해야 합니다. `index.html` 하나만 업로드하는 설정이면 `code-align/` 폴더가 빠질 수 있습니다.

---

## 체크리스트

- [ ] `code-align/index.html`이 실제로 커밋되어 있는가?
- [ ] GitHub Pages Source가 `main / root`인가?
- [ ] 배포가 완료되었는가?
- [ ] 실행 링크가 `/frontend-guide/code-align/` 형태인가?
- [ ] README의 링크가 소스 보기와 실행 링크로 구분되어 있는가?
- [ ] 루트에 `.nojekyll` 파일이 있는가?
