# iOS Deployment Target
### 글 쓰게 된 이유
날씨 정보 앱을 회고하는 과정에서 Deploymnet Target과 관련된 에러가 발생하여 설정을 바꿔주어야 하는 경우가 있었는데 해결 방법으로는 코드로 어노테이션을 붙여주는 방법과 직접 Deployment Target을 바꿔주는 방법 2가지 정도가 있다고 생각이 들었는데, Project iOS Deployment Target을 알맞게 설정해 주어도 해결이 되지 않았다. 이론상으로 해결될 것이라고 생각했는데 빌드가 실패하였고 이유를 찾아 정리해 보기로 하였다.

***
### 문제 상황
프로젝트의 초기 설정에 `PROJECT iOS Deployment Target`이 12.0으로 설정되어 있었고, 때문에 13.0 이상부터 사용할 수 있는 `UIScene` 관련 클래스, 메소드들을 사용할 수 없어 오류가 발생 하였다. <br>
<br>
따라서 `PROJECT iOS Deployment Target`을 13.0이상으로 설정을 해준후 빌드를 하였는데도 오류가 발생하였다. <br>
<br>

---
### iOS Deployment Target
iOS Deployment Target이란 앱이 실행 가능한 최소 iOS 버전이다. <br>
iOS Deployment Target는 PROJECT에서만 설정할 수 있는것이 아니고 TARGETS에서도 iOS Deployment Target을 설정해 줄 수 있다. <br>
`PROJECT iOS Deployment Target`는 말 그대로 프로젝트 전체의 Deployment Target을 설정해 주는 것이고, `TARGETS iOS Deployment Target`에서 iOS를 포함한 macOS, tvOS, watchOS의 Deloyment Target을 각각 다르게 상세하게 설정해 줄 수 있다. <br>
<br>

---
### 해결 방법
그렇다면 왜 `PROJECT iOS Deployment Target`을 13.0이상으로 설정을 해준후 빌드를 하였는데도 오류가 발생하였을까? <br>
그 이유는 TARGETS이 PROJECT를 OVERRIDE 하기 때문이였다.<br>
그래서 `TARGETS iOS Deployment Target`를 확인해보니 12.0으로 되어 있었다.<br>
<br>
`PROJECT iOS Deployment Target`이 13.0이여도 `TARGETS iOS Deployment Target`이 12.0이라면 오버라이드 되기 때문에 최종적으로 이 앱의 iOS Delployment Target은 12.0이기 때문에 `UIScene`과 관련된 클래스, 메서드들을 사용할 수 없는 상황이 바뀌지 않은 것이다. <br>
`TARGETS iOS Deployment Target`을 13.0으로 바꿔주어 문제를 해결하였다. <br>
<br>
근거를 좀 더 공식적인 문서에서 찾고 싶었는데 그러진 못하였다. <br>
<br>

---
### 마무리 글
회고를 통해 중요한 설정 중 하나인 iOS Deployment Target에 대한 개념을 정리할 수 있어서 의미있는 시간이였다. 회고의 중요성을 느끼는 하루다. <br>
<br>

***
### 참고
- [참고블로그](https://adervise1.tistory.com/104, "참고블로그")
- [참고블로그](https://velog.io/@eunjiha/iOS-Xcode-IDE-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0, "참고블로그")
