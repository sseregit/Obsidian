Primitive type도 Long, String으로 씀 컴파일러가 알아서 변환

?. Safe Call

?: null일 경우 삼항연산자

!!. 절대 not null

플랫폼타입 Java Type -> Kotlin

---
Type

Int, Long, Float, String...

java `instanceof` == kotlin `is` or `!is` Java처럼 전체 조건식에 !가 아닌 is앞에 !추가

obj as Person 형변환
obj as? Person null이면 null

Kotlin `Any` == Java `Object`

Kotlin `Unit` == Java `void`

Kotlin `Nothing` 
함수가 정상적으로 끝나지 않았다는 사실을 표현하는 역할

`val log = 사람의 이름은 ${person.name}이다.` 
중괄호 생략 가능
쓰는것이 가독성, 일괄변환, 정규식활용 측면에서 더 좋았음.

```kotlin
val str = “ABCD”
val a: String = str[0]
```

---
연산자

단항,산술연산자 동일

비교 연산자 Java와 동일
객체를 비교할 때 비교 연산자를 사용하면 자동으로 `compareTo`호출

동일성 `===`, 동등성 `==`

`in \ !in`
- 컬렉션이나 범위에 포함되어 있다. 포함되어 있지 않다.
`a..b`
- a부터 b까지의 범위 객체 생성
---
조건문

`number in 0..100` == `(number >= 0 && number <= 100)`

```kotlin
when (score / 10) {
	9 -> “A”
	8 -> “B”
	7 -> “C”
	else -> “D”
}

when (score) {
	in 90..99 -> “A”
	in 80..89 -> “B”
	in 70..79 -> “C”
	else -> “D”
}

when (score) {
	0, 1, -1 -> “A”
	else -> “D”
}

when {
	number == 0 -> “A”
	else -> “D”
}

```
---
반복문
```kotlin
for (i in 1..3) {}

for (i in 3 downTo 1) {}

for (i in 1..3 step 2) {}
```
---
예외
Kotlin에서는 Checked Exception 과 Unchecked Exception을 구분하지않는다 모두 Unchecked Exception

try with resources - Kotlin엔 없음 대신 `use`사용
`BufferedReader(FileReader(path)).use {reader -> ...}`

---
함수