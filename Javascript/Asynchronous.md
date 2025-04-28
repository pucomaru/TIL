# 📚 비동기 (Asynchronous)

## ✅ 동기(Synchronous)

- 프로그램의 실행 흐름을 **순차적**으로 진행
- 하나의 작업이 **완료된 후** 다음 작업이 실행되는 방식

## ✅ 비동기(Asynchronous)

- 특정 작업이 완료될 때까지 기다리지 않고 다음 작업을 즉시 실행하는 방식
- 작업의 완료 여부에 관계없이 **동시에 다른 작업들을 수행**할 수 있음

## ✅ 비동기의 특징

- 병렬적 수행
- 당장 처리를 완료할 수 없고 시간이 필요한 작업들은 백그라운드에서 실행되며 빠른 결과를 먼저 처리

---

#  JavaScript = Single Thread 언어

### ✅ Thread란?

- 작업을 처리할 때 실제로 작업을 수행하는 주체
- Multi-thread: 여러 개의 작업을 동시에 수행할 수 있음
- Single-thread: 하나의 작업만 수행 가능

### ✅ JavaScript는?

- **Single-thread** 언어이다.
- 하나의 작업을 요청한 순서대로 처리할 수밖에 없다.

### ❓ Single Thread인 JavaScript는 어떻게 비동기 처리를 할까?

→ 답: **JavaScript Runtime** 환경 덕분이다.

---

#  JavaScript Runtime

- JavaScript가 동작할 수 있는 환경 (브라우저 또는 Node.js)
- JavaScript는 Single Thread이므로 비동기 처리를 할 수 있도록 도와주는 환경이 필요하다.

---

#  브라우저 환경에서의 JavaScript 비동기 처리 관련 요소

1. JavaScript Engine의 **Call Stack**
2. **Web API**
3. **Task Queue**
4. **Event Loop**

---

#  브라우저 환경에서의 JavaScript 비동기 처리 동작 방식

1. 모든 작업은 Call Stack(LIFO)으로 들어간 후 처리된다.
2. 오래 걸리는 작업이 Call Stack으로 들어오면 Web API로 보내 별도로 처리한다.
3. Web API에서 처리가 끝난 작업들은 곧바로 Call Stack으로 들어가지 못하고 Task Queue(FIFO)에 순서대로 들어간다.
4. Event Loop가 Call Stack이 비어 있는 것을 계속 체크하고, 비어 있다면 Task Queue에서 가장 오래된 작업을 Call Stack으로 보낸다.

---

##  오래 걸리는 작업 기준

- 브라우저(JavaScript 엔진)가 '비동기로 따로 처리해야 한다'고 판단하는 작업
- 즉시 끝나지 않고 기다려야 하는 작업들 (ex: setTimeout, 서버 요청, DOM 이벤트 등)

---

#  주요 개념 정리

### ✅ Call Stack

- 요청이 들어올 때마다 순차적으로 처리하는 Stack (LIFO)
- 기본적으로 JavaScript의 Single Thread 작업 처리 공간

### ✅ Web API

- JavaScript 엔진이 아닌 브라우저가 제공하는 runtime 환경
- 시간이 소요되는 작업을 처리 (setTimeout, DOM 이벤트, 비동기 요청 등)

### ✅ Task Queue (Callback Queue)

- 비동기 작업이 완료된 후 Callback 함수가 대기하는 Queue (FIFO)

### ✅ Event Loop

- Call Stack과 Task Queue를 지속적으로 모니터링
- Call Stack이 비어 있는지 확인하고, 비어있다면 Task Queue에서 오래된 작업을 Call Stack으로 push

---

# 📚 정리

> JavaScript는 한 번에 하나의 작업을 수행하는 Single Thread 언어로 동기적 처리를 진행하지만, 브라우저 환경에서는 Web API에서 처리된 작업이 Task Queue를 거쳐 Event Loop에 의해 Call Stack에 들어와 순차적으로 실행됨으로써 비동기 작업이 가능해진다.

---

#  AJAX (Asynchronous JavaScript and XML)

- 비동기적인 웹 애플리케이션 개발을 위한 기술
- 브라우저와 서버 간의 데이터를 비동기적으로 교환하는 기술
- 페이지 전체를 새로고침하지 않고도 동적으로 데이터를 불러와 화면을 갱신할 수 있음
- AJAX의 'X'는 XML이라는 데이터 타입을 의미하지만, 요즘은 JSON을 주로 사용

### ✅ 목적
- 비동기 통신
- 부분 업데이트
- 서버 부하 감소

### ✅ 특징
- 하나의 특정한 기술이 아니라, 비동기적인 웹 애플리케이션 개발에 사용하는 기술들의 집합을 의미

---

#  Axios

- 브라우저와 Node.js 환경 모두에서 사용할 수 있는 **Promise 기반 HTTP 클라이언트 라이브러리**
- 서버와의 HTTP 요청과 응답을 간편하게 처리할 수 있도록 지원
- Promise API를 기반으로 비동기 처리를 더 쉽게 할 수 있음

### ✅ 요약
- **AJAX** = 서버랑 통신하는 기본 기술
- **Axios** = AJAX를 더 쉽게 사용할 수 있게 해주는 라이브러리

✅ 프론트엔드에서 Axios를 활용하여 DRF(Django REST Framework) API 서버로 요청을 보내고 받아온 데이터를 비동기적으로 처리하는 로직을 작성할 수 있다.

---

#  Promise Object

- 자바스크립트에서 비동기 작업을 처리하기 위한 객체
- 주요 메서드:
  - `.then()` → 작업이 성공적으로 완료되었을 때 실행될 콜백 함수 지정
  - `.catch()` → 작업이 실패했을 때 실행될 콜백 함수 지정

---

#  콜백 지옥 (Callback Hell)

- 비동기 처리를 위한 콜백을 작성할 때 마주치는 문제
- 콜백 함수가 중첩되면서 코드의 가독성이 떨어지고 유지보수가 어려워짐

### ✅ 원인
- 비동기 작업을 순차적으로 실행하기 위해 콜백을 중첩해서 작성했을 때 발생

---

#  Promise

- JavaScript에서 비동기 작업의 결과를 나타내는 객체
- 비동기 작업이 완료되었을 때 성공 결과를 반환하거나, 실패 시 에러를 처리할 수 있도록 지원

---

#  then() 메서드 Chaining의 장점

1. 가독성 향상
2. 에러 처리를 일관성 있게 할 수 있음
3. 유연성 높음
4. 코드 관리 편리

---

