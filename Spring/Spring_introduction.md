단축키
Alt + insert : 클래스 내부에서 getter/setter, constructor, override, method 등을 자동 생성
Alt + Enter : 코드 자동 완성, 구현/오버라이드, 빠른 수정 등
shift + F6 : 변수이름 한꺼번에 바꾸기
Ctrl + alt + v: 변수추출 
Ctrl + T : 메서드추출
Ctrl + Shift + T : 해당 클래스의 테스트 클래스 생성
Ctrl + Shift + 화살표(아래) : 메서드 등 블록 자체를 아래로 내릴 수 있음 


## Map & HashMap 정리

###  Map이란?

* **Key-Value(키-값)** 쌍으로 데이터를 저장하는 인터페이스
* 키는 중복 ❌ / 값은 중복 ⭕

```java
Map<String, Integer> map;
```

---

### HashMap이란?

* `Map`의 대표 구현 클래스
* 내부적으로 **해시 알고리즘**으로 빠르게 데이터를 저장/검색
* 자바 기본 내장 클래스 (`java.util.HashMap`)
* 순서 보장 ❌ (입력 순서와 무관함)

```java
Map<String, String> map = new HashMap<>();
map.put("한국", "서울");
System.out.println(map.get("한국")); // 서울
```

---

###  주요 메서드

| 메서드                | 설명         |
| ------------------ | ---------- |
| `put(key, value)`  | 키-값 저장     |
| `get(key)`         | 키로 값 조회    |
| `remove(key)`      | 키-값 삭제     |
| `containsKey(key)` | 키 존재 여부 확인 |
| `size()`           | 저장된 개수     |
| `isEmpty()`        | 비어 있는지 확인  |

---

###  사용 예시

```java
Map<Long, Member> store = new HashMap<>();
store.put(1L, new Member("다예"));
Member m = store.get(1L);
System.out.println(m.getName());  // 출력: 다예
```

---

###  정리 요약

| 항목      | 내용                  |
| ------- | ------------------- |
| Map     | 키-값 저장 인터페이스        |
| HashMap | Map 구현체 (빠름, 순서 없음) |
| 키 중복    | ❌ (덮어쓰기 됨)          |
| 값 중복    | ⭕ 가능                |
| 순서 유지   | ❌ (순서 보장 안 됨)       |
| 내장 여부   | ✅ (`java.util`에 포함) |

Gradle = 자바 프로젝트 관리 자동화 도구
-> 컴파일, 라이브러리 추가, 빌드, 실행까지 알아서

스프링 컨테이너(Spring Container)
: 객체(빈)를 생성하고 관리하는 엔진 . 즉, 스프링의 핵심 동작을 담당하는 '중앙 관리자'

스프링 부트(Spring Boot)
: 스프링 프레임워크를 더 쉽게 빠르게 사용할 수 있게 도와주는 자동 설정 도구

톰캣(Tomcat)
: 자바 웹 애플리케이션을 실행할 수 있게 해주는 웹 서버이자 서블릿 컨테이너 . 톰캣이 없으면 자바 웹 서버는 외부 요청을 받을 수 없음 따라서 톰캣은 잦바 웹 서버가 외부 HTTP 요청을 받고,처리하고, 응답하는 통로 역할을 해주는 필수 구성요소이다.

MVC:Model, View, Controller

@ResponseBody
: 메서드의 리턴값을 JSON 등 HTTP 응답 바디에 직접 넣어주는 역할을 함

웹 애플리케이션 전형적인 흐름
: [사용자 요청] -> 컨트롤러 -> 서비스 -> 리포지터리 -> DB

각 계층의 역할
1. 컨트롤러
- 웹 MVC의 컨트롤러 역할
- 사용자의 요청을 받아 처리 시작
- 서비스 계층 호출해서 결과를 받아 사용자에게 응답(JSON,HTML 등)
2. 서비스(Service)
- 핵심 비즈니스 로직 구현 
- 여러 리포지토리나 도메인 객체를 조합해서 처리
- ex) 회원 가입 시 중복 체크 + 저장 처리
3. 리포지토리 (Repository)
- DB 접근, 도메인 객체를 DB에 저장하고 ㅈ관리
- JPA나 JDBC를 통해 도메인 객체를 저장/조회/삭제
JPA : 자바 객체로 DB 다루는 자동화 방식 (ORM)
4. 도메인 (Domain)
- 실제 데이터의 구조 / 비즈니스 도메인 객체
- EX) 회원, 주문, 쿠폰 등등 주로 DB에 저장하고 관리됨

스프링 패키지
main - 실제로 실행되는 코드
test - 그 코드가 잘 작동하는지 검사하는 테스트 코드 


##  제네릭(Generic)
- 클래스나 메서드 내부에서 사용할 **타입을 외부에서 지정할 수 있게 하는 문법**
- 코드의 **재사용성과 타입 안정성**을 높여줌
- 형식: `클래스이름<T>` 또는 `메서드이름<T>`

### 예시
```java
List<String> list = new ArrayList<>();
Optional<Member> member = Optional.of(new Member());
````

---

##  List<T>

* 자바의 **자료구조 컬렉션**
* **같은 타입의 데이터를 여러 개** 저장할 수 있음 (순서 있음, 중복 허용)
* 대표 구현체: `ArrayList`, `LinkedList`

### 주요 메서드

* `add(value)` : 값 추가
* `get(index)` : 값 꺼내기
* `size()` : 전체 개수
* `remove(index)` : 삭제

### 예시

```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");
```

---

##  Optional<T>

* 값이 있을 수도, 없을 수도 있음(null일 수도 있음)을 표현하는 래퍼 클래스
* **NullPointerException을 방지**하기 위해 사용
* 주로 리턴 타입으로 사용됨

### 주요 메서드

* `isPresent()` : 값 존재 여부 확인
* `get()` : 값 꺼내기 (주의: 값 없으면 에러)
* `orElse(default)` : 값이 없을 경우 기본값 반환
* `ifPresent(람다)` : 값이 있을 경우만 실행

### 예시

```java
Optional<String> name = Optional.of("다예");
name.ifPresent(n -> System.out.println(n)); // 다예 출력

Optional<String> empty = Optional.empty();
System.out.println(empty.orElse("없음")); // 없음
```

@AfterEach
: 각 테스트 메서드가 끝날 때마다 자동으로 실행되는 메서드에 붙이는 어노테이션 

@BeforeEach
: 각 테스트 메서드가 실행되기 전에 항상 먼저 실행되는 메서드

assertThat()
` asserThat(실제값).isEqualTo(기대한 값)`
: 실제 실행 결과가 기대한 값과 같은 지 비교하는 코드

테스트 패턴
given - when- then 패턴
given: 테스트에 필요한 준비 코드
when: 테스트 대상 메서드를 실행
then: 결과를 검정 (assertThat 등 사용)

테스트는 각각 독립적으로 실행되어야 한다. 테스트 순서에 의존관계가 있는 것은 좋은 테스트가 아니다.

IllegalStateException
: 자바에 내장된 표준 예외 클래스 / 프로그램이 현재 상테에서 하면 안되는 일을 했을 때 사용하는 런타임 예외
ex) 이미 존재하는 회원을 또 가입시키려 할 때/ 이미 닫힌 파일을 다시 열려할 때

DI: 의존성 주입(Dependency Injection)
:필요한 객체를 직접 생성하지 않고, 외부에서 주입받도록 만드는 설계 방식


