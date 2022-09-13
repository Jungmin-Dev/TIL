<h1> v-mask </h1>

<h3> v-mask 설치 </h3>

```
// Install NPM
npm install v-mask
```

<h3> v-mask </h3>

1. import

```javascript
import VueMask from 'v-mask'
Vue.use(VueMask);
```
 
2. v-mask 사용하기

```html
<v-text-field
  v-mask="'###-###-###'"
  :value="phoneValue" />
```
