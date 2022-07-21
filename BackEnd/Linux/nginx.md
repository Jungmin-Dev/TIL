<h1> vue.js 빌드한 파일 배포 </h1>

<h3> vue.js 빌드</h3>

- npm 명령어를 통하여 build

`npm run build`

- dist 파일 생성되는 것을 확인할 수 있다.

<h3> repository 설정 </h3>

- 경로 이동

`cd /etc/yum.repos.d/`

`vi nginx.repo` 

- 실행 후 아래 내용 작성

```
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/7/$basearch/
gpgcheck=0
enabled=1
```

<h3>eginx 설치</h3>

`yum install nginx -y`

<h3>nginx 설정 변경</h3>

`vim /etc/nginx/conf.d/default.conf`

 - 실행 후 아래 내용 작성

```
server {
    listen      {포트번호} default_server;
    listen      [::]:{포트번호} default_server;
    server_name  _;

    location / {
        root #dist파일 경로
        index index.html index.htm;
    }
}
```

<h3>dist 파일 경로</h3>

- 아래 경로에 dist파일 이동

![image](https://user-images.githubusercontent.com/74536458/180177706-a97e4cf7-c735-4842-a959-3e809c171722.png)


<h3> ginx 실행 및 정지 </h3>

`systemctl enable nginx`

`systemctl start nginx`

`systemctl stop nginx`


