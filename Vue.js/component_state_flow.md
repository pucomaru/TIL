
# 📌 Vue Props & Emit 정리

## Props란?
- 부모 컴포넌트로부터 자식 컴포넌트로 **데이터를 전달할 때 사용하는 속성**
- 부모는 자식에게 **props를 전달(Pass Props)**  
- 자식은 자신에게 일어난 일을 부모에게 **이벤트로 알림(Emit Event)**

---

##  Props의 특징

- 부모 → 자식으로만 데이터 전달 가능 (단방향)
- 자식 컴포넌트 내부에서 props 값을 **직접 수정 불가**
- 부모 컴포넌트가 갱신되면, 자식 컴포넌트의 props도 자동으로 최신 상태로 갱신됨

---

##  One-Way Data Flow

- 모든 props는 **부모 → 자식** 간의 **단방향 바인딩(one-way-down binding)**  
- 즉, 자식은 props를 수신만 하며 직접 수정하지 않음

---

##  Props 사용법

### 1. 부모 컴포넌트에서 props 전달

```html
<template>
  <ParentChild my-msg="message" />
</template>
````

* HTML에서는 **kebab-case**로 작성

---

### 2. 자식 컴포넌트에서 props 선언

#### 방식 1: 문자열 배열 사용

```js
<script setup>
defineProps(['myMsg'])
</script>
```

#### 방식 2: 객체 타입 사용

```js
<script setup>
defineProps({
  myMsg: String
})
</script>
```

---

##  Props 세부사항

### 1. Props 이름 컨벤션 (Name Casing)

| 위치              | 컨벤션          |
| --------------- | ------------ |
| 부모 컴포넌트(HTML)   | `kebab-case` |
| 자식 컴포넌트(JS 템플릿) | `camelCase`  |

```html
<!-- Parent -->
<ParentChild user-name="Alice" />
```

```js
// Child.vue
defineProps({
  userName: String
})

<p>{{ userName }}</p>
```

---

### 2. Static Props vs Dynamic Props

```html
<!-- 정적 props: 문자열 "1" -->
<SomeComponent num-props="1" />

<!-- 동적 props: 숫자 1 -->
<SomeComponent :num-props="1" />
```

* `:`을 붙이면 JavaScript 표현식으로 바인딩됨
* `:` 없으면 문자열 리터럴로 전달됨

---

##  Emit

###  자식 → 부모로 이벤트 전달

* 자식은 `$emit()`을 사용해서 부모에게 이벤트 알림
* 부모는 `@event-name`으로 이벤트 수신

###  \$emit() 메서드 구조

```js
$emit('eventName', payload1, payload2, ...)
```

* `eventName`: 이벤트 이름
* `payload`: 부모에게 전달할 데이터

###  예시

#### 자식 컴포넌트

```vue
<script setup>
const props = defineProps({ item: Object })
const emit = defineEmits(['someEvent'])

const buttonClick = () => {
  emit('someEvent', props.item)
}
</script>

<template>
  <button @click="buttonClick">클릭</button>
</template>
```

#### 부모 컴포넌트

```vue
<ChildItem @some-event="handleSomeEvent" />

<script setup>
const handleSomeEvent = (item) => {
  console.log('자식이 보낸 아이템:', item)
}
</script>
```

---

## 📌 핵심 요약

| 구분                 | 설명                 |
| ------------------ | ------------------ |
| `props`            | 부모 → 자식 데이터 전달     |
| `defineProps()`    | 자식에서 props 선언      |
| `emit` / `$emit()` | 자식 → 부모로 이벤트 전달    |
| `v-bind` or `:`    | 동적 props 전달 (JS 값) |
| `kebab-case`       | HTML에서의 props 이름   |
| `camelCase`        | JS/템플릿에서의 props 이름 |

