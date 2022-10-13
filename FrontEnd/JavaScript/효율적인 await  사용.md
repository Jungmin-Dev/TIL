<h1> 효율적인 await  사용 </h1>

<h3> 비동기 처리 할 수 있는 부분은 한꺼번에 몰아서 처리하면 효율적으로 작업을 할 수 있다. </h3>

- delayP(3000) 과 delayP(6000)은 같이 처리해도 문제없다고 가정하여 예시를 작성한다.

``` javascript

function delayP(ms){
  return new Promise((resolve, reject) => {
    setTimeout(resolve, ms);
  });
};

async function a() {
  await delayP(3000); // 3초
  await delayP(6000); // 6초
  await delayP(9000); // 9초
} // 총 18초

// 
async function b() {

  const p1 = delayP(3000); // 3초
  const p2 = delayP(6000); // 6초
  await Promise.allSettled([p1, p2]);
  await delayP(9000); // 9초
} // 총 15초


```

- 위와 같이 같이 처리하면 걸리는 시간을 단축할 수 있다.

출처 : https://www.youtube.com/c/ZeroChoTV [ZeroCho Tv 강좌]
