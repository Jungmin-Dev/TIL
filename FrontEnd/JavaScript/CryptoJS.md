<h1> CryptoJS </h1>

- CryptoJS 라이브러리를 사용하여 AES(Advanced Encryption Standard) 암복호화 예제를 구현

1. CryptoJS 설치

`$ npm install --save crypto-js`


2. AES를 사용하여 객체를 암호화하고 다시 복호화한 뒤 데이터를 비교 이때, 암복호화에 사용되는 키는 동일하며 실제로 AES를 사용할 때에는 키를 비밀로 유지

```javascript
var CryptoJS = require("crypto-js");

var secretKey = 'secret key';
var data = {
    username: 'Pierre-Emerick Aubameyang',
    age: 31
};
console.log('original:', data);

// encrypt
var encrypted = CryptoJS.AES.encrypt(JSON.stringify(data), secretKey).toString();
console.log('encrypt:', encrypted);

// decrypt
var bytes = CryptoJS.AES.decrypt(encrypted, secretKey);
var decrypted = JSON.parse(bytes.toString(CryptoJS.enc.Utf8));
console.log('decrypted:', data);
```

3. 실행 및 결과:
```javascript
original: { username: 'Pierre-Emerick Aubameyang', age: 31 }
encrypt: U2FsdGVkX187GNjaMrHiOvHXHjxEJnHN67ICG9gVqh0/us0FP6uugGEBCUJ28VRQakaVGy2YhydURaL9zgxoCoH24KSMv/JeKBSdbNge7Dc=
decrypted: { username: 'Pierre-Emerick Aubameyang', age: 31 }
```

출처 : https://daehopark.tistory.com/entry/NodeJS-CryptoJS-AES-%EC%95%94%EB%B3%B5%ED%98%B8%ED%99%94-%EC%98%88%EC%A0%9C [ [NodeJS] CryptoJS AES 암복호화 예제 ]
