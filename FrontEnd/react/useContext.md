<h1> useContext </h1>

- 이 Hook 을 사용하면 함수형 컴포넌트에서 Context 를 보다 더 쉽게 사용 할 수 있다.

- src 디렉터리에 ContextSample.js 이라는 컴포넌트를 만들어 보자.

```javascript

ContextSample.js
import React, { createContext, useContext } from 'react';

const ThemeContext = createContext('black');
const ContextSample = () => {
  const theme = useContext(ThemeContext);
  const style = {
    width: '24px',
    height: '24px',
    background: theme
  };
  return <div style={style} />;
};

export default ContextSample;
```

- 다 만들었으면 App 컴포넌트에서 렌더링 해준다.

```javascript

App.js
import React from 'react';
import ContextSample from './ContextSample';

const App = () => {
  return <ContextSample />;
};

export default App;

```

다 작성하셨으면 브라우저를 확인해보보자. 검정색 사각형이 나타났다.

![image](https://user-images.githubusercontent.com/74536458/198812348-a8bd96a4-28fc-4deb-ae85-ad3a2bf9e7dd.png)


출처 : https://velog.io/@velopert/react-hooks#1-usestate -  [ 리액트의 Hooks 완벽 정복하기 ]
