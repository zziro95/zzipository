# [WWDC 2019] Architecting Your App for Multiple
### 글 쓰게 된 이유
AppDelegate SceneDelegate를 공부하기 위해 알아보던 도중 관련 WWDC가 있다는 것을 알게 되었고 보면서 정리하기 위해 글을 쓰게 되었습니다. <br>

***
### 정리 글
[[WWDC 2019] Architecting Your App for Multiple Windows](https://developer.apple.com/videos/play/wwdc2019/258/)에서 세 가지 주제에 관하여 이야기를 합니다. <br>
#### Changes to app lifecycle, Using the scene delegate
시작하기 앞서 iOS 12 및 이전 버전에서 AppDelegate의 역할과 책임에 대해서 알아봅니다. <br>
- 첫 번째 역할은 애플리케이션에 프로세스 수준 이벤트(프로세스가 시작되거나 종료 되는)를 알리는 것이다.
- 두 번째 역할은 어떤 방법을 통해 foreground 상태에 들어가거나, active 상태에서 빠져나오는 것과 같은 애플리케이션의 UI 상태를 알리는 것이다. <br>
<br>

<img src="https://github.com/zziro95/zzipository/blob/main/images/iOS12&EarlierAppDelegate.png" width="70%" height="70%" title="iOS12&EarlierAppDelegate" alt="iOS12&EarlierAppDelegateImg"></img> <br>
iOS 12 이전 버전에서는 애플리케이션에는 하나의 프로세스와 하나의 사용자 인터페이스 인스턴스가 있기 때문에 괜찮았다. <br>
그러나 이건 iOS 13버전부터는 유효하지 않다. <br>
여전히 애플리케이션은 하나의 프로세스만 공유하지만 여러 사용자 인터페이스 인스턴스 또는 `scene session`을  가질 수 있기 때문이다.<br>
<br>

##### scene session?
`scene session`이란 사용자가 앱에 새 화면(스냅샷 개념을 대입해봄)을 띄우거나 요청할 때 새로 나타나거나 다시 나타나게 될 화면에 대한 정보를 가지고 있는 오브젝트이다.
이것들의 생명주기를 SceneDelegate에서 관리한다고 생각한다. <br>
<br>

<img src="https://github.com/zziro95/zzipository/blob/main/images/AppDelegateChange.png" width="70%" height="70%" title="AppDelegateChange" alt="AppDelegateChangeImg"></img> <br>
iOS 13버전 이후부터는 AppDelgate의 책임은 `프로세스 수준 이벤트를 알리는 것`, `프로세스의 생명주기를 관리하는 것`으로 줄어들고, SceneDelegate가 `애플리케이션의 UI 상태를 알리는 것`에 대해 관리한다. <br>
**또 중요한 변경 사항은 앱딜리게이트가** `Session LifyCycle` **관리도 한다.** <br>
여기서  `Session`이란 `Scene Session`을 의미하고, `Scene Session`이 생성되거나 삭제될 때 시스템이 AppDelegate에게 알리게 된다고 한다.  <br>
<br>

<img src="https://github.com/zziro95/zzipository/blob/main/images/UIStaterelatedmethods.png" width="70%" height="70%" title="UIStaterelatedmethods" alt="UIStaterelatedmethodsImg"></img> <br>
위의 메서드 집합들을 유지하면 버전에 맞게 UIKit이 런타임에 올바른 집합을 호출하기 때문에 iOS 13.0 이상과 그 아래의 버전 모두 정상적으로 작동한다고 한다. <br>

#### Architecture
상태 복원에 대해서 iOS 13에서는 별로 좋지 않다고 이야기한다. 애플리케이션이 `scene-base` 상태 복원을 구현하는 게 더 중요하다고 합니다. <br>
보여준 예시를 살펴보며 이해해 보자. <br>
<img src="https://github.com/zziro95/zzipository/blob/main/images/sameTime&ConversationDifferentView.png" width="70%" height="70%" title="sameTime&ConversationDifferentView" alt="sameTime&ConversationDifferentViewImg"></img> <br>
두 개의 다른 `View`와 `Scene`에서 같은 대화를 보고 있다. <br>
<br>

<img src="https://github.com/zziro95/zzipository/blob/main/images/updateOnlyOneScene.png" width="70%" height="70%" title="updateOnlyOneScene" alt="updateOnlyOneSceneImg"></img> <br>
이 상태에서 하나의 `View`, `Scene`을 이용해 추가적으로 대화를 보낸 상황이다. <br>
그림과 같이 하나의 `Scene`만 업데이트되었음을 볼 수 있다. <br>
<br>

<img src="https://github.com/zziro95/zzipository/blob/main/images/structuredImage.png" width="70%" height="70%" title=" structuredImage" alt=" structuredImageImg"></img> <br>
버튼 탭을 통해 보내기 버튼을 누르면 뷰 컨트롤러가 자체 UI를 업데이트한다. <br>
그 후 뷰 컨트롤러는 모델 또는 모델 컨트롤러에 알린다. <br>
이건 하나의 사용자 인터페이스 인스턴스를 가질 때(iOS 12 이전 버전)는 괜찮지만 위와 같이 동일한 데이터를 보여주는 다른 `Scene`에 다른 `ViewController`를 도입하면 새 데이터로 자체 업데이트하라는 알림을 받지 않는다. <br>
<br>

<img src="https://github.com/zziro95/zzipository/blob/main/images/Resolution.png" width="70%" height="70%" title=" Resolution" alt=" ResolutionImg "></img> <br>
이를 해결하기 위한 방법은 뷰 컨트롤러가 이벤트를 받을 때 바로 모델 컨트롤러에 알려 모델 컨트롤러가 관련 뷰 컨트롤러에게 새 데이터에게 업데이트해야 한다고 알리도록 하는 방식이다. <br>
이를 수행하는 방법에는 `delegate`, `notification`을 쓰거나, 2019년에 새로 발표된 `Swift Combine` 프레임워크를 사용하는 방법이 있다고 한다. <br>

***
### 마무리 글
다른 WWDC에 비해 짧은 영상이지만 처음으로 WWDC를 제대로 본 것 같다. <br>
새로운 개념들에 대해 애플에서 직접 설명해 주는 자료이기 때문에 생겨난 이유, 이전과의 비교, 방향성 등 좋은 내용들로 꽉 차있었다. <br>
내용을 100% 이해하지는 못했지만 전보다는 개념이 잡힌 것 같아 기쁘다. <br>
그리고 느낀 점은 애플이 iOS 새 버전을 출시할 때마다 내가 프로젝트를 좀 더 효율적인 코드로 바꾸기 위해 리팩토링 하듯이 정말 큰 iOS라는 프로젝트를 리팩토링 하는 과정이라는 생각이 들었다. <br>
엄청 멀게만 느껴졌던 WWDC가 조금 친숙해져서 다행인 것 같다. <br>

***
### 참고
- [[WWDC2019] Architecting Your App for Multiple Windows](https://developer.apple.com/videos/play/wwdc2019/258/)
