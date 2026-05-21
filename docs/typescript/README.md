# TypeScript Guide

> TypeScript를 타입 문법 모음이 아니라, 프론트엔드 코드를 안전하게 유지하는 도구로 정리한 가이드입니다.

정리: Heo Do Kyung

---

## 목차

- [TypeScript를 쓰는 이유](#typescript를-쓰는-이유)
- [기본 타입과 타입 추론](#기본-타입과-타입-추론)
- [type과 interface](#type과-interface)
- [optional과 undefined](#optional과-undefined)
- [union과 narrowing](#union과-narrowing)
- [any, unknown, never](#any-unknown-never)
- [generic](#generic)
- [utility types](#utility-types)
- [as const와 satisfies](#as-const와-satisfies)
- [API 응답 타입](#api-응답-타입)
- [Vue/React에서의 기준](#vuereact에서의-기준)
- [tsconfig 기준](#tsconfig-기준)
- [체크리스트](#체크리스트)

---

## TypeScript를 쓰는 이유

TypeScript는 JavaScript를 완전히 대체하는 다른 언어라기보다, JavaScript 위에 타입이라는 안전망을 더하는 도구입니다.

제가 TypeScript를 쓸 때 기대하는 효과는 세 가지입니다.

1. 런타임 전에 오류를 발견합니다.
2. 함수와 데이터의 의도를 코드에 남깁니다.
3. 리팩터링할 때 안전망을 만듭니다.

TypeScript를 잘 쓴다는 것은 타입을 많이 적는다는 뜻이 아닙니다. 필요한 곳에는 명확히 적고, 추론 가능한 곳은 TypeScript에게 맡기는 쪽이 오래 유지하기 좋습니다.

---

## 기본 타입과 타입 추론

```ts
const name = 'Dk'
const age = 42
const isActive = true
const tags = ['frontend', 'vue']
```

초기값이 명확하면 타입을 직접 쓰지 않아도 됩니다.

```ts
// 불필요하게 길어질 수 있음
const name2: string = 'Dk'
```

반대로 빈 배열, 외부 API 응답, 함수 매개변수처럼 추론이 불안정한 곳은 타입을 명시합니다.

```ts
const selectedIds: string[] = []

function getUser(id: string) {
  return api.get(`/users/${id}`)
}
```

---

## type과 interface

객체 구조는 `type` 또는 `interface`로 정의합니다.

```ts
type User = {
  id: string
  name: string
  age?: number
}
```

선택 기준:

| 상황 | 추천 |
|---|---|
| 일반 객체 모델 | `type` 또는 `interface` 모두 가능 |
| union, tuple, primitive 조합 | `type` |
| 라이브러리 확장, 선언 병합 | `interface` |
| 팀 규칙이 이미 있음 | 팀 규칙 우선 |

프로젝트 안에서 일관되게 쓰는 것이 더 중요합니다.

---

## optional과 undefined

`?`는 값이 없을 수 있음을 의미합니다.

```ts
type User = {
  name: string
  age?: number
}
```

optional 값은 확인 후 사용합니다.

```ts
function printAge(user: User) {
  if (user.age === undefined) return

  console.log(user.age + 1)
}
```

Truthy 체크는 조심합니다.

```ts
// age가 0이면 조건을 통과하지 않음
if (user.age) {}

// 의도가 명확함
if (user.age !== undefined) {}
```

---

## union과 narrowing

Union은 여러 타입 중 하나일 수 있음을 표현합니다.

```ts
type Status = 'idle' | 'loading' | 'success' | 'error'

function renderStatus(status: Status) {
  if (status === 'loading') return '불러오는 중'
  if (status === 'success') return '완료'
  if (status === 'error') return '오류'
  return '대기'
}
```

객체 상태가 여러 형태로 바뀐다면 discriminated union을 사용합니다.

```ts
type AsyncState<T> =
  | { status: 'idle' }
  | { status: 'loading' }
  | { status: 'success'; data: T }
  | { status: 'error'; message: string }

function getMessage(state: AsyncState<string[]>) {
  switch (state.status) {
    case 'success':
      return `${state.data.length}개 로드됨`
    case 'error':
      return state.message
    default:
      return ''
  }
}
```

이 방식은 `data`와 `error`가 동시에 존재하는 애매한 상태를 줄여줍니다.

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

외부 API, `JSON.parse`, `catch`의 에러 객체처럼 구조가 확실하지 않은 값에는 `unknown`을 먼저 고려합니다.

### never

`never`는 발생할 수 없는 상태를 표현할 때 사용합니다.

```ts
function assertNever(value: never): never {
  throw new Error(`Unexpected value: ${value}`)
}
```

Union 타입을 모두 처리했는지 확인할 때 유용합니다.

---

## generic

Generic은 타입을 매개변수처럼 받는 방식입니다.

```ts
function getFirstItem<T>(items: T[]): T | undefined {
  return items[0]
}

const firstName = getFirstItem(['도경', '철수'])
const firstNumber = getFirstItem([1, 2, 3])
```

API 응답 래퍼에도 자주 사용합니다.

```ts
type ApiResponse<T> = {
  data: T
  message: string
  success: boolean
}

type User = {
  id: string
  name: string
}

const response: ApiResponse<User> = {
  data: { id: 'u1', name: 'Dk' },
  message: 'ok',
  success: true,
}
```

---

## utility types

TypeScript는 자주 쓰는 타입 변환 도구를 제공합니다.

| Utility | 용도 |
|---|---|
| `Partial<T>` | 모든 속성을 optional로 변경 |
| `Required<T>` | 모든 속성을 필수로 변경 |
| `Pick<T, K>` | 일부 속성만 선택 |
| `Omit<T, K>` | 일부 속성 제외 |
| `Record<K, T>` | 키-값 객체 타입 생성 |
| `Readonly<T>` | 읽기 전용으로 변경 |
| `ReturnType<T>` | 함수 반환 타입 추출 |

```ts
type User = {
  id: string
  name: string
  email: string
}

type UserPreview = Pick<User, 'id' | 'name'>
type UserForm = Omit<User, 'id'>
type UserPatch = Partial<UserForm>
```

---

## as const와 satisfies

`as const`는 값을 더 좁은 타입으로 고정합니다.

```ts
const STATUS = ['idle', 'loading', 'success', 'error'] as const

type Status = (typeof STATUS)[number]
```

`satisfies`는 값의 타입을 검사하면서도 실제 값의 좁은 타입을 유지합니다.

```ts
type MenuItem = {
  label: string
  path: string
}

const menuItems = [
  { label: '홈', path: '/' },
  { label: '가이드', path: '/guide' },
] satisfies MenuItem[]
```

`as`로 억지 캐스팅하는 것보다 안전합니다.

---

## API 응답 타입

외부에서 들어오는 값은 TypeScript 타입만으로 완전히 안전해지지 않습니다. 런타임 데이터가 타입과 다를 수 있기 때문입니다.

```ts
type User = {
  id: string
  name: string
}

async function fetchUser(id: string): Promise<User> {
  const response = await fetch(`/api/users/${id}`)

  if (!response.ok) {
    throw new Error('사용자 정보를 불러오지 못했습니다.')
  }

  return response.json() as Promise<User>
}
```

더 안전하게 하려면 API 응답을 검증하는 계층을 둡니다. 프로젝트 규모가 커지면 Zod 같은 런타임 검증 도구를 검토할 수 있습니다.

---

## Vue/React에서의 기준

### Vue

```ts
type Props = {
  title: string
  count?: number
}

const props = withDefaults(defineProps<Props>(), {
  count: 0,
})
```

- props 타입은 컴포넌트 상단에서 확인할 수 있게 둡니다.
- emit 이벤트 이름과 payload 타입을 명확히 합니다.
- `ref([])`처럼 빈 배열은 타입을 명시합니다.

```ts
const selectedIds = ref<string[]>([])
```

### React

```tsx
type ButtonProps = {
  children: React.ReactNode
  disabled?: boolean
  onClick?: () => void
}

function Button({ children, disabled = false, onClick }: ButtonProps) {
  return (
    <button type="button" disabled={disabled} onClick={onClick}>
      {children}
    </button>
  )
}
```

- props 타입은 컴포넌트 가까이에 둡니다.
- `React.FC` 사용 여부는 팀 기준을 따릅니다.
- 이벤트 타입은 필요할 때만 명시합니다.

---

## tsconfig 기준

가능하면 `strict`를 켭니다.

```json
{
  "compilerOptions": {
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "noUncheckedIndexedAccess": true
  }
}
```

처음부터 모든 옵션을 켜기 어렵다면 아래 순서로 적용합니다.

1. `strictNullChecks`
2. `noImplicitAny`
3. `noUncheckedIndexedAccess`
4. 전체 `strict`

---

## 체크리스트

- [ ] 불필요한 타입 표기를 줄였는가?
- [ ] 빈 배열과 외부 데이터에는 타입을 명시했는가?
- [ ] `any` 대신 `unknown`을 고려했는가?
- [ ] optional 값은 확인 후 사용했는가?
- [ ] 문자열 상태값은 union으로 제한했는가?
- [ ] API 응답 타입과 실제 데이터 검증을 구분했는가?
- [ ] 타입 이름이 도메인을 설명하는가?
- [ ] `as` 캐스팅을 남발하지 않았는가?
- [ ] 컴포넌트 props와 emit/event 타입이 명확한가?
- [ ] `tsconfig` strict 기준을 점진적으로 적용하고 있는가?
