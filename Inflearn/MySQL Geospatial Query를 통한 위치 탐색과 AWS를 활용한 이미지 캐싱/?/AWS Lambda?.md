# AWS Lambda
- 코드 조각(function)을 서버 없이(Serverless) 실행할 수 있도록 해주는 이벤트 기반 컴퓨팅 서비스
### 핵심 특성
- 서버 관리 불필요 (운영체제, 인스턴스 X)
- 자동 확장 (요청 많아지면 자동으로 병렬 실행)
- 이벤트 기반 실행 (S3 업로드, API Gateway, DynamoDB 등과 연결)
- 짧은 실행 시간 (기본 최대 15분)
- 요금은 실행 시간 기준 (사용한 만큼만 과금)