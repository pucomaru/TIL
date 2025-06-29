

#  IntelliJ 단축키

| 단축키                | 설명                                                          |
| ------------------ | ----------------------------------------------------------- |
| `Alt + Insert`     | 클래스 내부에서 Getter/Setter, Constructor, Override, Method 자동 생성 |
| `Alt + Enter`      | 코드 자동 완성, 구현/오버라이드, 빠른 수정 등                                 |
| `Shift + F6`       | 변수 이름 한꺼번에 바꾸기 (Rename)                                     |
| `Ctrl + Alt + V`   | 변수 추출 (Introduce Variable)                                  |
| `Ctrl + T`         | 메서드 추출 (Extract Method)                                     |
| `Ctrl + Shift + T` | 테스트 클래스 생성                                                  |
| `Ctrl + Shift + ↓` | 메서드/블록을 아래로 이동                                              |

---

#  Map & HashMap 정리

##  Map 이란?

* **Key-Value(키-값)** 쌍으로 데이터를 저장하는 인터페이스
* **키는 중복 ❌ / 값은 중복 ⭕**

```java
Map<String, Integer> map;
```

---

##  HashMap 이란?

* `Map`의 대표 구현 클래스
* 내부적으로 **해시 알고리즘**으로 빠르게 데이터를 저장/검색
* 자바 기본 내장 클래스 (`java.util.HashMap`)
* **순서 보장 ❌** (입력 순서와 무관)

```java
Map<String, String> map = new HashMap<>();
map.put("한국", "서울");
System.out.println(map.get("한국")); // 서울
```

---

## 🔧 주요 메서드

| 메서드                | 설명         |
| ------------------ | ---------- |
| `put(key, value)`  | 키-값 저장     |
| `get(key)`         | 키로 값 조회    |
| `remove(key)`      | 키-값 삭제     |
| `containsKey(key)` | 키 존재 여부 확인 |
| `size()`           | 저장된 개수 확인  |
| `isEmpty()`        | 비어 있는지 확인  |

---

##  사용 예시

```java
Map<Long, Member> store = new HashMap<>();
store.put(1L, new Member("다예"));
Member m = store.get(1L);
System.out.println(m.getName());  // 출력: 다예
```

---

## 🧾 요약 정리

| 항목      | 내용                  |
| ------- | ------------------- |
| Map     | 키-값 저장 인터페이스        |
| HashMap | Map 구현체 (빠름, 순서 없음) |
| 키 중복    | ❌ (덮어쓰기 됨)          |
| 값 중복    | ⭕ 가능                |
| 순서 유지   | ❌ (순서 보장 안 됨)       |
| 내장 여부   | ✅ (`java.util`에 포함) |

---

# 🛠 Gradle

* 자바 프로젝트 관리 자동화 도구
* **컴파일, 라이브러리 추가, 빌드, 실행**까지 자동으로 처리

---

#  스프링 핵심 개념

##  스프링 컨테이너 (Spring Container)

* 객체(빈)를 생성하고 관리하는 **엔진**
* 스프링의 핵심 동작을 담당하는 **중앙 관리자**

---

##  스프링 부트 (Spring Boot)

* 스프링 프레임워크를 **더 쉽고 빠르게 사용**할 수 있도록 도와주는 **자동 설정 도구**

---

##  톰캣 (Tomcat)

* 자바 웹 애플리케이션을 실행하게 해주는 **웹 서버 + 서블릿 컨테이너**
* **외부 요청을 받고 응답하는 통로 역할**

---

##  MVC 패턴

**Model - View - Controller**

---

##  @ResponseBody

* 메서드의 **리턴값을 HTTP 응답 바디에 직접 넣음**
* JSON 등으로 변환되어 클라이언트에 전달됨

---

##  웹 애플리케이션 흐름

```
[사용자 요청] → Controller → Service → Repository → DB
```

---

##  각 계층 역할

1. **Controller**

   * 사용자 요청을 받아 처리 시작
   * Service 계층 호출 후 결과 응답
   * JSON / HTML 등으로 응답

2. **Service**

   * 핵심 비즈니스 로직 처리
   * 여러 Repository 또는 도메인 객체 조합
   * 예) 회원가입 시 중복 체크 + 저장

3. **Repository**

   * DB 접근 및 도메인 객체 저장/조회/삭제
   * JPA 또는 JDBC 사용

4. **Domain**

   * 실제 데이터 구조
   * 예) 회원, 주문, 쿠폰 등 → DB에 저장됨

---

##  스프링 패키지 구조

| 디렉토리   | 설명       |
| ------ | -------- |
| `main` | 실제 실행 코드 |
| `test` | 테스트 코드   |

---

#  제네릭 (Generic)

* 클래스나 메서드에서 **타입을 외부에서 지정**
* **재사용성과 타입 안정성** 향상
* 형식: `클래스명<T>` 또는 `메서드<T>`

### 예시

```java
List<String> list = new ArrayList<>();
Optional<Member> member = Optional.of(new Member());
```

---

#  List<T>

* **같은 타입의 데이터** 여러 개 저장 (순서 있음, 중복 허용)
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

#  Optional<T>

* 값이 **있을 수도, 없을 수도** 있음
* `null` 체크로부터 자유로워짐
* 주로 **리턴 타입**으로 사용

### 주요 메서드

| 메서드               | 설명                    |
| ----------------- | --------------------- |
| `isPresent()`     | 값 존재 여부 확인            |
| `get()`           | 값 꺼내기 (주의: null이면 에러) |
| `orElse(default)` | 값 없을 때 기본값 반환         |
| `ifPresent(람다)`   | 값이 있으면 실행             |

### 예시

```java
Optional<String> name = Optional.of("다예");
name.ifPresent(n -> System.out.println(n)); // 다예 출력

Optional<String> empty = Optional.empty();
System.out.println(empty.orElse("없음")); // 없음
```

---

#  테스트 관련 어노테이션

* `@BeforeEach` : 각 테스트 **시작 전** 실행
* `@AfterEach` : 각 테스트 **종료 후** 실행

---

##  `assertThat()`

```java
assertThat(실제값).isEqualTo(기대한값);
```

---

##  테스트 패턴: `given - when - then`

| 단계    | 설명                        |
| ----- | ------------------------- |
| given | 테스트 준비                    |
| when  | 테스트 실행 대상 메서드 호출          |
| then  | 결과 검증 (`assertThat` 등 사용) |

* 테스트는 **각각 독립적으로** 실행되어야 함
* **순서에 의존하는 테스트는 좋지 않음**

---

#  예외 처리

##  `IllegalStateException`

* 자바 내장 런타임 예외 클래스
* **현재 상태에서 하면 안 되는 작업을 했을 때** 발생

### 예시

* 이미 존재하는 회원 가입 시도
* 닫힌 파일 다시 열기 시도 등


#  DI (Dependency Injection)

* 객체를 직접 생성하지 않고 **외부에서 주입받는 설계 방식**
* 스프링이 DI 컨테이너로 객체를 관리하고 주입해줌

