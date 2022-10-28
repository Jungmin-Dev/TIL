<h1> useEffect </h1>

- useEffect 는 리액트 컴포넌트가 렌더링 될 때마다 특정 작업을 수행하도록 설정 할 수 있는 Hook 이다.
- 클래스형 컴포넌트의 componentDidMount 와 componentDidUpdate 를 합친 형태로 보아도 무방하다.

- 한번, 우리가 기존에 만들었던 Info 컴포넌트에 useEffect 를 적용해보자.

``` javascript

Info.js
import React, { useState, useEffect } from 'react';

const Info = () => {
  const [name, setName] = useState('');
  const [nickname, setNickname] = useState('');
  useEffect(() => {
    console.log('렌더링이 완료되었습니다!');
    console.log({
      name,
      nickname
    });
  });

  const onChangeName = e => {
    setName(e.target.value);
  };

  const onChangeNickname = e => {
    setNickname(e.target.value);
  };

  return (
    (...)
  );
};

export default Info;

```

<h3> 마운트 될 때만 실행하고 싶을 때 </h3>

- 만약 useEffect 에서 설정한 함수가 컴포넌트가 화면에 가장 처음 렌더링 될 때만 실행되고 업데이트 할 경우에는 실행 할 필요가 없는 경우엔 함수의 두번째 파라미터로 비어있는 배열을 넣어주면 된다..

```javascript

Info.js - useEffect
  useEffect(() => {
    console.log('마운트 될 때만 실행됩니다.');
  }, []);
  
```

<h3> 특정 값이 업데이트 될 때만 실행하고 싶을 때 </h3>

- useEffect 를 사용 할 때 특정 값이 변경이 될 때만 호출하게 하고 싶을 경우도 있다. 
- 클래스형 컴포넌트는 다음과 같이 작성한다.

```javascript
componentDidUpdate(prevProps, prevState) {
  if (prevProps.value !== this.props.value) {
    doSomething();  
  }
}
```

- useEffect 의 두번째 파라미터로 전달되는 배열 안에 검사하고 싶은 값을 넣어주면 위와 동일하다.

```javascript

Info.js - useEffect
  useEffect(() => {
    console.log(name);
  }, [name]);
  ```
  
- 배열 안에는 useState 를 통해 관리하고 있는 상태를 넣어줘도 되고, props 로 전달받은 값을 넣어주어도 된다.



<h3> 뒷정리 하기 </h3>

- useEffect 는 기본적으로 렌더링 되고난 직후마다 실행되며, 두번째 파라미터 배열에 무엇을 넣느냐에 따라 실행되는 조건이 달라진다.

- 만약 컴포넌트가 언마운트되기 전이나, 업데이트 되기 직전에 어떠한 작업을 수행하고 싶다면 useEffect 에서 뒷정리(cleanup) 함수를 반환해주면 된다.

```javascript

Info.js - useEffect
  useEffect(() => {
    console.log('effect');
    console.log(name);
    return () => {
      console.log('cleanup');
      console.log(name);
    };
  });
```

- App 컴포넌트에서 Info 컴포넌트의 가시성을 바꿀 수 있다. (useState 를 사용하여 상태를 관리)

```javascript

App.js
import React, { useState } from 'react';
import Info from './Info';

const App = () => {
  const [visible, setVisible] = useState(false);
  return (
    <div>
      <button
        onClick={() => {
          setVisible(!visible);
        }}
      >
        {visible ? '숨기기' : '보이기'}
      </button>
      <hr />
      {visible && <Info />}
    </div>
  );
};

export default App;

```

- 렌더링이 될 때마다 뒷정리 함수가 계속 보여지고 있는 것을 확인 할 수 있다. 그리고, 뒷정리 함수가 호출 될 때에는 업데이트 되기 직전의 값을 보여주고 있다.

- 만약에, 오직 언마운트 될 때만 뒷정리 함수를 호출하고 싶으면 useEffect 함수의 두번째 파라미터에 비어있는 배열을 넣으면 된다.

``` javascript
Info.js - useEffect
  useEffect(() => {
    console.log('effect');
    console.log(name);
    return () => {
      console.log('cleanup');
      console.log(name);
    };
  }, []);
  ```
