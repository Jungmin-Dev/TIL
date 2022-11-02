<h1> useMemo </h1>
- useMemo 를 사용하면 함수형 컴포넌트 내부에서 발생하는 연산을 최적화 할 수 있다. 
- 먼저 리스트에 숫자들을 추가하면 해당 숫자들의 평균을 나타내는 함수형 컴포넌트를 작성해보자.

```javascript

Average.js
import React, { useState } from 'react';

const getAverage = numbers => {
  console.log('평균값 계산중..');
  if (numbers.length === 0) return 0;
  const sum = numbers.reduce((a, b) => a + b);
  return sum / numbers.length;
};

const Average = () => {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState('');

  const onChange = e => {
    setNumber(e.target.value);
  };
  const onInsert = e => {
    const nextList = list.concat(parseInt(number));
    setList(nextList);
    setNumber('');
  };

  return (
    <div>
      <input value={number} onChange={onChange} />
      <button onClick={onInsert}>등록</button>
      <ul>
        {list.map((value, index) => (
          <li key={index}>{value}</li>
        ))}
      </ul>
      <div>
        <b>평균 값:</b> {getAverage(list)}
      </div>
    </div>
  );
};

export default Average;

```


그 다음엔, App 에서 이 컴포넌트를 렌더링한다.

```javascript

App.js
import React from 'react';
import Average from './Average';

const App = () => {
  return <Average />;
};

export default App;

```


![image](https://user-images.githubusercontent.com/74536458/199441862-7780734f-6ade-4eaf-87d1-18971ce65ce3.png)


- 평균 값은 잘 보여지고 있는데, 숫자를 등록할 때뿐만 아니라 인풋 내용이 수정 될 때도 getAverage 함수가 호출되고 있는것을 확인 할 수 있다. 

- `useMemo` Hook 을 사용하면 이러한 작업을 최적화 할 수 있다. 
- 렌더링 하는 과정에서 특정 값이 바뀌었을 때만 연산을 실행하고 만약에 원하는 값이 바뀐 것이 아니라면 이전에 연산했던 결과를 다시 사용하는 방식이다.


``` javascript

Average.js
import React, { useState, useMemo } from 'react';

const getAverage = numbers => {
  console.log('평균값 계산중..');
  if (numbers.length === 0) return 0;
  const sum = numbers.reduce((a, b) => a + b);
  return sum / numbers.length;
};

const Average = () => {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState('');

  const onChange = e => {
    setNumber(e.target.value);
  };
  const onInsert = e => {
    const nextList = list.concat(parseInt(number));
    setList(nextList);
    setNumber('');
  };

  const avg = useMemo(() => getAverage(list), [list]);

  return (
    <div>
      <input value={number} onChange={onChange} />
      <button onClick={onInsert}>등록</button>
      <ul>
        {list.map((value, index) => (
          <li key={index}>{value}</li>
        ))}
      </ul>
      <div>
        <b>평균 값:</b> {avg}
      </div>
    </div>
  );
};

export default Average;

```

- 이제는 list 배열의 내용이 바뀔 때에만 getAverage 함수가 호출된다.


출처 : https://velog.io/@velopert/react-hooks#1-usestate - [ 리액트의 Hooks 완벽 정복하기 ]
