<h1> SolidJS </h1>

 - SolidJS는 2021년 정식 출시한 오픈 소스 프론트엔드 웹 프레임워크이다.

<h3> 특징 </h3>

- React 에서 사용하는 JSX 문법을 사용하며, 가장 빠른 성능과 가장 정확한 반응성을 강점으로 내새우고 있어 혜성같이 등장하였지만 벌써 Cloudflare 및 Netify 등의 주요 클라우드 업체에서 주목받고 사용하고 있는 웹 프레임워크이다.
- Svelte와 같이 가상 DOM 을 사용하지 않는 라이브러리이다. 가상DOM 사용 및 미 사용의 차이, 장단점은 React 와 Svelte 각 문서에 설명된 바 있다.

<h3> 예시 </h3>

- 예를 들어, 두 개의 input 요소에서 숫자를 입력받고 그 숫자들을 더한 값을 출력해주도록 구현을 한다고 가정하자.

```javascript
React 구현 예제.
import React, { useState } from 'react';

export default () => {
  const [a, setA] = useState(1);
  const [b, setB] = useState(2);

  function handleChangeA(event) {
    setA(+event.target.value);
  }

  function handleChangeB(event) {
    setB(+event.target.value);
  }

  return (
    <>
      <input type="number" value={a} onChange={handleChangeA}/>
      <input type="number" value={b} onChange={handleChangeB}/>

      <p>{a} + {b} = {a + b}</p>
    </>
  );
};
```

``` javascript
그리고 본 문서인 SolidJS의 구현 예제. React 와 동일하게 JSX 문법으로 작성한다.
import { createSignal } from "solid-js";

export default () => {
  const [a, setA] = createSignal(1);
  const [b, setB] = createSignal(2);

  function handleChangeA(event) {
    setA(+event.target.value);
  }

  function handleChangeB(event) {
    setB(+event.target.value);
  }

  return (
    <>
      <input type="number" value={a} onChange={handleChangeA}/>
      <input type="number" value={b} onChange={handleChangeB}/>

      <p>{a} + {b} = {a + b}</p>
    </>
  );
};

```

- 사실 이렇게 보면 React 와는 달리 함수 차이 말고는 별다른 문법적 차이는 없어 보인다. JSX 문법을 사용하고, 패턴도 React 와 차이가 없다.
- 그러나, React와 달리 라이브러리의 진가는 2가지로 나오는데, 바로 속도와 번들링 사이즈다.
- 한 개발자가 같은 앱을 React 와 SolidJS로 구현하여 비교(영문)한 포스트 본문에서는,
- React 앱의 스크립트 읽기 속도 475ms, 렌더링 속도 129ms, 배포 번들 크기는 핵심과 앱 순으로 각 161KB, 5KB
- SolidJS 앱의 스크립트 읽기 속도 176ms, 렌더링 속도 79ms, 배포 번들 크기는 핵심과 앱 순으로 각 25KB, 5KB
- 앱 자체 크기의 차이는 유의미할 정도는 아니지만, 웹에서 구동할 핵심 라이브러리 크기부터 차이가 엄청나며, 게다가 **스크립트 읽기 속도에서 확실히 차이가 나며 렌더링 속도도 유의미하게 상승했음**을 도출했다.

출처 : https://namu.wiki/w/SolidJS - 나무위키
