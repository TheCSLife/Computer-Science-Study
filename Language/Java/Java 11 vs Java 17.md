# 📋 Java 11 vs 17

<br>

## 📌 Java 11


<br><br>

### ✅ 인터페이스에 private 메서드 추가 가능

- 이전에는 인터페이스에 선언된 모든 메서드가 암묵적으로 public

    - 해당 메서드를 구현하는 구현 클래스에서도 반드시 public으로 선언했어야 했다.

<br>

- 장점

1. 코드 재사용 및 모듈화 : 인터페이스 내부에서 공통 로직을 private 메서드로 구현하면 이를 여러 메서드에서 재사용할 수 있다.

<br>

2. 코드 가독성 : 규모가 큰 인터페이스의 경우 다양한 public 메서드가 선언되어 있을 수 있는데, 이 때 private 메서드를 활용하여 인터페이스 내부 코드를 작고 읽기 쉽게 유지 가능하다.

<br>

3. 인터페이스 확장 : 인터페이스에 새로운 메서드를 추가할 때 기존 클래스들이 해당 메서드를 반드시 구현해야 하는데, 이때 private 메서드를 사용하면 이를 효율적으로 수행할 수 있다

<br>

```java
public interface MyInterface {
    // public 추상 메서드
    void publicMethod();

    // Java 11부터 추가된 private 메서드
    private void privateMethod() {
        // private 메서드의 구현
        System.out.println("This is a private method.");
    }

    // public 메서드에서 private 메서드 호출
    default void callPrivateMethod() {
        privateMethod();
    }
}

```

<br><br>

### ✅ OpenJDK와 OracleJDK의 통합

- Java11부터 OracleJDK가 유료화 되었다.

- 그에 따라 무료인 OpenJDK의 중요성이 올라갔다.

- 따라서 Oracle은 OracleJDK와 OpenJDK를 통합하기로 했다.

    - 두 JDK의 코드 베이스를 비슷하게 유지한다.
    - Oracle JDK의 무료버전이 곧 OpenJDK와 거의 동일하다

- Java11부터 LTS(Long-Term Support)와 비LTS 구분

    - LTS : 장기 지원을 받으며 긴 지속시간 동안 업데이트와 보안 패치 제공
    - 비LTS : 짧은 업데이트 주기와 제한된 지원


<br><br>

### ✅ G1(Garbage-First) GC(가비지 컬렉터)가 기본 GC로 설정됨

- G1 GC의 특징

    - 분산된 가비지 컬렉터 : 전체 힙을 일정 크기 영역으로 나누고 각 영역에서 가장 많은 가비지를 가진 영역을 우선 수집

        - 일정 시간 안에 안정적인 가비지 컬렉션 수행 가능

    - 힙 크기 제한 : 미리 최대 힙 크기를 설정하여 메모리 사용량을 미리 제한

    - 영역별 가비지 컬렉션 제어 : 영역별로 제어가 가능하기에 응답 시간의 향상을 이끌어낸다.

<br>

- Java 11 이전 까지는 CMS(Collector-Mark-Sweep) GC가 기본 GC였다.

    - Java 11에서는 성능 및 예측 가능성이 더 우수한 G1 GC를 기본 GC로 설정

<br>

- G1 GC의 장점

    - 응답 시간을 향상시키고 일시 중단 시간을 감소시킨다.
    - 힙 크기를 효과적으로 관리하고, 메모리 사용량을 최적화하는데 도움을 준다.
    - CMS GC에 비해 예측이 쉬워 서비스 목표를 달성하는데 도움을 줄 수 있다.

<br>

- G1 GC 주의사항

    - 적절한 힙 크기 및 다른 JVM 옵션을 설정해야 한다.

        - application의 특성에 따라 최적화된 설정이 달라진다.

    - 원하는 성능에 따라 튜닝과 모니터링이 필요할 수 있다.


<br><br>

### ✅ 람다 표현식과 var 키워드의 조합

- 람다 표현식(Lamdah Expressions)

    - Java 8에서 이미 도입된 개념
    - 익명 함수를 정의하는 방법 중 하나
    - 함수를 변수에 할당하거나 다른 함수에 전달하는 파라미터로서 사용이 가능하다
    - 코드를 간결하게 만든다
    - 함수형 프로그래밍 스타일을 지원한다.

```java
// Java 8 이전의 익명 내부 클래스를 사용한 예제
Runnable runnable = new Runnable() {

    @Override
    public void run() {
        System.out.println("Hello, World!");
    }
};

// Java 8에서의 람다 표현식
Runnable runnable = () -> {
    System.out.println("Hello, World!");
};

```

<br><br>

- 지역 변수 타입 추론 (Local Variable Type Inference)

    - Java 10에서 이미 도입된 개념
    - 지역 변수 타입 추론을 위해 `var` 키워드가 도입되었다.
    - 변수의 타입을 명시적으로 선언하지 않고도 컴파일러가 변수의 타입을 유추할 수 있다.

```java
// Java 10 이후의 var 키워드 사용
var name = "John"; // String으로 유추
var age = 30;      // int로 유추
```

<br><br>

- 람다와 var의 조합

    - Java 11에 새로 도입된 기능
    - 람다 표현식 내부에서 var 키워드를 활용하여 지역 변수 선언 가능
    - 코드를 더욱 간결하게 만든다
    - 람다 냅웨서 지역 변수의 타입을 명시할 필요가 없다.

```java
// Java 11에서의 람다와 var의 조합
(var x, var y) -> {
    var result = x + y; // result 변수의 타입은 컴파일러가 유추
    
    System.out.println(result);
};
```

<br><br>

- 장점

    - 람다 표현식 내에서 지역 변수의 타입을 더 간결하게 표현 가능
    - 코드 가독성 향상, 변수 이름과 초기화 값 강조 효과
    - 컴파일러가 변수의 타입을 추론 -> 유지 보수성 향상 , 실수 줄임

<br><br>

### ✅ 컬렉션, 스트림 등 메소드 추가

1. List.of() / Set.of()

- Java 9에서 도입된 불변 컬렉션을 생성하기 위한 메서드, List.of() / Set.of()가 Java 11에서는 더욱 많은 요소를 받을 수 있는 오버로딩 버전이 추가 되었다.

```java
// Java 9의 불변 리스트 생성
List<String> list = List.of("A", "B", "C");

// Java 11에서 더 많은 요소를 포함하는 불변 리스트 생성
List<String> list = List.of("A", "B", "C", "D", "E");
```

<br><br>

2. Map.ofEntries()

- Key-Value 형태를 이용하여 불변 Map 생성

- 이전에는 Key, Value를 직접 나열해야 했지만 Map.ofEntries()를 활용하여 편리한 불변 맵 생성 가능

```java
// Java 11에서 불변 맵 생성
Map<String, Integer> map = Map.ofEntries(
    entry("A", 1),
    entry("B", 2),
    entry("C", 3)
);
```

<br><br>

3. Collectors.toUnmodifiableList() / Collectors.toUnmodifiableSet()

- 스트림에서 불변 리스트 및 불변 집합 생성 가능

```java
// 불변 리스트 생성
List<String> list = Stream.of("A", "B", "C")
    .collect(Collectors.toUnmodifiableList());

// 불변 집합 생성
Set<Integer> set = Stream.of(1, 2, 3)
    .collect(Collectors.toUnmodifiableSet());
```

<br><br>

4. String.lines()

- 문자열 줄단위 분할

```java
String text = "Hello\nWorld\nJava\n11";

// 문자열을 줄 단위로 분할
List<String> lines = text.lines()
    .collect(Collectors.toList());

// 결과: ["Hello", "World", "Java", "11"]

```

<br><br>

5. Optional.isEmpty()

- Optional 객체가 비어있는지 확인

```java
String text = "Hello\nWorld\nJava\n11";

// 문자열을 줄 단위로 분할
List<String> lines = text.lines()
    .collect(Collectors.toList());

// 결과: ["Hello", "World", "Java", "11"]

```

<br><br>

- 전반적으로 코드를 간결하게 작성하고 불변성을 유지하는데 도움이 되는 메서드들

<br><br>

### ✅ 지역 변수의 final 효과 확장

- 기존 : final을 사용하여 선언한 변수는 재할당 금지 -> 불변성 보장

    - 그러나 var 변수는 타입 추론 시 초기화 이후에 다시 할당될 수 있었다.

- Java 11 : var 변수 또한 초기화 이후 재할당 금지 -> 불변성 보장

<br><br>

1. var로 선언된 변수 한 번만 할당

- 변수를 선언하고 초기화한 후 다시 다른 값을 할당하려고 하면 컴파일 오류가 발생

```java
var x = 10; // 초기화
x = 20;     // 컴파일 오류! 재할당 불가능
```

<br>

2. 불변성 강화

- var 변수가 한 번 초기화되면 해당 변수를 다른 값으로 변경할 수 없으므로 코드의 안정성을 향상

<br>

3. 가독성 향상

- var 변수를 한 번만 할당해야 하므로 코드의 의도를 더 명확하게 표현

<br><br>

## 📌 Java 17

<br>

### ✅ recode

- `record` 클래스 키워드 : 클래스를 간결하게 정의하고 데이터 객체를 생성하는데 사용

    - Java의 데이터 클래스로 볼 수 있다.

<br>

- 장점

1. 불변성(Immutability) : record 클래스 필드는 기본적으로 final으로 선언되어 불변성을 보장

    - 객체의 상태 변경 불가능

2. 필드 정의(Field Definitions) : 필드를 간결하게 정의한다.

    - 필드 접근 제어자가 생략되면 자동으로 `private final`로 간주

3. Getter 메서드(Accessor Methods) : 자동 생성된 `getter` 메서드 제공

4. `equals()`, `hashCode()`, `toString()` 메서드 자동 생성

5. 생성자(Constructor) 자동 생성

6. 명시적 메서드 추가 가능 : 필요하다면 `record` 클래스에 추가 메서드 정의 가능

    - 인스턴스 메서드로 정의

```java
record Person(String name, int age) {
    // 다른 메서드를 추가할 수 있음
}

// Usage
Person person = new Person("Alice", 30);

System.out.println(person.name()); // "Alice"
System.out.println(person.age());  // 30
```

<br>

- 불필요한 보일러플레이트 코드(약간 공통적으로 사용되는 코드)를 줄이고 가독성을 높이며, 더 간단하고 안전한 데이터 클래스를 제공한다.

<br><br>

### ✅ 난수 생성 API 추가

- 난수 생성 API `java.util.random` 패키지에 추가

    - 기존에 사용되던 `java.util.Random` 클래스보다 더 강력하고 예측 가능성 낮은 난수를 생성하기 위한 새로운 방법을 제공

<br><br>

1. 새로운 난수 생성기 : `RandomGenerator` 인터페이스를 도입 -> `SplittableRandom`, `Xoshiro256PlusPlus`, `L64Xoshiro256PlusPlus`, `L64Xoshiro512PlusPlus` 등 여러 구현체 포함

2. `SplittableRandom` 클래스

    - 난수 생성기 : 잘 정의된 시드 값에서 파생된 난수 시퀀스 생성 가능

    ```java
    SplittableRandom random = new SplittableRandom();
    
	int randomNumber = random.nextInt(1, 100); // 1부터 99까지의 난수 생성
    ```

3. 추가 기능

    - `split()` 메서드를 활용하여 어러 독립적인 난수 생성기 생성 가능
    - `nextBytes()` 메서드를 사용하여 바이트 배열에 난수를 채울 수 있다.

4. 무결성과 예측 불가능성

    - 보안 및 예측 불가능성을 충족하도록 설계됨
    - 안전한 난수를 생성하는데 적합
    - `java.security.SecureRandom`과 비슷한 용도

<br><br>

- 이전 방식(`java.util.Random`)보다 `java.util.random` 패키지는 더 강력하고 안전한 난수 생성을 제공한다.

<br><br>

### ✅ 봉인 클래스(Sealed Class)

- 클래스와 인터페이스를 제한된 하위 클래스 집합으로 제어하고 캡슐화를 강화하는 기능 제공

- 특정 클래스를 확장하거나 인터페이스를 구현하는 클래스를 제한하고 런타임 시에 클래스 계층 구조를 더 안정적으로 만들 수 있다.

<br>

1. `sealed` : 봉인 클래스 정의 시 클래스 선언 앞에 붙임

    - 이 클래스를 상속하는 하위 클래스를 명시적으로 지정

2. `permits` 키워드 : 허용되는 하위 클래스 명시

```java
sealed class Shape permits Circle, Rectangle, Triangle {
    // 클래스 멤버 정의
}
```

3. 제한된 상속: sealed 클래스의 하위 클래스는 명시적으로 허용된 클래스

    - 위 예시에서 다른 클래스에서 Shape 클래스를 상속하려고 하면 컴파일 오류가 발생

4. 열거 형식과의 결합 : 특정 상수 집합만 허용되는 경우 유용하게 사용

```java
sealed interface TrafficSignal permits RedSignal, GreenSignal, YellowSignal {
    void display();
}

enum RedSignal implements TrafficSignal {
    RED {
        @Override
        public void display() {
            System.out.println("Red Signal");
        }
    }
}

enum GreenSignal implements TrafficSignal {
    GREEN {
        @Override
        public void display() {
            System.out.println("Green Signal");
        }
    }
}

enum YellowSignal implements TrafficSignal {
    YELLOW {
        @Override
        public void display() {
            System.out.println("Yellow Signal");
        }
    }
}
```

5. 유연한 설계 : 클래스 계층 구조를 더욱 유연하게 설계 가능

    - 클래스 간 결합도를 낮추고 코드 유지보수를 용이하게 만든다.

6. API 설계에 활용

    - API 제공 시 어떤 클래스를 확장하거나 인터페이스를 구현할 수 있는지 명확하게 정의하여 API의 안정성과 확정성 보장


<br><br>

- Java의 타입 시스템을 보다 강력하게 활용하여 코드를 안정적으로 만들고 예상치 못한 하위 클래스의 무분별한 생성을 막는다.

    - 코드의 신뢰성을 향상시키고 유지 보수를 더욱 쉽게 만든다.

<br><br>

### ✅ 텍스트 블록 기능

- 텍스트 블록(Text Block) : 여러 줄로 이루어진 문자열 리터럴을 더욱 쉽게 작성 가능

    - 코드의 가독성 향상 / 긴 문자열을 포함하는 문자열을 더욱 명확하게 표현할 수 있는 방법 제공

- 텍스트 블록 : `"` 세개로 시작하고 끝, 그 사이에 여러 줄의 텍스트 입력 가능

```java
String textBlock = """
    This is a
    text block
    in Java 17.
    """;
```

```java
String name = "Alice";
String textBlock = """
    Hello, ${name}!
    Welcome to Java 17.
    """;
```

<br><br>

- SQL 쿼리, HTML 또는 JSON 템플릿, 메시지 리소스 파일, 소스 코드 생성 등 다중 줄 텍스트를 다루어야 할 때 유용하게 사용

- 코드의 가독성을 높이고 유지보수를 더욱 쉽게 만듦

<br><br>

### ✅ `NumberFormat` 클래스, `DateTimeFormatter` 기능 향상

1. `NumberFormat` 클래스 기능 향상

    - 속도 개선
    - 새로운 `compact` 스타일 : `NumberFormat.Style.COMPACT` : 대규모 숫자를 간략하게 표현하는데 유용 ex> "1K", "1M"

    ```java
    NumberFormat compactFormat = NumberFormat.getCompactNumberInstance(Locale.US, NumberFormat.Style.SHORT);
	String formatted = compactFormat.format(1000);

	System.out.println(formatted); // 출력: "1K"
    ```

2. `DateTimeFormatter` 클래스 기능 향상

    - Locale 지원 개선 : 추가적인 로케일 관련 형식 지원 -> 지역 별 날짜 및 시간 형식 더욱 정확하게 사용 가능
    - 커스텀 형식 지정 : 사용자 정의 패턴을 통해 날짜 및 시간 형식을 세밀하게 지정할 수 있는 기능 제공

    ```java
    DateTimeFormatter customFormatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss", Locale.US);
	String formattedDateTime = LocalDateTime.now().format(customFormatter);
	
    System.out.println(formattedDateTime);
    ```

3. 새로운 메서드와 유틸리티

    - `DateTimeFormatter.parseBest()` 메서드를 사용하여 여러 형식의 입력을 파싱할 수 있다.

    ```java
    DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd");
	TemporalAccessor temporal = DateTimeFormatter.parseBest("2023-09-17", LocalDate::from, YearMonth::from);
    ```

<br><br>

- 숫자와 날짜/시간 형식화 작업을 더욱 간편하게 만들어 국제화 및 지역화에 더욱 적합한 도구 제공

    - 코드 가독성과 효율성을 향상시킬 수 있다.

<br><br>

### ✅ Stream.toList()

- `Stream.toList()` : Stream 요소를 List로 손쉽게 변환

```java
import java.util.*;
import java.util.stream.*;

public class Main {
    public static void main(String[] args) {
        Stream<String> stringStream = Stream.of("A", "B", "C");
        List<String> stringList = stringStream.toList();
        System.out.println(stringList); // 출력: [A, B, C]
    }
}
```

<br><br>

### ✅ NPE 발생 변수에 대한 설명

- `NullPointerException`이 발생한 위치와 관련 정보를 더욱 자세히 제공한다.

    - 코드 디버깅 문제 및 해결이 더욱 쉬워진다.

1. `NullPointerException.getMessage()` : 변수 이름과 null 값을 포함한 더욱 자세한 정보를 반환

```java
Exception in thread "main" java.lang.NullPointerException: Cannot invoke "String.length()" because "str" is null
```

2. `NullPointerException.printStackTrace()` : 어떤 변수에서 null이 발생했는지 포함

<br><br>

### ✅ ZGC 도입

- ZGC(Z Garbage Collector) : 실시간 및 대규모 메모리 관리를 목표로 하는 GC 알고리즘 중 하나.

<br>

- 기존 G1 GC (Java 11)과 비교한 주요 특징

1. 실시간(Low-Latency) GC : 메모리 관리 수행 동안 일시 중지 시간을 최소화하려고 노력

2. 대규모 메모리 지원 : 매우 큰 힙 크기에서도 효율적으로 작동 -> 대규모 데이터 처리 및 메모리 집약적 애플리케이션에 적합

3. 안정적 성능 : 예측 가능하고 더욱 안정적인 성능 제공

4. 구성 가능한 일시 중지 시간 : 개발자가 직접 일시 중지 시간 목표 설정 가능 -> GC의 Trade-Off 조정

5. 멀티 스레드 환경 지원 : 동시성 및 병렬 처리를 최대한 활용하여 GC 수행

6. 안전성 및 신뢰성 : 다양한 안전 메커니즘 내재

7. 100% Java 기반 : JVM 밖에서 별도의 Native 라이브러리를 필요로 하지 않음

<br><br>

- ZGC를 사용하려면 Java 11 이상의 버전 필요, Java 17 버전 이상 권장

<br><br>

## 📌 Java 11 vs Java 17

- 로컬 변수 유형 추론의 개선:
  자바 11에서는 'var' 키워드를 사용하여 로컬 변수의 유형을 추론할 수 있게 되었다.
  자바 17에서는 로컬 변수 유형 추론이 더 개선되었으며, 람다식과 익명 클래스에서도 'var'를 사용할 수 있게 되었다.

- 새로운 기능과 개선된 API:
  자바 17에서는 다양한 새로운 기능과 API 개선이 이루어졌다.
  예를 들어, 'Sealed Classes'가 도입되어 클래스의 상속을 제한하고, 'Pattern Matching for switch'가 확장되어 패턴 매칭 기능이 향상되었다.

- Garbage Collector 개선:
  자바 17에서는 'Z Garbage Collector'의 개선과 함께 새로운 'Shenandoah Garbage Collector'가 추가되었다.
  이러한 변경으로 GC 성능과 응답 시간이 개선되었다.

- 암호화화 관련 업데이트:
  자바 17에서는 암호화와 보안 관련 업데이트가 이루어졌다.
  암호화 알고리즘과 보안 기능의 업데이트로 애플리케이션의 보안성이 향상되었다.

- 언어 및 컴파일러 개선:
  자바 17에서는 언어 및 컴파일러 개선이 이루어져 더 나은 코드 작성이 가능해졌다.
  예를 들어, 'sealed', 'record', 'permits' 등의 키워드를 사용하여 코드를 더 명확하고 안전하게 작성할 수 있다.

- Deprecation과 Removal:
  자바 17에서는 일부 구식된 기능들이 표시되어 Deprecated 상태로 변경되거나, 더 이상 사용되지 않는 기능들이 제거되었다.

- 성능 개선:
  자바 17은 전반적으로 성능 개선이 이루어져 더 빠르고 효율적인 실행이 가능해졌다.

- 다양한 다른 업데이트:
  자바 17은 모듈 시스템, 컨테이너 지원, 런타임 성능 분석 등 여러 가지 다양한 개선 사항들을 포함하고 있다.

<br><br>

## 📌 Java 17이 좋아보이지만 11을 사용하는 이유

- 레거시 코드와의 호환성:
  기존에 자바 11을 사용하던 프로젝트나 레거시 코드와의 호환성을 유지해야 하는 경우 자바 17로 업그레이드 하는 것에 어려움을 초래

- 프로젝트 특성과 요구사항:
  특정 라이브러리나 프레임워크가 자바 11을 기반으로 개발되었거나, 특정 기능을 지원하는 경우에는 자바 11을 사용하는 것이 유리할 수 있다.

- 개발자 스킬과 경험:
  프로젝트 팀의 개발자들이 자바 1에 더 익숙하고 경험이 있을 경우 자바 11을 선택하는 것이 더 효율적일 수 있다.

- 이전 버전과의 호환성 유지:
  자바 11은 이전 버전과의 호환성 유지를 하는 데 도움이 될 수 있다.
  업그레이드에는 더 많은 작업이 필요할 수 있다.

<br><br>

## 📌 어떤 자바 버전을 사용해야 할까?

- 기업의 기존 프로젝트에는 Java 8을 사용하는 경우가 많다.

- 최신 IDE, 프레임워크 및 빌드 도구를 활용한 프로젝트를 시작하는 경우, 망설임 없이 Java 11(LTS), Java 17(LTS)를 사용할 수 있다.

- 안드로이드 개발의 경우 여전히 Java 7, Java 8 기반이 주류.

    - 안드로이드 개발을 위해 Java와 100% 호환되는 Kotlin을 사용하기도 한다.
    - 더 간결하고 효율적이고 안전한 코드 작성을 가능하게 한다.

<br><br>

## 📌 특정 자바 버전 '만' 학습해야할까?

- Python은 2와 3 릴리스 사이에 심각한 문제가 있다.

    - but> 자바는 하위 호환성이 매우 높다.

- 하위 호환성(backward compatible) : Java 5 또는 Java 8 프로그램이 Java 8 - 17 가상 머신에서 실행되도록 보장한다.

    - 반대로 Java 17을 Java 8 JVM에서 돌리면 컴파일이 안된다.
    - java.lang.UnsuportedClassVersionError

- Java 8에 대한 내용들로 우선 토대를 쌓고, 11, 17 등으로 추가 기능을 학습하자.

<br><br>

## 📌 OracleJDK vs OpenJDK

| 특징 | **OracleJDK** | **OpenJDK** | 
|:----------:|:----------:|:----------:|
| 가격 | 상용(유료) | 오픈소스 기반(무료) | 
| 라이선스 | Oracle BCL (Binary Code License) | Oracle GPL v2 |  
| 업데이트 정책 | LTS(장기 지원) 업데이트 지원 받음 | LTS 없이 6개월마다 새 버전 배포 | 
| 플러그인 | Sun Microsystems 플러그인 지원 | 지원 X |
| 성능 | 상대적으로 CPU 사용량 작음, 메모리 사용량 작음, 응답시간 높음 | 상대적으로 CPU 사용량 높음, 메모리 사용량 높음, 응답시간 낮음 |

<br><br>

## 📌 참조

- https://velog.io/@jinyeong-afk/%EA%B8%B0%EC%88%A0-%EB%A9%B4%EC%A0%91-Java-11-vs-Java-17-%EC%B0%A8%EC%9D%B4
- https://velog.io/@ljo_0920/java-%EB%B2%84%EC%A0%84%EB%B3%84-%EC%B0%A8%EC%9D%B4-%ED%8A%B9%EC%A7%95
- Chat GPT 4
