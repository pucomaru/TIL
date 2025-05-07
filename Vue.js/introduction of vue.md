Vue.js
: 사용자 인터페이스를 구축하기 위한 JavaSciprt 프레임워크

Vue의 2가지 핵심 기능
1. 선언적 렌더링
2. 반응성

Vue의 주요 특징 정리
1. 반응형 데이터 바인딩
2. 컴포넌트 기반 아키텍처
3. 간결한 문법과 직관적인 API
4. 유연한 스케일링

Component
:재사용 가능한 코드 블럭 

ref()
: 반응형 상태(데이터)를 선언하는 함수
-.value 속성이 있는 ref 객체로 래핑하여 반환하는 함수
- ref로 선언된 변수의 값이 변경되면, 해당 값을 사용하는 템플릿에서 자동으로 업데이트
- 인자는 어떠한 타입도 가능
-> 반응형을 가지는 참조 변수를 만드는 것 
```python
const {createApp,ref} = Vue

const app = createApp({
  setup(){
    const message = ref('Hello vue!')
    console.log(message)  //ref 객체
    console.log(message.value) // Hello vue!
  }
})
```

Vue 기본 구조
- createApp()에 전달되는 객체는 Vue 컴포넌트
- 컴포넌트의 상태는 setup() 함수 내에서 선언되어야 하며 객체를 반환해야 함
``` python
const app = createApp({
  setup() {
    const message = ref('Hello vue!')
    return {
      message
    }
  }
})
```

ref 객체가 필요한 이유
- 일반적인 변수가 아닌 객체 데이터 타입으로 사용하는 이유는? 
- Vue는 템플릿에서 ref를 사용하고 나중에 ref의 값을 변경하면 자동으로 변경 사항을 감지하고 그에 따라 DOM을 업데이트 함 ("의존성 추적 기반의 반응형 시스템")
- Vue는 렌더링 중에 사용된 모든 ref를 추적하며, 나중에 ref가 변경되면 이를 추적하는 구성 요소에 대해 다시 렌더링
- 이를 위해서 참조 자료형의 객체 타입으로 구현한 것 (JavaScript에서는 일반 변수의 접근 또는 변형을 감지할 방법이 없기 때문에)

Ref Unwrap
: ref()로 만든 변수는 .value를 통해 실제 값을 꺼낼 수 있는데 템플릿에서는 .value를 생략해도 자동으로 꺼내주는 것 
주의사항
1. 객체안에 ref가 들어가 있을 땐 자동 언랩이 안됨 
2. 배열 안에 ref도 언랩되지 않음
3. ref를 구조 분해 할당하면 반응형이 깨질 수 있음

