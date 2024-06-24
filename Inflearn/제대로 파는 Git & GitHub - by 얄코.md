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

## branch를 합치는 두 가지 방법
- merge
	- 히스토리를 남긴다.
	- 브랜치의 사용 내역들을 남겨둘 필요가 있다면 merge
- rebase
	- 깔끔하게 뒤에 최신커밋 뒤에 붙기 때문에 히스토리가 따로 남지 않는다.
	- 이미 팀원들과 공유된 커밋들에 대해서는 rebase를 사용하지 않는게 좋다.

## branch 합치기 실습
- rebase
	- rebase할 브랜치로 이동후 타겟에 리베이스를 해야한다.
	- merge와 반대
	- rebase를 했다고 해서 타겟이 그 커밋에 있는것이 아니다.
	- merge를 해주어야 한다.

## 충돌 해결하기
`git merge --abort`
- merge를 중단한다.
`git rebase --abort`
- rebase 중단

- 해결 가능시
	- 충돌 부분을 수정한 뒤 `git add .`
	- `git rebase --continue`
	- 충돌이 해결될때 까지 반복
- 충돌 해결에 타겟 브랜치를 선택하면 rebase가 의미가 없어져 커밋이 따로 추가되지 않는다.

## SourceTree로 진행해보기
- **rebase는 충돌 가능시 CLI로 진행 권장**

## Github은 뭐고 왜 쓰나요?

## 원격 저장소 사용하기
- `git remote add origin (원격 저장소 주소)`
- `git branch -M main`
- `git push -u origin main`
- `git clone (원격 저장소 주소)`

## push와 pull
- `git push`
- `git pull`
- `git pull --no-rebase`
	- merge
- `git pull --rebase`
	- pull 상의 rebase는 다름(협업시 사용 OK)
- 협업때 rebase를 사용하지 말라는 이유는
	- 이미 공유된 사항들을 rebase해서 위에 올리지 말라는 것
- pull 상황에 rebase는 상관없음
- `git push --force`
	- 협업시 위험하다

## 원격의 브랜치 다루기
- `git push --set-upstream origin from-local`
	- `git push -u origin from-local`
		- -u 로 축약가능
- `git branch --all` or `git branch -a`
	- 원격저장소 branch까지 확인한다.
- `git fetch`
	- 원격의 변경사항 확인
- `git switch -t origin/from-remote`
	- local의 from-remote와 연결하겠다는 의미
- `git push (원격이름) --delete (원격의 브랜치명)`
	- 원격 브랜치 삭제

## Git을 특별하게 만드는것
- Snapshot
- 분산 버전 관리

## Git의 3가지 공간
- Working directory
	- untracked
		- gitignore된 파일
		- Add된 적 없는 파일
	- tracked
- Staging area
	- 커밋을 위한 준비 단계
- Repository
	- 커밋된 상태

- `git rm <파일명>`
	- 삭제와 동시에 staging area 로 add된다.
- `git mv <변경전 파일> <변경할 파일>`
	- 이름 변경뒤 바로 add가 된다.
- `git restore --staged <파일명>`
	- --staged를 빼면 working directory에서도 제거
	- staging area에서 제거한다. 변경 사항은 유지
- rest의 세가지 옵션
	- --soft
		- repository에서만 제거하고 staging area에 남겨둔다.
		- add가 된 상태를 유지한다.
	- --mixed
		- 변화를 working directory에는 남겨둔다.
		- staging area에서 제거된다.
	- --hard
		- 수정사항 완전히 삭제
		- working directory에서 까지 날려버린다.