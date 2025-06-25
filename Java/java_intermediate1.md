##  단축키

###  Ctrl + Alt + N

* Inline Variable: 변수 추출 없이 표현식을 직접 삽입하는 리팩토링

---

##  Object 클래스

###  기본 개념

* 자바에서 모든 클래스의 최상위 부모 클래스는 항상 Object 클래스
* 부모가 없으면 묵시적으로 Object 클래스를 상속받는다.
* toString()은 Object 클래스의 메서드

###  자바에서 Object 클래스가 최상위 부모 클래스인 이유

#### 🔹 공통 기능 제공

* 모든 객체는 공통기능을 편리하게 제공(상속)받을 수 있다.

  * 객체의 정보를 제공하는 toString()
  * 객체의 같음을 비교하는 equals()
  * 객체의 클래스 정보를 제공하는 getClass()
  * 등등

#### 🔹 다형성의 기본 구현

* 부모는 자식을 담을 수 있다.
* Object는 모든 클래스의 부모 클래스이다. 따라서 모든 객체를 참조할 수 있다.

---

##  instanceof 핵심 정리

* instanceof는 변수 타입이 아니라 실제 객체의 타입을 확인한다.
* obj가 Object 타입으로 선언돼도, 안에 실제로 Dog 객체가 들어있으면 obj instanceof Dog는 true가 된다.
* instanceof는 true/false만 반환하며 타입 확인만 한다.
* 자바 16부터 instanceof에 패턴 매칭을 적용해 자동으로

---

##  Object를 활용한 다형성의 한계

* Object는 모든 객체를 대상으로 다형적 참조를 할 수 있다.

* Object를 통해 전달받은 객체를 호출하려면 각 객체에 맞는 다운캐스팅 과정이 필요하다.

* Object가 모든 메서드를 알고 있는 것이 아니다.

* toString 오버라이딩 : alt+insert로 하면 매우 편리함

---

##  정적 의존관계 vs 동적 의존관계

###  정적 의존관계

* 코드 상에서 직접 new로 객체 생성
* 컴파일 시점에 의존성이 결정
* 코드 수정 없이는 의존성 교체 어려움

###  동적 의존관계

* 객체를 외부에서 주입 (생성자, setter, DI)
* 런타임 시점에 의존성 결정
* 코드 변경 없이 객체 교체 가능

---

##  equals() 동일성과 동등성

###  동일성

* == 연산자를 사용해서 두 객체의 참조가 동일한 객체를 가리키고 있는지 확인

###  동등성

* equals() 메서드를 사용하여 두 객체가 논리적으로 동등한지 확인
* 동등성 비교가 항상 필요한 것은 아니다. 동등성 비교가 필요한 경우에만 equals()를 재정의하면 된다.

---

##  기본형과 참조형의 경우

* 기본형: 하나의 값을 여러 변수에서 절대로 공유하지 않는다.
* 참조형: 하나의 객체를 참조값을 통해 여러 변수에서 공유할 수 있다.
* 자바는 항상 값을 복사해서 대입한다.

---

##  사이드 이펙트

* 프로그래밍에서 어떤 계산이 주된 작업 외에 추가적인 부수 효과를 일으키는 것을 말함. (부정적인 의미)
* 여러 변수가 하나의 객체를 공유하는 것을 막을 방법은 없다.
* 기본형은 항상 값을 복사해서 대입하기 때문에 값이 절대로 공유되지 않는다.
* 하지만 참조형의 경우 같은 참조값을 복사해서 대입하기 때문에 여러 변수에서 얼마든지 같은 객체를 공유할 수 있다.

---

##  불변 객체

* 객체의 상태(객체 내부의 값, 필드, 멤버 변수)가 변하지 않는 객체
* 불변이라는 단순한 제약을 사용해서 사이드 이펙트라는 큰 문제를 막을 수 있다.
* 불변 객체는 값을 변경할 수 없다.
* 따라서 불변 객체의 값을 변경하고 싶다면 변경하고 싶은 값으로 새로운 불변 객체를 생성해야 한다.
* 이렇게 하면 기존 변수들이 참조하는 값에 영향을 주지 않는다.

### 참고 - withXxx()

* 불변 객체에서 값을 변경하는 경우 withYear()처럼 'with'로 시작하는 경우가 많다.

* 불변 객체의 메서드가 'with'로 이름 지어진 경우, 그 메서드가 지정된 수정사항을 포함하는 객체의 새 인스턴스를 반환한다는 사실을 뜻한다.

* 정리하자면 with는 관례처럼 사용되는데, 원본 객체의 상태가 그대로 유지됨을 강조하면서 변경사항을 새 복사본에 포함하는 과정을 표현.

* 모든 클래스를 불변으로 만드는 것은 아니다.

---

##  String

* String은 클래스다. int, boolean 같은 기본형이 아니라 참조형이다.

```java
String str1 = "hello"; //기존
String str1 = new String("Hello"); //변경
```

* 문자열은 매우 자주 사용된다.
* 그래서 편의상 쌍따옴표로 문자열을 감싸면 자바 언어에서 new String("hello")와 같이 변경된다.

###  String 기능

* length(): 문자열 길이 반환
* charAt(int index): 특정 인덱스의 문자 반환
* substring(int beginIndex, int endIndex): 문자열의 부분 문자열 반환
* indexOf(String str): 특정 문자열이 시작되는 인덱스 반환
* toLowerCase(), toUpperCase(): 문자열을 소문자 또는 대문자로 반환
* trim(): 문자열 양 끝의 공백을 제거
* concat(String str): 문자열을 더함 (기존 문자열을 바꾸는 것이 아니라 새로운 변수를 지정해줘야함)

---

##  String 클래스 - 비교

* String 클래스 비교할 때는 == 비교가 아니라 항상 equals() 비교를 해야한다.

```java
String str3 = "hello"
String str4 = "hello"
str3 == str4  // true
```

* 문자열 리터럴을 사용하는 경우 자바는 메모리 효율성과 성능 최적화를 위해 문자열 풀을 사용한다.

* 자바가 실행되는 시점에 클래스에 문자열 리터럴이 있으면 문자열 풀에 String 인스턴스를 미리 만들어둔다.

* 이때 같은 문자열이 있으면 만들지 않는다.

* 프로그래밍에서 풀은 공용 자원을 모아둔 곳을 뜻함.

* 참고로 문자열 풀은 힙 영역을 사용.

* 그래도 문자열 비교는 항상 equals()를 사용해서 동등성 비교를 해야 한다.

* String은 불변 객체이다. 따라서 생성 이후에 절대로 내부의 문자열 값을 변경할 수 없다.

---

##  String 클래스 - 주요 메서드

###  문자열 정보 조회

* length(): 문자열 길이 반환
* isEmpty(): 문자열이 비어있는지 확인 (길이가 0)
* isBlank(): 문자열이 비어있는지 확인 (길이가 0이거나 공백만 있는 경우)
* charAt(int index): 지정된 인덱스에 있는 문자를 반환

###  문자열 비교

* equals(Object anObject): 두 문자열 동일한지 비교
* equalsIgnoreCase(String anotherString): 두 문자열을 대소문자 구분 없이 비교
* compareTo(String anotherString): 두 문자열을 사전 순으로 비교
* compareToIgnoreCase(String str): 두 문자열을 대소문자 구분 없이 사전적으로 비교
* startsWith(String prefix): 문자열이 특정 접두사로 시작하는지 확인
* endsWith(String suffix): 문자열이 특정 접미사로 끝나는지 확인

###  문자열 검색

* contains(CharSequence s): 문자열이 특정 문자열을 포함하고 있는지 확인
* indexOf
* lastIndexOf

###  문자열 조작 및 변환

* substring(int beginIndex) / substring(int beginIndex, int endIndex)
* concat(String str)
* replace(CharSequence target, CharSequence replacement)
* replaceAll(String regex, String replacement)
* replaceFirst(String regex, String replacement)
* toLowerCase() / toUpperCase()
* trim()
* strip()

###  문자열 분할 및 조합

* split(String regex)
* join(CharSequence delimiter, CharSequence... elements)

###  기타 유틸리티

* valueOf(Object obj): 다양한 타입을 문자열로 변환

* toCharArray(): 문자열을 문자 배열로 변환

* format(String format, Object... args): 형식 문자열과 인자를 사용하여 새로운 문자열을 생성

* matches(String regex): 문자열이 주어진 정규 표현식과 일치하는지 확인

* 불변인 String 클래스의 단점은 문자를 더하거나 변경할 때마다 계속해서 새로운 객체를 생성해야 한다는 점이다.

* 문자를 자주 더하거나 변경해야 하는 상황이라면 더 많은 String 객체를 만들고, GC해야 한다.

---

##  StringBuilder

* String 클래스 단점 해결법. 가변 String이 존재하면 된다.
* StringBuilder는 append()로 문자열을 이어붙여도 동일한 StringBuilder 객체 내부에서만 작업한다.
* String은 불변이라 이어붙일 때마다 새로운 String 객체가 만들어진다.
* 그래서 StringBuilder가 반복적인 문자열 조작에 더 효율적이다.
* toString 메소드를 사용해 StringBuilder의 결과를 기반으로 String을 생성할 수 있다.
* StringBuilder는 보통 문자열을 변경하는 동안만 사용하다가 문자열 변경이 끝나면 안전한(불변) String으로 변환하는 것이 좋다.

###  StringBuilder를 직접 사용하는 것이 더 좋은 경우

* 반복문에서 반복해서 문자를 연결할 때
* 조건문을 통해 동적으로 문자열을 조합할 때
* 복잡한 문자열의 특정 부분을 변경해야 할 때
* 매우 긴 대용량 문자열을 다룰 때

---

##  메서드 체이닝 (Method Chaining)

* 메서드 호출 결과로 리턴된 객체에서 또 메서드를 호출하는 방식이다.
* 주로 같은 객체(this)를 리턴해 메서드를 연속 호출할 수 있도록 만든다.
* 코드가 간결해지고 가독성이 좋아진다.

###  예시

```java
StringBuilder sb = new StringBuilder();
sb.append("Hello")
  .append(" ")
  .append("World!")
  .reverse();

System.out.println(sb.toString());
```

* append()는 StringBuilder 객체를 리턴하기 때문에 연속 호출 가능하다.

###  주요 특징

* 한 객체에서 여러 메서드를 연속 호출해 작업을 수행한다.
* 메서드가 return this 형태로 객체 자기 자신을 반환해야 가능하다.
* Setter 메서드나 빌더 패턴에서 자주 사용된다.

###  장점

* 코드가 간결하고 직관적이다.
* 여러 메서드를 연속 호출해 한 번에 여러 작업을 처리할 수 있다.

###  단점

* 디버깅이 어려울 수 있다.
* 너무 길어지면 가독성이 떨어질 수 있다.

###  사용 예시: 빌더 패턴

```java
Person person = new PersonBuilder()
                    .setName("Alice")
                    .setAge(25)
                    .build();
```

---

##  기본형의 한계

* 객체가 아님: 객체는 유용한 메서드를 제공할 수 있는데 기본형은 객체가 아니므로 메서드 제공 X
* null 값을 가질 수 없음: 기본형 데이터 타입은 null 값을 가질 수 없다. 때로는 데이터가 없음 이라는 상태를 나타내야 할 필요가 있는데, 기본형은 항상 값을 가지기 때문에 이런 표현을 할 수 없다.

---

##  래퍼 클래스

* 기본형을 객체로 감싸서 더 편리하게 사용하도록 도와줌.

| 기본형     | 래퍼 클래스    |
| ------- | --------- |
| byte    | Byte      |
| short   | Short     |
| int     | Integer   |
| long    | Long      |
| float   | Float     |
| double  | Double    |
| char    | Character |
| boolean | Boolean   |

###  자바가 제공하는 기본 래퍼 클래스 특징

* 불변
* equals로 비교해야 한다.

###  래퍼 클래스 생성 - 박싱(Boxing)

* new Integer(10)은 직접 사용 X, 작동은 하지만 향후 자바에서 제거될 예정.
* 대신에 Integer.valueOf(10)

###  intValue() - 언박싱(Unboxing)

* 래퍼 클래스에 들어있는 기본형 값을 다시 꺼내는 메서드.

###  비교는 equals() 사용

* 래퍼클래스는 객체이기 때문에 == 비교를 하면 인스턴스의 참조값을 비교한다.
* 래퍼 클래스는 내부의 값을 비교하도록 equals()를 재정의 해두었다. 따라서 값을 비교하려면 equals()를 사용.
* toString()도 재정의했다.
* 자바 오토 언박싱, 박싱 지원: 컴파일러가 개발자 대신 valueOf, xxxValue() 등의 코드 추가해주는 기능.

###  래퍼클래스 주요 메서드

* valueOf(): 래퍼 타입을 반환. 숫자, 문자열을 모두 지원한다.
* parseInt(): 문자열을 기본형으로 변환.
* compareTo(): 내 값과 인수로 넘어온 값을 비교. 내 값이 크면 1, 같으면 0, 내 값이 작으면 -1을 반환.

---

## Class 클래스 기능

* 타입 정보 얻기
* 리플렉션
* 동적 로딩과 생성
* 애노테이션 처리

###  class vs clazz

* class는 자바의 예약어이다. 따라서 패키지명, 변수명으로 사용할 수 없다.
* 이런 이유로 자바 개발자들은 class 대신 clazz라는 이름을 관행으로 사용.

###  class 클래스의 주요 기능

* getDeclaredFields(): 클래스의 모든 필드를 조회.
* getDeclaredMethods(): 클래스의 모든 메서드를 조회.
* getSuperclass(): 클래스의 부모 클래스를 조회.
* getInterfaces(): 클래스의 인터페이스들을 조회.

---

##  열거형 - Enum Type

* 상수들을 사용하여 코드 내에서 미리 정의된 값들의 집합
* 열거형도 클래스이다.
* 열거형은 toString()을 재정의 하기 때문에 참조값을 직접 확인할 수 없다.

###  열거형의 장점

* 타입 안정성 향상
* 간결성 및 일관성
* 확장성

###  Enum - 주요 메서드

* values(): 모든 ENUM 상수를 포함하는 배열을 반환한다
* valueOf(String name): 주어진 이름과 일치하는 ENUM 상수를 반환한다.
* name(): ENUM 상수의 이름을 문자열로 반환한다.
* ordinal(): ENUM 상수의 선언 순서(0부터 시작)를 반환한다.
* toString(): ENUM 상수의 이름을 문자열로 반환한다. name() 메서드와 유사하지만, toString()은 직접 오버라이드 할 수 있다.

###  주의

* ordinal()은 가급적 사용하지 않는 것이 좋다.

  * 이 값을 사용하다가 중간에 상수를 선언하는 위치가 변경되면 전체 상수의 위치가 모두 변경될 수 있기 때문이다.

###  열거형 정리

* 열거형은 java.lang.Enum을 자동으로 상속 받는다.
* 열거형은 이미 java.lang.Enum을 상속 받았기 때문에 추가로 다른 클래스를 상속을 받을 수 없다.
* 열거형은 인터페이스를 구현할 수 있다.
* 열거형에 추상 메서드를 선언하고, 구현할 수 있다.
* 열거형은 상수로 지정하는 것 외에 일반적인 방법으로 생성이 불가능하다. 따라서 생성자에 접근제어자를 선언할 수 없게 막혀있다. private이라고 생각하면 된다.
