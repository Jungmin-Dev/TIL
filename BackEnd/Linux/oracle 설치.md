<h1> Linux Oracle 11g xe 설치 </h1>

<h3>1. 11g xe Linux x64 버전 다운로드 </h3>

https://www.oracle.com/database/technologies/xe-prior-release-downloads.html

![image](https://user-images.githubusercontent.com/74536458/179701761-3b1f6847-8840-4ea1-9dee-7d3be0eaac89.png)

<h3>2. 다운로드 한 파일 Linux 로 이동(oracle-xe-11.2.0-1.0.x86_64.rpm.zip) </h3>

- 이번에는 winscp를 이용하여 Linux로 이동시켰지만, 다른 방법도 있으니 구글에 검색하면 잘 찾을 수 있을 것이다.

<h3>3. 압축 풀기</h3>

- 다운로드한 폴더로 이동한 후 `unzip oracle-xe-11.2.0-1.0.x86_64.rpm.zip` 를 실행하여 압축 푼다.(정상적으로 풀리면 아래와 같이 Disk1 폴더가 생긴다.)

![image](https://user-images.githubusercontent.com/74536458/179704917-9075daa3-4552-4a39-8025-671433d46977.png)
 
<h3> 4. 자동 설치 프로그램 실행(rpm)</h3>

- Disk1 폴더로 이동 후 `rpm -ivh oracle-xe-11.2.0-1.0.x86_64.rpm` 를 실행하여 설치를 시작한다.

![image](https://user-images.githubusercontent.com/74536458/179705371-99650e3e-3a17-4683-ba18-167ed6d607c5.png)

- 설치 완료 시 메시지는 아래와 같다

![image](https://user-images.githubusercontent.com/74536458/179705572-0b3f2497-e15c-4302-84a4-c70ce95338f1.png)

<h3> 5. 환경 설정 </h3>

- `/etc/init.d/oracle-xe  configure` 를 실행하고 환경 설정한다.

- 포트번호를 설정한다.(톰캣 8080을 사용할 것으로 기본값 8080 사용 - 다른 포트를 사용한다면 그 포트를 작성하고 Enter 누르면 된다.)

![image](https://user-images.githubusercontent.com/74536458/179705759-1ed4a28e-f68e-412a-8faf-903412a745b6.png)

- 데이터베이스 리스너를 위한 포트를 설정한다. (기본값 1521를 사용할 것이므로 Enter 누르면 된다.)

![image](https://user-images.githubusercontent.com/74536458/179706230-f576c472-cd76-4003-88eb-29558cd13b85.png)


- system계정의 비밀번호 설정이다. 

![image](https://user-images.githubusercontent.com/74536458/179706326-6e99d5d6-6025-401a-b356-059d285f2aaf.png)

- 오라클 자동 실행 설정한다. (기본값으로 설정했다.)

![image](https://user-images.githubusercontent.com/74536458/179706446-3b6c5b21-7ba9-4a52-9b54-d11871820495.png)


<h3> 6. 방화벽 및 환경변수 설정 </h3>

- 먼저 오라클 실행한다

`/etc/init.d/oracle-xe start`

![image](https://user-images.githubusercontent.com/74536458/179707160-ad539f40-822b-466c-af7c-4ae4c16158ff.png)

- 방화벽 설정한다.

```
firewall-cmd --permanent --add-port=1521/tcp

firewall-cmd --reload
```

- 환경변수 설정한다.

`vi /etc/profile`

- 맨 아래에 아래 코드 추가 후 저장

```
export ORACLE_HOME=/u01/app/oracle/product/11.2.0/xe
export ORACLE_SID=XE
export PATH=$ORACLE_HOME/bin:$PATH
```

- 환경변수 설정한 값 적용 시키고 재부팅 한다.

```
source /etc/profile -> systemctl reboot
```

<h3> 7. 설치 확인 </h3>

- `sqlplus` 실행하고 id : system, password 를 입력한다.

![image](https://user-images.githubusercontent.com/74536458/179708097-02095bbf-b220-4a64-9bcf-a199b9bd3656.png)

- 쿼리문이 정상적으로 출력된다면 정상적으로 설치가 완료된 것이다.

![image](https://user-images.githubusercontent.com/74536458/179708112-407c7260-3e42-4610-b750-42c1ac4be0b6.png)

<h3> 8. user 생성 및 권한 주기 </h3>

- sqlplus 를 실행 한 상태로 진행하였다. (아래 JUNGMIN 자리에 사용자명을 작성하면 된다.)

```
// 오라클 유저 생성
CREATE USER JUNGMIN IDENTIFIED BY 7587`

// 생성한 USER에 권한주기
GRANT CONNECT, RESOURCE, DBA TO JUNGMIN (모든 권한 주기).

// 오라클 유저 삭제
DROP USER JUNGMIN CASCADE;
```

- 좀 더 자세한 내용은 아래 출처를 들어가보면 확인 할 수 있다.

<br>
<br>
출처 : https://thinmug.tistory.com/21 - [리눅스] 오라클 Oracle 11g XE 설치.txt <br>
출처 : https://fordev.tistory.com/23 - 오라클 사용자 생성 및 권한주기
