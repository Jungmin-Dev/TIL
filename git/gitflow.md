<h1> Git branch 전략 </h1>

<h3> gitflow </h3>

- gitflow에는 5가지 브랜치가 존재

1. master : 기준이 되는 브랜치로 제품을 배포하는 브랜치
2. develop : 개발 브랜치로 개발자들이 이 브랜치를 기준으로 각자 작업한 기능들을 Merge
3. feature : 단위 기능을 개발하는 브랜치로 기능 개발이 완료되면 develop 브랜치에 Merge
4. release : 배포를 위해 master 브랜치로 보내기 전에 먼저 QA(품질검사)를 하기위한 브랜치
5. hotfix : master 브랜치로 배포를 했는데 버그가 생겼을 떄 긴급 수정하는 브랜치

<h4> master와 develop가 중요한 매인 브랜치이고 나머지는 필요에 의해서 운영하는 브랜치이다. </h4>

<hr>

<h3> gitflow 과정 </h3>

![image](https://user-images.githubusercontent.com/74536458/204782078-2a158474-04e5-4b80-9cf8-bc02b9a255c1.png)

- `master` 브랜치에서 `develop` 브랜치를 분기합니다.
- 개발자들은 `develop` 브랜치에 자유롭게 커밋을 합니다.
- 기능 구현이 있는 경우 `develop` 브랜치에서 `feature/*` 브랜치를 분기한다.
- 배포를 준비하기 위해 `develop` 브랜치에서 `release/*` 브랜치를 분기한다.
- 테스트를 진행하면서 발생하는 버그 수정은 `release/*` 브랜치에 직접 반영한다.
- 테스트가 완료되면 `release` 브랜치를 `master`와 `develop`에 `merge`한다.
- 긴급 수정할 경우 `hotfix/*` 브랜치를 분기하고 수정 후 `master`에 배포한다.

출처: https://techblog.woowahan.com/2553/ [우아한형제들 기술블로그 (우린 Git-flow를 사용하고 있어요)]
