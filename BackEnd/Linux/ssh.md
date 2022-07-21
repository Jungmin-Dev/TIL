<h1>ssh 인증서 적용하기(http -> https)</h1>

<h3>1. EPEL 다운로드 </h3>

 - EPEL은 Extra Packages for Enterprise Linux 의 약자로 RHEL/CentOS 에 포함되지 않은 여러 패키지들을 설치할 수 있는 community 기반의 저장소

`yum install epel-release -y`

<h3>2. snapd 설치</h3>

`yum install snapd`

<h3>3. core 설치</h3>

`snap install core`

 - 이미 설치 되어있는 경우 최신버전인지 확인

`sudo snap install core; sudo snap refresh core`

<h3>4. certbot-auto 및 모든 Certbot OS 패키지 제거</h3>

`sudo yum remove certbot`

 - 에러 발생 시 실행

`ln -s /var/lib/snapd/snap /snap`

<h3>5. cerbot 설치</h3>

`snap install --classic certbot`

- cerbot 명령 준비

`sudo ln -s /snap/bin/certbot /usr/bin/certbot`

<h3>6. nginx ssl 적용</h3>

 - Certbot 실행 방법 선택(둘 중 하나)

`sudo certbot --nginx`

`sudo certbot certonly --nginx`

- 첫 번째 방식이 간단하게 설정되므로 선택했다.

 - 명령 실행 후 작성 및 확인사항

-> 이메일 작성 <br>
-> https 서버 선택<br>
-> fullchain.pem, privkey.pem 경로 확인해두기<br>


<h3>7. tomcat ssl 적용</h3>

- ssl 경로 /etc/letsencrypt/live/uni-core-test.kro.kr/

- server.xml 수정

`vi /home/oracle/tool/tomcat8/conf/server.xml`

- 실행 후 아래내용 추가

```
<Connector port="443" protocol="org.apache.coyote.http11.Http11NioProtocol"
               maxThreads="150" SSLEnabled="true" >
        <UpgradeProtocol className="org.apache.coyote.http2.Http2Protocol" />
        <SSLHostConfig>
            <Certificate certificateKeyFile="/etc/letsencrypt/live/YOUR_WEBSITE_HERE/privkey.pem"
                         certificateFile="/etc/letsencrypt/live/YOUR_WEBSITE_HERE/cert.pem"
                         certificateChainFile="/etc/letsencrypt/live/YOUR_WEBSITE_HERE/chain.pem"
                         type="RSA" />
        </SSLHostConfig>
    </Connector>
```

- web.xml 수정

`vi /home/oracle/tool/tomcat8/conf/web.xml`

- 리다이렉트 설정
```
...
<security-constraint>
<web-resource-collection>
<web-resource-name>SSL Forward</web-resource-name>
<url-pattern>/*</url-pattern>
</web-resource-collection>
<user-data-constraint>
<transport-guarantee>CONFIDENTIAL</transport-guarantee>
</user-data-constraint>
</security-constraint>
...
```

- /images/*, /css/* 리소스는 http 또는 https 모두에서 처리 설정

```
<security-constraint>    
<web-resource-collection>        
<web-resource-name>HTTPS or HTTP</web-resource-name>       
<url-pattern>/images/*</url-pattern>        
<url-pattern>/css/*</url-pattern>    
</web-resource-collection>    
<user-data-constraint>       
<transport-guarantee>NONE</transport-guarantee>   
</user-data-constraint></security-constraint>
```

<h3>8. 포트 설정</h3>

`firewall-cmd --permanent --zone=public --add-port=443/tcp`

`iptables -I INPUT 1 -p tcp --dport 443 -j ACCEPT`

`iptables -I OUTPUT 1 -p tcp --dport 443 -j ACCEPT`

`firewall-cmd --permanent --zone=public --add-port=8443/tcp`

`iptables -I INPUT 1 -p tcp --dport 8443 -j ACCEPT`

`iptables -I OUTPUT 1 -p tcp --dport 8443 -j ACCEPT`

<h3>9. 인증서 자동 갱신</h3>

 - Crontab 보기
`sudo crontab -l`

 - Crontab 편집
`sudo crontab -e`

 - crontab 명령어 규칙

![image](https://user-images.githubusercontent.com/74536458/180174472-0249b1e2-d09a-4a71-ba82-00548e2e0bdc.png)

 - 매월 1일 03시에 인증서를 갱신하는 명령어

`0 18 1 * * /usr/bin/certbot renew --renew-hook="sudo systemctl restart apache2"`

<br>
<br>
출처 : https://devlog.jwgo.kr/2019/04/16/how-to-lets-encrypt-ssl-renew/
