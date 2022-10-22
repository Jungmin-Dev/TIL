## Promise
**Promise** 는 비동기 작업의 단위이다.

첫번째 인수는 **resolve**, 두번째 인수는 **reject** 받는다.
```javascript
const promise1 = new Promise((resolve, reject) => {
  // 비동기 작업
});
```
**resolve**를 호출하게 된다면 비동기 작업이 **정상적**으로 동작했다는 뜻이다. 
반대로, **reject**를 호출하게 된다면 비동기 작업이 **실패**했다는 뜻이다.


**then** 메소드는 해당 Promise 가 성공했을 때의 동작하고, 
**catch** 메소드는 해당 Promise 가 실패했을 때의 동작한다.
첫 번째 reject 혹은 resolve만 **유효**한다. 
(두 번째부터는 무시된다. 이미 해당 함수가 호출되었다면 throw 또한 무시된다.)
```javascript
// resolve 만 실행
const several1 = new Promise((resolve, reject) => {
  resolve();
  reject();
});
```
![](https://velog.velcdn.com/images/kimjungmin96/post/2469e5ca-fb41-4d24-bf48-9e460535c90e/image.png)
## 예제
```javascript
function startAsync(age) {
  return new Promise((resolve, reject) => {
    if (age > 20) resolve();
    else reject();
  });
}

setTimeout(() => {
  const promise1 = startAsync(25);
  promise1
    .then(() => {
      console.log("1 then!");
    })
    .catch(() => {
      console.log("1 catch!");
    });
  const promise2 = startAsync(15);
  promise2
    .then(() => {
      console.log("2 then!");
    })
    .catch(() => {
      console.log("2 catch!");
    });
}, 1000);

/* 결과
1 then!
2 catch!
*/
```

## async, await
async와 await는 기존의 비동기 처리 방식인 콜백 함수와 프로미스의 단점을 보완한 기법이다.

function 키워드 앞에 async, 비동기로 처리되는 부분 앞에 await 붙여주면 된다.

```javascript
// async을 지정해주면 Promise를 리턴하는 함수로 만들어준다.
async function p2(){
//리턴값은 Promise{<resolved>: "hello2"} 자동 resolve해준다는걸 알 수있다.
return 'hello2'; 
// reject는 throw 에러를 날리면 된다.
}
```
함수에 async만 붙이면 자동 Promise객체로 인식되고 return값은 resolve()값과 똑같다.
## 예제
```javascript
function delay() {
  return new Promise((resolve, reject) => {
    setTimeout(() => resolve(), 1000);
  });
}
async function getApple() {
  await delay();
  return "apple";
}
async function getBanana() {
  await delay();
  return "banana";
}
async function getFruites() {
  // 리턴값이 resolve()의 값이니까 대입 가능
  let a = await getApple();
  let b = await getBanana();
  console.log(`${a} and ${b}`);
}
getFruites(); // 결과 : apple and banana
```
위와 같이 async, await 사용하면 좀 더 편리하게 사용할 수 있다.
하지만, 위의 코드는 하나씩 await을 사용하여 2초를 기다려야한다.

**병렬** 처리를 하고싶다면 아래와 같이 처리하면 된다.
(병렬 처리하는 다른 좋은 방법을 아래에서 다룬다.)
```javascript
async function getFruites(){
  
 // async함수를 실행시킨다.(바로 실행)
let getApplePromise = getApple();
  
// 리턴으로 프로미스 객체로 감싸진 결과값을 받는다.
let getBananaPromise = getBanana(); 
  
// 리턴으로 받은 프로미스객체를 done(data)를 await으로 빼서 변수에 넣음
let a = await getApplePromise; 
let b = await getBananaPromise;
/* 
본래라면 1초+1초 를 기다려야 하는데, 위에서 1초 기다리는 함수를 한번에 불러왔기 때문에 
대충 1.001초만 기다리면 동기식으로 처리된다.
*/
console.log(`${a} and ${b}`);
}
```
## all, race
처리하고자 하는 프로미스들을 배열로 담아 **Promise.all**로 실행하면 위의 병렬처리 코드와 동일한 결과를 얻을 수 있다.
```javascript
function pickAllFruit(){
  return Promise.all([getApple(), gerBanana()])
  .then(fruits => fruits.join(' and '));
}
pickAllFruit().then(console.log); // 결과 : apple and banana
```
처리하고자 하는 프로미스들을 배열로 담아 **Promise.race**로 실행하면 위의 병렬 처리 코드중 **가장 빨리 응답받은 결과만** resolve한다.
```javascript
// 이 코드에서는 Banana의 delay를 2000으로 설정했다고 가정한다.
function pickOnlyOne(){
  return Promise.race([getApple(), gerBanana()]);
}
pickAllFruit().then(console.log); // 결과 : apple
```

## async / await의 예외 처리

리턴값이 Promise객체이니 잡는 방법도 Promise.catch() 방법과 똑같다.

```javascript
function p() {
  return new Promise((resolve, reject) => {
    reject("Error!!");
  }, 1000);
}

async function p2() {
  try {
    await p(); //Promise에서 reject가 될때까지 await한다.
  } catch (e) {
    console.error(e);
  }
};
p2();
```

출처: [JS] 📚 비동기처리 (async / await) 개념 & 문법 💯 정리
https://inpa.tistory.com/entry/JS-📚-비동기처리-async-await [👨‍💻 Dev Scroll]

출처: [Javascript] 비동기, Promise, async, await 확실하게 이해하기
https://elvanov.com/2597 - Under The Pencil

출처: 자바스크립트 13. 비동기의 꽃 JavaScript async 와 await 그리고 유용한 Promise APIs | 프론트엔드 개발자 입문편 (JavaScript ES6)
https://www.youtube.com/watch?v=aoQSOZfz3vQ - 드림코딩
