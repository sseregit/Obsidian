[Spring Batch](https://spring.io/projects/spring-batch)
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