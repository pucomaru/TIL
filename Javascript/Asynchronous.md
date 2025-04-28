비동기 Asynchronous

동기 : 프로그램의 실행 흐름이 순차척으로 질행 / 하나의 작업이 완료된 후에 다음 작업이 실행되는 방식

비동기 : 특정 작업의 실행이 완료될 때까지 기다리지 않고 다음 작업을 즉시 실행하는 방식 /작업의 완료 여부를 신경 쓰지 않고 동시에 다른 작업들을 수행할 수 있음

비동기 특징 
- 병렬적 수행
- 당장 처리를 완료할 수 없고 시간이 필요한 작업들은 백그라운드에서 실행되며 빨리 완료되는 작업부터 처리

JavaScript = Single Thread 언어
Thread 란 ? 작업을 처리할 때 실제로 작업을 수행하는 주체로, multi-thread라면 업무를 수행할 수 있는 주체가 여러 개라는 의미 

JavaScript는 한번에 여러 일을 수행할 수 없다. 즉, JavaScript는 하나의 작업을 요청한 순서대로 처리할 수 밖에 없음. 
그러면 어떻게 Single Thread인 JavaScript가 비동기 처리를 할 수 있을까?

JavaScript Runtime 
- JavaScript가 동작할 수 있는 환경 (브라우저 또는 Node.js)
- JavaScript는 Single Thread이므로 비동기 처리를 할 수 있도록 도와주는 환경이 필요

브라우저 환경에서의 JavaScript 비동기 처리 관련 요소
1. JavaScript Engine의 Call Stack
2. Web API
3. Task Queue
4. Event Loop

브라우저 환경에서의 JavaScript 비동기 처리 동작 방식
1. 모든 작업은 Call Stack(LIFO)으로 들어간 후 처리된다.
2. 오래 걸리는 작업이 Call Stack으로 들어오면 Web API로 보내 별도로 처리하도록 한다.
3. Web API에서 처리가 끝난 작업들은 곧바로 Call Stack으로 들어가지 못하고 Task Queue(FIFO)에 순서대로 들어간다.
4. Event Loop가 Call Stack이 비어 있는 것을 계속 체크하고 Call Stack이 빈다면 Task Queue에서 가장 오래된(가장 먼저 처리되어 들어온) 작업을 Call stack으로 보낸다. 

여기서 오래걸리는 작업 기준 : 브라우저(JavaScript 엔진)가 '비동기로 따로 처리해야 한다'고 판단하는 작업 보통 즉시 끝나지 않고 기다려야 하는 작업들 / 바로 처리할 수없고, '언제 끝날지 모르는 대기'가 필요한 작업들은 브라우저가 Call Stack에 쌓지 않고 Web API 쪽으로 보낸다. 

Call Stack
- 요청이 들어올 때 마다 순차적으로 처리하는 Stack(LIFO)
- 기본적으로 JavaScript의 Single Thread 작업 처리

Web API
- JavaScript 엔진이 아닌 브라우저에서 제공하는 runtime 환경
- 시간이 소요되는 작업을 처리(setTimeout, DOM EVENT, 비동기 요청 등등)

Task Queue (Callback Queue)
- 비동기 처리된 Callback 함수가 대기하는 Queue(FIFO)

Event Loop
- 태스트가 들어오길 기다렸다가 태스가 들어오면 이를 처리하고, 처리할 태스그가 없는 경우에 잠드는, 끊임없이 돌아가는 자바스크립트 내 루프
- Call Stack과 Task Queue를 지속적으로 모니터링
- Call Stack이 비어 있는지 확인 후 비어있다면 Task Queue에서 대기 중인 오래된 작업을 Call Stack으로 push

정리 :JavaScript는 한 번에 하나의 작업을 수행하는 Single Thread 언어로 동기적 처리를 진행 하지만 브라우저 환경에서는 Web API에서 처리된 작업이 지속적으로 Task Queue를 거쳐 Event Loop에 의해 Call Stack에 들어와 순차적으로 실행됨으로써 비동기 작업이 가능한 환경이 됨 

Ajax (Asynchronous JavaScript and XML)
- 비동기적인 웹 애플리케이션 개발을 위한 기술 
- 브라우저와 서버 간의 데이터를 비동기적으로 교환하는 기술
- Ajax를 사용하면 페이지 전체를 새로고침 하지 않고도 동적으로 데이터를 불러와 화면을 갱신할 수 있음 
- Ajax의 'x'는 XML이라는 데이터 타입을 의미하긴 하지만, 요즘은 더 가벼운 용량과 JavaScript의 일부라는 장점 때문에 JSON을 많이 사용
목적 : 비동기 통신, 부분 업데이트, 서버 부하 감소
- 하나의 특정한 기술을 의미하는 것이 아니라, 비동기적인 웹 애플리케이션 개발에 사용하는 기술들의 집합을 지칭 

Axios
- 브라우저와 Node.js에서 사용할 수 있는 Promise 기반의 HTTP 클라이언트 라이브러리
- 서버와의 HTTP 요청과 응답을 간편하게 처리할 수 있도록 도와주는 도구
- 주로 웹 애플리케이션에서 서버와 통신할 때 사용
- Promise API를 기반으로 하여 비동기 처리를 더 쉽게할 수 있음

AJAX = 서버랑 통신하는 기술 / Axios = AJAX를 더 쉽게 쓰게 해주는 도구
-> 프론트에서 Axios를 활용해 DRF로 만든 API 서버로 요청을 보내고, 받아온 데이터를 비동기적으로 처리하는 로직을 작성하게 됨 

'Promise' object
- 자바스크립트에서 비동기 작업을 처리하기 위한 객체
- 주요 메서드 : then() -> 작업이 성공적으로 완료되었을 때 실행될 콜백 함수를 지정 / catch() -> 작업이 실패했을 때 실행될 콜백 함수를 지정

콜백 지옥
- 비동기 처리를 위한 콜백을 작성할 때 마주하는 문제

콜백함수는 비동기 작업을 순차적으로 실행할 수 있게 하는 반드시 필요한 로직 / 비동기 코드를 작성하다 보면 콜백 함수로 인한 콜백 지옥은 빈번히 나타나는 문제이며 이는 코드의 가독성을 해치고 유지 보수가 어려워짐 

Promise
- JavaScript에서 비동기 작업의 결과를 나타내는 객체 / 비동기 작업이 완료되었을 때 결과 값을 반환하거나, 실패 시 에러를 처리할 수 있는 기능을 제공 

then 메서드 chaining의 장점 
1. 가독성
2. 에러 처리
3. 유연성
4. 코드 관리
