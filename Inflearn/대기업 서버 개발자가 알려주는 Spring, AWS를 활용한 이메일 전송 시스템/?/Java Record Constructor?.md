# Record Constructor
### Compact Constructor
```java
record Record(
	String name
) {
	public Record {
		...
	}
}
```
- 필드 선언은 상관없이 로직만 작성하면 된다.
- 간단한 검증, 가공등 필요할 때 유용하다.
### Canoical Constructor
```java
record Record(
	String name
) {
	public Record(String name) {
		this.name = name
		...
	}
}
```
- 일반적인 클래스 생성자와 동일하다.