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
