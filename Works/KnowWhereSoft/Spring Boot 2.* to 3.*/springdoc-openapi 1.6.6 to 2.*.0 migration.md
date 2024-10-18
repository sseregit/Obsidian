## 참고 사이트
[springdoc-openapi v2.5.0](https://springdoc.org/#migrating-from-springdoc-v1)
[Springdoc-openapi Properties](https://springdoc.org/properties.html)
[Spring Boot 3에 Swagger 적용하기(springdoc-openapi)](https://velog.io/@najiexx/Spring-Boot-3%EC%97%90-Swagger-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0springdoc-openapi)
[# SpringDoc UI 인증을 위한 토큰 기본값 표시](https://kdev.ing/springdoc-ui-bearer-authentication/)
[# Swagger - Springdoc access token, refresh token 설정](https://velog.io/@seulpace/Swagger-Springdoc-access-token-refresh-token-%EC%84%A4%EC%A0%95)
[# OpenAPI에 대한 JWT 인증 구성](https://www.baeldung.com/openapi-jwt-authentication)
[## Swagger OAuth 2.0 Flows](https://swagger.io/docs/specification/authentication/oauth2/)
```groovy
// swagger  
implementation ('org.springdoc:springdoc-openapi-ui:1.6.6'){  
    exclude group: 'com.fasterxml.jackson.dataformat', module:'jackson-dataformat-yaml'  
}  

// 아래로 변경
implementation 'org.springdoc:springdoc-openapi-starter-webmvc-ui:2.5.0'
```

## JWT 적용
```groovy
springdoc.show-login-endpoint=true
```
- login endpoint를 추가할수 있다.
- endpoint만 추가되는 것이고 Authorize버튼 생성이 되는건 아님.

```java
@Bean  
public OpenAPI openAPI() {  
    Info info = new Info()  
            .title("PIONEER RMS Rest API Document").version("v2.0");  
  
    final String securitySchemeName = "bearerAuth";  
  
    return new OpenAPI()  
            .addSecurityItem(new SecurityRequirement().addList(securitySchemeName))  
            .components(new Components()  
                    .addSecuritySchemes(securitySchemeName, new SecurityScheme().name(securitySchemeName).type(SecurityScheme.Type.HTTP).scheme("bearer").bearerFormat("JWT")))  
            .info(info);  
  
}
```
- SecurityRequirement로 모든 API에 토큰 인증을 한다는 조건을 걸고
- SecurityScheme로 로 인증을 만든다.

### flow 적용
```java
@Bean  
public OpenAPI openAPI() {  
    Info info = new Info()  
            .title("PIONEER RMS Rest API Document").version("v2.0");  
  
    final String securitySchemeName = "bearerAuth";  
  
    return new OpenAPI()  
            .components(  
                    new Components()  
                            .addSecuritySchemes(securitySchemeName, new SecurityScheme()  
                                    .type(SecurityScheme.Type.HTTP)  
                                    .name(securitySchemeName)  
                                    .scheme("bearer")  
                                    .bearerFormat("JWT")  
                                    .in(SecurityScheme.In.HEADER)  
                                    .description("test Bearer token : " + JwtProcess.create(getTestLoginUser(), JwtVO.EXPIRATION_TIME * 358))))  
            .security(List.of(new SecurityRequirement().addList(securitySchemeName)))  
            .info(info);  
}
```
- flow에 대한 종류는 여러가지 이므로 적용전 체크할것