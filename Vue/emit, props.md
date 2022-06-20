<h1> props / event </h1>

- props는 아래로 전달 (데이터)

- event는 위로 전달 (이벤트)

<h2>(1) props </h2>

``` vue

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <!-- <app-header v-bind:프롭스 속성 이름="상위 컴포넌트의 데이터 이름"></app-header> -->
        <app-header v-bind:propsdata="message"></app-header>
        <app-content v-bind:propsdata2="num"></app-content>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        let appHeader = {            
            template: '<h1>{{propsdata}}</h1>',
            props: ['propsdata']
        }

        let appContent = {
            template: '<div>{{propsdata2}}</div>',
            props: ['propsdata2']
        }

        new Vue({
            el: '#app',
            components:{
                'app-header': appHeader,
                'app-content': appContent
            },
            data: {
                message: 'hi',
                num : 10
            }
        })
    </script>
</body>
</html>

```

- `root(#app)` 컴포넌트가 `<app-header>` 컴포넌트를 포함하고 있다.

- `root(#app)`의 data num과 message가 하위컴포넌트 태그`<app-header>`의 `v-bind:하위컴포넌트 변수="상위 컴포넌트 변수"`를 통해서 하위 컴포넌트에 전달된다. 

- 하위 컴포넌트에는 `props:[ '변수이름' ]`을 통해 받는 변수를 정의 해 놓는다. 

 

 

<h2> (2) event-emit </h2>

``` vue
  
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <p>{{num}}</p>
        <!-- <app-header v-on:하위 컴포넌트에서 발생한 이벤트 이름="상위 컴포넌트 메서드 이름"></app-header>-->
        <app-header v-on:pass="logText"></app-header>
        <app-content v-on:increase="addNum"></app-content>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        let appHeader = {
            template: '<button v-on:click="passEvent">click me</button>',
            methods:{
                passEvent: function(){
                    this.$emit('pass');
                }
            }
        }
        let appContent = {
            template: '<button v-on:click="addNumber">add</button>',
            methods:{
                addNumber: function(){
                    this.$emit('increase');
                }
            }
        }
        let vm = new Vue({
            el: '#app',
            components:{
                'app-header': appHeader,
                'app-content': appContent
            },
            methods:{
                logText: function(){
                    console.log('hi');
                },
                addNum: function(){
                    this.num = this.num + 1
                }
            },
            data: {
                num: 10
            }
        });
    </script>
</body>
</html>
  ```
  
  1. template에 `v-on:click="메소드이름"` 으로 클릭시 실행될 메소드 설정

  2. methods 속성에서 메소드 구현 내용 중 `this.$emit('pass')`를 통해  pass 이벤트를 보냄

  3. 하위 컴포넌트 태그에서 `v-on:이벤트이름="메소드이름"` 을 통해서 상위 컴포넌트에서 실행될 메소드를 정의

  4. 상위 컴포넌트인 root 컴포넌트 `let vm = new Vue()`의 methods 속성에서 메소드를 정의 한다.

cf) this.num 에서 this는 vm 이다. num이 data로 감싸져 있지만 실제로 console.log를 찍어보면 감싸고 있지 않고 vm 안에 바로 num 속성이 있다.
 
  
<h2>(3) 하위 컴포넌트끼리 주고 받는 경우</h2>

- 하위 컴포넌트`<app-content>`에서 상위컴포넌트 `<div id="app">`으로 보낸뒤 다시 `<app-header>`로 내려보낸다.
  
  <br>아래 코드 참고
  
``` vue
  
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <app-header v-bind:propsdata="num"></app-header>
        <app-content v-on:pass="deliverNum"></app-content>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        let appHeader = {
            template: '<div>header</div>',
            props: ['propsdata']            
        }
        let appContent = {
            template: '<div>content<button v-on:click="passNum">pass</button></div>',
            methods:{
                passNum: function(){
                    this.$emit('pass', 10);
                }
            }
        }

        new Vue({
            el: '#app',
            components:{
                'app-header': appHeader,
                'app-content': appContent
            },
            data: {
                num : 0
            },
            methods:{
                deliverNum: function(value){ // value는 하위컴포넌트에서 올라온값
                    this.num = value;
                }
            }
        })
    </script>    
</body>
</html>
  ```
  
  - `this.$emit('pass',10)` 에서 10의 값을 같이 올려보내면 `deliverNum(value)`가 실행될때 value에 10이 들어가게 된다.
