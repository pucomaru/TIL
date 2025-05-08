
#  Vue.js Template Syntax 정리 노트

## 📌 Template Syntax란?
HTML 기반 템플릿 구문으로, **DOM과 Vue 인스턴스의 데이터를 선언적으로 바인딩**할 수 있게 해줍니다.  
→ Vue가 DOM을 구성 요소 인스턴스와 연결해주는 방식입니다.

---

##  Template Syntax 종류

1. **Text Interpolation (텍스트 보간)**
2. **Raw HTML**
3. **Attribute Bindings**
4. **JavaScript Expressions (JS 표현식)**

---

## 1️⃣ Text Interpolation (텍스트 보간)

```html
<p>Message: {{ msg }}</p>
````

* `{{ }}` ← 콧수염 구문 사용
* 가장 기본적인 데이터 바인딩 방식
* `msg` 값이 바뀌면 화면도 자동 갱신됨

---

## 2️⃣ Raw HTML

```html
<div v-html="rawHtml"></div>
```

```js
const rawHtml = ref('<span style="color:red">This should be red.</span>');
```

* `v-html`을 사용하면 **HTML 문자열을 실제 HTML 요소로 렌더링**
* 콧수염 구문(`{{ }}`)은 HTML을 텍스트로 처리하므로 사용 불가

⚠️ 보안상 사용자 입력을 그대로 넣지 않도록 주의!

---

## 3️⃣ Attribute Bindings (속성 바인딩)

```html
<div v-bind:id="dynamicId"></div>
```

```js
const dynamicId = ref('my-id');
```

* HTML 속성에 Vue 데이터를 바인딩할 때 사용
* 값이 `null` 또는 `undefined`면 속성이 제거됨

### ✅ 약어(Shorthand)

```html
<img :src="imageSrc" />
<a :href="myUrl">Move to url</a>
```

* `v-bind:`는 `:`으로 축약 가능

###  동적 속성 이름

```html
<button :[key]="myValue"></button>
```

* 대괄호 `[]` 안에 JavaScript 표현식 사용 가능
* 속성 이름은 **소문자**로만 가능 (브라우저에서 소문자로 처리)

---

## 4️⃣ JavaScript Expressions (JS 표현식)

```html
{{ number + 1 }}
{{ ok ? 'YES' : 'NO' }}
{{ message.split('').reverse().join('') }}

<div v-bind:id="`list-${id}`"></div>
```

* 콧수염이나 디렉티브 내에서 JS 표현식 사용 가능
* 단, 복잡한 로직은 **템플릿에서 피하고 메서드나 계산된 속성으로 분리**하는 것이 좋음

---

##  Directive란?

* `v-` 접두사가 붙은 **Vue 특수 속성**
* 값은 단일 JavaScript 표현식이어야 하며, **데이터 변화에 반응해 DOM을 업데이트**

---

##  v-bind 사용 예시

### ✅ 속성 바인딩

```html
<img v-bind:src="imageSrc" />
<a v-bind:href="myUrl">Move to url</a>
```

### ✅ 클래스 & 스타일 바인딩

* 객체나 배열을 이용해 동적 스타일 적용 가능

```html
<div :class="{ active: isActive }"></div>
<div :style="{ color: activeColor }"></div>
```

---

##  Event Handling (이벤트 처리)

### 기본 형태

```html
<button v-on:click="doSomething">Click me</button>
```

###  약어

```html
<button @click="doSomething">Click me</button>
```

* `v-on:` → `@`로 축약 가능
* 인라인 핸들러와 메서드 핸들러 모두 가능

---

##  Form Input Bindings (폼 입력 바인딩)

### 🔸 단방향 바인딩

```html
<p>{{ message }}</p>
```

```js
data(){
  return {
    message: '안녕'
  }
}
```

* JS → 화면
* 사용자가 입력해도 `message` 값은 변경되지 않음

---

### 🔹 양방향 바인딩 (v-model 사용)

```html
<input v-model="username" />
```

```js
data() {
  return {
    username: ''
  }
}
```

* JS ⇄ 화면 (양방향 실시간 동기화)
* 사용자가 입력한 값이 `username`에 반영되고, 반대도 마찬가지

###  v-model 요약

* `v-model`은 **폼 요소에서 양방향 바인딩을 제공**
* 내부적으로는 `v-bind`와 `v-on:input`을 함께 처리하는 것과 같음

