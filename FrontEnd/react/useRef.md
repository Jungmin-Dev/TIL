<h1> useRef </h1>

- useRef Hook 은 함수형 컴포넌트에서 ref 를 쉽게 사용 할 수 있게 해준다. 
- Average 컴포넌트에서 등록 버튼을 눌렀을 때 포커스가 인풋 쪽으로 넘어가도록 해보자.

```javascript

Average.js
import React, { useState, useMemo, useRef } from 'react';

const getAverage = numbers => {
  console.log('평균값 계산중..');
  if (numbers.length === 0) return 0;
  const sum = numbers.reduce((a, b) => a + b);
  return sum / numbers.length;
};

const Average = () => {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState('');
  const inputEl = useRef(null);

  const onChange = useCallback(e => {
    setNumber(e.target.value);
  }, []); // 컴포넌트가 처음 렌더링 될 때만 함수 생성
  const onInsert = useCallback(
    e => {
      const nextList = list.concat(parseInt(number));
      setList(nextList);
      setNumber('');
      inputEl.current.focus();
    },
    [number, list]
  ); // number 혹은 list 가 바뀌었을 때만 함수 생성


  const avg = useMemo(() => getAverage(list), [list]);

  return (
    <div>
      <input value={number} onChange={onChange} ref={inputEl} />
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

- useRef 를 사용하여 ref 를 설정하면, useRef 를 통해 만든 객체 안의 current 값이 실제 엘리먼트를 가르키게 됩니다

<h3> 로컬 변수 사용하기 </h3>

- 컴포넌트 로컬 변수를 사용해야 할 때도 useRef 를 활용 할 수 있다. 
- 로컬 변수는 렌더링이랑 관계 없이 바뀔 수 있는 값을 의미한다. 만약에 클래스 형태의 컴포넌트로 따지자면 다음과 같은 코드이다.

``` javascript
import React, { Component } from 'react';

class MyComponent extends Component {
  id = 1
  setId = (n) => {
    this.id = n;
  }
  printId = () => {
    console.log(this.id);
  }
  render() {
    return (
      <div>
        MyComponent
      </div>
    );
  }
}

export default MyComponent;
```

함수형 컴포넌트로 작성한다면 다음과 같이 할 수 있다.

```javascript
import React, { useRef } from 'react';

const RefSample = () => {
  const id = useRef(1);
  const setId = (n) => {
    id.current = n;
  }
  const printId = () => {
    console.log(id.current);
  }
  return (
    <div>
      refsample
    </div>
  );
};

export default RefSample;
```

- 주의 할 점은, 이렇게 넣는 ref 안의 값은 바뀌어도 컴포넌트가 렌더링 되지 않는다는 점 이다. 
- 렌더링과 관련 되지 않은 값을 관리 할 때만 이러한 방식으로 코드를 작성하면 된다.

출처 : https://velog.io/@velopert/react-hooks#1-usestate - [ 리액트의 Hooks 완벽 정복하기 ]
