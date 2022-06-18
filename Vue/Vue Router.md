<h1>Vue Router</h1>

- Vue에서 SPA(Single Page Application) 웹 페이지 변경/전환을 지원하는 라이브러리
- 페이지 변경을 위해서 DOM을 새로 갱신하는 것이 아닌 변경된 요소영역(컴포넌트)만 갱신

<h2>Vue Router 태그</h2>

```<router-link to="URL 값">```
- 페이지 이동 태그, HTML `<a>` 태그로 표시되어 클릭 시 URL 값으로 이동

``` vue
<div>
    <router-link to="/login">Login</router-link>
</div>
```

``` <router-view> ```

- 변경되는 URL에 따라 해당 컴포넌트를 표시해주는 영역

``` vue
<div>
  <router-view></router-view>
</div>
```

<h2>Vue Router 인스턴스</h2>

- Vue Router 기능은 Router인스턴스를 통해서 사용 가능

``` javascript
// Router 인스턴스 생성
var router = new VueRouter({
  mode: "history", // 기본 값은 Hash모드(history 모드를 사용하면 브라우저 히스토리 스택에 기록)
  routes: [    // 페이지의 라우팅 정보
  {
    path: "/login", // 페이지 URL
    component: LoginComponent, // 표시될 컴포넌트
    components: {},  // 컴포넌트 여러개(Named View) 일 경우
    children: [ ... ],   // 하위 라우팅 정보
    redirect: ..., // redirect 처리(url과 화면 모두 redirect 설정으로 표시)
    alias: ...    // url은 alias로 표시되지만 화면은 component의 화면 표시
  }
  ...
  ]
});
```

* Vue Router 4버전부터는 인스턴스를 호출하지 않고, createRouter()메서드를 사용해 라우터를 생성

``` javascript
const router = createRouter({
  history : createWebHistory(),
  routes : [ ... ]
});
```

<h2>Vue Router 샘플(.html)</h2>

``` vue
<body>
    <div id="app">
      <div>
        <!-- Router 링크 -->
        <router-link to="/login">Login</router-link>
        <router-link to="/main">Main</router-link>
      </div>
      <!-- URL에 따른 해당 컴포넌트가 표시되는 영역-->
      <router-view></router-view>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script src="https://unpkg.com/vue-router@3.5.3/dist/vue-router.js"></script>
    <script>
      var LoginComponent = {
        template: "<div>login</div>",
      };
      var MainComponent = {
        template: "<div>main</div>",
      };

      // Router 인스턴스 생성
      var router = new VueRouter({
        routes: [
          {
            path: "/login", // 페이지 URL
            component: LoginComponent, // 표시될 컴포넌트
          },
          {
            path: "/main", // 페이지 URL
            component: MainComponent, // 표시될 컴포넌트
          },
        ],
      });
      new Vue({
        el: "#app",
        router: router, // 라우터 등록
      });
    </script>
  </body>
  ```
  
Login, Main 컴포넌트를 생성 후 각 링크를 클릭할 때 마다 하단에 해당 컴포넌트 내용 화면 표시

![](https://velog.velcdn.com/images/kimjungmin96/post/aa348e07-f3b0-4cef-865b-0a9b526ede32/image.png)

<h2>Vue Router 구성</h2>

일반적으로 vue router 구성 시 npm을 통해 설치하고, SFC(싱글파일컴포넌트, .vue파일)에서 사용법은 아래와 같다

- vue router npm 설치

```npm install vue-router --save```

- 프로젝트 루트에 router/index.js 파일 생성 후 라우터 설정 추가

``` javascript
import Vue from 'vue'
import VueRouter from 'vue-router'

Vue.use(VueRouter)

const router = new VueRouter({
  mode: 'history',
  routes: [
      {
        path: "/login", // 페이지 URL
        component: LoginComponent, // 표시될 컴포넌트
      },
      {
        path: "/main", // 페이지 URL
        component: MainComponent, // 표시될 컴포넌트
      },
  ],
})
export default router
```
 
<h3>Vue Router 구성(Vue Router Plugin 사용)</h3>
Vue에서 router 구성 작업들의 편의를 위해 VueRouter Plugin(cli-plugin-router)을 제공한다

```
vue add router
```

위 명령어 하나면 입력하면 vue router 설치 및 기본 설정을 한번에 진행 할 수 있다. 진행되는 작업들은 아래와 같다

1. Vue router 설치
2. Vue Router 설정 파일 생성 (router/index.js 파일)
3. Vue Router 샘플 컴포넌트 생성(AboutView.vue, HomeView.vue)
4. App.vue에 Router 샘플 컴포넌트 실행을 위한 router-link, router-view 생성
5. main.js에 Vue Router 적용: .use(router)
 

설치 후 package.json파일을 보면 dependencies에 vue-router, devDependencies에 @vue/cli-plugin-router가 추가된 것을 볼 수 있다.

![](https://velog.velcdn.com/images/kimjungmin96/post/f6f1eb57-09dd-4416-be2a-cc7a53f306a0/image.png)


프로젝트 루트에 router/index.js 파일에는 기본 router 설정이 되어있고, 샘플을 위한 views/AboutView.vue, HomeView.vue 파일이 생성되어 있다.

![](https://velog.velcdn.com/images/kimjungmin96/post/5a633c40-0b5e-41b0-a5a0-8fda33716254/image.png)

App.vue파일의 template에 router-link, router-view 태그가 적용되어 있다.

![](https://velog.velcdn.com/images/kimjungmin96/post/e182d3bb-ba3e-4ab9-9cc6-63fe1ca44b23/image.png)

main.js파일에서도 router설정을 import하여 적용되어 있다.

![](https://velog.velcdn.com/images/kimjungmin96/post/c3f16a5f-9505-41c7-bda1-58e604e08f93/image.png)

어플리케이션을 npm run serve로 실행해서 접속해보면 router 적용 동작을 확일 할 수 있다.

![](https://velog.velcdn.com/images/kimjungmin96/post/08a44a82-284d-42f9-aff2-790ead956fbf/image.png)


<h2>Named View</h2>

페이지에서 여러 개의 컴포넌트를 동시에 표시하는 라우팅 방식

``` vue
<div>
  <router-view name="header"></router-view>
  <router-view></router-view>  <!-- name이 없는 경우 디폴트 -->
  <router-view name="footer"></router-view>
</div>
```

<h2>Named View 샘플</h2>

``` vue
<div id="app">
  <!-- URL에 따른 해당 컴포넌트가 표시되는 영역-->
  <router-view name="header"></router-view>
  <router-view></router-view>
  <router-view name="footer"></router-view>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script src="https://unpkg.com/vue-router@3.5.3/dist/vue-router.js"></script>
<script>
  var BodyComponent = {
    template: "<div>Body</div>",
  };
  var HeaderComponent = {
    template: "<div>Header</div>",
  };
  var FooterComponent = {
    template: "<div>Footer</div>",
  };

  // Router 인스턴스 생성
  var router = new VueRouter({
    routes: [
      {
        path: "/", // 페이지 URL
        components: {
          default: BodyComponent,
          header: HeaderComponent,
          footer: FooterComponent,
        },
      },
    ],
  });
  new Vue({
    router,
  }).$mount("#app"); // $mount()로 'el'속성과 동일한 기능
</script>
```

```<router-view name="...">```에 name 속성을 사용하여 해당하는 Router인스턴스의 'components' 속성의 key에 해당하는 컴포넌트가 화면에 표시된다

<br>
출처 : https://happy-jjang-a.tistory.com/119 - jjang-a 블로그
