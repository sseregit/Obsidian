[jenkinsci/jenkins](https://github.com/jenkinsci/jenkins)
[Contributing to Jenkins](https://github.com/Bandagiswapnil/jenkins/blob/af424b5e64e89d9ec741e05363dcf6102adbfd62/CONTRIBUTING.md#contributing-to-jenkins)
[Developer Documentation](https://www.jenkins.io/doc/developer/)
[IntelliJ Setup for Jenkins Core Development](https://www.jenkins.io/doc/developer/building/intellij/)

zip파일로 실행할시에 git관련 정보를 불러오는 소스들이 많아 건드려야할 곳이 많다 **clone**으로 진행할 것

Intellij 기준
- Building Jenkins
	- Run -> Edit Configurations -> Add -> Maven ->  Run 입력 `am -pl war,bom -DskipTests -Dspotbugs.skip clean install` -> 실행
- Run Jenkins
	- Run -> Edit Configurations -> Add -> Maven ->  Run 입력 `-pl war jetty:run` -> 실행
	- 그대로 Debug으로 실행하면 Debug 모드로 실행

