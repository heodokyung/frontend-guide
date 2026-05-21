# Clean Code Guide

> 좋은 코드는 “멋있어 보이는 코드”가 아니라, 시간이 지나도 읽고 고치고 확장할 수 있는 코드입니다.

이 문서는 기존에 작성한 “clean-code는 무엇인가?” 글의 메시지를 유지하면서, 실제 프론트엔드 작업에 바로 적용할 수 있도록 기준과 체크리스트를 보강한 문서입니다.

---

## 먼저 결론

좋은 코드는 아래 질문에 답할 수 있어야 합니다.

1. 처음 보는 사람이 의도를 이해할 수 있는가?
2. 문제가 생겼을 때 수정 위치를 찾을 수 있는가?
3. 기능이 늘어날 때 기존 코드를 덜 깨뜨리는가?
4. 테스트하거나 검증하기 쉬운가?
5. 이름과 구조만 봐도 역할이 예측되는가?

좋은 코드는 단순히 짧은 코드가 아닙니다. **의도가 잘 드러나는 코드**입니다.

---

## 좋은 코드란 무엇인가?

좋은 코드에 대한 답은 사람마다 다를 수 있습니다.

- 버그 없이 잘 돌아가는 코드
- 재사용성이 좋은 코드
- 최신 기술로 작성된 코드
- 성능이 좋은 코드
- 짧고 간결한 코드

모두 중요한 기준이지만, 이 기준만으로는 부족합니다. 실무에서 좋은 코드는 결국 **유지보수 가능한 코드**입니다.

유지보수 가능한 코드는 읽기 쉽고, 수정하기 쉽고, 영향 범위를 예측하기 쉽습니다.

> 좋은 코드는 컴퓨터만 이해하는 코드가 아니라, 다음 개발자가 읽을 수 있는 코드입니다.

---

## 가독성이 중요한 이유

개발은 혼자 하는 작업처럼 보여도 대부분 협업을 전제로 합니다.

여기서 협업자는 꼭 다른 사람만을 의미하지 않습니다. 한 달 뒤의 나, 반년 뒤의 나도 협업자입니다.

지금은 모든 맥락을 알고 있기 때문에 대충 쓴 코드도 이해할 수 있습니다. 하지만 시간이 지나면 왜 그렇게 작성했는지 기억하기 어렵습니다. 그래서 좋은 코드는 현재의 나보다 미래의 읽는 사람을 기준으로 작성해야 합니다.

---

## 주석은 언제 필요한가?

주석은 나쁜 것이 아닙니다. 다만 주석이 코드를 대신 설명해야 한다면 코드 자체가 불명확한 것일 수 있습니다.

### 좋지 않은 주석

```js
// 사용자 정보를 가져온다
function getUserInfo() {
  return api.get('/user')
}
```

함수명만 봐도 알 수 있는 내용입니다.

### 좋은 주석

```js
// 레거시 API가 빈 문자열을 null 대신 반환하므로 화면 표시 전에 정규화한다.
function normalizeProfileName(name) {
  return name === '' ? null : name
}
```

이 주석은 “무엇”이 아니라 “왜”를 설명합니다.

---

## 네이밍 원칙

이름은 코드의 첫 번째 문서입니다.

### 1. 검색 가능한 이름을 사용합니다

```js
// Bad
setTimeout(save, 86400)

// Good
const ONE_DAY_SECONDS = 86400
setTimeout(save, ONE_DAY_SECONDS)
```

숫자, 문자열, 불리언 값이 특별한 의미를 가진다면 이름을 붙입니다.

### 2. 함수명에는 동사를 사용합니다

```js
// Bad
function userData() {}

// Good
function getUserData() {}
function updateUserData() {}
function deleteUserData() {}
```

함수는 행동입니다. 이름만 보고 무엇을 하는지 알 수 있어야 합니다.

### 3. 불리언은 질문처럼 읽히게 만듭니다

```js
const isOpen = true
const hasError = false
const canSubmit = true
const shouldShowModal = false
```

`flag`, `check`, `data`처럼 의미가 넓은 이름은 피합니다.

---

## 함수 작성 원칙

### 하나의 함수는 하나의 책임을 가집니다

```js
// Bad
function handleUser(param) {
  if (param.mode === 'create') {
    // 생성
  } else if (param.mode === 'delete') {
    // 삭제
  }
}

// Good
function createUser(user) {}
function deleteUser(userId) {}
```

하나의 함수가 여러 모드를 갖기 시작하면 읽기도 어렵고 테스트도 어려워집니다.

### 매개변수가 많다면 객체로 받습니다

```js
// Bad
function createUser(name, age, email, job, userId) {}

// Good
function createUser({ name, age, email, job, userId }) {}
```

객체 매개변수는 호출부에서 의미가 드러납니다.

```js
createUser({
  name: '홍길동',
  age: 24,
  email: 'test@example.com',
  job: 'frontend developer',
  userId: 'hong',
})
```

---

## 조건문 정리

조건문이 복잡하면 코드의 의도를 읽기 어렵습니다.

### 복잡한 조건은 이름을 붙입니다

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

중첩을 줄이면 코드의 흐름이 단순해집니다.

---

## 중복 제거 기준

중복은 항상 나쁜 것이 아닙니다. 너무 빠른 추상화는 오히려 코드를 어렵게 만듭니다.

아래 기준에 해당할 때 중복 제거를 고려합니다.

- 같은 코드가 세 번 이상 반복된다.
- 수정할 때 여러 곳을 동시에 고쳐야 한다.
- 같은 규칙이 서로 다른 이름으로 흩어져 있다.
- 복사한 코드가 조금씩 달라져 버그 가능성이 커진다.

반대로 아직 요구사항이 불안정하다면, 억지로 공통화하지 않는 편이 더 안전합니다.

---

## 좋은 주석과 나쁜 주석

| 주석 유형 | 판단 |
|---|---|
| 코드가 그대로 말하는 내용을 반복 | 피하기 |
| 왜 이런 예외 처리를 했는지 설명 | 권장 |
| 레거시/브라우저/서버 제약 설명 | 권장 |
| TODO만 남기고 맥락 없음 | 피하기 |
| 임시 코드 제거 조건 기록 | 권장 |

```js
// TODO: 나중에 수정
```

보다는 아래처럼 적는 것이 좋습니다.

```js
// TODO(2026-06): 결제 API v2 전환 후 legacyPaymentFallback 제거
```

---

## 프론트엔드에서 특히 중요한 Clean Code

### 컴포넌트는 너무 많은 일을 하지 않아야 합니다

컴포넌트 하나가 API 호출, 상태 관리, 검증, 렌더링, 모달 제어를 모두 담당하면 금방 복잡해집니다.

분리 후보:

- API 호출 로직
- 복잡한 계산 로직
- 폼 검증 로직
- 반복되는 UI 패턴
- 상태 변환 로직

### 상태 이름은 화면 의미를 드러냅니다

```js
// Bad
const flag = ref(false)
const data = ref([])

// Good
const isFilterOpen = ref(false)
const selectedProducts = ref([])
```

### 화면 조건은 읽히게 만듭니다

```js
const shouldShowEmptyState = products.length === 0 && !isLoading
const shouldShowError = Boolean(errorMessage)
```

---

## 리팩터링 기준

리팩터링은 코드를 예쁘게 꾸미는 작업이 아닙니다. 기능은 유지하면서 구조를 더 안전하게 바꾸는 작업입니다.

리팩터링이 필요한 신호:

- 같은 수정이 여러 파일에 반복된다.
- 함수 이름과 실제 동작이 다르다.
- 한 파일이 너무 많은 책임을 가진다.
- 조건문이 너무 깊다.
- 버그를 고치면 다른 곳이 자주 깨진다.
- 테스트하거나 수동 확인해야 하는 범위가 너무 넓다.

리팩터링 전 체크:

1. 현재 동작을 먼저 확인한다.
2. 한 번에 너무 많이 바꾸지 않는다.
3. 파일 이동과 로직 변경을 가능하면 분리한다.
4. 변경 후 이전 기능이 유지되는지 확인한다.

---

## Clean Code 체크리스트

- [ ] 함수 이름만 보고 역할을 알 수 있다.
- [ ] 변수명이 너무 추상적이지 않다.
- [ ] 하나의 함수가 하나의 책임을 가진다.
- [ ] 매개변수가 너무 많지 않다.
- [ ] 조건문이 과도하게 중첩되지 않는다.
- [ ] 주석은 “왜”를 설명한다.
- [ ] 중복 제거가 과도한 추상화로 변하지 않았다.
- [ ] 컴포넌트가 너무 많은 일을 하지 않는다.
- [ ] 임시 코드에는 제거 조건이 있다.
- [ ] 수정 영향 범위를 예측할 수 있다.

---

## 한 줄 결론

> 좋은 코드는 처음 작성할 때보다 다시 읽고 고칠 때 진짜 가치가 드러납니다.
