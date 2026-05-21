# UI Guide

> 버튼, 폼, 모달, 탭, 카드처럼 반복해서 사용하는 UI 패턴의 구현 기준을 정리합니다.

작성: Heo Do Kyung

---

## 목차

- [기본 원칙](#기본-원칙)
- [버튼](#버튼)
- [폼](#폼)
- [모달과 바텀시트](#모달과-바텀시트)
- [탭과 아코디언](#탭과-아코디언)
- [카드와 리스트](#카드와-리스트)
- [상태 화면](#상태-화면)
- [체크리스트](#체크리스트)

---

## 기본 원칙

1. UI는 예쁘기 전에 먼저 읽히고 눌려야 합니다.
2. 클릭 가능한 요소는 가능하면 `button`, 이동은 `a`를 사용합니다.
3. 색상만으로 상태를 전달하지 않습니다.
4. 모달, 드롭다운, 탭은 키보드 접근성을 함께 고려합니다.
5. 모바일에서는 터치 영역을 충분히 확보합니다.
6. 반복되는 UI는 컴포넌트로 분리합니다.
7. 상태 이름은 `is-active`, `is-disabled`, `is-loading`, `is-expanded`처럼 예측 가능하게 작성합니다.

---

## 버튼

버튼은 행동을 실행합니다. 페이지 이동은 링크로 처리합니다.

```html
<button class="button" type="button">저장</button>
<a class="link-button" href="/projects">프로젝트 보기</a>
```

아이콘 버튼에는 접근 가능한 이름을 제공합니다.

```html
<button type="button" aria-label="메뉴 열기">
  <svg aria-hidden="true" focusable="false"></svg>
</button>
```

---

## 폼

입력 요소에는 항상 레이블을 연결합니다.

```html
<label for="email">이메일</label>
<input id="email" name="email" type="email" autocomplete="email">
```

오류는 색상만으로 전달하지 않습니다.

```html
<input id="email" aria-describedby="email-error" aria-invalid="true">
<p id="email-error">이메일 형식이 올바르지 않습니다.</p>
```

---

## 모달과 바텀시트

- 열릴 때 모달 내부로 초점이 이동해야 합니다.
- 닫을 때 원래 버튼으로 초점이 돌아와야 합니다.
- `Esc`로 닫을 수 있어야 합니다.
- 배경 스크롤을 막아야 합니다.
- 모바일에서는 하단 안전 영역을 고려합니다.

---

## 탭과 아코디언

탭은 선택된 패널만 보여주는 구조입니다.

- 선택 상태를 시각적으로 보여줍니다.
- 현재 탭은 `aria-selected` 또는 `aria-current`로 표현합니다.
- 키보드 이동 규칙을 정합니다.

아코디언은 열림 상태를 전달해야 합니다.

```html
<button type="button" aria-expanded="false" aria-controls="panel-1">
  상세 보기
</button>
<div id="panel-1" hidden>
  내용
</div>
```

---

## 카드와 리스트

카드는 정보를 묶는 단위입니다. 카드 전체가 클릭 가능하다면 키보드 접근성과 링크 목적을 함께 봅니다.

```html
<article class="project-card">
  <h2 class="project-card__title">
    <a href="/projects/life-planner">인생플래너</a>
  </h2>
  <p class="project-card__description">목표와 습관을 관리하는 앱입니다.</p>
</article>
```

---

## 상태 화면

빈 상태, 로딩, 오류 상태는 사용자가 다음 행동을 알 수 있어야 합니다.

| 상태 | 포함할 내용 |
|---|---|
| 로딩 | 무엇을 불러오는 중인지 |
| 빈 상태 | 왜 비어 있는지, 다음 행동은 무엇인지 |
| 오류 | 무엇이 실패했는지, 다시 시도할 수 있는지 |
| 성공 | 무엇이 완료되었는지 |

---

## 체크리스트

- [ ] 클릭 가능한 요소가 명확한가?
- [ ] 키보드로 사용할 수 있는가?
- [ ] 포커스가 보이는가?
- [ ] 모바일 터치 영역이 충분한가?
- [ ] 오류 메시지가 구체적인가?
- [ ] 로딩/빈 상태/오류 상태가 준비되어 있는가?
- [ ] 같은 UI 패턴이 화면마다 다르게 동작하지 않는가?
