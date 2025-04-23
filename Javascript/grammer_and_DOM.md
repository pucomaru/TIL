# 📘 JavaScript TIL 정리

자바스크립트의 기본 개념부터 DOM 조작까지 정리한 문서입니다.  
변수 선언, 스코프, 실행 환경, DOM 구조 및 조작 방법을 핵심 위주로 요약했습니다.

---

## ✅ 식별자(변수명) 작성 규칙

- 반드시 **문자, 달러($), 밑줄(_)**로 시작
- **대소문자 구분**
- **예약어**(for, if, function 등) 사용 금지

---

## ✅ 변수명 네이밍 케이스

| 케이스         | 사용 위치               |
|----------------|------------------------|
| `camelCase`    | 변수, 함수, 객체 이름에 사용 |
| `PascalCase`   | 생성자 함수, 클래스 이름 |
| `SNAKE_CASE`   | 상수 이름에 사용         |

---

## ✅ 변수 선언 키워드

### 1. `let`
- 블록 스코프
- 재할당 가능
- 재선언 불가능

### 2. `const`
- 블록 스코프
- 재할당 ❌
- 재선언 ❌
- **선언 시 반드시 초기화 필요**

### 3. ~~`var`~~ (권장 ❌)
- 함수 스코프
- 호이스팅 이슈 존재
- 예측 어려운 동작 가능성 있음

---

## ✅ 블록 스코프 (Block Scope)

- 중괄호 `{}` 안이 **스코프 범위**
- 예: `if`, `for`, `function` 내부
- **블록 바깥에서는 변수 접근 불가**

---

## ✅ const를 기본으로 사용하는 이유

- **의도 명확성**: 변경 불가 → 실수 예방
- **코드 안전성**: 불필요한 재할당 방지
- 필요 시에만 `let` 사용 (변경 가능성 명확할 때)

---

## ✅ JavaScript 실행 환경

1. HTML의 `<script>` 태그
2. `.js` 확장자 파일로 외부 스크립트
3. 브라우저 개발자 도구의 Console

---

## ✅ DOM (Document Object Model)

- HTML 문서를 **객체 트리 형태로 표현**
- 자바스크립트로 **문서 구조, 스타일, 콘텐츠 조작** 가능

---

## ✅ `document` 객체

- DOM 트리의 **최상위 객체**
- 페이지 내 모든 요소, 텍스트, 속성에 접근 가능
- DOM 조작의 시작점 역할

---

## ✅ DOM 요소 선택 메서드

| 메서드                    | 설명                   |
|---------------------------|------------------------|
| `document.querySelector()`     | 조건에 맞는 **요소 1개 선택** |
| `document.querySelectorAll()`  | 조건에 맞는 **요소 여러 개 선택** |

---

## ✅ DOM 조작 방법

### 🔸 속성(attribute) 조작

#### 📍 classList 관련
- `element.classList.add("클래스")`
- `element.classList.remove("클래스")`
- `element.classList.toggle("클래스")`

#### 📍 일반 속성
- `getAttribute("속성명")`
- `setAttribute("속성명", "값")`
- `removeAttribute("속성명")`

---

### 🔸 HTML 콘텐츠 조작

- `element.textContent` : 텍스트 변경

---

### 🔸 DOM 요소 생성 / 삭제

- `document.createElement("태그명")`
- `Node.appendChild(요소)`
- `Node.removeChild(요소)`

---

### 🔸 스타일 조작

- `element.style.속성명 = "값"`

---

## ✅ Node vs Element

| 개념     | 설명                           |
|----------|--------------------------------|
| `Node`   | DOM의 가장 기본 단위             |
| `Element`| Node의 하위 유형, 실제 HTML 요소 |

---

## ✅ 호이스팅 (Hoisting)

- 변수 선언이 **코드 최상단으로 끌어올려지는 현상**
- `var`: 선언 전 접근 가능하나 값은 `undefined`
- `let`, `const`: 호이스팅되지만 **TDZ(Temporal Dead Zone)**로 인해 선언 전 접근 시 오류 발생

---

