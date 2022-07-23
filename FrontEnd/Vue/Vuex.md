<h1>Vuex</h1>
Vuex는 중앙 위치에서 상태를 저장하여 어떤 컴포넌트라도 쉽게 상호 작용할 수 있게 돕는 라이브러리다.
state  , mutations  , actions  , getter  4가지 형태로 관리가 되며 관리 포인트는  store 라 불린다.


<h2>State</h2>

Vue component에서는 원본 소스 역할인 data로 볼 수 있고, state는 mutation을 통해서만 변경이 가능하다.

<h2>Mutations</h2>

유일하게 state를 변경할 수 있는 방법이며 메서드와 유사하고, commit을 통해서만 호출 할 수 있으며 함수로 구현된다.

API를 통해 전달받은 데이터를 mutations에서 가공하여 state를 변경한다.

<h2>Actions</h2>

비동기 작업이 가능하고, mutation을 호출하기 위한 commit이 가능하다.

action은 dispatch를 통해 호출할 수 있다.

axios를 통한 api 호출과 그 결과에 대해 return을 하거나 mutation으로 commit하는 용도로 사용된다.

<h2>Getter</h2>
  
Vue componet의 computed처럼 계산된 속성이다.

state에 대해 연산을 하고 그 결과를 view에 바인딩 할 수 있다.

state의 변경 여부에 따라 view를 업데이트한다.

<h2>Vuex의 데이터 흐름</h2>

![](https://velog.velcdn.com/images/kimjungmin96/post/298cc207-23bf-433e-8de4-228e68b91697/image.png)

<center><h3>Vuex의 단방향 데이터 흐름</h3></center>

<h4>실행 순서</h4>

``` 
1. Vue Component에서 Dispatch([action method name])를 통해 action을 실행
(ex. 버튼클릭 이벤트발생 등등)

2. Action에서는 외부 Api를 호출하는 등 비동기 로직을 처리

3. 그 결과를 이용해 동기 로직인 Mutaions을 호출
 --> Commit([mutations method name])를 통해 Mutation을 실행

4. Mutation에서 State(data)를 변경

5. getter를 이용하여 다시 Compoent에 바인딩돼 화면을 갱신 
```

State(data)를 변경할 수 있는 것은 오로지 Mutations

이 안에서 filter, reduce 등 다양한 방법으로 데이터를 가공할 수 있다.

modules에서 각종 목적에 맞는 항목을 분리할 수 있다.
 

<h2>⚠️Vuex 정리⚠️</h2>

- Vuex는 Vue.js에서 사용하는 상태 관리 라이브러리
- 모든 데이터 통신을 한 곳에서 중앙 집중식으로 관리하는 패턴
- 모든 컴포넌트에서 state에 접근하거나 action을 실행할 수 있음
- 단순한 App에서 Vuex를 무작정 사용하는 것 보다 props&emit 또는 Event Bus를 사용하는 것이 좋음
그러나, 중대형 규모의 SPA를 구축하는 경우 Vuex를 통해 Vue컴포넌트 외부의 상태를 보다 잘 처리할 수 있음

<br>

출처 : https://bbosong-develop.tistory.com/3 - bbosong - tiStory <br>
출처 : https://velog.io/@yjyoo/vue.js-Vuex-%EC%A0%95%EB%A6%AC - yjyoo
