<h1> 새로고침 시 Vuex 데이터 상태 유지 </h1>

- Vuex라는 상태관리 패턴을 사용한 페이지에선 새로고침을 하면 State에 저장해놓은 데이터가 초기화된다.

<h3> vuex-persistedstate ? </h3>

>vuex에 저장되는 값(State)들을 사용하는 웹 브라우저의 LocalStorage에 저장하여, 새로고침 시에도 해당 로컬스토리지의 값은 없어지지 않기 때문에 해당 값을 가져와 동기화시켜주는 역할을 한다.

<h4> 설치 </h4>

```npm install --save vuex-persistedstate```

<h4> 사용법 </h4>

``` javascript
// state가 저장된 파일에서 vuex-persistedstate를 import하여 사용한다.
import createPersistedState from 'vuex-persistedstate';

// Vuex.Store 내부에 추가한다.
// 세션에 저장하고 Content의 모듈에 대해서만 데이터 상태 유지한다.
  plugins: [
    createPersistedState({
      storage: window.sessionStorage,
// 전체 값을 저장 하려고 하면 아래 paths를 제거한다.
      paths: ['Content']
    })
  ]
```

위와 같이 설정을 해주었고 만약 createPersistedState에서 paths없이 단일로 작성한다면 모든 페이지의 데이터가 로컬 스토리지에 저장이 되기 떄문에 사용자가 여러 페이지를 넘나들 수 록 페이지가 느려지는 현상을 겪을 수 있다.

그렇기에 본인이 로컬스토리지에 저장하여 새로고침을 해도 날라기지 않기를 원하는 페이지에만 작성하기를 권장한다.

출처: https://jeongkyun-it.tistory.com/169 [나의 과거일지:티스토리]
