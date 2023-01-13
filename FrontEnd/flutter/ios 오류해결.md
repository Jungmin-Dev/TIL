<h1> Flutter ios 오류해결 : Error output from CocoaPods: Searching for inspections failed: undefined method 'map' for nil:NilClass </h1>

- 구글링을 해보니 M1 맥북을 써서 나오는 오류로 빌더에서 계속 오류가 났다.

```
#1 Install ffi 터미널에서 입력
sudo arch -x86_64 gem install ffi

#2 Re-install dependencies ios/ 위치에서 입력
arch -x86_64 pod install
```

출처 : https://velog.io/@chanhook/Flutter-ios-%EC%98%A4%EB%A5%98%ED%95%B4%EA%B2%B0-Error-output-fromCocoaPods-Searching-for-inspections-failed-undefined-method-map-for-nilNilClass
