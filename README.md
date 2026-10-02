# Assignment 2-3. Simple CRUD Service UI with JavaScript

오픈소스 스튜디오 02분반 / 박찬 (22300330)

JavaScript의 DOM, Event, Array를 이용해서 서버와 DB 없이 한 페이지에서 동작하는 도서 관리 CRUD 서비스를 만들었습니다.

## Deployment

- Vercel 배포 URL: https://2026ossweek5.vercel.app/
- GitHub Repository: https://github.com/2026-2-OSS/assign05-c02-22300330

| 페이지 | 파일 |
| --- | --- |
| 메인 | `index.html` |
| JavaScript DOM Practice | `js_dynamic.html` |
| Simple CRUD Service | `crud.html` |

## Key Learning

1. Array를 사용한 데이터 저장 및관리
2. DOM과제를 통한 동적인 html 관리
3. JavaScript 부모 자식관계 및 영역 관리로 인한 변수 사용불가 유무 차이

## CRUD Service

### 주제

도서 관리 (Book Management)

### 데이터 Field

`id`, `title`(제목), `publishedYear`(출시년도), `price`(가격), `author`(작가), `category`(분류)

초기 데이터는 3개(java, python, C)를 Array에 넣어 두었고, 페이지를 처음 열면 표에 바로 표시된다. 새 데이터의 id는 `++id`로 1씩 증가시켜 부여한다.

### 구현 방법

| 기능 | 구현 방법 |
| --- | --- |
| **Create** | Form 입력값을 Validation으로 검사한 뒤 객체로 만들어 `push()`로 Array에 추가한다. 이후 `form.reset()`으로 입력창을 비우고 `cre()`로 화면을 다시 그린다. |
| **Read** | `cre()` 함수가 표를 비운 뒤(`textContent = ""`) `forEach()`로 Array를 돌면서 행을 만들어 표에 붙인다. 최초 실행(`window.onload`), 추가, 수정, 삭제 후에 호출한다. |
| **Update** | [수정] 버튼을 누르면 해당 도서를 Form에 채우고 `stcheck`에 저장한 뒤 제출 버튼 글자를 "수정"으로 바꾼다. 제출하면 Validation을 거쳐 `findIndex()`로 찾은 Array의 해당 위치를 새 객체로 바꾸고 화면을 갱신한다. |
| **Delete** | `confirm()`으로 확인한 뒤 `filter()`로 해당 id를 제외한 새 Array를 만들어 `books`에 다시 대입한다. 화면 요소만 지우는 것이 아니라 Array에서도 지워진다. |

### Validation

- 제목(`title`)이 비어 있는지 확인 (`trim()` 사용)
- 가격(`price`)이 3000 미만이면 거부
- 작가(`author`)가 비어 있는지 확인 (`trim()` 사용)

Create와 Update가 같은 `add()` 함수를 거치므로 두 기능 모두에 적용된다. 틀리면 `alert()` → `focus()` → `return` 순서로 처리하고 데이터는 추가하지 않는다.

## JavaScript

- `querySelector()` / `getElementById()`: HTML 요소를 찾을 때 사용했다. 선택자에 `#`나 `.`를 빠뜨리면 `null`이 된다.
- `addEventListener()`: 버튼 클릭이나 submit 같은 이벤트에 함수를 연결했다. 함수 이름 뒤에 괄호를 붙이면 바로 실행되므로, 값을 넘길 때는 `() => {}`로 감쌌다.
- `createElement()` / `appendChild()`: 메모리에 요소를 만들고 부모의 마지막 자식으로 붙여 화면에 표시했다.
- `textContent` / `innerText`: 값을 대입하면 기존 자식 요소가 모두 사라지므로 대입 순서에 주의했다.
- `event.preventDefault()`: form submit 시 페이지가 새로고침되어 Array가 초기화되는 것을 막았다.
- Array 메서드: `push()`, `forEach()`, `filter()`, `findIndex()`를 사용했다.
- `classList.add()`: JS로 만든 요소에 CSS 클래스를 붙였다.
- `window.onload`: 페이지가 열릴 때 처음 화면을 그리도록 사용했다.
- `confirm()`: 삭제 전에 사용자에게 확인을 받았다.

## AI / Search Usage



- **사용한 도구**: Claude (AI)
- **사용 방식**: 

1.막힌 부분의 원인 확인

2. Array 메서드와 이벤트 처리 방법등 이해되지 않는 내용에 대한 질문 

3.README 초안 작성

4.README 초안 작성을 제외한 모든 작업에서 Cowork 기능 사용하지 않음.



## Problem & Solution

| 문제 | 원인 | 해결 |
| --- | --- | --- |
| `querySelector("informs")`가 `null` | id 선택자의 `#`를 빠뜨림 | `#informs`로 수정 |
| `appendChild`가 동작하지 않음 | 부모와 자식 방향이 뒤바뀜 | `부모.appendChild(자식)`으로 수정 |
| 삭제 버튼이 사라짐 | `textContent` 대입이 자식 요소를 지움 | 대입 순서를 바꿈 |
| 클릭하기 전에 삭제가 실행됨 | `addEventListener("click", delele(line))`의 괄호 때문에 즉시 실행됨 | `() => delele(line)`으로 감쌈 |
| 삭제해도 데이터가 안 지워짐 | `books.filter(...)` 결과를 저장하지 않음 | `books = books.filter(...)`로 대입 (`let` 사용) |
| 삭제 조건이 항상 `false` | filter 콜백의 `book`이 바깥 `book`을 가려서 `book.id !== book.id`가 됨 | 콜백 매개변수 이름을 `com`으로 바꿔서 구분 |
| `null.value` 에러 | 입력창 id가 불일치 (`publishedYear` vs `year`) | HTML과 JS의 id를 통일 |
| 추가하면 Array가 초기화됨 | form submit이 새로고침을 일으킴 | `event.preventDefault()` 추가 |
| 수정 버튼을 누르자마자 저장됨 | 수정 버튼 리스너에서 `add()`를 직접 호출함 | 수정 버튼은 Form 채우기만 하고, 저장은 제출 버튼에서 처리 |
| `ReferenceError` | `titlle` 오타 | 변수 이름 수정 |
| CSS가 적용 안 된 것처럼 보임 | `.abutton` 클래스가 폼 버튼에는 붙어 있지 않았음 | 해당 버튼에 클래스 추가 |

## Reflection

- 가장 불만이였던 점은 function() 사용시 매개변수를 ()안에 넣기 힘들다는 점이였다. function 간 상호작용을 위해선 전역 변수를 지정해 function간에 변수를 통한 간접적 사용이였다(stcheck변수). 
- 또 위계질서나 위치에따라서 코드가 실행되기도 하고 안되기도 해서 매우 불편했다.