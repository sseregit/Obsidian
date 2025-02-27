[First steps](https://prometheus.io/docs/introduction/first_steps/)

설치 OS darwin
- Apple이 자사 제품용으로 개발한 운영체제

[prometheus-3.2.1.darwin-amd64.tar.gz](https://github.com/prometheus/prometheus/releases/download/v3.2.1/prometheus-3.2.1.darwin-amd64.tar.gz) 설치
```bash
tar xvfz prometheus-*.tar.gz
cd prometheus-*
```

[prometheus-3.2.1.darwin-amd64.tar.gz](https://github.com/prometheus/prometheus/releases/download/v3.2.1/prometheus-3.2.1.darwin-amd64.tar.gz)설치 이슈

amd64로 설치시 보안허용이 필요하고
arm64로 설치시 보안허용이 필요없이 진행이 가능하다.

시스템 설정 -> 개인정보 보호 및 보안 -> 보안 탭 -> Mac을 보호 blabla ‘prometheus’ 차단했습니다 -> 그래도 허용 클릭

`./prometheus --help`가 가능해진다.
****
==prometheus.yml== 샘플 설정파일

`global`
- 프로메테우스 서버의 글로벌 설정을 지정한다.
- `scrape_interval`
	- 프로메테우스가 타겟을 스크랩할 간격을 나타낸다.
	- 해당 설정은 타겟마다 개별적으로 재정의할 수 있다.
- `evaluation_interval`
	- 프로메테우스가 rule을 평가할 주기를 지정한다.
	- 프로메테우스는 rule을 사용해서 새 시계열을 만들고 alert를 생성한다.

`scrape_configs`
- 프로메테우스가 모니터링할 리소스를 지정한다.
- 프로메테우스는 자기 자신에 대한 데이터도 HTTP 엔드포인트로 노출하기 때문에, 자체 상태도 스크랩하고 모니터링할 수 있다.
[전체 설정 옵션](https://prometheus.io/docs/prometheus/latest/configuration/configuration/)
****
````bash
./prometheus --config.file=prometheus.yml
````
- `--config.file=`
	- 로드할 설정 파일을 지정한다.