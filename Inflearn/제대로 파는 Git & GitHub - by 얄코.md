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

## HEAD
- `git checkout HEAD^`
	- ^ or ~
		- 갯수만큼 이전이전 으로 이동
- `git checkout -`
	- 한 단계 되돌리기
- `git reset HEAD(원하는단계) (옵션)`

## fetch와 pull
- fetch
	- 원격 저장소의 최신 커밋을 로컬로 가져오기만 한다.
	- `git switch origin/(브랜치명)`으로 이동해서 변경된 코드 확인
	- 그후에 `git pull`을 진행한다.
- pull
	- 원격 저장소의 최신 커밋을 로컬로 가져와 merge 또는 rebase
- `git checkout origin/(브랜치명)`
- `git switch -t origin/(브랜치명)`

## Help와 문서 활용하기
- `git (명령어) -h`
	- 해당 명령어의 설명과 옵션보기
- `git help (명령어)`
	- 웹사이트를 열어주지만 안열어주는 버전도 존재
- `git (명령어) --help`
	- 위와 같은 역할을 한다.

## Git의 각종 설정
- global 설정과 local 설정
- `git config (global) --list`
	- 현재 모든 설정값 보기
- `git config (global) -e`
	- 에디터로 열지만 설정없이는 vim으로 제공
- `git config --global core.editor "code --wait"`
	- - 또는 `code` 자리에 원하는 편집 프로그램의 .exe파일 경로 연결
	- `--wait` : 에디터에서 수정하는 동안 CLI를 정지
	- 💡 `git commit` 등의 편집도 지정된 에디터에서 열게 됨
- `git config --global core.autocrlf (윈도우: true / 맥: input)`
	- 줄바꿈 호환 문제 해결
- `git config pull.rebase (false or true)`
	- pull 기본전략
- `git config --global init.defaultBranch main`
	- 기본 브랜치명
- `git config --global push.default current`
	- push시 로컬과 동일한 브랜치명으로
- `git config --global alias.(단축키) "명령어"`

## 어떻게 커밋하는게 좋을까요?
- 한단위의 작업은 커밋하나에 담기는 것이 좋다.
- 커밋 메시지의 컨벤션

### Type

| 타입       | 설명                           |
| -------- | ---------------------------- |
| feat     | 새로운 기능 추가                    |
| fix      | 버그 수정                        |
| docs     | 문서 수정                        |
| style    | 공백, 세미콜론 등 스타일 수정            |
| refactor | 코드 리팩토링                      |
| perf     | 성능 개선                        |
| test     | 테스트 추가                       |
| chore    | 빌드 과정 또는 보조 기능(문서 생성기능 등) 수정 |
### Subject
- 커밋의 작업 내용 간략히 설명

### Body
- 길게 설명할 필요가 있을 시 작성

### Footer
- Braking Point 가 있을 때
- 특정 이슈에 대한 해결 작업일 때

```git
type : subject

body (optional)

footer (optional)
```

## 보다 세심하게 스테이징하고 커밋하기
- `git add -p`
	- hunk별 스테이징 진행
- editor를 사용하면 `git commit`이 editor 편집기에 나타나서 진행할수 있게 된다.
- `git commit -v`
	- 커밋에 반영될것들이 editor에 나오게 된다.
- `git diff --staged`
	- 이번 커밋에 담길 변경사항들을 볼수 있다.

## 커밋하기 애매한 변화 치워두기
- stash
	- 잠시 다른 공간에 치워둘수 있다.
- `git stash`
- `git stash pop`
	- 원하는 시점, 브랜치에서 다시 적용
- `git stash -p`
	- 원하는 작업만 stash가 가능하다.
- `git stash -m '(메시지)'`
- `git stash list`
	- stash 리스트를 볼수 있다.
- `git stash apply (stash list에 있는 넘버)`
	- 적용한다. 커밋이 아니다
- `git stash drop (stash list에 있는 넘버)`
	- 삭제
- `git stash pop (stash list에 있는 넘버)`
	- apply와 drop을 동시에

|명령어|설명|비고|
|:--|:--|:--|
|git stash|현 작업들 치워두기|끝에 save 생략|
|git stash apply|치워둔 마지막 항목(번호 없을 시) 적용|끝에 번호로 항목 지정 가능|
|git stash drop|치워둔 마지막 항목(번호 없을 시) 삭제|끝에 번호로 항목 지정 가능|
|git stash pop|치워둔 마지막 항목(번호 없을 시) 적용 및 삭제|apply + drop|
|💡 git stash branch (브랜치명)|새 브랜치를 생성하여 pop|충돌사항이 있는 상황 등에 유용|
|git stash clear|치워둔 모든 항목들 비우기|

## 커밋 수정하기
- `git commit --amend`
	- 커밋 메시지 변경
	- `git add (파일)` 을 한 파일도 함께 커밋된다.
- `git commit --amend -m (메시지)`
	- 한번에 처리할수 있다.
- `git commit -a --amend -m (메시지)`
	- git add 까지 하고 처리 한다.

## 과거의 커밋들을 수정, 삭제, 병합, 분할하기
- `git rebase -i (커밋 ID)`
- `git rebase --abort`
	- rebase 중지
- `git rebase --continue`

|명령어|설명|
|:--|:--|
|p, pick|커밋 그대로 두기|
|r, reword|커밋 메시지 변경|
|e, edit|수정을 위해 정지|
|d, drop|커밋 삭제|
|s, squash|이전 커밋에 합치기|

## 취소와 되돌리기 보다 깊이 알기

`git clean`
- Git에서 추적하지 않는 파일들 삭제

|옵션|설명|
|:--|:--|
|-n|삭제될 파일들 보여주기|
|-i|인터렉티브 모드 시작|
|-d|폴더 포함|
|-f|강제로 바로 지워버리기|
|-x|⚠️ `.gitignore`에 등록된 파일들도 삭제|
- 흔히 쓰이는 조합
	- `git clean -df`

## 커밋하지 않은 변경사항 되돌리기
`git restore (파일명)`
- 워킹 디렉토리의 특정 파일 복구
- 파일명 자리에 . : 모든 파일 복구

`git resotre --staged (파일명)`
- 변경상태를 스테이지에서 워킹 디렉토리로 돌려놓기

`git restore --source=(헤드 또는 커밋 해시) 파일명`
- 파일을 특정 커밋의 상태로 되돌리기

## reset했어도 희망은 있다!
`git reflog`

## 커밋에 태그 달기

### Git의 Tag
- 특정 시점을 키워드로 저장하고 싶을 때
- 커밋에 버전 정보를 붙이고자 할 때
[Sementic Versioning](https://semver.org/lang/ko/)

|태그 종류|설명|
|:--|:--|
|lightweight|특정 커밋을 가리키는 용도|
|annotated|작성자 정보와 날짜, 메시지, GPG 서명 포함 가능|
`git tag v2.0.0`
	마지막 커밋에 태그 달기(lightweight)

`git show (태그명)`
	태그명을 확인

`git tag -a (태그명)`
	annotated로 작성
`git tag (태그명) -m 메시지`
	-m은 -a를 사용한다는 의미도 포함된다.
`git tag -l 'v1.*'`
	원하는 패턴으로 필터링 하기
`git checkout v1.2.1`
	원하는 버전으로 체크아웃

## 원격의 태그 관리
`git push (원격명) (태그명)`
	특정 태그 원격에 올리기
`git push --delete (원격명) (태그명)`
	특정 태그 원격에서 삭제
`git push --tags`
	로컬의 모든 태그 원격에 올리기

## Fastforward vs 3-way merge

### Fastforward
- 병합할때 해당 브랜치를 그대로 병합한 커밋으로 이동시킨다.
- 기록이 남지 않는 단점이 있다.
- `git merge --no-ff (병합할 브랜치명)`
### 3-way merge
- 각각의 브랜치가 커밋을 가지고 있는 상황에서 사용된다.

## 다른 브랜치에서 원하는 커밋만 따오기

`git cherry-pick (커밋해시)`
	커밋해시를 해당 브랜치로 가져온다.

## 다른 가지의 잔가지만 가져오기
`git rebase --onto (도착 브랜치) (출발 브랜치) (이동할 브랜치)`

## 다른 가지의 마디들 묶어서 가져오기
`git merge --squash (대상 브랜치)`
	변경사항들 스테이지 되어 있다

## 협업을 위한 브랜치 활용법
### Gitflow
	협업을 위한 브랜칭 전략
[참고](https://nvie.com/posts/a-successful-git-branching-model/)

### 사용되는 브랜치들

|브랜치|용도|
|:--|:--|
|main|제품 출시/배포|
|develop|다음 출시/배포를 위한 개발 진행|
|release|출시/배포 전 테스트 진행(QA)|
|feature|기능 개발|
|hotfix|긴급한 버그 수정|
## [log 더 자세히 알아보기](https://yalco.kr/@git-github-dive/11-1/)
`git log -p`
	각 커밋마다의 변경사항 함께보기
`git log -(갯수)`
	최근 n개 커밋만 보기

## [차이 살펴보기](https://www.yalco.kr/@git-github-dive/11-2/)
`git diff`

## [누가 코딩했는지 알아내기](https://www.yalco.kr/@git-github-dive/11-3/)
`git blame`

## [오류가 발생한 시점 찾아내기](https://www.yalco.kr/@git-github-dive/11-4/)
`git bisect`
	이진 탐색 알고리즘으로 문제의 발생 시점을 찾아냅니다.

## Git Hooks

### Git Hooks
Git상의 이벤트마다 자동으로 실행될 스크립트를 지정합니다.

#### .git/hooks
- pre-commit
	- 커밋이 이뤄지기 전
- pre-push
	- 푸시가 이뤄지기 전

## Git Submodules

### 서브모듈
프로젝트 폴더 안에 또 다른 프로젝트가 포함될 때 사용
여러 프로젝트에 사용되는 공통모듈일 때 유용하다

`git submodule add (submodule의 github 레포지토리 주소) (하위폴더명, 없을 시 생략)`

submodule이 생기지만 가지고 있는 곳에서 수정을 하던 실제로 프로젝트 내에서 수정을 하던 해당 submodule에서 commit push를 해야 main project에도 commit하고 push해 적용할 수 있다.

git clone 으로 프로젝트를 받아오면 submodule은 존재하지만 안에 내용이 없다

`git submodule init`을 하고
`git submodule update`를 하면 submodule도 클론이 된다

`git submodule update --remote` 로 원격저장소의 변경사항을 적용한다

## 프로젝트와 폴더에 대한 문서
### READ.md

[Markdown Guide](https://www.markdownguide.org/cheat-sheet/)

## 풀 리퀘스트와 이슈

## 오픈소스에 참여하기

### fork
레포지토리 전체를 복사하는 것

## GitHub에 블로그 만들기

### GitHub Pages 사용하기
[GitHub Pages](https://pages.github.com/)

## SSH로 접근하기

## GPG로 커밋에 사인하기