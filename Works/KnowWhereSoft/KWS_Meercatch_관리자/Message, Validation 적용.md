
# 다국어
- 스프링 MVC 2편
	- 섹션 3
```java
@Bean
public MessageSource messageSource() {
 ResourceBundleMessageSource messageSource = new
ResourceBundleMessageSource();
 messageSource.setBasenames("messages", "errors");
 messageSource.setDefaultEncoding("utf-8");
 return messageSource;
}
```
- 직접 등록 방법
- /resources/messages.properties
- 여러파일 지정 가능

- 스프링 부트는 자동으로 스프링 빈을 등록해준다.
	- [messages 속성](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties.core.spring.messages.always-use-message-format)
	- 해당 속성을 정의하면 된다.
[Spring MessageSource 자동설정으로 MessageSource 쉽게 세팅하기](https://velog.io/@youjung/Spring-MessageSource-%EC%9E%90%EB%8F%99%EC%84%A4%EC%A0%95%EC%9C%BC%EB%A1%9C-MessageSource-%EC%89%BD%EA%B2%8C-%EC%84%B8%ED%8C%85%ED%95%98%EA%B8%B0)

| 속성                      | 타입       | 설명                                                                            | 기본값                    |
| ----------------------- | -------- | ----------------------------------------------------------------------------- | ---------------------- |
| basename                | String   | - 쉼표로 구분된 basename 리스트                                                        | "messages"             |
| encoding                | Charset  | - 메세지 인코딩 방식                                                                  | StandardCharsets.UTF_8 |
| cacheDuration           | Duration | - 로드된 리소스 번들 파일 캐시 기간.  <br>- 단위를 지정하지 않으면 초가 사용됨.                            | 영구적으로 캐시됨              |
| fallbackToSystemLocale  | boolean  | - 요청받은 Locale에 대한 파일을 찾지 못할 경우 시스템 설정 Locale을 사용할 것인지에 대한 유무                  | true                   |
| alwaysUseMessageFormat  | boolean  | - 전달받은 인자를 제외하고 메세지를 읽어들이는 MessageFormat 규칙을 항상 적용할 것인지에 대한 유무                | false                  |
| useCodeAsDefaultMessage | boolean  | - 메세지 파일에 코드에 대해당하는 값이 없을 때 NoSuchMessageException 대신 코드를 메세지로 사용할 것인지에 대한 유무 | false                  |

- messages_{언어 정보}.properties

`public interface MessageSource {...}`
- 값을 호출하여 사용 가능.

- properties파일에 대한 인코딩을 변경해야한다.
	- intellij 설정 -> 에디터 -> 파일 인코딩 -> 프로퍼티 파일에 대한 디폴트 인코딩 -> UTF-8
- [Internationalization](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.internationalization)

## Validation에 MessageSource활용
- 스프링 MVC 2편
	- 섹션 4 ~ 섹션 5
[Validation](https://docs.spring.io/spring-boot/docs/current/reference/html/io.html#io.validation)
[Validation, Data Binding, and Type Conversion](https://docs.spring.io/spring-framework/reference/core/validation.html)

- BindingResult에 검증 오류를 적용하는 3가지 방법 
	1. @ModelAttribute 의 객체에 타입 오류 등으로 바인딩이 실패하는 경우 스프링이 FieldError 생성해서 BindingResult 에 넣어준다. 
	2. 개발자가 직접 넣어준다. 
		1. 필드 오류
			1. `bindingResult.addError(new FieldError(...))`
			2. `bindingResult.rejectValue(...)`
		2. 글로벌 오류 (Rule)
			1. `bindingResult.addError(new ObjectError(...))`
			2. `bindingResult.rejectValue(...)`
		3. ValidationUtils
	3. Validator 사용

- MessageCodesResolver
	- 오류 코드를 이해하기
	- 객체 오류
		- 코드 + "." + Object
		- 코드
	- 필드 오류
		- 코드 + "." + Object + "." + Field
		- 코드 + Field
		- 코드 + Field Type (Java.lang.String)
		- 코드

- 스프링은 타입 오류시 typeMismatch 오류 코드를 사용한다.

- Validator 구현하기
	- 직접 의존성 받아서 사용하기
	- WebDataBinder 사용하기
```java
@InitBinder
public void init(WebDataBinder dataBinder) {
	dataBinder.addValidators(itemValidator);
}
```
	- 호출하는데 RequestMapping에 @Validated 적용
		- 검증기를 실행하라는 애노테이션

	- 글로벌 설정
```java
@SpringBootApplication
public class Application implements WebMvcConfigurer {
	public static void main(String[] args) {
		SpringApplication.run(ItemServiceApplication.class, args);
	}

	@Override
	public Validator getValidator() {
		return new ItemValidator();
	}
}
```

	- 글로벌 적용을 하면 BeanValidator가 자동 등록되지 않는다.

- Bean Validation
	- 메시지 코드 규칙
		- @애노테이션 + "." + Object + "." + Field
		- @애노테이션 + "." + Field
		- @애노테이션 + Field Type(Java.lang.String)
		- @애노테이션
	- Messages를 사용하는 properties에 적용하면 된다.
	- 글로벌 오류 처리방법 (Rule)
```java
@Data @ScriptAssert(lang = "javascript", script = "_this.price * _this.quantity >= 10000") public class Item { //... }
```

	- 해당 적용되는 메시지 코드
		- ScriptAssert + "." + Object
		- ScriptAssert

- Bean Validation 으로 Field Error를 잡고 
- Object Error는 `bindingResult.reject(...)`를 활용하고 
- typeMismatch는 스프링이 잡아준다.

- 같은 객체로 각각 다르게 검증하는 방법
	- BeanValidation의 groups 기능 사용
	- 같은 객체로 사용하지 않고 각각의 객체를 만든다.

- BeanValidation의 group
```java
public class ... {

	@NotNull(groups = GroupClass.class)
	....

}
```

	- GroupClass라는 interface선언이 필요하다.
	- 그룹 기능을 사용할 모든 애노테이션에 추가해야함
	- {}를 활용해 여러개도 가능
- 사용법
```java
@...Mapping("/...")
... ... ...(@Validated(GroupClass.class)) ... {
	...
}
```
- @Valid는 사용 불가능

- 배보다 배꼽이 더 크다. 각각의 객체를 만드는게 좋다.