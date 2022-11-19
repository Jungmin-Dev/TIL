<h1> Git 명령어 </h1>

![image](https://user-images.githubusercontent.com/74536458/202854889-81960476-0027-4bbd-8fdb-e187ee8525e5.png)


## GitHub 원격저장소 연결

저장소 초기화<br>
저장소로 사용하고자 하는 **디렉토리**로 이동 <br>
↓
`git init`

관리할 파일 추가<br>
`git add [파일명]` `.`인자를 통하여 전체 파일을 추가할 수 있다.<br>

커밋<br>
`git commit -m "[메시지]"`<br>

깃허브 연결하기<br>
`git remote add origin [URL(GitHub 주소)]`<br>

remote 연결 확인<br>
`git remote get-url origin`<br>

로컬에 있는 내역을 GitHub 원격저장소로 전송<br>
`git push origin [브랜치명]`<br>

## Push/Pull

로컬에 있는 내역을 GitHub 원격저장소로 전송<br>
`git push origin [브랜치명]`

GitHub 원격저장소의 내역을 로컬로 가져옴<br>
`git pull origin [브랜치명]`

## Status

현재 상태 확인<br>
`git status`

## Commit

commit/commit 메시지 작성 <br>
`git commit -m "[메시지]"`

add/commit 메시지 작성<br>
`git commit -am "메시지"`<br>
`git add .`과 메시지 작성하는 것을 한번에 하는 명령어이다.


## .gitignore

![](https://velog.velcdn.com/images/kimjungmin96/post/fe70a8c3-c422-4b8f-9902-ce3278f11019/image.png)

<br>

`.gitignore 파일` 만들고 보안에 문제가 되는 파일을 작성하면 git에서 관리하지 않는다.

## Config
git 이름 설정<br>
`git config --global user.name "[이름]"`

git email 설정<br>
`git config --global user.email "[이메일]"`

환경설정 내역 수정<br>
`git config --global --edit`

한글깨짐 해결<br>
`set LC_ALL=ko_KR.UTF-8` 

## Log

로그 확인<br>
`git log`<br>

![](https://velog.velcdn.com/images/kimjungmin96/post/2fd51f2d-0e8c-4551-a6e9-e79d59f67a93/image.png)

간략한 로그 확인<br>
`git shortlog`<br>

![](https://velog.velcdn.com/images/kimjungmin96/post/79db937c-f36b-460f-95be-f22b05cea937/image.png)

## Reset/Revert

혼자 작업할 때 커밋 되돌리기 <br>
-> 실수한 내역을 삭제하고 되돌린다.<br>
`git reset [commit ID]`

협업시 커밋 되돌리기<br>
실수한 내역을 커밋하고 되돌린다.<br>
`git revert [commit ID]` <br>

-> `[commit ID]`에 HEAD~1을 작성하면 현재 커밋에서 1단계 전으로 되돌리기

## Branch

브랜치 생성<br>
`git branch [생성할 브랜치명]` <br>

현재 브랜치 확인<br>
`git branch`<br>

브랜치 삭제<br>
`git brach -D [브랜치명]`<br>

브랜치 변경<br>
`git checkout [브랜치명]`<br>

## Diff

바뀐부분 확인(추가 삭제된 사항 확인)<br>
`git diff` <br>

## Merge

소스코드 합치기<br>
`git merge [브랜치명]`<br>

현재 브랜치에서 `[브랜치명]`을 가져와 합친다.

## Stash

잠시 다른 브런치 이동하거나 브랜치 착각했을 때 유용<br>

임시 저장 <br>
`git stash`

임시 저장 리스트 확인<br>
`git stash list` 

임시 저장한 것 불러오기<br>
`git stash apply`

임시 저장 삭제<br>
`git stash drop`

임시저장 불러오면서 삭제<br>
`git stash pop`

## Cherry-pick

원하는 commit 가져오기<br>
`git cherry-pick [commit ID]`

## Tag

현재 커밋위치에 Tag 설정<br>
Reset/Revert/cherry-pick 등 명령어 사용할 때 `commit ID` 대신 태그 명으로 사용할 수 있다.<br>

`git tag [태그명(v1.0.0)]`

## Git fork

`git fork`를 사용하면 Git을 UI로 사용할 수 있어 사용하기 편리하다.<br>
관심이 있다면 해당 자료가 많으니 참고해서 사용하면 될 것 같다.

![](https://velog.velcdn.com/images/kimjungmin96/post/1681976d-fdef-4d00-8ffd-6b09f3a9c396/image.png)

## Tip

Git으로 협업하고 있다면 출근하자마자 사용하면 좋은 명령어가 있다.

현재 branch 확인<br>
`git branch`

팀원의 수정된 작업 반영<br>
`git pull origin master`

더 많은 명령어가 존재하지만 Flow를 잘 짜서 위 명령어들을 사용한다면 별문제 없이 사용할 수 있을 것이다.

출처 : 제로초 TV(Git 강좌)
https://www.youtube.com/channel/UCp-vBtwvBmDiGqjvLjChaJw
