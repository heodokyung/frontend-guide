# Clean Code Guide

> 시간이 지나도 다시 읽고 고칠 수 있는 코드를 만들기 위한 기준입니다.

정리: Heo Do Kyung

---

## 목차

- [내가 생각하는 클린 코드](#내가-생각하는-클린-코드)
- [가독성이 먼저다](#가독성이-먼저다)
- [네이밍](#네이밍)
- [함수](#함수)
- [조건문](#조건문)
- [중복과 추상화](#중복과-추상화)
- [주석](#주석)
- [프론트엔드 컴포넌트 기준](#프론트엔드-컴포넌트-기준)
- [리팩터링 순서](#리팩터링-순서)
- [리뷰 체크리스트](#리뷰-체크리스트)

---

## 내가 생각하는 클린 코드

클린 코드는 짧은 코드나 멋진 문법을 많이 쓴 코드가 아닙니다.

제가 생각하는 좋은 코드는 아래 질문에 답할 수 있는 코드입니다.

1. 처음 보는 사람이 의도를 이해할 수 있는가?
2. 문제가 생겼을 때 수정 위치를 찾을 수 있는가?
3. 기능이 늘어날 때 기존 코드를 덜 깨뜨리는가?
4. 테스트하거나 검증하기 쉬운가?
5. 이름과 구조만 봐도 역할이 예측되는가?

결국 좋은 코드는 유지보수 가능한 코드입니다. 조금 더 현실적으로 말하면, 다음 사람이 겁먹지 않고 열어볼 수 있는 코드입니다.

---

## 가독성이 먼저다

개발은 혼자 하는 일처럼 보이지만, 실제로는 늘 누군가와 이어집니다. 그 사람이 동료일 수도 있고, 한 달 뒤의 나일 수도 있습니다.

지금은 대충 적은 코드도 이해할 수 있습니다. 하지만 시간이 지나면 왜 그렇게 작성했는지 기억나지 않습니다. 그래서 코드는 현재의 내가 아니라 미래의 읽는 사람을 기준으로 작성해야 합니다.

```js
// Bad
if (u.a >= 19 && u.v && !u.s) {
  pay()
}

// Good
const canUsePayment = user.age >= 19 && user.verified && !user.suspended

if (canUsePayment) {
  showPaymentButton()
}
```

---

## 네이밍

이름은 코드의 첫 번째 문서입니다.

### 검색 가능한 이름을 사용합니다

```js
// Bad
setTimeout(save, 86400)

// Good
const ONE_DAY_SECONDS = 86400
setTimeout(save, ONE_DAY_SECONDS)
```

### 함수명에는 동사를 사용합니다

```js
// Bad
function userData() {}

// Good
function getUserData() {}
function updateUserData() {}
function deleteUserData() {}
```

### 불리언은 질문처럼 읽히게 만듭니다

```js
const isOpen = true
const hasError = false
const canSubmit = true
const shouldShowModal = false
```

피하고 싶은 이름:

```js
const data = {}
const temp = []
const flag = true
const check = false
```

이름이 넓으면 읽는 사람이 다시 구현 내용을 열어봐야 합니다.

---

## 함수

### 하나의 함수는 하나의 책임을 가집니다

```js
// Bad
function handleUser(mode, user) {
  if (mode === 'create') {
    // 생성
  }

  if (mode === 'delete') {
    // 삭제
  }
}

// Good
function createUser(user) {}
function deleteUser(userId) {}
```

### 매개변수가 많다면 객체로 받습니다

```js
// Bad
function createUser(name, age, email, job, userId) {}

// Good
function createUser({ name, age, email, job, userId }) {}
```

호출부에서 의미가 보입니다.

```js
createUser({
  name: '도경',
  age: 42,
  email: 'example@example.com',
  job: 'frontend developer',
  userId: 'dk',
})
```

### 부수효과를 드러냅니다

값만 계산하는 함수와 외부 상태를 바꾸는 함수는 다르게 보여야 합니다.

```js
function calculateTotalPrice(items) {
  return items.reduce((sum, item) => sum + item.price, 0)
}

function saveOrder(order) {
  return api.post('/orders', order)
}
```

---

## 조건문

조건문은 코드가 복잡해지는 가장 흔한 지점입니다.

### 복잡한 조건에는 이름을 붙입니다

```js
// Bad
if (user.age >= 19 && user.verified && !user.suspended) {
  showPaymentButton()
}

// Good
const canUsePayment = user.age >= 19 && user.verified && !user.suspended

if (canUsePayment) {
  showPaymentButton()
}
```

### 빠른 반환을 사용합니다

```js
// Bad
function submit(form) {
  if (form.valid) {
    save(form)
  }
}

// Good
function submit(form) {
  if (!form.valid) return

  save(form)
}
```

중첩을 줄이면 흐름이 가벼워집니다.

### switch보다 매핑 객체가 나을 때도 있습니다

```js
const statusLabelMap = {
  pending: '대기',
  progress: '진행 중',
  done: '완료',
}

function getStatusLabel(status) {
  return statusLabelMap[status] ?? '알 수 없음'
}
```

---

## 중복과 추상화

중복은 항상 나쁜 것이 아닙니다. 너무 이른 추상화는 오히려 코드를 어렵게 만듭니다.

중복 제거를 고려할 때:

- 같은 코드가 세 번 이상 반복됩니다.
- 수정할 때 여러 곳을 동시에 고쳐야 합니다.
- 같은 규칙이 서로 다른 이름으로 흩어져 있습니다.
- 복사한 코드가 조금씩 달라져 버그 가능성이 커졌습니다.

아직 두 번만 반복된 코드라면 조금 더 지켜봐도 됩니다. 반복의 모양이 충분히 보인 뒤에 분리하는 편이 안전합니다.

---

## 주석

주석은 “무엇을 하는지”보다 “왜 그렇게 했는지”를 설명할 때 좋습니다.

```js
// Bad: 함수명만 봐도 알 수 있음
// 사용자 정보를 가져온다
function getUserInfo() {
  return api.get('/user')
}
```

```js
// Good: 코드만 봐서는 알기 어려운 이유를 설명함
// 레거시 API가 빈 문자열을 null 대신 반환하므로 화면 표시 전에 정규화한다.
function normalizeProfileName(name) {
  return name === '' ? null : name
}
```

주석이 많아졌다면 먼저 이름과 구조가 불명확한 것은 아닌지 봅니다.

---

## 프론트엔드 컴포넌트 기준

프론트엔드에서 클린 코드는 컴포넌트 구조와도 연결됩니다.

### 컴포넌트는 역할이 보여야 합니다

```txt
components/
├─ AppButton.vue
├─ AppModal.vue
├─ UserProfileCard.vue
└─ UserProfileForm.vue
```

`Common`, `Box`, `Wrap`, `Temp` 같은 이름은 정말 공통인지 다시 확인합니다.

### 화면 컴포넌트와 재사용 컴포넌트를 구분합니다

```txt
views/
└─ ProjectDetailView.vue

components/
└─ ProjectCard.vue
```

### props가 너무 많다면 분리 신호입니다

props가 많아지는 이유는 대체로 둘 중 하나입니다.

1. 컴포넌트가 너무 많은 역할을 하고 있다.
2. 여러 상태를 하나의 컴포넌트로 억지로 처리하고 있다.

이때는 slot, 하위 컴포넌트 분리, preset 객체, 상태별 컴포넌트 분리를 검토합니다.

---

## 리팩터링 순서

리팩터링은 한 번에 갈아엎는 작업이 아닙니다. 안전하게 바꾸는 순서가 중요합니다.

1. 현재 동작을 확인합니다.
2. 변경 범위를 작게 잡습니다.
3. 이름부터 고칩니다.
4. 중복을 묶습니다.
5. 조건문을 정리합니다.
6. 함수와 컴포넌트를 나눕니다.
7. 마지막에 스타일과 폴더 구조를 정리합니다.
8. 빌드와 주요 화면을 다시 확인합니다.

리팩터링의 목표는 “내가 보기 좋은 코드”가 아니라 “다음 수정이 쉬운 코드”입니다.

---

## 리뷰 체크리스트

- [ ] 이름만 보고 역할을 알 수 있는가?
- [ ] 하나의 함수가 한 가지 일을 하는가?
- [ ] 조건문 중첩이 깊지 않은가?
- [ ] 매직 넘버나 의미 없는 문자열이 남아 있지 않은가?
- [ ] 주석이 “왜”를 설명하는가?
- [ ] 중복 제거가 너무 이르지 않은가?
- [ ] 컴포넌트 props가 과하게 많지 않은가?
- [ ] 사이드 이펙트가 드러나는가?
- [ ] 삭제해도 되는 코드가 남아 있지 않은가?
- [ ] 수정 후 빌드와 주요 흐름을 확인했는가?
