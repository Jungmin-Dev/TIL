<h1> profile의 차이점 </h1>

리눅스 시스템에 로그인 할 경우 바로 적용되는 파일이 있다. `/etc/profile` , `/.bash_profile` 등의 파일이 이런 파일이다.
이런 파일에 환경변수를 설정하고 root 또는 일반 사용자로 로그인 할 경우 설정한 환경변수가 리눅스 시스템에 적용이 된다. 

root 사용자의 경우 /root/.bash_profile
일반 사용자의 경우 /home/아이디/.bash_profile 

먼저 리눅스 시스템에 로그인하면 /etc/profile 파일이 먼저 적용이 됩니다. 이 파일은 모든 사용자에게 적용이 되는 파일이다.
그 후 root 사용자는 root 사용자의 홈 디렉토리에 존재하는 .bash_profile 이 적용 되고
일반 사용자는 일반 사용자의 홈 디렉토리에 존재하는 .bash_profile 이 적용이 된다.


/etc/profile 에는 시스템에 적용해야 할 전반적인 환경 설정을 하고 그 후
각각의 사용자에게 환경 설정을 적용하기 위해 각각의 사용자 홈 디렉토리에 존재하는 .bash_profile 에 환경 설정을 하면 된다


/etc/profile : 시스템 전역(모든사용자들)에 대한 환경설정파일
~/.bash_profile : 개인사용자들에 대한 환경설정 파일



출처: https://klero.tistory.com/entry/root-사용자와-일반-사용자에-존재하는-profile-파일-차이점 [Pororo:티스토리]

출처: https://itcoach.tistory.com/29
