1. Spring Security가 적용되어 있는 프로젝트 이므로 Spring Security를 이용하기로 한다.

#### AuthorityAuthorizationManager
- #### AccessDecisionManager
	- 액세스 제어 결정을 내리는 핵심 구성 요소
	- 사용자가 보호받는 리소스에 접근할 수 있는 적절한 권한이 있는지 확인한다.
	- voter 개념이 있어 의사 결정을 하는데 사용된다.
	- decide는 반드시 구현해야한다
		- AffirmativeBased
			- AccessDecisionVoter가 승인하면 이전에 거부된 내용과 관계없이 접근이 승인
		- ConsensusBased
			- 다수의 AccessDecisionVoter가 승인하면 접근 승인
		- UnanimousBased
			- 모든 AccessDecisionVoter가 만장일치로 승인해야 접근 승인
- #### AccessDecisionVoters
	- 기본전략은 WebExpressionVoter으로 prefix로 ROLE_XXX가 사용된다.
	- 특정 Object에 접근할 때 필요한 ConfigAttributes들을 만족하는지 확인한다.
	- 권한 허용이나 인가등이 configAttributes가 되고 configure에서 지정한 리소스가 Object가 된다.
#### Custom Authorization Managers
- [blog article](https://spring.io/blog/2009/01/03/spring-security-customization-part-2-adjusting-secured-session-in-real-time/)

#### AuthorizationManager
- Authorization처리를 담당한다.
- 두가지 메서드
	- check
		- 구현체에서 반드시 구현되어야하고 AuthorizationDecision을 반환한다.
	- verify
		- 내부적으로 check를 호출하여 사용한다.
- #### AccessDecisionManager와 AccessDecisionVoters 대체한다.
- 인증이 된다음에 호출하기 때문에 인증전에 사용하기엔 적절하지 않다.

#### SecurityMetadataSource
- 지정된 보안 객체 호출에 적용되는 구성 속성을 저장하고 식별할 수 있는 클래스에 의해 구현된다.

- 사용자 정의 필터로 처리하는법
```java
public class LicenseFilter implements Filter {
    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        HttpServletRequest httpRequest = (HttpServletRequest) request;
        HttpServletResponse httpResponse = (HttpServletResponse) response;
			...
       throw new AccessDeniedException("접근하지마");
    }
}
```
- 가장 현실적으로 편하고 문제가 없을수도 있다.
- 고려해야할사항
	- `http.addFilterBefore(new LicenseFilter(), AuthorizationFilter.class);`
		- 이런식으로 AuthorizationFilter앞에 붙일수도있지만
		- AuthorizationFilter를 상속받아 사용할수도 있을꺼같다.

- Filter를 이용해서 Application접근을 막고
- AuthorizationManager를 구현해서 로그인한 후에도 접근이 가능한지 안한지를 막을수 있다.

License 검증용 필터 라이브러리를 등록하는법
1. 적용할 프로젝트에 동일한 스프링 버전을 의존성으로 추가한다.
	1. *주의*
		1. Gradle Version에 따라 의존성 추가에 대한 버그가 존재한다.
		2. 최신버전으로 했을때 추가가 안됬고 버전을 낮추어서 처리했다.
2. Filter를 구현한다
	1. implement javax.servlet.Filter
		1. 구현할시 redirect나 forward 등등의 이유로 중복호출이 일어난다
	2. extends OncePerRequestFilter
		1. 필터를 단한번만 호출한다. 최초 접속을 막을 방법으로 구현하고 있으므로 이것을 상속받아 구현하는것이 맞다.
3. Bean을 등록한다.
	1. Spring에 사용할것이므로 Bean으로 등록해야하며
	2. *@AutoConfiguration*을 사용해 자동 빈등록을 한다
		1. 경우에따라 @Condition~~ 를 활용해 등록이 되는경우와 안되는 경우로 나눌수도 있다.
		2. @AutoConfiguration을 활용하기 위해선
		3. src/**resources/META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports** 를 추가해야한다 반드시 지켜야하는 룰!
		4. 해당패키지.Class 를 추가한다 `org.example.Config`
		5. ./gradlew clean build로 jar파일을 내가 원하는 프로젝트의 libs/jar파일을 옮긴다.
4. `implementation files('lib/untitled1-1.0-SNAPSHOT.jar')` 의존성을 추가해준다.
	1. 인식이 되었는지 안되었는지에 대한 여부를 체크해야한다.

License에 사용할 암호화
- AES-256
	- 대칭키 암호화의 장점
		- **암호화와 복호화에 동일한 키를 사용한다.**
	- 높은 보안성
		- 256비트의 길이의 키를 사용하기 때문에 무차별 대입 공격에 강하다.
	- 속도
		- 대량의 데이터를 빠르게 암호화 하거나 복호화할때 유리하다.