<h1> Axios </h1>

<h3>npm 사용하기</h3>

`$ npm install axios`

<h3>bower 사용하기</h3>

`$ bower install axios`

<h3>yarn 사용하기</h3>

`$ yarn add axios`

<h3>jsDelivr CDN 사용하기</h3>

`<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>`

<h3>unpkg CDN 사용하기</h3>

`<script src="https://unpkg.com/axios/dist/axios.min.js"></script>`

## API
Hackers News API: 
https://github.com/tastejs/hacker-news-pwas/blob/master/docs/api.md

## API 호출 예제
Hackers News :
https://news.ycombinator.com/

Hackers News html, css의 일부를 작성하여 호출하는데 사용하였다.

`main.js`
```javascript
const baseUrl = "https://api.hnpwa.com/v0";

// html의 onClick 속성으로 menu값 할당한다.
const menuMoveEvent = (menu) => {
  let pagetop = document.querySelectorAll(".pagetop a");
  for (let item of pagetop) {
    if (menu.toLowerCase() === item.textContent.toLowerCase()) 
      api(menu);
  }
};

const api = (menu) => {
  axios
    .get(`${baseUrl}/${menu}/1.json`)
    .then(({ data }) => {
    console.log(data);
    })
    .catch((error) => {
      console.error(error);
    });
};
```

현재 `main.js`는 `https://api.hnpwa.com/v0/{menu}/1.json`과 같이 각 메뉴의 1번 API만 호출이 되는 소스코드이다.

위 소스를 참고하여 동적으로 호출하는 방법을 작성해보면 좋을 것 같다.

--

<h2> Axios Interceptors </h2>

- then 또는 catch로 처리되기 전에 요청과 응답을 가로챌수 있다.

```javascript
// 요청 인터셉터 추가하기
axios.interceptors.request.use(function (config) {
    // 요청이 전달되기 전에 작업 수행
    return config;
  }, function (error) {
    // 요청 오류가 있는 작업 수행
    return Promise.reject(error);
  });


// 응답 인터셉터 추가하기
axios.interceptors.response.use(function (response) {
    // 2xx 범위에 있는 상태 코드는 이 함수를 트리거 합니다.
    // 응답 데이터가 있는 작업 수행
    return response;
  }, function (error) {
    // 2xx 외의 범위에 있는 상태 코드는 이 함수를 트리거 합니다.
    // 응답 오류가 있는 작업 수행
    return Promise.reject(error);
  });
  
  ```
  
나중에 필요할때 인터셉터를 제거할 수 있다.

``` javascript
const myInterceptor = axios.interceptors.request.use(function () {/*...*/});
axios.interceptors.request.eject(myInterceptor);
```

커스텀 인스턴스에서도 인터셉터를 추가할 수 있다.

``` javascript
const instance = axios.create();
instance.interceptors.request.use(function () {/*...*/});
```
