<h1> useState </h1>

- useState 는 가장 기본적인 Hook 으로서, 함수형 컴포넌트에서도 가변적인 상태를 지니고 있다.

- src 디렉터리에 Counter.js 파일을 생성하고 다음 코드를 입력하여 Counter를 구현한다.

```javascript

Counter.js
import React, { useState } from 'react';

const Counter = () => {
  const [value, setValue] = useState(0);
  return (
    <div>
      <p>
        현재 카운터 값은 <b>{value}</b> 입니다.
      </p>
      <button onClick={() => setValue(value + 1)}>+1</button>
      <button onClick={() => setValue(value - 1)}>-1</button>
    </div>
  );
};

```

- useState 를 사용 할 땐 코드의 상단에서 import 구문을 통하여 불러오고, 다음과 같이 사용한다.

```javascript
const [value, setValue] = useState(0);
```

- 이 문법은 배열 비구조화 할당 문법이다. 다음 코드는 배열 비구조화 할당의 더 쉬운 예제이다.

```javascript
const array = ['dog', 'cat', 'sheep'];
const [first, second] = array;
console.log(first, second); // dog cat
```

- 이제 다시 useState Hook 을 이해 해보자면, 이 함수의 파라미터에는 상태의 기본값을 넣어준다. 현재 0 을 넣어줬는데, 결국 카운터의 기본값을 0 으로 설정하겠다는 의미이다. 
- 이 함수가 호출되고 나면 배열을 반환하는데 그 배열의 첫번째 원소는 상태 값이고, 두번째 원소는 상태를 설정하는 함수이다. 
- 이 함수에 파라미터를 넣어서 호출하게 되면 전달받은 파라미터로 값이 바뀌게 되고 컴포넌트는 정상적으로 리렌더링 된다.

``` javascript

App.js
import React from 'react';
import Counter from './Counter';

const App = () => {
  return <Counter />;
};

export default App;

```

<h2> useState 를 여러번 사용하기 </h2>

- 하나의 useState 함수는 하나의 상태 값만 관리를 할 수 있기 때문에 만약에 컴포넌트에서 관리해야 할 상태가 여러 개라면 useState 를 여러번 사용하면 된다.

- 이번에는 src 디렉터리에 Info.js 파일을 생성하여 다음 코드를 작성한다.

```javascript

Info.js
import React, { useState } from 'react';

const Info = () => {
  const [name, setName] = useState('');
  const [nickname, setNickname] = useState('');

  const onChangeName = e => {
    setName(e.target.value);
  };

  const onChangeNickname = e => {
    setNickname(e.target.value);
  };

  return (
    <div>
      <div>
        <input value={name} onChange={onChangeName} />
        <input value={nickname} onChange={onChangeNickname} />
      </div>
      <div>
        <div>
          <b>이름:</b> {name}
        </div>
        <div>
          <b>닉네임: </b>
          {nickname}
        </div>
      </div>
    </div>
  );
};

export default Info;
```

- 그 다음엔 App 컴포넌트에서 이 컴포넌트를 렌더링해보세요.

``` javascript

App.js
import React from 'react';
import Info from './Info';

const App = () => {
  return <Info />;
};

export default App;
```

출처 : https://velog.io/@velopert/react-hooks#1-usestate -  [ 리액트의 Hooks 완벽 정복하기 ]
