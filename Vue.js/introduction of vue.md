
# Vue.js 정리

Vue.js는 사용자 인터페이스를 구축하기 위한 JavaScript 프레임워크입니다.

---

##  Vue의 핵심 기능

1. **선언적 렌더링 (Declarative Rendering)**  
   → HTML 템플릿에 데이터를 선언적으로 연결할 수 있음  
2. **반응성 (Reactivity)**  
   → 데이터가 변경되면 화면이 자동으로 갱신됨

---

## 📌 Vue의 주요 특징

- 반응형 데이터 바인딩
- 컴포넌트 기반 아키텍처
- 간결한 문법과 직관적인 API
- 유연한 스케일링 (소형 ~ 대형 앱까지 확장 가능)

---

##  Component란?

> 재사용 가능한 UI 단위 블록  
→ 하나의 화면 조각을 독립적으로 구성하여 유지보수를 쉽게 함

---

##  `ref()` 함수

`ref()`는 반응형 상태(데이터)를 선언하는 함수입니다.

- `.value` 속성이 있는 ref 객체를 반환
- 값이 변경되면 템플릿에서도 자동으로 업데이트됨
- 어떤 타입이든 인자로 사용 가능

### 예제:
```js
const { createApp, ref } = Vue

const app = createApp({
  setup() {
    const message = ref('Hello vue!')
    console.log(message)         // ref 객체
    console.log(message.value)   // 'Hello vue!'
  }
})
````

---

##  Vue 애플리케이션 기본 구조

* `createApp()`에 전달되는 객체는 Vue 컴포넌트 정의
* `setup()` 함수 안에서 상태를 선언하고, `return`으로 템플릿에 노출해야 함

### 예제:

```js
const app = createApp({
  setup() {
    const message = ref('Hello vue!')
    return {
      message
    }
  }
})
```

---

## ❓ 왜 ref 객체를 써야 하나?

JavaScript의 일반 변수는 Vue가 감지할 수 없기 때문입니다.
→ Vue는 템플릿에서 사용된 `ref` 값을 추적하여, 값이 변경되면 자동으로 관련 UI를 다시 렌더링합니다.

### 요점 정리:

* Vue는 렌더링 시 사용된 ref를 추적함
* 추적된 ref가 변경되면 자동으로 DOM을 다시 그림
* 이를 위해 `ref()`는 내부적으로 객체 타입을 사용

---

##  Ref Unwrap (언랩)

> 템플릿에서는 `.value`를 생략해도 ref의 실제 값을 자동으로 꺼내주는 기능입니다.

```html
<!-- 템플릿 -->
<p>{{ count }}</p> <!-- 내부적으로는 count.value -->
```

JS 코드에서는 여전히 `.value`로 접근해야 함.

---

## ⚠️ Ref Unwrap 주의사항

| 상황         | 설명                                  | `.value` 생략 가능? |
| ---------- | ----------------------------------- | --------------- |
| 템플릿 내 사용   | `{{ count }}`                       | ✅ 가능            |
| JS 코드 내 사용 | `count.value`                       | ❌ 불가능           |
| 객체 안에 ref  | `{ count: ref(0) }` → `count.value` | ❌               |
| 배열 안에 ref  | `[ref(1), ref(2)]`                  | ❌               |
| 구조 분해 할당   | `const { count } = reactive(obj)`   | ❌ (반응성 깨짐)      |

### ✅ 구조 분해 시 반응성 유지하는 법:

```js
import { reactive, toRefs } from 'vue'

const state = reactive({ count: 0 })
const { count } = toRefs(state) // 반응성 유지
```

---

## ✅ 요약

* `ref()`는 Vue 3에서 반응형 상태를 만들기 위한 핵심 함수
* 템플릿에서는 언랩되어 `.value` 없이 사용 가능
* JS 코드나 객체/배열/구조분해 시에는 `.value`가 필요하거나 `toRefs`가 필요
* Vue는 렌더링 시 ref를 추적하고 변경 시 자동 반영하는 **반응형 시스템**을 가지고 있음

