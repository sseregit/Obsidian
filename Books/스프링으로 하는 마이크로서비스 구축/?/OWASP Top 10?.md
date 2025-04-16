# OWASP Top 10
- 웹 애플리케이션 보안 위험을 관리하기 위한 핵심 가이드 라인

### 핵심 위험 요소 (2021 기준)

| 순번  | 위험 요소                                      | 설명 요약                             |
| --- | ------------------------------------------ | --------------------------------- |
| A01 | Broken Access Control                      | 인가되지 않은 리소스 접근                    |
| A02 | Cryptographic Failures                     | 데이터 암호화 실패(HTTPS 누락, 약한 해시등)      |
| A03 | Injection                                  | SQL Injection, XSS등 사용자 입력 처리 실패  |
| A04 | Insecure Design                            | 아예 설계부터 보안이 빠져 있는 경우              |
| A05 | Security Misconfiguration                  | 디폴트 설정, 잘못된 CORS, 디버그 모드          |
| A06 | Vulnerable and Outdated Components         | 오래된 라이브러리/프레임워크 사용                |
| A07 | Identification and Authentication Failures | 인증 실패 (약한 로그인, brute-force 방지 실패) |
| A08 | Software and Data Integrity Failures       | CI/CD 또는 서명되지 않은 업데이트 등 신뢰성 문제    |
| A09 | Security Logging and Monitoring Failures   | 이상행위 탐지 및 알림 부재                   |
| A10 | Server-Side Request Forgery (SSRF)         | 서버가 외부 요청을 보내도록 속이는 공격            |
