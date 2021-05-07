# AppDelegate SceneDelegate
### 글 쓰게 된 이유
iOS Deployment Target이 12.0 버전으로 적용된 프로젝트를 진행해보면서 `UIScene`과 관련된 이슈, 변경 사항이 있다는 것을 알게 되었고 본질적인 이해를 위해 AppDelegate SceneDelegate에 대해 살펴보아야 겠다 생각하여 이 글을 작성합니다. <br>

***
### Scene과 Multiple Windows
[Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/ios/system-capabilities/multiple-windows/)를 보면 iOS 13버전 이상에서 iPad 앱은 멀티 윈도우를 지원한다는 것을 알 수 있습니다. <br>
<img src="https://github.com/zziro95/zzipository/blob/main/images/MultipleWindowsiPad.png" width="70%" height="70%" title="MultipleWindowsiPad" alt="MultipleWindowsiPadImg"></img> <br>

`UIScene`과 관련이 깊은 내용이며 연관 WWDC로는 [[WWDC 2019] Architecting Your App for Multiple Windows](https://developer.apple.com/videos/play/wwdc2019/258/), [[WWDC 2019] Introducing Multiple Windows on iPad](https://developer.apple.com/videos/play/wwdc2019/212/)가 있는 것으로 보이며
각각의 WWDC를 본 저의 정리글은 [[WWDC 2019] Architecting Your App for Multiple 정리글](https://github.com/zziro95/zzipository/blob/main/iOS/ArchitectingYourAppforMultiple(App%26SceneDelegate).md), (아직못봄..)에 있습니다.

***
### iOS 12 이하에서의 구조
<img src="https://github.com/zziro95/zzipository/blob/main/images/iOS12&EarlierAppDelegate.png" width="70%" height="70%" title="iOS12&EarlierAppDelegate" alt="iOS12&EarlierAppDelegateImg"></img> <br>
<br>
#### AppDelegate
- Process LifeCycle 관리
- UI LifeCycle 관리 <br>
어플리케이션은 하나의 Process와 그에 매치되는 **하나의** User Interface Instance를 가진다. <br>

***
### iOS 13 부터의 구조
<img src="https://github.com/zziro95/zzipository/blob/main/images/AppDelegateChange.png" width="70%" height="70%" title="AppDelegateChange" alt="AppDelegateChangeImg"></img> <br>
<br>
어플리케이션은 여전히 하나의 Process를 공유하지만 **여러개의** User Interface Instance 또는 Scene Session을 가질수 있다. <br>
<br>
#### AppDelegate
- Process LifeCycle 관리
- Session LifyCycle 관리 <br>
여기서  `Session`이란 `Scene Session`을 의미한다.
<br>

#### SceneDelegate
- UI LifeCycle 관리 <br>

***

### AppDelegate

---
### SceneDelegate

---
### 마무리 글
[[WWDC 2019] Architecting Your App for Multiple Windows](https://developer.apple.com/videos/play/wwdc2019/258/)와 블로그들을 보고 다시 정리해 보는 느낌으로 이 글을 작성하였는데 역시 한 번 정리하는 것보다 두 번 정리하는게 더 나은 것 같다. <br>
그런 의미로 다음 기회에는 AppDelegate와 SceneDelegate를 각각 좀 더 상세하게 알아보고 정리하는 시간을 가지면 좋겠다는 생각이다. <br>
참, 아직 살펴보지 못한 [[WWDC 2019] Introducing Multiple Windows on iPad](https://developer.apple.com/videos/play/wwdc2019/212/)도 꼭 살펴보고 정리하자! <br>
***
### 참고
- [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/ios/system-capabilities/multiple-windows/)
- [[WWDC 2019] Architecting Your App for Multiple Windows](https://developer.apple.com/videos/play/wwdc2019/258/)
- [[WWDC 2019] Introducing Multiple Windows on iPad 도 살펴보기 (13:29~26:30)](https://developer.apple.com/videos/play/wwdc2019/212/)
- [Zedd님 블로그](https://zeddios.tistory.com/811)
