[Spring Batch 5.1.x](https://spring.io/projects/spring-batch)
[Spring Batch 4.2.x 한글번역](https://godekdls.github.io/Spring%20Batch/contents/)
[Spring Batch Guide](https://spring.io/guides/gs/batch-processing#scratch)
- `schema-@@platform@@.sql`
	- @@platform@@
		- 특정 데이터베이스 플랫폼을 넣으면 해당 플랫폼에서 자동실행시켜준다.
		- ``schema-all.sql``
			- 모든 플랫폼에서 실행한다는 의미가 된다.
[Spring Batch Document](https://docs.spring.io/spring-batch/reference/index.html)
- 낙관적 잠금은 온라인 애플리케이션에 어울리고
- 비관적 잠금은 배치 애플리케이션에 더 적합하다.
![[Batch Stereotypes.png]]

## [Job](https://docs.spring.io/spring-batch/reference/domain.html#job)	
- 전체 배치 프로세스를 캡슐화하는 엔티티
![[Job Hierarchy.png]]
- 스텝 인스턴스를 위한 컨테이너

JobInstance
- 논리적 작업의 실행 개념을 나타낸다.
- 로드할 데이터와 전혀 관련이 없다.
	- 데이터 로드되는 방식은 전적으로 ItemReader 구현에 달려있다.
- JobInstance = Job + JobParameter 식별 가능하다.

JobParameters
- JobInstance를 구별할수 있게 해준다.
- 배치 작업을 시작하는 데 사용되는 매개변수 집합을 보유 한다.

JobExecution
- 잡을 실행하려는 단일 시도에 대한 기술적 개념
- 실행이 성공적으로 완료되지 않는 한 주어진 실행에 해당하는 JobInstance는 완료된 것으로 간주되지 않는다.

## [Step](https://docs.spring.io/spring-batch/reference/domain.html#step)
- 배치 작업의 독립적이고 순차적인 단계를 캡슐화하는 도메인 객체
- 모든 작업은 전적으로 하나 이상의 단계로 구성
- 일괄처리를 정의하고 제어하는 필요한 모든 정보를 포함한다.
![[Job Hierarchy With Steps.png]]

StepExecution
- 스텝을 실행하려는 한 번의 시도를 나타낸다.
- 스텝이 실행될 때마다 새 StepExecution이 생성되며, JobExecution과 유사하다.
- 앞 단계가 실패하여 실행에 실패하면 해당 단계에 대한 실행은 유지되지 않는다.

## [ExecutionContext](https://docs.spring.io/spring-batch/reference/domain.html#executioncontext)
- 개발자에게 StepExecution 또는 JobExecution 범위가 지정된 영구상태를 저장할 수 잇는 장소를 제공한다.
- JobExecution당 하나 이상의 ExecutionContext가 있고 모든 StepExecution당 하나씩 있다는것에 유의해야 한다.
- Step으로 범위가 지정된 것은 단계의 모든 커밋 지점에 저장 되는 반면, 작업으로 범위가 지정된 것은 모든 단계 실행 사이에 저장된다.

## [JobRepository](https://docs.spring.io/spring-batch/reference/domain.html#jobrepository)
- 위에서 언급된 모든 저장(persistence) 매커니즘을 담당한다.

## [JobLauncher](https://docs.spring.io/spring-batch/reference/domain.html#joblauncher)
- JobParameters로 Job을 실행한느 간단한 인터페이스

## [ItemReader](https://docs.spring.io/spring-batch/reference/domain.html#itemreader)
- Step에서 아이템을 한 번에 하나씩 읽어오는 작업을 추상화한 개념이다.
- 더 이상 읽을 아이템이 없으면 null을 리턴한다.

## [ItemWriter](https://docs.spring.io/spring-batch/reference/domain.html#itemwriter)
- Step에서 배치나 청크 단위로 아이템을 출력하는 작업을 추상화한다.
- 다음에 받을 입력이 무엇인지는 알지 못하며 현재 받은 아이템만 알고 있다.

## [ItemProcessor](https://docs.spring.io/spring-batch/reference/domain.html#itemprocessor)
- 아이템을 처리하는 비즈니스 로직을 나타내는 추상화 개념이다.
- 데이터 변환이나 다른 비즈니스 처리를 담당한다.

## [단위 테스트](https://docs.spring.io/spring-batch/reference/testing.html)