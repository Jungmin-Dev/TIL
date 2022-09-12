<h1>html 영역 이미지 복사</h1>

<h3> html2canvas 설치 </h3>

```
// Install NPM
npm install --save html2canvas
```

```
// Install Yarn
yarn add html2canvas
https://html2canvas.hertzen.com/
```
 

<h3> html2canvas 사용하기 </h3>

1. 사용할 페이지에 import 하기

```javascript
import html2canvas from "html2canvas"
```
 

2. 캡쳐할 html 가장 바깥쪽 element 에 ref 지정

```html
<div ref="chartcapture" ......  > .. <div/>
```

3. canvas를 캡쳐하는 이벤트를 실행할 버튼을 만든다
( 필요에 따라 해당하는 이벤트를 만들면된당 )

```html
<button @click="copyChartImg" />
``` 

4. copyChartImg 메소드 작성

```javascript
copyChartImg() {
      html2canvas(self.$refs.chartcapture.$el).then(canvas => {
        canvas.toBlob(blob => navigator.clipboard.write([new ClipboardItem({"image/png": blob})]))
      })
    }
``` 

출처 : https://im-designloper.tistory.com/66 [DESIGNLOPER]
