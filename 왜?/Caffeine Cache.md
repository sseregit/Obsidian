왜? Caffeine 

원인
자주 쓰는 테이블이 컬럼 10개가 하나의 테이블의 정규화로 매번 code -> codeName으로 변경해야함.
이걸 조회할 때 마다 테이블 조회, code 테이블 조회후 map으로 만들어서 같이 던진다음에 thymeleaf로 loop를 돌때 처리함

고민
캐시 == Redis 라고 생각했지만 굳이 이정도 프로젝트에 I/O를 또두고 Redis를 관리 하는 번거로움을 안고 갈 필요가 없음

caffeine은 인 메모리 캐시 인데 라이브러리 하나 추가하면 그만임. 굳

필수
implementation 'org.springframework.boot:spring-boot-starter-cache'
implementation 'com.github.ben-manes.caffeine:caffeine'

@Cacheable
캐시 생성 및 전달을 담당
캐시에 데이터가 없을 경우에는 기존의 로직을 실행 후 캐시에 데이터를 추가 있으면 캐시 데이터를 반환

@CachePut
캐시 내용 수정을 담당
@Cacheable과 유사하게 실행 결과를 캐시에 저장하지만, 조회 시에 저장된 캐시 내용을 사용하지 않고 항상 메서드를 실행한다.

@CacheEvict
캐시 삭제 담당
@CacheEvict에 캐시 이름을 넣어주면 메소드가 실행될 때 캐시의 내용이 제거된다. 

---
구조적인 문제로 적용 실패 분석좀더 해봐야함.