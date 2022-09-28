<h1> http 헤더 </h1>

<h3> http 헤더 용도 </h3>

- HTTP 전송에 필요한 모든 부가정보
  - 예) 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언트, 서버 정보, 캐시 관리 정보...
- 표준 헤더가 너무 많음
  - https://en.wikipedia.org/wiki/List_of_HTTP_header_fields
- 필요시 임의의 헤더 추가 가능
  - helloworld: hihi

<h3> 표현(Representation) </h3>

<h4> Content-Type </h4> 

- 표현 데이터의 형식 설명
- 미디어 타입, 문자 인코딩
- 예)
  - text/html; charset=utf-8
  - application/json
  - image/png

<h4> Content-Encoding </h4>

- 표현 데이터 인코딩
- 표현 데이터를 압축하기 위해 사용
- 데이터를 전달하는 곳에서 압축 후 인코딩 헤더 추가
- 데이터를 읽는 쪽에서 인코딩 헤더의 정보로 압축 해제
- 예)
  - gzip
  - deflate
  - identity

<h4> Content-Language </h4>

- 표현 데이터의 자연 언어
- 표현 데이터의 자연 언어를 표현
- 예)
  - ko
  - en
  - en-US

<h4> Content-Length </h4>

- 표현 데이터의 길이
- 바이트 단위
- Transfer-Encoding(전송 코딩)을 사용하면 Content-Length를 사용하면 안됨


> 표현 헤더는 전송, 응답 둘다 사용

<h3> 협상 </h3>

- Accept: 클라이언트가 선호하는 미디어 타입 전달
- Accept-Charset: 클라이언트가 선호하는 문자 인코딩
- Accept-Encoding: 클라이언트가 선호하는 압축 인코딩
- Accept-Language: 클라이언트가 선호하는 자연 언어
- 협상 헤더는 요청시에만 사용


<h4> 우선순위 </h4>

- Quality Values(q) 값 사용
- 0~1, 클수록 높은 우선순위
- 생략하면 1
- Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
  - 1. ko-KR;q=1 (q생략)
  - 2. ko;q=0.9
  - 3. en-US;q=0.8
  - 4. en:q=0.7

- 구체적인 것이 우선한다.
- Accept: text/*, text/plain, text/plain;format=flowed, */*
  - 1. text/plain;format=flowed
  - 2. text/plain
  - 3. text/*
  - 4. */*

- 구체적인 것을 기준으로 미디어 타입을 맞춘다.
- Accept: text/*;q=0.3, text/html;q=0.7, text/html;level=1,
 text/html;level=2;q=0.4, */*;q=0.5

<h3> http 헤더 일반 정보 </h3>

<h4> From </h4>

- 유저 에이전트의 이메일 정보
- 일반적으로 잘 사용되지 않음
- 검색 엔진 같은 곳에서, 주로 사용
- 요청에서 사용

<h4> Referer </h4>

- 이전 웹 페이지 주소
- 현재 요청된 페이지의 이전 웹 페이지 주소
- A -> B로 이동하는 경우 B를 요청할 때 Referer: A 를 포함해서 요청
- Referer를 사용해서 유입 경로 분석 가능
- 요청에서 사용
- 참고: referer는 단어 referrer의 오타

<h4>User-Agent</h4>

- 유저 에이전트 애플리케이션 정보
- user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.183 Safari/537.36
- 클리이언트의 애플리케이션 정보(웹 브라우저 정보, 등등)
- 통계 정보
- 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능
- 요청에서 사용

<h4> Server </h4>

- 요청을 처리하는 ORIGIN 서버의 소프트웨어 정보
- Server: Apache/2.2.22 (Debian)
- server: nginx
- 응답에서 사용

<h4> Date </h4>

- 메시지가 발생한 날짜와 시간
- Date: Tue, 15 Nov 1994 08:12:31 GMT
- 응답에서 사용

<h3> http 헤더 특별한 정보 </h3>

<h4> Host </h4>

- 요청한 호스트 정보(도메인)
- 요청에서 사용
- **필수**
- 하나의 서버가 여러 도메인을 처리해야 할 때
- 하나의 IP 주소에 여러 도메인이 적용되어 있을 때

<h4> Location </h4>

- 페이지 리다이렉션
- 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동 (리다이렉트)
- 201 (Created): Location 값은 요청에 의해 생성된 리소스 URI
- 3xx (Redirection): Location 값은 요청을 자동으로 리디렉션하기 위한 대상 리소스를 가리킴

<h4> Allow </h4>

- 허용 가능한 HTTP 메서드
- 405 (Method Not Allowed) 에서 응답에 포함해야함
- Allow: GET, HEAD, PUT

<h4> Retry-After </h4>

- 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간
- 503 (Service Unavailable): 서비스가 언제까지 불능인지 알려줄 수 있음
- Retry-After: Fri, 31 Dec 1999 23:59:59 GMT (날짜 표기)
- Retry-After: 120 (초단위 표기)

<h3> 인증 </h3>

<h4> Authorization </h4>

- 클라이언트 인증 정보를 서버에 전달
- Authorization: Basic xxxxxxxxxxxxxxxx

<h4> WWW-Authenticate </h4>

- 리소스 접근시 필요한 인증 방법 정의
- 401 Unauthorized 응답과 함께 사용
- WWW-Authenticate: Newauth realm="apps", type=1, title="Login to \"apps\"", Basic realm="simple"
 


출처 : https://www.inflearn.com/users/@yh [인프런 - 김영한]
