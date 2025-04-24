# 📌 JavaScript TIL 

## 데이터 타입
1. 원시 자료형
 - 변수에 값이 직접 저장되는 자료형 (불변, 값이 복사)
 - 변수에 할당될 때 값이 복사됨 / 변수 간에 서로 영향을 미치지 않음 
2. 참조 자료형
 - 객체의 주소가 저장되는 자료형 ( 가변, 주소가 복사)
 - 객체를 생성하면 객체의 메모리 주소를 변수에 할당 / 변수 간에 서로 영향을 미침

## Template literals
- 내장된 표현식을 허용하는 문자열 작성 방식
- Backtick(``)을 이용하며, 여러 줄에 걸쳐 문자열을 정의할 수도 있고 JavaScript의 변수를 문자열 안에 바로 연결할 수 있음
- 표현식은 '$'와 중괄호{}로 표기
```python
const age = 10
const message = '홍길동은 ${age}세입니다.'
console.log(message) // 홍길동은 100세입니다.
```

## null vs undefined
null = 프로그래머가 의도적으로 값이 없음을 나타날 때 사용  
undefined = 시스템이나 JavaScript 엔진이 '값이 할당되지 않음'을 나타낼 때 사용

## Boolean
 - true / false
 - 조건문 또는 반복문에서 Boolean이 아닌 데이터 타입은 자동 형변환 규칙에 따라 true 또는 false 변환됨

## 동등 연산자 (==)
- 두 피연산자 같은 값으로 평가되는지 비교 후 boolean 값을 반환 
- '암묵적 타입 변환' 통해 타입을 일치시킨 후 같은 값인지 비교
- 두 피연산자가 모두 객체일 경우 메모리의 같은 객체를 바라보는지 판별
```python
console.log(1 = 1) // true
console.log('hello' == 'hello') // true
console.log('1' == 1 ) // true
console.log(0 == false) // true
```

## 일치 연산자 (===)
 - 두 피연산자의 값과 타입이 모두 같은 경우 true를 반환
 - 엄격한 비교가 이뤄지며 암묵적 타입 변환이 발생하지 않음
 - 특수한 경우를 제외하고는 동등 연산자가 아닌 일치 연산자 사용 권장
 ```python
 console.log(1 === 1) // true
 console.log('hello' === 'hello') // true
 console.log('1' === 1) // false
 console.log(0 === false) // false
 ```

 ## 논리 연산자
 - and 연산 (&&)
 - or 연산 (||)
 - not 연산 (!)

 ## if 
 - 조건 표현식의 결과값을 boolean 타입으로 변환 후 참/거짓을 판단
```python
const name = 'customer'

if (name === 'admin'){
  console.log('관리자님 환영해요')
} else if (name === 'customer'){
  console.log('고객님 환영해요')
} else {
  console.log('반갑습니다. ${name}님')
}
```

## 삼항 연산자
```python
condition ? expression1 : expression2
```
- condition 조건이 참이면 expression1 실행 / 거짓이면 expression2
 
## 반복문 종류
- while
- for
- for ...in
- for ...of

## while
```python
while (조건문){
  // do something
}
```
## for 
```python
for ([초기문]; [조건문]; [증감문]){
  // do something
}
```

## for ...in
```python
for (variable in object){
  statement
}
```

## for ...of
```python
for (variable of iterable){
  statement
}
```

## for ...in / for ...of
- for ...in -> 객체 속성 돌 때
- for ...of -> 배열 값, 문자열, Set,Map 등 이터러블 돌 때
- for ...in은 배열 순회에 권장되지 않는다 
- 배열이나 컬렉션엔 for...of가 더 안전하고 직관적

## 반복문 사용시 cosnt 사용 여부
- for 문 : 최초 정의한 i를 '재할당'하면서 사용하기 때문에 const를 사용하면 에러 발생
- for...in, for...of : 재할당이 아니라, 매 반복마다 다른 속성 이름이 변수에 지정되는 것이므로 const를 사용해도 에러 발생 x

## 함수 정의 2가지 
1. 선언식
``` python
function funcName (){
  statements
}
```
- 호이스팅 됨

2. 표현식
``` python
const funcName = function (){
  statements
}
```
- 호이스팅 되지 않음

### 함수 표현식 사용을 권장하는 이유
- 예측 가능성
- 유연성
- 스코프 관리

## 매개변수 정의 방법
1. 기본 함수 매개변수
``` python
const greeting = function (name = 'Anonymous'){
  return 'Hi ${name}'
}

greeting() // Hi Anonymous
```
2. 나머지 매개변수
- 임의의 수의 인자를 '배열'로 허용하여 가변 인자를 나타내는 방법
``` python
const myFunc = function (param1,param2, ...restPrams){
  return [param1, param2, restPrams]
}
myFunc(1,2,3,4,5) // [1,2,[3,4,5]]
myFunc(1,2) // [1,2,[]]

```

## '...' (Spread syntax)
- 전개 구문
- 배열이나 문자열과 같이 반복 가능한 항목을 펼치는 것 (확장, 전개)

## 화살표 함수 표현식
- 함수 표현식의 간결한 표현법
```python
const arrow = function (name) {
  return 'Hello, ${name}'
}

- >

const arrow = name => 'Hello, ${name}'
```

## Object
- 키로 구분된 데이터 집합을 저장하는 자료형
- 중괄호('{}')를 이용해 작성
- 중괄호 안에는 key: value 쌍으로 구성된 속성을 여러 개 작성 가능
- key 는 문자형만 허용
- value는 모든 자료형 허용
- 속성 참조 : 점 또는 대괄호('[]')로 객체 요소 접근 / key 이름에 띄어쓰기 같은 구분자가 있으면 대괄호 접근만 가능

## Method 
- 객체 속성에 정의된 함수
- object.method() 방식으로 호출

## 'this' keyword
- 함수나 메서드를 호출한 객체를 가리키는 키워드 -> 함수 내에서 객체의 속성 및 메서드에 접근하기 위해 사용
- Javascript에서 this는 함수를 **'호출하는 방법'** 에따라 가리키는 대상이 다름
1. 단순 호출 시 this  : 가리키는 대상 -> 전역 객체
```python
const MyFunc = function(){
  return this
}

console.log(myFunc()) // window
```

2. 메서드 호출 시 this
```python
const myObj = {
  data: 1,
  myFunc: function (){
    return this
  }
}

console.log(myObj.myFunc()) // myObj
```

## this 정리
- JavaScript의 함수는 호출될 때 this를 암묵적으로 전달 받음
- JavaScript에서 this는 함수가 '호출되는 방식'에 따라 결정되는 현재 객체를 나타냄
- Python의 self와 Java의 this가 선언 시 이미 값이 정해지는 것에 비해 Javascript의 this는 함수가 호출되기 전까지 값이 할당되지 않고 호출 시에 결정됨 (동적 할당)
- this가 미리 정해지지 않고 호출방식에 의해 결정되는 것은 함수(메서드)를 하나만 만들어 여러 객체에서 재사용할 수 있다는 장점이 있고 이런 유연함이 실수로 이어질 수 있다는 단점이 있다.

## 추가 객체 문법
1. 단축 속성 : 키 이름과 값으로 쓰이는 변수의 이름이 같은 경우 단축 구문을 사용할 수 있음
```python 
const name = 'Alice'
const age = 30

const user = {
  name: name,
  age: age,
}
-> 
const user ={
  user,
  age,
}
```
2. 단축 메서드 : 메서드 선언 시 function 키워드 생략 가능
```python
const myObj1 ={
  myFunc: function(){
    return 'Hello'
  }
}
->
const myObj1 ={
  myFunc(){
    return 'Hello'
  }
}
```
3. 계산된 속성 (computed property name)
- 키가 대괄호([])로 둘러싸여 있는 속성
-> 고정된 값이 아닌 변수 값을 사용할 수 있음
```python
const product = prompt('물건 이름을 입력해주세요')
const prefix = 'my'
const suffix = 'property'

const bag = {
  [product] : 5,
  [prefix + suffix]: 'value',
}

console.log(bag) // {연필: 5, myproperty: 'value'}
```

4. 구조 분해 할당 
- 배열 또는 객체를 분해하여 객체 속성을 변수에 쉽게 할당할 수 있는 문법
```python 
const userInfo = {
  fistName: 'Alice',
  userId: 'alice123',
  email : 'alice123@gmail.com'
  }

const { fistName} = userInfo
const { fistName, userId} = userInfo
const { firstName, userId, email } = userInfo

console.log(firstName, userId, email)
// Alice alice123 alice123@gmail.com
```

5. Object with '전개 구문'
```python
const obj = {b:2, c:3, d:4}
const newObj = {a: 1, ...obj, e:5}

console.log(newObj) // {a: 1, b:2, c:3, d:4, e:5}
```

6. 유용한 객체 메서드
- Object.keys(객체명) : 객체 key 반환
- Object.values(객체명) : 객체 value 반환

7. Optional chaining('?.')
- 속성이 없는 중첩 객체를 에러 없이 접근할 수 있는 방법
- 만약 참조 대상이 null 또는 undefined라면 에러가 발생하는 것 대신 평가를 멈추고 undefined를 반환
- 장점 : 참조가 누락될 가능성이 있는 경우 연결된 속성으로 접근할 때 더 짧고 간단한 표현식을 작성할 수 있음 / 어떤 속성이 필요한지에 대한 보증이 확실하지 않는 경우에 객체의 내용을 보다 편리하게 탐색할 수 있음
- 존재하지 않아도 괜찮은 대상에만 사용해야 함(남용 X)

## Array
- 순서가 있는 데이터 집합을 저장하는 자료구조
- 대괄호 []를 이용해 작성 
- 주요 메서드 : push/pop -> 배열 끝 요소를 추가 /제거
unshift/shift -> 배열 앞 요소를 추가 / 제거

## 콜백 함수
- 다른 함수에 인자로 전달되는 함수
```python
const numbers2 = [1,2,3]

const callBackFunction = function(num) {
  console.log(num)
}

numbers2.forEach(callBackFunction)
// 1
// 2
// 3
```

## 주요 Array Helper Methods
- forEach : 배열 내의 모든 요소 각각에 대해 함수를 호출 / 반환 값 없음
- map : 배열 내의 모든 요소 각각에 대해 함수를 호출 /함수 호출 결과를 모아 새로운 배열을 반환

## forEach()
- 배열의 각 요소를 반복하여 모든 요소에 대해 함수를 호출
```python
array.forEach(function (item, index,array){
  // do something
})
```
- 콜백함수는 3가지 매개변수로 구성
1. item : 처리할 배열의 요소
2. index : 처리할 배열 요소의 인덱스 (선태 인자)
3. array : forEach를 호출한 배열 (선택 인자)

## map()
- 배열의 모든 요소에 대해 함수를 호출하고, 반환 된 결과 값을 모아 새로운 배열을 반환 
```python
const newArr = array.map(function (item,index,array){
  // do something
})
```