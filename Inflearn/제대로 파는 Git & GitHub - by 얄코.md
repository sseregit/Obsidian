[yalco git-github](https://www.yalco.kr/lectures/git-github/)

## Git을 배워야 하는 이유
- 개발자의 필수 소양
- Git
	- VCS
		- Version Control System

## CLI vs GUI

## Git 설정 & 프로젝트 관리 시작
`git config --global user.name "이름"`
`git config --global user.email "email"`
`git config --global init.defaultBranch main`
- master -> main

## Git에게 맡기지 않을 것들
- .gitignore

## 변화를 타임캡슐에 담아 묻기
`git diff`
- 변경내용을 확인
`git commit -am "(메시지)"`
- add와 commit을 한번에 할수 있다.
- 단 새로 추가된 파일이 없을때만 가능하다.

## 과거로 돌아가는 두 가지 방법
- reset
	- 원하는 시점으로 돌아간 뒤 이후 내역들을 지운다.
- revert
	- 되돌리기 원하는 시점의 커밋을 거꾸로 실행한다.