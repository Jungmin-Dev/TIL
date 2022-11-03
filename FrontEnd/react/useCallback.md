<h1> useCallback </h1>

- useCallback 은 useMemo와 상당히 비슷한 함수다. 
- 주로 렌더링 성능을 최적화해야 하는 상황에서 사용하는데, 이 Hook을 사용하면 이벤트 핸들러 함수를 필요할 때만 생성 할 수 있다.


```javascript

Average.js
import React, { useState, useMemo, useCallback } from 'react';

const getAverage = numbers => {
  console.log('평균값 계산중..');
  if (numbers.length === 0) return 0;
  const sum = numbers.reduce((a, b) => a + b);
  return sum / numbers.length;
};

const Average = () => {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState('');

  const onChange = useCallback(e => {
    setNumber(e.target.value);
  }, []); // 컴포넌트가 처음 렌더링 될 때만 함수 생성
  const onInsert = useCallback(
    e => {
      const nextList = list.concat(parseInt(number));
      setList(nextList);
      setNumber('');
    },
    [number, list]
  ); // number 혹은 list 가 바뀌었을 때만 함수 생성

  const avg = useMemo(() => getAverage(list), [list]);

  return (
    <div>
      <input value={number} onChange={onChange}  />
      <button onClick={onInsert}>등록</button>
      <ul>
        {list.map((value, index) => (
          <li key={index}>{value}</li>
        ))}
      </ul>
      <div>
        <b>평균값:</b> {avg}
      </div>
    </div>
  );
};

export default Average;
```

- useCallback 의 첫번째 파라미터에는 우리가 생성해주고 싶은 함수를 넣어주고, 두번째 파라미터에는 배열을 넣어주면 되는데 이 배열에는 어떤 값이 바뀌었을 때 함수를 새로 생성해주어야 하는지 명시해주어야 한다다.

- 만약에 onChange 처럼 비어있는 배열을 넣게 되면 컴포넌트가 렌더링 될 때 단 한번만 함수가 생성되며, onInsert 처럼 배열 안에 number 와 list 를 넣게 되면 인풋 내용이 바뀌거나 새로운 항목이 추가 될 때마다 함수가 생성된다.

- 참고로 다음 두 코드는 완벽히 똑같은 코드이다.


```javascript

useCallback(() => {
  console.log('hello world!');
}, [])

useMemo(() => {
  const fn = () => {
    console.log('hello world!');
  };
  return fn;
}, [])

```

- useCallback 은 결국 useMemo 에서 함수를 반환하는 상황에서 더 편하게 사용 할 수 있는 Hook 이다. 숫자, 문자열, 객체 처럼 일반 값을 재사용하기 위해서는 useMemo 를, 그리고 함수를 재사용 하기 위해서는 useCallback 을 사용하면 된다.

출처 : https://velog.io/@velopert/react-hooks#1-usestate - [ 리액트의 Hooks 완벽 정복하기 ]
