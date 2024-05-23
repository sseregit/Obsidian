스프링 MVC 2편
		1. 섹션 3 ~ 섹션 5
[Validation](https://docs.spring.io/spring-boot/docs/current/reference/html/io.html#io.validation)

[Validation, Data Binding, and Type Conversion](https://docs.spring.io/spring-framework/reference/core/validation.html)

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

- messages_{언어 정보}.properties

`public interface MessageSource {...}`
- 값을 호출하여 사용 가능.

- [Internationalization](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.internationalization)
- 
- 