# 📋 Java 8

<br>

## 📌 Stream API

- 기존 Java는 (Java 8 이전) 객체 지향 언어로서, 함수형 프로그래밍이 불가능했지만, JDK8 부터 Stream, 람다식, 함수형 인터페이스를 지원

  - Java로 함수형 프로그래밍이 가능해짐

- **Stream API** : 데이터를 추상화하고 처리하는데 자주 사용하는 함수들을 미리 정의

  - 추상화 : 데이터의 종류에 상관 없이 같은 방식으로 데이터를 처리할 수 있다는 것 => 재사용성 높임

```java
// Stream 사용 전
String[] nameArr = {"IronMan", "Captain", "Hulk", "Thor"}
List<String> nameList = Arrays.asList(nameArr);

// 원본의 데이터가 직접 정렬됨
Arrays.sort(nameArr);
Collections.sort(nameList);

for (String str: nameArr) {
  System.out.println(str);
}

for (String str : nameList) {
  System.out.println(str);
}


// Stream 사용 후
String[] nameArr = {"IronMan", "Captain", "Hulk", "Thor"}
List<String> nameList = Arrays.asList(nameArr);

// 원본의 데이터가 아닌 별도의 Stream을 생성함
Stream<String> nameStream = nameList.stream();
Stream<String> arrayStream = Arrays.stream(nameArr);

// 복사된 데이터를 정렬하여 출력함
nameStream.sorted().forEach(System.out::println);
arrayStream.sorted().forEach(System.out::println);
```

- 코드의 라인수 감소, 가독성 증가

<br><br>

### ✅ Stream API 의 특징

1. 원본 데이터 변경 X

```java
List<String> sortedList = nameStream.sorted().collect(Collections.toList());
```

<br>

2. 일회용

```java
userStream.sorted().forEach(System.out::print);

// 스트림이 이미 사용되어 닫혔으므로 에러 발생
int count = userStream.count(); 

// IllegalStateException 발생
java.lang.IllegalStateException: stream has already been operated upon or closed
    at java.util.stream.AbstractPipeline.evaluate(AbstractPipeline.java:229)
    at java.util.stream.ReferencePipeline.noneMatch(ReferencePipeline.java:459)
```


<br>

3. 내부 반복 방식으로 작업

```java
 // 반복문이 forEach라는 함수 내부에 숨겨져 있다.
nameStream.forEach(System.out::println);
```

- 간결

<br><br>

### ✅ Stream API 연산 종류

1. 생성 단계
2. 가공 단계
3. 결과 도출 단계

```java
List<String> list = Arrays.asList("a1", "a2", "b1", "c2", "c1");

list
    .stream()							// 생성하기
    .filter(s -> s.startsWith("c"))			// 가공하기
    .map(String::toUpperCase)			// 가공하기
    .sorted()							// 가공하기
    .count();							// 결과만들기
```

- 이렇게 Stream 연산이 연결된 것을 연산 파이프라인 이라고 한다.

- 중간 연산은 여러번 이어서 수행 가능하다.

- 매개변수로 함수형 인터페이스(Functional Interface)를 받도록 되어있다.

- 간혹 최종 연산 중 값을 반환하지 않는 경우도 있긴 하다. ex> forEach

- Stream 연산의 자세한 종류들과, 활용법, 주의 사항은 아래 두 링크가 잘 설명되어 있다.

https://mangkyu.tistory.com/114
https://mangkyu.tistory.com/115

<br><br>

## 📌 람다식과 함수형 인터페이스

<br>

### ✅ 람다식 (Lambda Expression)

- 메서드를 하나의 식으로 압축 표현한 것

  - 코드를 훨씬 간결하게 표현 가능
  - 불필요한 코드를 줄이고 가독성을 높인다.
  - 메서드를 매개변수로 전달 가능
  - 메서드의 이름이 필요 없기에, 익명 함수(Anonymous Function)의 느낌

- Stream 연산들은 **매개변수**로 함수형 인터페이스(Function Interface)를 받는다.

- 람다식은 **반환값**으로 함수형 인터페이스를 받는다.

```java
// 기존 방식
public String hello() {
	return "Hello World!";
}

// 람다식 : 순수 함수를 선언 할 수 있다!
() -> "Hello World!";
```

<br><br>

### ✅ 람다식의 특징

- 람다식 내부의 지역변수는 final이 없어도 상수로 간주

- 람다식으로 선언된 변수명은 다른 변수명과 중복 X

<br><br>

### ✅ 람다식의 장점

- 코드의 간결화

- 개발자의 의도가 명확히 드러남

  - 가독성 증가

- 함수를 만드는 과정 생략

  - 생산성 증가

- 병렬 프로그래밍에 용이

<br><br>

### ✅ 람다식의 단점

- 람다를 사용하며 만든 무명 함수(이름이 없는)는 재사용이 불가능하다

- 디버깅이 어렵다

- 비슷해보이는 함수가 다량 생성될 수 있다

- 재귀에 부적합하다

<br><br>

### ✅ 함수형 인터페이스 (Functional Interface)

- Java의 람다식이 함수형 인터페이스를 return한다.

- **@FunctionalInterface** 어노테이션을 활용하여 단 하나의 추상 메소드만 갖도록 제한한다.

```java
// 기존 코드
public class Lambda {
    public static void main(String[] args) {
        // 기존의 익명함수
        System.out.println(new LambdaFunction() {
            public int min(int a, int b) {
                return a < b ? a : b;
            }
        }.min(3, 5));
    }
}
```

- 함수형 인터페이스를 적용하게 되면, 함수를 변수처럼 선언할 수 있어 간결해진다.

```java
@FunctionalInterface
interface LambdaFunction {
    int min(int a, int b);
}

public class Lambda {
    public static void main(String[] args) {
        // 람다식을 이용한 익명함수
        LambdaFunction lambdaFunction = (int a, int b) -> a < b ? a : b;
        System.out.println(lambdaFunction.min(3, 5));
    }

}
```

- 람다식으로 생성된 함수는 함수형 인터페이스 로만 선언이 가능하다.

- @FunctionalInterface에서 여러 함수를 선언하면 컴파일 에러가 발생한다.

  - 1개의 함수만 갖도록 제한!

<br><br>

### ✅ Java에서 공식 제공하는 함수형 인터페이스

- Java가 보기에 자주 사용할 것 같은 4가지 함수형 인터페이스를 미리 정의해놓음

1. `Supplier<T>`

2. `Consumer<T>`

3. `Function<T, R>`

4. `Predicate<T>`

<br><br>

### ✅ `Supplier<T>`

- 매개변수 없이 반환값만 가지는 함수형 인터페이스

- T get()을 추상 메소드로 가진다.

```java
// 정의
@FunctionalInterface
public interface Supplier<T> {
	T get();
}

// 예시
Supplier<String> supplier = () -> "Hello World!";
System.out.println(supplier.get());
```

<br><br>

### ✅ `Consumer<T>`

- 객체 T를 매개변수로 받아 사용

- 반환값 : 함수형 인터페이스

- **void accept(T t)**를 추상메서드로 가짐

- **andThen** 함수 : 하나의 함수가 끝난 후, Consumer를 연쇄적으로 이용

```java
// 정의
@FunctionalInterface
public interface Consumer<T> {

    void accept(T t);

    default Consumer<T> andThen(Consumer<? super T> after) {
        Objects.requireNonNull(after);
        return (T t) -> { accept(t); after.accept(t); };
    }
}

// 예시
Consumer<String> consumer = (str) -> System.out.println(str.split(" ")[0]);
consumer.andThen(System.out::println).accept("Hello World");

// 출력
Hello
Hello World
```

<br><br>

### ✅ `Function<T, R>`

- 객체 T를 매개변수로 받아서 처리한 후, R로 반환

- R apply(T t)를 추상메소드로 가짐

- **andThen** 함수 제공

- **compose** 함수 제공

  - 첫 함수 실행 이전에 먼저 함수를 실행하여 연쇄적으로 연결해줌

- **identity** 함수 제공

  - 자기 자신을 반환하는 static 함수

```java
// 정의
@FunctionalInterface
public interface Function<T, R> {

    R apply(T t);

    default <V> Function<V, R> compose(Function<? super V, ? extends T> before) {
        Objects.requireNonNull(before);
        return (V v) -> apply(before.apply(v));
    }

    default <V> Function<T, V> andThen(Function<? super R, ? extends V> after) {
        Objects.requireNonNull(after);
        return (T t) -> after.apply(apply(t));
    }

    static <T> Function<T, T> identity() {
        return t -> t;
    }
}

// 예시, 메소드 참조로 간소화 가능(String::length;)
Function<String, Integer> function = str -> str.length();
function.apply("Hello World");
```

<br><br>

### ✅ `Predicate<T>`

- 객체 T를 매개 변수로 받아 처리한 후 Boolean을 반환

- Boolean test(T t)을 추상 메소드라고 가짐

```java
// 정의
@FunctionalInterface
public interface Predicate<T> {

    boolean test(T t);

    default Predicate<T> and(Predicate<? super T> other) {
        Objects.requireNonNull(other);
        return (t) -> test(t) && other.test(t);
    }

    default Predicate<T> negate() {
        return (t) -> !test(t);
    }

    default Predicate<T> or(Predicate<? super T> other) {
        Objects.requireNonNull(other);
        return (t) -> test(t) || other.test(t);
    }

    static <T> Predicate<T> isEqual(Object targetRef) {
        return (null == targetRef)
                ? Objects::isNull
                : object -> targetRef.equals(object);
    }
    
}

// 예시
Predicate<String> predicate = (str) -> str.equals("Hello World");
predicate.test("Hello World");
```

<br><br>

## 📌 메소드 참조 (Method Reference)

<br>

- 함수형 인터페이스를 람다식이 아닌 일반 메소드를 참조시켜 선언하는 방법

  - 조건 1 : 함수형 인터페이스 매개변수 타입 = 메소드 매개변수 타입
  - 조건 2 : 함수형 인터페이스 매개변수 개수 = 메소드 매개변수 개수
  - 조건 3 : 함수형 인터페이스 반환형 = 메소드 반환형

- 참조 가능한 메소드 : 일반 메소드, static 메소드, 생성자

- 참조 방법 : 클래스 이름::메소드 이름

<br>

### ✅ 일반 메소드 참조

```java
// 예시 : length()

// 기존 람다식
Function<String, Integer> function = (str) -> str.length();
function.apply("Hello World");

// 메소드 참조로 변경
Function<String, Integer> function = String::length;
function.apply("Hello World");
```

- 3가지 조건

  - 매개변수 X (타입 조건 넘김)
  - 매개변수 개수 : 0
  - 반환형 : int

<br>

```java
// 일반 메소드를 참조하여 Consumer를 선언한다.
Consumer<String> consumer = System.out::println;
consumer.accept("Hello World!!");

// 메소드 참조를 통해 Consumer를 매개변수로 받는 forEach를 쉽게 사용할 수 있다.
List<String> list = Arrays.asList("red", "orange", "yellow", "green", "blue");
list.forEach(System.out::println);

//interface Iterable<T>
default void forEach(Consumer<? super T> action) {
    Objects.requireNonNull(action);
    for (T t : this) {
        action.accept(t);
    }
}
```

- System.out.println() : 반환형 void, 파라미터 String

<br><br>

### ✅ Static 메소드 참조

```java
Predicate<Boolean> predicate = Objects::isNull;

// isNull 함수
public static boolean isNull(Object obj) {
    return obj == null;
}
```

- Objects의 isNull 반환값 : Boolean, 매개변수 값 : 1개, 매개변수 타입 : Object
  -> Predicate로 메소드 참조 가능

<br><br>

### ✅ 생성자 참조

```java
Supplier<String> supplier = String::new;
```

- 생성자 : new로 생성 => 클래스이름::new

- Supplier : 매개변수 없이 반환값만 갖는 인터페이스 => 위 케이스에 어울림

<br><br>

## 📌 인터페이스의 default 메서드와 static 메서드

### ✅ 인터페이스에 default 메소드가 필요한 이유

- default 메소드는 다른 인터페이스의 일반적인 메소드들 처럼 암시적으로 public (명시 필요 X)

  - but> 인터페이스의 일반 메소드들과 다르게, 메소드 앞에 `default`라는 키워드가 선언된다.

```java
public interface MyInterface {
    
    // 일반적인 메소드들 ...
    
    // default 메소드
    default void defaultMethod() {
        // 구현
    }
}
```

- 일반적인 인터페이스 메소드들은, 모든 구현 클래스에서 강제적으로 구현 해야 한다.

  - 구현 클래스가 늘어날 수록, 위는 곤혹스럽다.

- 인터페이스의 default 메서드는 자동적으로 구현 클래스에서도 사용할 수 있어, 구현 클래스를 수정할 필요가 없어지고, 이를 깔끔하게 `하위 호환`이 가능하다고 말한다.

- default 메소드의 가장 일반적인 사용 목적

  - 구현 클래스를 파괴하지 않으면서 점진적으로 추가적인 기능을 제공하는 것
  - 기존의 추상 메소드에 기능을 덧붙이는 것

<br><br>

### ✅ default 메소드 주의사항

- 자바는 인터페이스의 다중 상속을 허용한다.

  - 같은 default 메소드를 정의한 여러개의 인터페이스를 한 클래스가 다중 상속하면 충돌이 발생하여, 컴파일되지 않는다

    - `Diamond Problem` 이라고 부른다.

- 이러한 문제를 해결하기 위해, 메소드에 명시적으로 구현해야 한다.

```java
public interface Phone {
    
    String call();
    
    String message();
    
    default String turnAlarmOn() {
        return "Turning the phone alarm on.";
    }
    
    default String turnAlarmOff() {
        return "Turning the phone alarm off.";
    }
}
```

```java
public interface Alarm {

    default String turnAlarmOn() {
        return "Turning the alarm on.";
    }
    
    default String turnAlarmOff() {
        return "Turning the alarm off.";
    }
}
```

```java
public iphone Car implements Phone, Alarm {

	// Phone interface의 default 메소드 사용
	@Override
    public String turnAlarmOn() {
        return Phone.super.turnAlarmOn();
    }

	// Alarm interface의 default 메소드 사용
    @Override
    public String turnAlarmOff() {
        return Alarm.super.turnAlarmOff();
    }
}
```

### ✅ Static 인터페이스 메소드

- static 메소드는 특정 객체에 속하지 않기 때문에, 인터페이스를 구현하는 클래스 API의 한 부분이 아니다.

  - 메소드며 앞에 인터페이스 이름을 넣어 호출해야 한다.

```
public interface Vehicle {
    
    static int getHorsePower(int rpm, int torque) {
        return (rpm * torque) / 5252;
    }
}
```

```java
Vehicle.getHorsePower(2500, 480));
```

- 객체 생성 없이 한 공간에서 연관된 메소드들의 결합성을 높힌다.

- 추상 클래스와 흡사하지만, 추상 클래스는 생성자, 상태, 동작으로 이루어져 있다.

<br><br>

## 📌 `Optional<T>`

<br>

### ✅  Optional?

- 존재할 수도 있지만, 아닐수도 있는 객체 / null일수도 아닐수도 있는 객체를 감싸는 일종의 래퍼 클래스

- 기존에는 조건문 예외 처리 과정을 통해 직접 null을 체크하여 번거로웠지만, optional을 사용하면 더욱 간편해진다.

<br><br>

### ✅ Optional의 효과

- 명시적으로 해당 변수가 null의 가능성을 내포한다는 점을 시사

- NPE(NullPointerException)의 유발 X

- null 체크를 더욱 간편하게

<br><br>

### ✅ Optiona의 기본적인 사용방법

- Optional 선언

  - 제네릭을 통해 변수 선언 시 작성 타입 파라미터에 따라 래핑할 수 있는 객체의 타입 결정
  - 관례적으로 변수명에 maybe 또는 opt를 붙이기도 함.
```java
Optional<Order> optOrder;
```

<br>

- 객체 생성

  - **Optional.empty()**
    - null을 담는 Optional 객체 생성
    - 비어 있는 객체는 Optional 내부에 미리 생성해놓은 싱글턴 인스턴스
    ```java
    Optional<User> optUser = Optional.empty();
    ```
  - **Optional.of(value)**

    - null이 아닌 객체를 담고 있는 Optional 객체 생성
    - null이 넘어오면 NPE 발생
      ```java
      Optinal<User> optUser = Optional.of(user);
      ```
  - **Optional.ofNullable(value)**

    - null 여부를 모를 때 Optional 객체 생성
      ```java
      Optional<User> optUser = Optional.ofNullable(null);
      ```

<br>

- Optional 객체 존재 여부 확인

  - **isPresent()**

    - boolean 반환
    - 객체가 존재하면 true, 비었으면 false
      ```java
      Optional<String> optStr = Optional.ofNullable("test");
      
      if(optStr.isPresent())
          System.out.println(optStr.get());
      ```
  - **isEmpty()**

    - boolean 반환
    - 객체가 비었으면 true, 존재하면 false
       ```java
       Optional<String> optStr = Optional.ofNullable("test");
       
       if(optStr.isEmtpy())
           System.out.println("optStr은 null입니다.");
       ```

<br>

Optional이 담고 있는 객체 접근

- **get()**

  - 비어 있는 객체 : NoSuchElementException
     ```java
     Optional<String> optionalWithValue = Optional.of("Hello, World!");

     System.out.println(optionalWithValue.get());
     ```

- **orElse(T other)** : 옵셔널이 비어잇으면 파라미터로 입력한 인자 리턴

  ```java
  Optional<String> optionalWithValue = Optional.of("Hello, World!");
  String value = optionalWithValue.orElse("Default Value");
  System.out.println("Value: " + value);
  ```

- **orElseGet(Supplier<? extends T> other)** : 비어있는 Optional 객체는 넘어온 함수형 인자를 통해 생성된 객체 반환

```java
Optional<String> optionalWithValue = Optional.of("Hello, World!");
String value = optionalWithValue.orElseGet(() -> generateDefaultValue());
System.out.println("Value: " + value);
```

- **orElseThrow(Supplier<? extends X> exceptionSupplier)** : 비어있는 Optional 객체에 대해, 넘어온 함수형 인자를 통해 생성된 예외 던짐

```java
Optional<String> optionalWithValue = Optional.of("Hello, World!");
String value = optionalWithValue.orElseThrow(() -> new IllegalStateException("Value is not present"));
System.out.println("Value: " + value);
```


<br><br>


## 📌 참조

- https://mangkyu.tistory.com/112
- https://mslim8803.tistory.com/36
- https://mangkyu.tistory.com/113
- https://soft-dino.tistory.com/25
- https://developsd.tistory.com/127
