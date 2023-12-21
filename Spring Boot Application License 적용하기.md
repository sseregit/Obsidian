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

#### AuthoizationManager
- #### AccessDecisionManager와 AccessDecisionVoters 대체한다.
- AuthoizationManager로 작업해야함

#### SecurityMetadataSource
- 지정된 보안 객체 호출에 적용되는 구성 속성을 저장하고 식별할 수 있는 클래스에 의해 구현된다.

