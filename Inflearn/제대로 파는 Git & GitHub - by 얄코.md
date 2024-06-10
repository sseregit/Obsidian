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
- 한번 공유가 된 커밋들은 revert를 활용해서 되돌려야 한다.

## 과거로 돌아가기 실습
`git revert --no-commit (되돌릴 커밋 해시)`
- 바로 커밋이 되지 않는다.

## SourceTree로 진행해보기

## 여러 branch 만들어보기
`git branch branch명`
- 생성
`git branch`
- branch 목록 보기
`git switch branch명`
- branch 이동하기

- checkout 명령어가 Git 2.23버전부터 switch, restore로 분리되었다!

`git switch -c branch명`
- 브랜치 생성과 동시에 이동하기

`git branch -d branch명`
- 삭제
- -D
	- 지워질 브랜치에만 내용의 커밋이 있을 경우 강제 삭제 옵션

`git branch -m 기존branch명 새branch명`
- branch 이름변경

`git log --all --decorate --oneline --graph`
-  여러 브랜치의 내역 편리하게 보기

