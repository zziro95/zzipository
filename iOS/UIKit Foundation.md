# UIKit Foundation
### 글 쓰게 된 이유
[JSONSerialization](https://developer.apple.com/documentation/foundation/jsonserialization)를 공부하다가 공식문서에 `JSON`과 `Foundation` 객체간에 변환을 하는 객체라고 설명되어있는데 잘 이해가 되지 않았고, 예전에 `UIKit` 과 `Foundation` 에 대해 정리를 간략하게 했던 기억이 있는데 제대로 기록해 놓지 않아 다시 봐야하는 상황이 되어 버렸다. 잘 정리해 놓자!    

***
### UIKit
[UIKit](https://developer.apple.com/documentation/uikit) 공식문서를 살펴보면 "iOS 와 tvOS app을 위한 그래픽, 이벤트 기반 user interface를 구성하고 관리한다" 라고 나와있다.    
<br>

❗또한 `important` 부분을 보면 "달리 명시되지. 않은 경우에는 UIKit 클래스를 앱의 main thread 도는 main dispatch queue 에서만 사용하라"고 나와있다.

아마도 UI를 그리는 작업때문이지 않을까 draw()? 
이유에 대해서 좀 더 자세하게 쓰기.

다시 `UIKit` 을 정리해보면   
- `시스템과 상호작용`하고 `앱의 메인 이벤트 루프를 실행`, `화면에 콘텐츠를 표시`하는 등 iOS or tvOS 용 앱을 빌드하는 데 필요한 핵심 개체를 제공한다.
- 이런 개체를 사용하여 콘텐츠를 화면에 표시하고, 해당 콘텐츠와 상호 작용하고, 시스템과의 상호 작용을 관리한다.
- 앱의 기본 동작과 특정 요구 사항에 맞게 해당 동작을 사용자 지정할 수 있는 다양한 방법을 제공한다.   
<br>

<img src="https://github.com/zziro95/zzipository/blob/main/images/CoreAppObjects.png" width="70%" height="70%" title="CoreAppObjects" alt="CoreAppObjectsImg"></img> <br>

`UIKit`은 앱의 데이터 구조를 나타내는 모델 개체들을 제공한다.   
대부분 뷰 객체들을 제공하고, 데이터 개체들과 UIKit View 간의 데이터 교환을 조정하는건 `ViewController`, `App Delegate`가 맡아서 한다.   
***
### Foundation
"필수 data types, collections, operating-system services 에 접근하여 앱의 기본 기능 계층을 정의한다"라고 설명되어 있다.   
데이터 저장 및 지속성, 텍스트 처리, 날짜 및 시간 계산, 정렬 및 필터링, 네트워킹을 포함하여 앱 및 프레임 워크에 대한 기본 기능 계층을 제공한다. (정말 많은걸 해주는 구나...)   
`Foundation`에서 정의한 클래스, 프로토콜 및 데이터 타입들은 macOS, iOS, watchOS, tvOS 전체에서 사용된다
***
### import
Xcode를 통해 UIKit 정의부를 살펴보면 `Foundation`이 import 되어 있음을 확인 할 수 있다.   
<img src="https://github.com/zziro95/zzipository/blob/main/images/UIKit.png" width="70%" height="70%" title="UIKit" alt="UIKitImg"></img> <br>
따라서 View를 다루는 파일에는 기본적으로 UIKit이 import 되어 있고, 타입을 정의하는 파일에는 Foundation이 기본으로 import 되어잇는 모습을 볼 수 있다.    
잘 모르겠을 땐 UIKit을 일단 import 하면 되겠지만 좀 더 세분화하고 이유있는 코드를 쓰기 위해선 정확히 하자!   

***
### 정리
`UIKit` 및 `Foundation` 프레임 워크는 앱의 모델 객체를 정의하는 데 사용하는 많은 기본 유형을 제공한다.   
`UIKit`은 UIDocument 디스크 기반 파일에 속하는 데이터 구조를 구성하기 위한 개체를 제공하고, 일반적으로 콘텐츠를 화면에 표시하는 UIView 클래스를 정의한다.     
`Foundation`은 문자열, 숫자, 배열 및 기타 데이터 유형을 나타내는 기본 개체를 정의한다.   
덤으로 `Swift Standard Library`는 `Foundation` 프레임워크에서 사용할 수 있는 다수의 같은 타입들을 제공한다.     
***
### 참고
- [UIKit](https://developer.apple.com/documentation/uikit)
- [About App Development with UIKit](https://developer.apple.com/documentation/uikit/about_app_development_with_uikit)
- [Foundation](https://developer.apple.com/documentation/foundation)
