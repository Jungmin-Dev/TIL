<h1>Robots.txt와 Sitemap.xml 제대로 설정하기</h1>

텍스트 파일 형식의 로봇 텍스트 파일(robots.txt)과 xml형식의 사이트맵 파일(sitemap.xml)은 사이트에 방문하는 검색엔진의 크롤러를 제어하기 위해 설정하는 파일이다.

<h2> Robots.txt란 무엇인가? </h2>
Robots.txt는 검색의 크롤링 로봇이 웹에 접근할 때 로봇이 지켜야하는 규칙과 사이트맵(sitemap.xml) 파일의 위치를 알려주는 역할을 하는 파일이다.<br>

 - robots.txt 파일은 모든 사람이 접근할 수 있기 때문에 보안의 수단으로 사용해선 안된다.

<h2>Sitemap.xml(사이트맵) 이란 무엇인가? </h2>
Sitemap.xml(사이트 맵)  파일은 검색 엔진 크롤링 로봇에게 웹 사이트에서 크롤링 해야 할 URL 을 전달한다.<br>
 - Sitemap 파일은 UTF-8로 인코딩되야한다.
<br>
<br>

Sitemap은 구글에 create sitemap 검색하여 url을 등록하면 자동으로 Sitemap을 생성해준다.(https://www.xml-sitemaps.com/)<br>

<br>

![image](https://user-images.githubusercontent.com/74536458/172032538-07bf1fdf-685c-4f82-a8e9-f69eb461bd9d.png)

<h3>자동 Sitemap 생성 파일</h3><br>

![image](https://user-images.githubusercontent.com/74536458/172032582-8f507440-6aa2-40f7-9443-fcdca61cc89c.png)

<h3> Robots.txt </h3>

 - User-agent: * 을 통하여 모든 검색로봇에 대한 접근을 허용하고, Allow를 통하여 크롤링을 허가한다. 그리고 Sitemap을 작성해준다.

![image](https://user-images.githubusercontent.com/74536458/172032749-ee1fd934-c6b7-45ae-96b7-9ee95b4fb335.png)



이렇게 설정을 하면 검색엔진에서 좀 더 검색이 잘 된다.
