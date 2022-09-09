<h1> catalina.out 날짜별 저장 </h1>

> vim /etc/logrotate.d/tomcat 후 아래 사항 추가

```
/home/unicore/tool/tomcat8/logs/catalina.out {
        copytruncate
        daily
        rotate 365
        compress
        missingok
        notifempty
        dateext
}
```

<h3> 해당 옵션 설명 </h3>

```
 /usr/local/apache-tomcat-7.0.92/logs/catalina.out {
 su root root    
 copytruncate    //기존 파일 백업후 다른파일로 이동. 기존파일은 삭제    
 daily           //로그 파일을 날짜별로 저장
 rotate 30       //30개만큼 저장후 제거    
 compress        //로그파일들은 gzip 으로 압축    
 missingok       //로그파일이 없더라고 오류 발생 안함    
 notifempty      //파일내용이 없으면 새로운 로그 생성 안함    
 dateext         //순환된 로그파일의 날짜확장자}

```


<h3> crontab 설정 </h3> 

- crontab -e 입력 후 아래사항 추가(매 12시마다 실행)

`00 00 * * * logrotate -f /etc/logrotate.d/tomcat`

출처: https://trytoso.tistory.com/1301 [소행성왕자:티스토리]
