# jQuery to Vanilla JS Guide

> jQuery로 작성하던 DOM, 이벤트, 스타일, Ajax 코드를 순수 JavaScript로 옮기기 위한 실전 가이드입니다.

작성: Heo Do Kyung

---

## 목차

- [왜 Vanilla JS로 바꿀까](#왜-vanilla-js로-바꿀까)
- [전환할 때의 원칙](#전환할-때의-원칙)
- [요소 선택](#요소-선택)
- [반복 처리](#반복-처리)
- [DOM 탐색](#dom-탐색)
- [이벤트](#이벤트)
- [이벤트 위임](#이벤트-위임)
- [클래스 조작](#클래스-조작)
- [스타일 조작](#스타일-조작)
- [DOM 생성과 삽입](#dom-생성과-삽입)
- [텍스트와 HTML 업데이트](#텍스트와-html-업데이트)
- [Ajax와 fetch](#ajax와-fetch)
- [애니메이션과 표시 상태](#애니메이션과-표시-상태)
- [자주 쓰는 변환 표](#자주-쓰는-변환-표)
- [전환 체크리스트](#전환-체크리스트)

---

## 왜 Vanilla JS로 바꿀까

jQuery는 오랫동안 좋은 도구였습니다. 선택자, 이벤트, Ajax, 애니메이션을 간단하게 처리할 수 있었고, 브라우저 차이를 줄이는 데도 도움이 됐습니다.

하지만 지금은 상황이 달라졌습니다.

- 최신 브라우저의 DOM API가 충분히 좋아졌습니다.
- Vue, React 같은 프레임워크는 DOM을 직접 만지는 방식과 충돌할 수 있습니다.
- 작은 기능만 위해 jQuery를 추가하면 번들 크기와 의존성이 늘어납니다.
- 프레임워크 안에서는 상태를 기준으로 UI를 그리는 방식이 더 안전합니다.

그래서 신규 프론트엔드 프로젝트에서는 가능한 한 순수 JavaScript를 기본으로 두는 편이 좋습니다.

이 문서는 이전에 정리해둔 jQuery → 순수 JavaScript 변환 메모를 바탕으로, 실제 작업에서 바로 보기 좋게 다시 구성했습니다.

---

## 전환할 때의 원칙

1. 단순 치환보다 의도를 먼저 봅니다.
2. Vue/React 안에서는 DOM 직접 조작을 최소화합니다.
3. 이벤트는 가능하면 한 곳에서 관리합니다.
4. `innerHTML`보다 `textContent`를 우선합니다.
5. Ajax는 `fetch`와 `async/await` 기반으로 정리합니다.
6. 보여주기/숨기기는 인라인 스타일보다 클래스 토글을 우선합니다.

---

## 요소 선택

```js
// jQuery
$('.box')
$('#app')

// Vanilla JS
const box = document.querySelector('.box')
const boxes = document.querySelectorAll('.box')
const app = document.querySelector('#app')
```

`querySelector`는 첫 번째 요소만 가져옵니다. 여러 개를 다룰 때는 `querySelectorAll`을 사용합니다.

```js
const boxes = document.querySelectorAll('.box')
```

`querySelectorAll`의 결과는 배열처럼 보이지만 `NodeList`입니다. 대부분 `forEach`는 사용할 수 있지만, 배열 메서드가 필요하면 배열로 바꿉니다.

```js
const boxArray = [...document.querySelectorAll('.box')]
```

---

## 반복 처리

```js
// jQuery
$('.box').each(function () {
  $(this).hide()
})

// Vanilla JS
document.querySelectorAll('.box').forEach((box) => {
  box.hidden = true
})
```

단순 숨김은 `style.display = 'none'`보다 `hidden` 속성이나 클래스 토글이 더 의도가 분명할 때가 많습니다.

```js
box.classList.add('is-hidden')
```

---

## DOM 탐색

```js
const box = document.querySelector('.box')

box.parentElement
box.nextElementSibling
box.previousElementSibling
box.children
box.closest('.card')
```

jQuery와 비교하면 다음과 같습니다.

| jQuery | Vanilla JS |
|---|---|
| `.parent()` | `parentElement` |
| `.next()` | `nextElementSibling` |
| `.prev()` | `previousElementSibling` |
| `.find('.item')` | `element.querySelector('.item')` |
| `.closest('.card')` | `element.closest('.card')` |

```js
// jQuery
const item = $('.container').find('.item')

// Vanilla JS
const container = document.querySelector('.container')
const item = container.querySelector('.item')
```

---

## 이벤트

```js
// jQuery
$('.button').on('click', function (event) {
  console.log(event)
})

// Vanilla JS
const button = document.querySelector('.button')

button.addEventListener('click', (event) => {
  console.log(event)
})
```

여러 요소에 이벤트를 붙일 때:

```js
document.querySelectorAll('.button').forEach((button) => {
  button.addEventListener('click', handleClick)
})
```

문서 전체 이벤트:

```js
document.addEventListener('keyup', (event) => {
  if (event.key === 'Escape') {
    closeModal()
  }
})
```

---

## 이벤트 위임

동적으로 추가되는 요소에는 이벤트 위임이 좋습니다.

```js
// jQuery
$('.search-container').on('click', '.search-result', function () {
  console.log(this)
})
```

```js
// Vanilla JS
const container = document.querySelector('.search-container')

container.addEventListener('click', (event) => {
  const result = event.target.closest('.search-result')

  if (!result || !container.contains(result)) return

  console.log(result)
})
```

`event.target`이 내부 아이콘이나 span일 수 있으므로 `closest`를 사용하는 편이 안전합니다.

---

## 클래스 조작

```js
const box = document.querySelector('.box')

box.classList.add('is-active')
box.classList.remove('is-active')
box.classList.toggle('is-active')
box.classList.contains('is-active')
box.classList.replace('is-active', 'is-disabled')
```

jQuery와 비교:

| jQuery | Vanilla JS |
|---|---|
| `.addClass('on')` | `classList.add('on')` |
| `.removeClass('on')` | `classList.remove('on')` |
| `.toggleClass('on')` | `classList.toggle('on')` |
| `.hasClass('on')` | `classList.contains('on')` |

여러 클래스를 한 번에 처리할 수 있습니다.

```js
box.classList.add('is-active', 'is-highlighted')
box.classList.remove('is-active', 'is-highlighted')
```

---

## 스타일 조작

```js
// jQuery
$('.box').css('color', '#000')

// Vanilla JS
document.querySelector('.box').style.color = '#000'
```

여러 스타일:

```js
const box = document.querySelector('.box')

Object.assign(box.style, {
  color: '#000',
  backgroundColor: 'red',
})
```

다만 스타일을 직접 넣기보다 클래스 토글을 먼저 고려합니다.

```css
.box.is-error {
  color: var(--color-danger);
}
```

```js
box.classList.add('is-error')
```

---

## DOM 생성과 삽입

```js
// jQuery
const item = $('<li/>').text('새 항목')
$('.list').append(item)
```

```js
// Vanilla JS
const item = document.createElement('li')
item.textContent = '새 항목'

const list = document.querySelector('.list')
list.append(item)
```

여러 속성을 넣을 때:

```js
const button = document.createElement('button')
button.type = 'button'
button.className = 'button'
button.textContent = '저장'
```

---

## 텍스트와 HTML 업데이트

텍스트만 바꿀 때는 `textContent`를 사용합니다.

```js
// jQuery
$('.button').text('저장')

// Vanilla JS
document.querySelector('.button').textContent = '저장'
```

HTML을 넣어야 할 때는 `innerHTML`을 사용할 수 있지만, 외부 입력값을 그대로 넣으면 XSS 위험이 생길 수 있습니다.

```js
// 주의 필요
container.innerHTML = userInput
```

가능하면 요소를 만들어서 넣습니다.

```js
const message = document.createElement('p')
message.textContent = userInput
container.replaceChildren(message)
```

---

## Ajax와 fetch

```js
// jQuery
$.ajax({
  url: '/api/users',
}).done(function (data) {
  console.log(data)
}).fail(function () {
  console.error('error')
})
```

```js
// Vanilla JS
async function fetchUsers() {
  try {
    const response = await fetch('/api/users')

    if (!response.ok) {
      throw new Error('사용자 목록을 불러오지 못했습니다.')
    }

    const data = await response.json()
    console.log(data)
  } catch (error) {
    console.error(error)
  }
}
```

POST 요청:

```js
async function createUser(user) {
  const response = await fetch('/api/users', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(user),
  })

  if (!response.ok) {
    throw new Error('사용자 생성 실패')
  }

  return response.json()
}
```

---

## 애니메이션과 표시 상태

jQuery의 `.hide()`, `.show()`, `.fadeIn()`을 그대로 흉내 내기보다 CSS 클래스로 상태를 관리하는 편이 유지보수에 좋습니다.

```css
.panel {
  opacity: 1;
  visibility: visible;
  transition: opacity 0.2s ease, visibility 0.2s ease;
}

.panel.is-hidden {
  opacity: 0;
  visibility: hidden;
}
```

```js
panel.classList.add('is-hidden')
panel.classList.remove('is-hidden')
```

접근성까지 고려해야 한다면 `hidden`, `aria-hidden`, 포커스 이동까지 함께 봅니다.

---

## 자주 쓰는 변환 표

| jQuery | Vanilla JS |
|---|---|
| `$(document).ready(fn)` | `document.addEventListener('DOMContentLoaded', fn)` |
| `$('.box')` | `document.querySelectorAll('.box')` |
| `$('#app')` | `document.querySelector('#app')` |
| `.find('.item')` | `element.querySelector('.item')` |
| `.on('click', fn)` | `addEventListener('click', fn)` |
| `.addClass('on')` | `classList.add('on')` |
| `.removeClass('on')` | `classList.remove('on')` |
| `.toggleClass('on')` | `classList.toggle('on')` |
| `.hasClass('on')` | `classList.contains('on')` |
| `.css('display', 'none')` | `style.display = 'none'` 또는 클래스 토글 |
| `.text('hello')` | `textContent = 'hello'` |
| `.html(html)` | `innerHTML = html` |
| `.append(child)` | `append(child)` |
| `.remove()` | `remove()` |
| `$.ajax()` | `fetch()` |
| `.attr('disabled', true)` | `setAttribute('disabled', '')` 또는 `disabled = true` |
| `.data('id')` | `dataset.id` |

---

## 전환 체크리스트

- [ ] jQuery가 꼭 필요한 기능인지 먼저 확인했는가?
- [ ] 단순 선택자는 `querySelector` / `querySelectorAll`로 바꿨는가?
- [ ] 여러 요소 처리는 `forEach`로 순회했는가?
- [ ] 동적 요소 이벤트는 이벤트 위임으로 처리했는가?
- [ ] 상태 변경은 인라인 스타일보다 클래스 토글로 처리했는가?
- [ ] 텍스트 업데이트는 `textContent`를 우선했는가?
- [ ] `innerHTML`에 외부 입력을 넣지 않았는가?
- [ ] Ajax는 `fetch` + `async/await`로 정리했는가?
- [ ] Vue/React 안에서 직접 DOM 조작을 하지 않아도 되는지 검토했는가?
- [ ] 접근성 상태까지 함께 확인했는가?

---

## 참고

이 문서는 허도경이 예전에 정리한 jQuery → 순수 JavaScript 변환 메모를 바탕으로, 현재 프론트엔드 작업 기준에 맞게 다시 정리했습니다.
