# TypeScript Guide

> TypeScript를 처음 배우는 사람도, 프론트엔드 프로젝트에 적용하려는 사람도 기준으로 삼을 수 있는 실무형 정리 문서입니다.

TypeScript는 JavaScript를 완전히 대체하는 다른 언어가 아닙니다. JavaScript 위에 타입 시스템을 더해, 실행 전에 더 많은 오류를 발견하고 코드의 의도를 더 명확히 표현하게 도와주는 도구입니다.

---

## 먼저 결론

TypeScript를 쓰는 이유는 “타입을 많이 쓰기 위해서”가 아닙니다.

핵심은 아래 세 가지입니다.

1. 런타임 전에 오류를 더 빨리 발견한다.
2. 함수와 데이터의 의도를 코드에 남긴다.
3. 리팩터링할 때 안전망을 만든다.

---

## JavaScript에서 생기기 쉬운 문제

JavaScript는 유연하지만, 그만큼 실수를 늦게 발견할 수 있습니다.

```js
function add(a, b) {
  return a + b
}

add(1) // NaN
```

```js
const user = { name: 'Dk' }
user.email.toLowerCase() // 런타임 에러
```

TypeScript는 이런 문제를 실행 전에 더 많이 잡을 수 있게 도와줍니다.

---

## 기본 타입

```ts
const name: string = 'Dk'
const age: number = 42
const isActive: boolean = true
const tags: string[] = ['frontend', 'vue']
```

대부분의 경우 TypeScript가 타입을 추론하므로 불필요한 타입 표기는 줄입니다.

```ts
// Good
const name = 'Dk'
const age = 42

// 불필요하게 길어질 수 있음
const name2: string = 'Dk'
```

---

## 타입 추론

TypeScript는 변수에 할당된 값을 보고 타입을 추론합니다.

```ts
let message = 'hello'
message = 123 // Error
```

명확한 초기값이 있다면 타입을 직접 적지 않아도 됩니다. 반대로 빈 배열, 외부 API 응답, 함수 매개변수처럼 추론이 불안정한 곳은 타입을 명시합니다.

```ts
const selectedIds: string[] = []
```

---

## Type Alias와 Interface

객체 구조는 `type` 또는 `interface`로 정의합니다.

```ts
type User = {
  id: string
  name: string
  age?: number
}

const user: User = {
  id: 'u1',
  name: 'Dk',
}
```

### type과 interface 선택 기준

| 상황 | 추천 |
|---|---|
| 일반 객체 모델 | `type` 또는 `interface` 모두 가능 |
| union, tuple, primitive 조합 | `type` |
| 라이브러리 확장, 선언 병합 | `interface` |
| 팀 규칙이 이미 있음 | 팀 규칙 우선 |

중요한 것은 둘 중 무엇이 절대적으로 좋으냐가 아니라, 프로젝트 안에서 일관되게 쓰는 것입니다.

---

## Optional과 undefined

`?`는 값이 없을 수 있음을 의미합니다.

```ts
type User = {
  name: string
  age?: number
}
```

optional 값은 바로 사용하지 말고 확인합니다.

```ts
function printAge(user: User) {
  if (user.age === undefined) return

  console.log(user.age + 1)
}
```

Truthy 체크만으로 처리하면 `0` 같은 값이 의도치 않게 제외될 수 있습니다.

```ts
// 주의: age가 0이면 조건을 통과하지 않음
if (user.age) {}

// 명확함
if (user.age !== undefined) {}
```

---

## readonly와 불변성

`readonly`는 값을 실수로 바꾸지 않도록 막아줍니다.

```ts
type User = {
  readonly id: string
  name: string
}

const user: User = {
  id: 'u1',
  name: 'Dk',
}

user.id = 'u2' // Error
```

배열에도 사용할 수 있습니다.

```ts
const numbers: readonly number[] = [1, 2, 3]
numbers.push(4) // Error
```

---

## Tuple

Tuple은 순서와 개수가 정해진 배열입니다.

```ts
const position: [number, number] = [10, 20]
```

남용하면 읽기 어려워질 수 있습니다. 의미 있는 필드명이 필요하다면 객체를 사용합니다.

```ts
// 더 읽기 쉬움
type Position = {
  x: number
  y: number
}
```

---

## any, unknown, never

### any

`any`는 타입 검사를 포기하는 것과 비슷합니다.

```ts
let value: any = 'hello'
value.toFixed() // 컴파일 에러 없음, 런타임 에러 가능
```

가능하면 피합니다.

### unknown

`unknown`은 알 수 없는 값을 안전하게 다루기 위한 타입입니다.

```ts
function handleValue(value: unknown) {
  if (typeof value === 'string') {
    return value.toUpperCase()
  }

  return null
}
```

외부 API, JSON parse, 에러 객체처럼 구조가 확실하지 않은 값에는 `unknown`을 먼저 고려합니다.

### never

`never`는 절대 발생하지 않아야 하는 경우를 표현합니다.

```ts
type Status = 'idle' | 'loading' | 'success' | 'error'

function assertNever(value: never): never {
  throw new Error(`Unexpected value: ${value}`)
}

function getStatusText(status: Status) {
  switch (status) {
    case 'idle':
      return '대기'
    case 'loading':
      return '로딩'
    case 'success':
      return '성공'
    case 'error':
      return '오류'
    default:
      return assertNever(status)
  }
}
```

---

## 함수 타입

```ts
function add(a: number, b: number): number {
  return a + b
}
```

반환 타입은 TypeScript가 추론할 수 있지만, 외부에 공개되는 함수나 중요한 비즈니스 로직은 명시하면 좋습니다.

```ts
type Add = (a: number, b: number) => number

const add: Add = (a, b) => a + b
```

---

## Union 타입

Union은 여러 값 중 하나가 될 수 있음을 표현합니다.

```ts
type Theme = 'light' | 'dark'

function setTheme(theme: Theme) {}

setTheme('light')
setTheme('blue') // Error
```

상태값, 모드, 탭 이름처럼 선택지가 정해진 값에 유용합니다.

---

## Narrowing

Narrowing은 넓은 타입을 조건문을 통해 좁히는 과정입니다.

```ts
function print(value: string | number) {
  if (typeof value === 'string') {
    return value.toUpperCase()
  }

  return value.toFixed(2)
}
```

자주 쓰는 narrowing 방식:

- `typeof`
- `instanceof`
- `in`
- 사용자 정의 type guard
- discriminated union

---

## Discriminated Union

상태별 데이터 구조가 다를 때 가장 강력합니다.

```ts
type ApiState<T> =
  | { status: 'idle' }
  | { status: 'loading' }
  | { status: 'success'; data: T }
  | { status: 'error'; message: string }

function renderState(state: ApiState<string[]>) {
  switch (state.status) {
    case 'idle':
      return '대기 중'
    case 'loading':
      return '불러오는 중'
    case 'success':
      return state.data.join(', ')
    case 'error':
      return state.message
  }
}
```

상태와 데이터를 따로 분리해서 관리하는 것보다 실수가 줄어듭니다.

---

## Generics

Generics는 타입을 함수나 타입 정의를 사용하는 시점에 정하게 해줍니다.

```ts
function wrapArray<T>(value: T): T[] {
  return [value]
}

const numbers = wrapArray(1)
const strings = wrapArray('hello')
```

API 응답 타입에도 자주 사용합니다.

```ts
type ApiResponse<T> = {
  data: T
  message: string
}

type User = {
  id: string
  name: string
}

const response: ApiResponse<User> = {
  data: { id: 'u1', name: 'Dk' },
  message: 'ok',
}
```

---

## Utility Types

TypeScript에는 자주 쓰는 타입 변환 도구가 있습니다.

```ts
type User = {
  id: string
  name: string
  email: string
}

type UserPreview = Pick<User, 'id' | 'name'>
type UserForm = Omit<User, 'id'>
type PartialUser = Partial<User>
type RequiredUser = Required<User>
```

자주 쓰는 유틸리티:

| 타입 | 의미 |
|---|---|
| `Partial<T>` | 모든 속성을 optional로 변경 |
| `Required<T>` | 모든 속성을 필수로 변경 |
| `Pick<T, K>` | 특정 속성만 선택 |
| `Omit<T, K>` | 특정 속성을 제외 |
| `Record<K, T>` | 키와 값 타입으로 객체 생성 |
| `ReturnType<T>` | 함수 반환 타입 추출 |

---

## Type Assertion

타입 단언은 TypeScript보다 개발자가 더 잘 알고 있다고 말하는 것입니다.

```ts
const input = document.querySelector('.input') as HTMLInputElement
```

하지만 남용하면 타입 안정성이 약해집니다. 가능하면 먼저 타입을 좁히는 방식을 사용합니다.

```ts
const input = document.querySelector('.input')

if (input instanceof HTMLInputElement) {
  input.value = 'hello'
}
```

---

## as const와 satisfies

### as const

값을 더 좁은 리터럴 타입으로 고정합니다.

```ts
const tabs = ['home', 'about', 'contact'] as const
type Tab = (typeof tabs)[number]
```

### satisfies

객체가 특정 타입을 만족하는지 검사하면서, 실제 값의 구체적인 타입은 유지합니다.

```ts
type Route = {
  path: string
  label: string
}

const routes = {
  home: { path: '/', label: '홈' },
  about: { path: '/about', label: '소개' },
} satisfies Record<string, Route>
```

---

## tsconfig 기본 권장

신규 프로젝트라면 가능한 한 `strict`를 켜는 것을 권장합니다.

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "ESNext",
    "moduleResolution": "Bundler",
    "strict": true,
    "noUncheckedIndexedAccess": true,
    "exactOptionalPropertyTypes": true,
    "skipLibCheck": true
  }
}
```

단, 기존 JavaScript 프로젝트를 점진적으로 전환하는 경우에는 한 번에 모든 strict 옵션을 켜기보다 단계적으로 적용합니다.

---

## 프론트엔드 실무 적용 기준

### API 응답은 타입을 따로 둡니다

```ts
type UserResponse = {
  id: string
  name: string
  email: string
}
```

### 화면에서 쓰는 모델과 API 모델을 분리할 수 있습니다

```ts
type UserViewModel = {
  id: string
  displayName: string
}

function toUserViewModel(user: UserResponse): UserViewModel {
  return {
    id: user.id,
    displayName: user.name,
  }
}
```

### 이벤트 타입은 필요할 때 명시합니다

```ts
function handleInput(event: Event) {
  const target = event.target

  if (!(target instanceof HTMLInputElement)) return

  console.log(target.value)
}
```

---

## 피해야 할 패턴

### 무분별한 any

```ts
// Bad
function parse(data: any) {
  return data.user.name
}
```

### 타입 단언으로 오류 숨기기

```ts
// Bad
const user = response as User
```

### 타입과 실제 데이터가 다른데 억지로 맞추기

```ts
// Bad
const count: number = apiCount as number
```

외부 데이터는 런타임 검증이 필요할 수 있습니다. TypeScript 타입은 컴파일 시점 안전망이지, 서버 응답을 자동으로 검증하지 않습니다.

---

## TypeScript 체크리스트

- [ ] `any`를 꼭 필요한 곳에만 사용했다.
- [ ] 외부 데이터는 `unknown` 또는 명확한 응답 타입으로 다뤘다.
- [ ] optional 값은 사용 전에 확인했다.
- [ ] 상태값은 문자열 union으로 제한했다.
- [ ] 상태별 데이터는 discriminated union을 고려했다.
- [ ] 반복되는 타입 변환은 Utility Types를 사용했다.
- [ ] 타입 단언보다 narrowing을 먼저 사용했다.
- [ ] 공개 함수의 매개변수와 반환 타입이 명확하다.
- [ ] `strict` 적용 여부를 프로젝트 상황에 맞게 검토했다.

---

## 참고 자료

- TypeScript Handbook: https://www.typescriptlang.org/docs/handbook/intro.html
- Everyday Types: https://www.typescriptlang.org/docs/handbook/2/everyday-types.html
- Narrowing: https://www.typescriptlang.org/docs/handbook/2/narrowing.html
- Utility Types: https://www.typescriptlang.org/docs/handbook/utility-types.html
