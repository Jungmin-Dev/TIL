<h1> 오류 발생 </h1>

- flutter로 개발한 소스를 Xcode를 이용해 iPhone으로 실행하면서 나는 오류 발생하였다.

<h3> 에러내용 </h3>

- 에러 내용은 'The sandbox is not in sync with the Podfile.lock. Run 'pod install' or update your CocoaPods installation.' 이었다.
 
- The sandbox is not in sync with the Podfile.lock. Run 'pod install' or update your CocoaPods installation. 오류

- The sandbox is not in sync with the Podfile.lock. Run 'pod install' or update your CocoaPods installation. 오류
 

<h3> 해결 방법 </h3>

- (먼저 cocoaPods을 설치한 후, pod 명령어를 쓸 수 있는 환경이라고 가정)

- 실행하려는 프로젝트 내에 Podfile이 있는 경로에서 `pod install` 명령어를 한번 실행해주면 된다.


출처 : https://dc2348.tistory.com/11
