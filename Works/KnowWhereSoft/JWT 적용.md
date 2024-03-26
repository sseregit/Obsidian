[[Spring Boot 2.* to 3.*]]에서 만든 프로젝트에 JWT를 적용하기.

참고 자료
[스프링부트 JUnit 테스트 - 시큐리티를 활용한 Bank 애플리케이션](https://github.com/codingspecialist/junit-bank-class)
[spring security sample - JWT](https://github.com/spring-projects/spring-security-samples/tree/main/servlet/spring-boot/java/jwt/login)
[Spring Spring Security를 이용한 로그인 구현 (스프링부트 3.X 버전) [4] - JWT를 이용한 인증](https://velog.io/@dh1010a/Spring-Spring-Security%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EB%A1%9C%EA%B7%B8%EC%9D%B8-%EA%B5%AC%ED%98%84-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-3.X-%EB%B2%84%EC%A0%84-4-JWT%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EC%9D%B8%EC%A6%9D)
[Spring Security OAuth2로 JWT 검증하기](https://velog.io/@hong1008/spring-oauth-jwt)
[JWT 인증 작동 방식](https://docs.spring.io/spring-security/reference/servlet/oauth2/resource-server/jwt.html#oauth2resourceserver-jwt-architecture)
[JWT + Spring Security 구현](https://velog.io/@wooyong99/JWT-Spring-Security-%EA%B5%AC%ED%98%84)
[nimbus-jose-jwt](https://connect2id.com/products/nimbus-jose-jwt/examples/jwt-with-hmac)
[우테코 JWT 방식에서 로그아웃, Refresh Token 만들기(1): JWT의 Stateless한 특징을 최대한 살리려면?](https://engineerinsight.tistory.com/232)

변경하면서 생각해야 할것들
1. 로그인 로그아웃 로그
2. 메뉴접근 로그
3. swagger jwt 적용 방법

작업
1. 의존성 변경
```groovy
implementation "org.springframework.boot:spring-boot-starter-oauth2-client"

implementation "org.springframework.boot:spring-boot-starter-oauth2-resource-server"
```
- 둘의 차이점은 oauth2를 사용하는 클라이언트냐 리소스 서버이냐 의 차이
- JWT를 구현해서 사용하려면 resource-server로 충분하다.

2. JWT Token 생성
```java
@Test  
void nimbusJoseJwtCreate() throws JOSEException, ParseException, NoSuchAlgorithmException {  
  
    String secretKey = "01874e6c23522dda2b5bad947028a4b5ea55ffb273a2c650a4fef31469519942";  
  
    JWSSigner signer = new MACSigner(secretKey);  
  
    JWTClaimsSet claimsSet = new JWTClaimsSet.Builder()  
            .subject("JWT")  
            .claim("username", "hcinfotest")  
            .expirationTime(new Date(new Date().getTime() + (1000 * 60 * 60 * 24 * 7)))  
            .build();  
  
    SignedJWT signedJWT = new SignedJWT(new JWSHeader(JWSAlgorithm.HS256), claimsSet);  
  
    signedJWT.sign(signer);  
  
    String token = signedJWT.serialize();  
  
    System.out.println("token = " + token);  
  
    signedJWT = SignedJWT.parse(token);  
  
    JWSVerifier verifier = new MACVerifier(secretKey);  
  
    assertThat(signedJWT.verify(verifier)).isTrue();  
    assertThat(signedJWT.getJWTClaimsSet().getSubject()).isEqualTo("JWT");  
    assertThat(signedJWT.getJWTClaimsSet().getClaim("username")).isEqualTo("hcinfotest");  
    assertThat(new Date().before(signedJWT.getJWTClaimsSet().getExpirationTime())).isTrue();  
}
```
- oauth2에 이미 등록이 되어있는 `[Nimbus JOSE + JWT]`를 사용하였다.
- 발행은 내가하지만 검증은 oauth2-resource-server내에서 처리함.

`http.addFilterAt(new JwtAuthenticationFilter(authenticationManager()), UsernamePasswordAuthenticationFilter.class)`
- UsernamePasswordAuthenticationFilter을 상속받아 사용하기 위한 설정

```java
@Bean  
public AuthenticationManager authenticationManager(){  
    return new ProviderManager(customAuthenticationProvider());  
}  
  
@Bean  
public CustomAuthenticationProvider customAuthenticationProvider(){  
    return new CustomAuthenticationProvider(loginService(), passwordEncoder());  
}
```
- authenticationManager()를 등록해서 사용해야한다.
- `http.getSharedObject(AuthenticationManager.class);`를 사용할수 있다고 알고있었지만 무슨짓을 해도 null만 들어옴

`public class LoginService implements UserDetailsService`
- 입력받은 값의 유저아이디의 DB안에 데이터를 찾는 역할을 하고 `public class LoginUser implements UserDetails` 를 return 한다.

`public class CustomAuthenticationProvider implements AuthenticationProvider`
- 패스워드를 검증하고 검증이 완료되면 UsernamePasswordAuthenticationToken을 만들어 return 한다.

```java
public class JwtAuthenticationFilter extends UsernamePasswordAuthenticationFilter {
	@Override  
	protected void successfulAuthentication(HttpServletRequest request, HttpServletResponse response, FilterChain chain, Authentication authResult) throws IOException, ServletException {  
	    LoginUser loginUser = (LoginUser) authResult.getPrincipal();  
	  
	    String jwtToken = JwtProcess.create(loginUser);  
	  
	    response.addHeader(JwtVO.HEADER, jwtToken);  
	    response.setContentType(MediaType.APPLICATION_JSON_VALUE);  
	    response.setStatus(HttpStatus.OK.value());  
	    response.getWriter().println(mapper.writeValueAsString(new LoginResponse(loginUser)));  
	}
}
```
- JWT토큰을 헤더에 넣어 Login정보와 함께 리턴한다.

- Token검증
	- Token검증은 `implementation "org.springframework.boot:spring-boot-starter-oauth2-resource-server"`를 이용해서 한다.

```java
@Bean  
public JwtDecoder jwtDecoder() {  
    MacAlgorithm algorithm = MacAlgorithm.HS256;  
  
    return NimbusJwtDecoder.withSecretKey(new SecretKeySpec(JwtVO.SECRET.getBytes(), algorithm.getName()))  
            .macAlgorithm(algorithm)  
            .build();  
}
```
- Bean으로 등록해주고

BearerTokenAuthenticationFilter
- DefaultBearerTokenResolver
	- Header의 Authorization과 Bearer를 확인하고 Bearer를 제거한 token을 넘겨준다.
- 넘겨받은 토큰으로 BearerTokenAuthenticationToken을 만든다.
- JwtAuthenticationProvider
	- getJwt에서 등록한 JwtDecoder가 작동해 복호화를 한다.
	- `token.jwtAuthenticationConverter(new SimpleJwtAuthenticationConverter()))`
		- 등록한 Converter가 발동한다.
- **Provider와 Converter는 커스텀이 가능하다.** 

이후 부터 작업할 목록
1. Controller 제거
2. CustomEntryPoint 권한(401) 관련 에러 처리 변경
3. CustomAccessDeniedHandler 권한(403) 관련 에러 처리 변경
4. 예외처리용 Class 작성
5. Expiration_time의 대한 제한이 걸려있지 않음
	1. JwtDecoder를 내가 구현해야 적용 가능
6. 토큰 없이 시도했을 경우..?
7. Refresh token등등 고려해야함.