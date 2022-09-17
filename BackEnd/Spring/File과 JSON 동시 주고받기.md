<h1> File과 JSON 동시 주고받기 </h1>

- file과 dto를 함께 전달 받으려면 @RequestPart라는 어노테이션을 사용하면 된다. (관련된 레퍼런스: https://emoney96.tistory.com/258) </h4>

```java
@RequestMapping(value="/insert", method = RequestMethod.POST)
public void insert(
   @RequestPart Info   info,
  @RequestPart MultipartFile multipartFile
) {
   System.out.println(info);
  System.out.println(multipartFile);
}
```

- JSON.stringify()만 적용하여 보낼경우 415 Unsupported Media Type Error가 발생한다. 정확히는 아래에 나와있는 `application/octet-stream` 녀석 때문이다.

`appication/octet-stream`

- 8비트 단위의 바이너리 데이터를 의미한다.

<h4> 위 같은 문제가 발생한 이유는 서버에서는 json 타입으로 info을 받는 것으로 정의했는데, 클라이언트에서 string으로 변환해서 보냈기 때문에 에러가 발생한 것이다. </h4>

<h3> 해결법 </h3>

- formdata에 append할 때 JSON.stringify로 생성한 문자열을 Blob으로 만들고 그 타입을 application/json으로 지정해주면 된다.

```javasciprt
// 415 Error
await formData.append('uploader', JSON.stringify(uploader));

// Good 😋
const uploaderString = JSON.stringify(uploader);
await formData.append('uploader', newBlob([uploaderString], {type: 'application/json'}));
```

출처 : https://velog.io/@huewilliams/%ED%8C%8C%EC%9D%BC%EA%B3%BC-JSON-%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%A5%BC-%EB%8F%99%EC%8B%9C%EC%97%90-%EB%B3%B4%EB%82%B4%EA%B8%B0-2%ED%8E%B8-feat.-React-Express-Spring 
<br>[2편 React, Express, Spring으로 File과 JSON 동시에 주고 받기]
