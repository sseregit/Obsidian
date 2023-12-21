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
- AuthoizationManager로 작업해야함

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

1. 