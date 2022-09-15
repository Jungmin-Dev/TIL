<h1>  vue-daum-postcode </h1>

<h4> vue-daum-postcode는 다음 우편 서비스이고, 주소 찾기 기능을 제공한다. </h4>

<h3> vue-daum-postcode 설치 </h3>

```
// Install NPM
npm i vue-daum-postcode --save
```

<h3> vue-daum-postcode </h3>

1. import

```javascript
import VueDaumPostcode from "vue-daum-postcode"
Vue.use(VueDaumPostcode)

```
 
2. vue-daum-postcode 사용

```html
<template>
  <section class="test">
    <div class="post-box" v-if="postOpen">
      <template>
        <VueDaumPostcode @complete="oncomplete" />
      </template>
    </div>
    <div class="form-box">
      <input disabled v-model="address">
      <div v-on:click="search">검색</div>
    </div>
  </section>
</template>

<script>

import { VueDaumPostcode } from "vue-daum-postcode"

export default {
  name: "test",
  data(){
    return{
      address: null,
      postOpen: false
    }
  },
  components: {
    VueDaumPostcode,
  },
  methods: {
    search:function(){
      this.postOpen = true
    },
    oncomplete:function(result){
      if(result.userSelectedType === 'R'){  // 도로명 주소 선택
        this.address = result.roadAddress;
      }else{  // 지번 주소 선택
        this.address = result.jibunAddress;
      }
      this.postOpen = false
    }
  }
}
</script>

<style scoped>
  .form-box{ position:relative; z-index: 1; width:100%; height:500px; display:flex; justify-content: center; align-items: center; flex-wrap: wrap; }
  .form-box input{ width:400px; height:50px; border:1px solid; border-radius: 3px; }
  .form-box div{ margin-left:50px; width:150px; height:50px; background-color: #5366cf; font-size:15px; color:white; display: flex; justify-content: center; align-items: center; cursor:pointer; }
  .post-box{ z-index: 2; position:absolute; top:0; left:0; right:0; bottom:0; width:100%; height:100%; }
</style>
```

출처 : https://yoyostudy.tistory.com/41 [[Vue js] Daum PostCode API 로 주소찾기]
