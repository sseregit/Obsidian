## 코틀린에서 변수를 다루는 방법
- 모든 변수는 var / val을 붙여 주어야 한다.
	- var : 변경 가능하다 / val : 변경 불가능하다 (read-only)
	- 타입을 명시적으로 작성하지 않아도, 타입이 추론된다.
	- Primitive Type과 Reference Type을 구분하지 않아도 된다.
	- Null이 들어갈 수 있는 변수는 타입 뒤에 **?** 를 붙여주어야 한다.
		- 아예 다른 타입으로 간주된다.
	- 객체를 인스턴스화 할 때 new를 붙이지 않아야 한다.

## 코틀린에서 null을 다루는 방법
- 코틀린에서 null이 들어갈 수 있는 타입은 완전히 다르게 간주된다
	- 한번 null 검사를 하면 non-null임을 컴파일러가 알 수 있다.
- null이 아닌 경우에만 호출되는 Safe Call (?.) 이 있다.
- null인 경우에만 호출되는 Elvis 연산자 (?:) 가 있다.
- null이 절대 아닐대 사용할 수 있는 널 아님 단언 (!!) 이 있다.
- Kotlin에서 Java 코드를 사용할 때 플랫폼 타입 사용에 유의해야 한다.
	- Java 코드를 읽으며 널 가능성 확인 / Kotlin으로 wrapping

## 코틀린에서 Type을 다루는 방법
- 변수를 명시적으로 변환이 필요하다.
	- toType();
- Any
	- Java의 Object 역할
	- 모든 Primitive Type의 최상의 타입도 Any
- Unit
	- Java의 void 역할
	- Unit은 그 자체로 타입 인자로 사용 가능하다.
- Nothing
	- 함수가 정상적으로 끝나지 않았다는 사실을 표현하는 역할
	- 무조건 예외를 반환하는 함수 / 무한 루프 함수 등등..
- is , !is, as , as?를 이용해 타입을 확인하고 캐스팅한다.
- 문자열을 가공할때 ${변수} 와 """"""를 사용하면 깔끔한 코딩이 가능하다.
- 문자열에서 문자를 가져올때의 Java의 배열처럼 []를 사용한다.

## 코틀린에서 연산자를 다루는 방법
- 일반타입에 비교연산자를 사용하면 자동으로 compareTo를 호출해준다.
- 동일성 === 동등성 == 을 호출한다.

## 코틀린에서 조건문을 다루는 방법
- Statement
	- 프로그램의 문장, 하나의 값으로 도출되지 않는다.
- Expression
	- 하나의 값으로 도출되는 문장
	- Kotlin
- switch -> when으로 대체

## 코틀린에서 반복문을 다루는 방법
- for each문에서 in을 사용한다
- 전통적인 for문에서 등차수열과 in을 사용한다
	- downTo, step 중위함수 활용

## 코틀린에서 예외를 다루는 방법
- try catch가 expression 이다.
- Kotlin에서는 Checked Exception과 Unchecked Exception을 구분하지 않는다.
	- 모두 Unchecked Exception 이다.
- try - with -resources 구문이 존재 하지 않는다.
	- use inline 확장함수를 사용한다. (설명은 이후 강의에서)

## 코틀린에서 함수를 다루는 방법  
- default parameter
- named parameter
- 가변인자 앞에 vararg
- spread 연산자 *

## 코틀린에서 클래스를 다루는 방법
```kotlin
class Person(
	val name: String,
	var age: Int
) {
	init {
		...
	}

	constructor(name: String): this(name, 1)
}
```

- init block
	- 클래스가 생성되는 시점에 호출된다
- constructor
	- 새로운 생성자 생성
- Converting과 같은 경우 부생성자를 사용할 수 있지만, 그보다는 정적 팩토리 메소드를 추천 한다.

## 코틀린에서 상속을 다루는 방법

- 프로퍼티를 override 할 때 무조건 Open을 붙여 줘야만 한다.
- 인터페이스
	- 코틀린에서는 default를 굳이 사용하지 않아도된다.

```java
@Override  
public void act() {  
    JavaFlyable.super.act();  
    JavaSwimable.super.act();  
}
```
->
```kotlin
override fun act() {  
    super<Swimable>.act()  
    super<Flyable>.act()  
}
```
- kotlin에서는 backing field가 없는 프로퍼티를 interface에 만들 수 있다.
	- getter에 대한 default 메소드나 getter에 대한 추상 메소드를 인터페이스에 만들수 있다.
```kotlin
interface Swimable {  
  
    val swimAbility: Int  
        get() = 3  
  
    fun act() {  
        println(swimAbility)  
        println("어푸 어푸")  
    }  
}
```
- 클래스 상속받을 때 주의할 점
	- 상위 클래스에 constructor와 init 블락에서는 하위 클래스의 final이 아닌 field에 접근하면 안 된다
	- 상위 클래스를 설계할 때 생성자 또는 초기화 블록에 사용되는 프로퍼티에는 open을 피해야 한다.
- 상속 관련 키워드
	- final
		- overried를 할 수 없게 한다.
	- open
		- override를 열어 준다
	- abstract
		- 반드시 override 해야 한다.
	- override
		- 상위 타입을 오버라이드 하고 있다.
		- 어노테이션이 아니라 키워드임

## 코틀린에서 접근 제어를 다루는 방법
- 가시성 제어
	- protected
		- 같은 패키지 -> 선언된 클래스
	- default -> internal
		- internal
			- 같은 모듈에서만 접근 가능
	- kotlin의 기본 접근 지시어는 public
	- 생성자에 접근지시어를 붙이려면, constructor를 써줘야 한다.
- Java와 Kotlin을 함께 사용할 때 주의할 점
	- internal
		- 바이트 코드 상 public이 된다.
		- Java 코드에서는 Kotlin 모듈의 internal 코드를 가져올수 있다.
	- protected
		- Java는 같은 패키지의 Kotlin protected 멤버에 접근할 수 있다.

## 코틀린에서 object 키워드를 다루는 방법
```kotlin
    companion object {
        val MIN_AGE = 1 // 런타임시에 0값이 할당
        const val MIN_AGE = 1 // 컴파일시에 0값이 할당
		
		@JvmStatic
        fun newBaby(name: String): Person {
            return Person(name, MIN_AGE)
        }
    }
```
- Java의 static 변수 함수인것처럼 사용된다.
- companion object
	- 클래스와 동행하는 유일한 오브젝트
	- 동반객체도 하나의 객체로 간주된다.
		- 이름을 붙일 수도 있고, interface를 구현할 수도 있다.
- const
	- 진짜 상수에 붙이기 위한 용도
	- 기본타입과 String에 붙일 수 있다.
- @JvmStatic
	- Companion or 이름으로 부르지 않고 Person.newBaby()를 호출할수 있게한다.

- 싱글톤
	- `object Singleton`
- 익명 클래스
	- `object: Movable {...}`

## 코틀린에서 중첩 클래스를 다루는 방법
- 중첩 클래스의 종류
	- static을 사용하는 중첩 클래스
	- static을 사용하지 않는 중첩클래스
		- 내부 클래스(Inner Class)
		- 지역 클래스(Local Class)
		- 익명 클래스(Anonymous Class)
- 코틀린의 중첩 클래스와 내부클래스
	-  Java의 static 중첩 클래스 (권장되는 클래스 안의 클래스)
```kotlin
class JavaHouse(
    private val address: String,
    private val livingRoom: LivingRoom
) {
    class LivingRoom(
        private val area: Double
    )
}

```
- 권장되지 않는 클래스
```kotlin
class JavaHouse(
    private val address: String,
    private val livingRoom: LivingRoom
) {
    inner class LivingRoom(
        private val area: Double
    ) {
        val address: String
            get() = this@House.address;
    }
}
```
- 바깥 클래스 사용법
	- this@(바깥클래스명)
- 권장되지 않는 이유
	- 내부 클래스는 숨겨진 외부 클래스 정보를 가지고 있어 참조를 해지하지 못하는 경우 메모리 누수가 생길수 있고, 이를 디버깅 하기 어렵다.
	- 내부 클래스의 직렬화 형태가 명확하게 정의되지 않아 직렬화에 있어 제한이 있다.

## 코틀린에서 다양한 클래스를 다루는 방법

Data Class
```kotlin
data class PersonDto(
    private val name: String,
    private val age: Int
)
```
- 자동으로 equals, hashcode, toString을 만들어준다

Enum Class
```kotlin
enum class Country(
    private val code: String
) {
    KOREA("KO"),
    AMERICA("US")
    ;
}
```

Sealed Class, Sealed Interface
- 특징
	- **컴파일 타임때 하위 클래스의 타입을 모두 기억**한다.
		- 런타임때 클래스 타입이 추가될 수 없다.
	- 하위 클래스는 같은 패키지에 있어야 한다.
	- Enum과 다른 점
		- 클래스를 상속받을 수 있다.
		- 하위 클래스는 멀티 인스턴스가 가능하다.

## 코틀린에서 배열과 컬렉션을 다루는 방법
- Kotlin은 불변/가변을  지정해 주어야 한다는 사실을 꼭 기억해야 한다.
- Kotlin의 컬렉션이 Java에서 호출되면 컬렉션 내용이 변할 수 있음을 감안해야 한다.

## 코틀린에서 다양한 함수를 다루는 방법

### 확장함수
	자바 코드위에 자연스럽게 코틀린 코드를 사용할 수 는 없을까? 라는 고민에서 시작되었다.
	어떤 클래스 안에 있는 메소드처럼 호출할 수 있지만 위치가 클래스 밖에 존재 한다.
	수객객체 타입 == 확장하려는 클래스
		this를 이용할 수 있다.
	수신객체클래스의 private or protected 멤버를 호출할수 없다.
	멤버함수와 확장함수가 이름이 같다면 우선순위는 멤버함수가 먼저다.

### infix 함수
	함수를 호출하는 새로운 방법
		`(변수) 함수이름 (argument)`

### inline 함수
	함수가 호출되는 대신, 함수를 호출한 지점에 함수 본문을 그대로 복붙하고 싶은 경우
	함수를 호출하는 쪽에 해당 함수 코드가 그냥 들어가는것
	성능 측정과 함께 신중하게 사용되어야 한다.

### 지역함수
	함수 안에 함수를 선언할수 있다.

## 코틀린에서 람다를 다루는 방법
### Java에서 람다를 다루기 위한 노력
	간결한 스트림의 등장 (병렬처리에 강점이 생겼다)
	자바에서 함수는 변수에 할당되거나 파라미터로 전달할 수 없다.
### 코틀린에서의 람다
	코틀린에서는 함수가 그 자체로 값이 될 수 있다.
	변수 할당과 파라미터로 넘기는것이 가능하다.
```kotlin
    // 만드는법
    // 만드는법
    val isApple: (Fruit) -> Boolean = fun(fruit: Fruit): Boolean {
        return fruit.name == "사과"
    }
    val isApple2: (Fruit) -> Boolean = { fruit: Fruit -> fruit.name == "사과" }
    // 호출하는법
    isApple(fruits[0])
    isApple.invoke(fruits[0])
```
### Closure
	코틀린에서는 람다가 시작하는 지점에 참조하고 있는 변수들을 모두 포획하여 그 정보를 가지고 있다.
	실행시점에 쓰고 있는 변수들을 모두 포획한 데이터 구조를 Closure라고 부른다.

### try-with-resources

## 코틀린에서 컬렉션을 함수형으로 다루는 방법

### 필터와 맵

### 다양한 컬렉션 처리 기능

### List를 Map으로

### 중첩된 컬렉션 처리

## 코틀린의 이모저모

### Type Alias와 as import

### 구조분해와 componentN 함수

### Jump와 Label
forEach에서 break를 하는 방법
```kotlin
run {
	List.forEach {
		number -> 
		if (number == 2) {
			return@run
		}
	}
}
```
continue
	return@forEach를 사용하면 된다.
### TakeIf와 TakeUnless
```kotlin
	fun getNumberOrNullV2(): Int? {
		return number.takeIf { it > 0}
	}
```
taskIf
	 주어진 조건을 만족하면 그 값이, 그렇지 않으면 null이 반환된다.
taskUnless
	주어진 조건을 만족하지 않으면 그 값이 그렇지 않으면 null이 반환된다.