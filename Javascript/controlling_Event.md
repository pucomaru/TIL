

# 📌 JavaScript Controlling Event

## `event` object
- DOM에서 이벤트가 발생하면 브라우저가 해당 이벤트에 관한 정보를 담은 `event object`를 자동으로 생성

## `event` object 역할
- 이벤트 결과에 대해 그 순간의 상황(어느 요소에서 결과가 발생했는지, 마우스 좌표는 어디인지, 누르는 키는 무엇인지 등)을 지닌 정보를 가지고 있음
- 이를 통해 이벤트와 관련된 구체적인 정보를 참조할 수 있음음

## 이벤트 처리기(event handler)
- DOM 요소에서 이벤트가 발생하면 연결되어 있는 이벤트 처리기가 해당 이벤트를 처리
- **이벤트 처리기 = 이벤트가 발생할 때 실행되는 함수 (콜백 함수)**
- 자주 `addEventListener`로 DOM 요소에 등록

## `.addEventListener()`
- 지정한 DOM 요소에 이벤트 처리기를 건네 준비하는 메서드

```javascript
EventTarget.addEventListener(type, handler);
```

- `type` : 수신할 이벤트 유형 (e.g., 'click', 'mouseover')
- `handler` : 이벤트 발생시 호출되는 콜백 함수 (event object를 처음 매개변수로 받음)

---

## 버블링 (Bubbling)
- 이벤트가 안쪽 요소에서 바깥 요소로 퍼짐 
- 예) 버튼 클릭 -> 버튼의 부모 div도 같이 이벤트 호출

## target vs currentTarget
- **`target`** : 실제로 클릭한 요소 
- **`currentTarget`** : 이벤트를 들고고있는 요소 

## 캡처링 (Capturing)
- 이벤트가 바깥요소에서 안쪽요소로 내려감감

## .preventDefault()
- 해당 이벤트의 **기본 동작을 비활성화**한다
- 예) 좋아요를 눌렀는데 페이지 새로고침 

```javascript
document.querySelector('a').addEventListener('click', function(event) {
  event.preventDefault();
  console.log('링크 이동을 막았습니다!');
});
```
