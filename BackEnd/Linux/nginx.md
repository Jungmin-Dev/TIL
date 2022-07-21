<h1> vue.js 빌드한 파일 배포하기 </h1>

<h2> vue.js 빌드하기 </h2>

- `npm run build`로 빌드 하면 dist 파일이 생성된다.


<h2> nginx 세팅 </h2>
<h3> repository 설정 </h3>
- 리눅스 서버에서 아래와 같이 경로 이동한다

`cd /etc/yum.repos.d/`

- `vi nginx.repo` 후 아래 내용 작성한다.
```
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/7/$basearch/
gpgcheck=0
enabled=1
```

- eginx 설치<br>

`yum install nginx -y`

- nginx 설정 변경<br>

`vim /etc/nginx/conf.d/default.conf`

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
 
<h2> ginx 실행 및 정지 </h2>

`systemctl enable nginx`

`systemctl start nginx`

`systemctl stop nginx`

