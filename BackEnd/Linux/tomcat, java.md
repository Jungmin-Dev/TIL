<h1> tomcat, Java 11 설치 </h1>

<h3>1. Java 11 다운로드 </h3>

- open jdk 11 설치

`yum install java-11-openjdk-devel.x86_64`

<h3>2. tomcat8.5 다운로드</h3>

- tomcat-8.5.27 설치

`wget http://archive.apache.org/dist/tomcat/tomcat-8/v8.5.27/bin/apache-tomcat-8.5.27.tar.gz`

 - 압축 풀기

`tar zxvf apache-tomcat-8.5.27.tar.gz`

 - 압축 해제한 톰캣 이동(이 글에서는 /home/oracle/tool/tomcat8로 이동한다.)

`mv apache-tomcat-8.5.27 /home/oracle/tool/tomcat8`


<h3>3. 환경변수 설정 </h3>

- JAVA 설치 경로는 /usr/lib/jvm/[자바버전] 의 경로확인

![image](https://user-images.githubusercontent.com/74536458/180166616-26ba321c-2bc3-41c8-9726-d0d962a0ddee.png)

`vi /etc/profile`

- 실행 후 아래 사항 추가

```
JAVA_HOME=/usr/lib/jvm/java-11-openjdk-11.0.11.0.9-1.el7_9.x86_64
CATALINA_HOME=/home/oracle/tool/tomcat8
CLASSPATH=$JAVA_HOME/jre/lib:$JAVA_HOME/lib/tools.jar:$CATALINA_HOME/lib-jsp-api.jar:$CATALINA_HOME/lib/servlet-api.jar
PATH=$PATH:$JAVA_HOME/bin:/bin:/sbin
export JAVA_HOME PATH CLASSPATH CATALINA_HOME
```

<h3>4. 소스 등록</h3>

`source /etc/profile`

<h3>5. server.xml 설정</h3>

`vi /home/oracle/tool/tomcat8/conf/server.xml`

 - 아래 설정에서 URIEncoding="UTF-8" 추가

```
...
<Connector port="8080" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8443"
           URIEncoding="UTF-8" />
...
```

<h3>6. 8080 포트 열기</h3>

`firewall-cmd --permanent --zone=public --add-port=8080/tcp`

`iptables -I INPUT 1 -p tcp --dport 8080 -j ACCEPT`

`iptables -I OUTPUT 1 -p tcp --dport 8080 -j ACCEPT`

<h3>7. systemctl 등록</h3>

`vi /etc/systemd/system/tomcat.service`

 - 아래 내용 추가하여 등록

```
[Unit]
Description=tomcat 8
After=network.target syslog.target

[Service]
Type=forking
Environment="CATALINA_HOME=/home/oracle/tool/tomcat8"
User=root
Group=root
ExecStart=/home/oracle/tool/tomcat8/bin/startup.sh
ExecStop=/home/oracle/tool/tomcat8/bin/shutdown.sh

[Install]
WantedBy=multi-user.target
```

<h3>8. 명령어 실행</h3>

`systemctl start tomcat`

`systemctl enable tomcat`

`systemctl status tomcat`
