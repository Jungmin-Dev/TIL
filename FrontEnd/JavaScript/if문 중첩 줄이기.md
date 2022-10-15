## 순서

1. if문 다음에 나오는 공통된 절차를 각 분기점 내부에 넣는다.
2. 분기점에서 짧은 절차부터 실행하게 if 문을 작성한다.
3. 짧은 절차가 끝나면 return(함수 내부의 경우)이나 break(for 문 내부의 경우)로 중단한다.
4. else를 제거한다(이때 중첩 하나가 제거된다.)

## 예제
```javascript
function test(){
  let result ='';
  if(a){
    if(!b){
      result = 'c';
    }
  }
  else{
    result = 'a';
  }
  result += 'b';
  return result;
}
```
↓ 변경 후

```javascript
  let result = "";
  if (!a) {
    result = "a";
    result += "b";
    return result;
  }
  if (!b) {
    result = "c";
  }
  result += "b";
  return result;
}
```


출처 : 제로초 TV(자바스크립트 강좌)
https://www.youtube.com/channel/UCp-vBtwvBmDiGqjvLjChaJw
