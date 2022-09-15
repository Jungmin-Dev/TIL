<h1>  moment </h1>

<h4> moment는 자바스크립트에서 거의 표준으로 사용되고 있는 날짜관련 라이브러리다. </h4>

<h3> moment 설치 </h3>

```
// Install NPM
$ npm install vue-moment --save
```

 1. import

```javascript
import Vue from 'vue'
import vueMoment from 'vue-moment'
Vue.use(vueMoment)
```
 
2. moment 사용법

- HTML부분에서 필터처럼 사용

```html
<p>등록일 : {{ createDate | moment('YYYY-MM-DD HH:mm:ss') }}</p>
<p>현재일 : {{ new Date() | moment('YYYY-MM-DD HH:mm:ss') }}</p>
```

- 결과값 : 등록일 : 2020-11-13 23:15:34
- 결과값 : 현재일 : 2020-11-13 23:15:34

<h3> 상대 시간 </h3>

- 지정된 시간으로 부터 상대적인 시간을 얻을 수 있다. 
- 지금(now) 시간으로 부터 someDate는 몇년 전일지 보여준다.

```html
copy html<span>{{ someDate | moment("from", "now") }}</span>
<span>{{ someDate | moment("from", "now", true) }}</span>
<span>{{ someDate | moment("from", "Jan. 11th, 2000", true) }}</span>
```

- 결과값 : 4 years ago   
- 결과값 : 4 years  --> true인 경우는 ago없이 값만 보여준다.
- 결과값 : 20 years --> Jan. 11th, 2000 으로 부터  someDate 의 상대적인 시간을 보여준다.

<h3> 달력형식 </h3>

- 특정 날짜에 따라 문자열로 날짜를 형식화하고 참조 날짜 및 옵션을 전달할 수도 있다.

``` html
copy html<span>{{ someDate | moment("calendar") }}</span>
```

- 결과값 : Last Monday 2:30 AM   

<h3> 시간 더하기 </h3>

- 기본 시간에 주어진 시간을 추가하여 원래 시간을 변경

``` html
copy html<span>{{ someDate | moment("add", "7 days") }}</span>
<span>{{ someDate | moment("add", "1 year, 3 months, 30 weeks, 10 days") }}</span>
```

- 결과값 : 2020-11-13 23:15:34  --> 7일이 추가된 시간
- 결과값 : 2020-11-13 23:15:34  --> 1년, 3개월, 30주, 10일이 추가된 시간  

<h3> 시간 빼기 </h3>

- 기본 시간에서 주어진 시간을 빼서 원래 시간을 변경

```html
copy html<span>{{ someDate | moment("subtract", "7 days") }}</span>
<span>{{ someDate | moment("subtract", "1 year, 3 months, 30 weeks, 10 days") }}</span>
```

- 결과값 : 2020-11-13 23:15:34  --> 7일을 뺀 시간
- 결과값 : 2020-11-13 23:15:34  --> 1년, 3개월, 30주, 10일을 뺸 시간

출처: https://ux.stories.pe.kr/188 [UX 공작소:티스토리]
