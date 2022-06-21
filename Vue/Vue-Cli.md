<h1> Vue-cli </h2>
Vue 프로젝트를 손쉽게 만들 수 있도록 기본 vue 개발 환경을 설정해주는 도구이다.<br> 
vue-cli 가 기본적인 프로젝트 세팅을 해주기 때문에 폴더 구조에 대한 고민, lint, build, 어떤 라이브러리로 구성을 해야되는지 webpack 설정은 어떻게 해야되는지에 대한 고민을 덜을 수 있다.

<h2> cli란? </h2>
명령 줄 인터페이스(CLI, Command line interface) 또는 명령어 인터페이스는 텍스트 터미널을 통해 사용자와 컴퓨터가 상호 작용하는 방식을 뜻한다. 
<br>즉, 작업 명령은 사용자가 컴퓨터 키보드 등을 통해 문자열의 형태로 입력하며, 컴퓨터로부터의 출력 역시 문자열의 형태로 주어진다. (위키백과)

공식문서 : <a href="https://cli.vuejs.org/"> Vue-cli </a>

<h2> Vue-cli 설치하기 </h2>

-npm 또는 yarn이 설치되어 있어야한다.

```
npm install -g @vue/cli
# OR
yarn global add @vue/cli
```

- 설치 후 정상 설치 확인

```
vue --version
```

<h2> Vue-cli로 프로젝트 생성하기 </h2>

```
// vue create <프로젝트명>
vue create board
```

<h2> vue-cli로 만들어진 만들어진 프로젝트 구조</h2>

![vue-cli](https://user-images.githubusercontent.com/74536458/174766462-1507c1e2-92c1-4caf-821a-559604759065.png)


<br>
출처 : https://ocblog.tistory.com/63 - 마라톤 코딩<br>
출처 : https://simplevue.gitbook.io/intro/01.-vue-cli - simpleVue
