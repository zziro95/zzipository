# 면접 스터디 
면접 스터디 모임에서 이야기 나눌 질문들을 정리하기 위한 글입니다.   
출처는 [제르시](https://github.com/JeaSungLEE/iOSInterviewquestions)가 정리해 놓으신 질문들을 참고로 했고,    
스터디에서 추가적으로 생긴 질문들이나 해결하지 못한 궁금증 들을 남기기 위한 글입니다.   

### **1) GCD (iOS)**
- [ ]  NSOperationQueue 와 GCD Queue 의 차이점을 설명하시오. (GCD)
- [ ]  GCD API 동작 방식과 필요성에 대해 설명하시오. (GCD)
- [ ]  Global DispatchQueue 의 Qos 에는 어떤 종류가 있는지, 각각 어떤 의미인지 설명하시오. (GCD)
- [ ]  멀티 쓰레드로 동작하는 앱을 작성하고 싶을 때 고려할 수 있는 방식들을 설명하시오. (GCD)   

---
### **2) URL / Network / JSONDecoder (iOS)**
- [ ]  NSURLConnection 에서 사용하는 Delegate 메서드들에 대해 설명하시오. (URL)
- [ ]  Synchronous 방식과 Asynchronous 방식으로 URL Connection을 처리할 경우의 장단점을 비교하시오. (URL)
- [ ]  웹 서버와 HTTP 연결을 사용해서 데이터를 주거나 받으려면 사용해야 하는 클래스와 동작을 설명하시오. (URL)
- [ ]  JSON 데이터를 처리하는 방식과 파서, 객체 변환 방식에 대해 설명하시오. (JSON Parsing)   

---
### **3-1) Struct / Class (Swift)**
- [ ]  Struct 가 무엇이고 어떻게 사용하는지 설명하시오.(Struct)
- [ ]  instance 메서드와 class 메서드의 차이점을 설명하시오.(Class)
- [ ]  shallow copy와 deep copy의 차이점을 설명하시오. (Struct class)
- [ ]  mutating 키워드에 대해 설명하시오.(mutating)   

### **3-2) 프로토콜 / 익스텐션 (Swift)**
- [ ]  프로토콜이란 무엇인지 설명하시오.(프로토콜)
- [ ]  Protocol에서는 왜 var만 되는지 설명하시요.(프로토콜)
- [ ]  Extension에 대해 설명하시오.(Extension)
- [ ]  Hashable이 무엇이고, Equatable을 왜 상속해야 하는지 설명하시오.(Hashable).  

---
### **4-1) View Hierarchy, View Programming, View Controller (iOS)**
- [ ]  UIKit 클래스들을 다룰 때 꼭 처리해야하는 애플리케이션 쓰레드 이름은 무엇인가? (UIKit)
- [ ]  Bounds 와 Frame 의 차이점을 설명하시오. (View)
- [ ]  자신만의 Custom View를 만들려면 어떻게 해야하는지 설명하시오. (View)
- [ ]  View 객체에 대해 설명하시오. (View)
- [ ]  UIView 에서 Layer 객체는 무엇이고 어떤 역할을 담당하는지 설명하시오. (View)
- [ ]  UIWindow 객체의 역할은 무엇인가? (View)
- [ ]  NSObject부터 UIButton 까지 상속 과정의 계층과 역할을 설명하시오. (ViewProgramming)
- [ ]  UINavigationController 의 역할이 무엇인지 설명하시오. (ViewController, Navigation)
- [ ]  모든 View Controller 객체의 상위 클래스는 무엇이고 그 역할은 무엇인가? (ViewController)
- [ ]  앱 화면의 콘텐츠를 표시하는 로직과 관리를 담당하는 객체를 무엇이라고 하는가? (ViewController)   

---
### **4-2) TableView / CollectionView (iOS)**
- [ ]  TableView를 동작 방식과 화면에 Cell을 출력하기 위해 최소한 구현해야 하는 DataSource 메서드를 설명하시오. (TableView)
- [ ]  하나의 View Controller 코드에서 여러 TableView Controller 역할을 해야 할 경우 어떻게 구분해서 구현해야 하는지 설명하시오. (TableView).  

---
### **5-1) 클로저 / 옵셔널 (Swift)**
- [ ]  Swift의 클로저와 Objective-C의 블록은 어떤 차이가 있는가? (클로저)
- [ ]  탈출 클로저에 대하여 설명하시오.(클로저)
- [ ]  Optional 이란 무엇인지 설명하시오.(옵셔널)
- [ ]  defer란 무엇인지 설명하시오.(defer)
- [ ]  defer가 호출되는 순서는 어떻게 되고, defer가 호출되지 않는 경우를 설명하시오.(defer)   

---
### **5-2) 접근제어 / defer (Swift)**
- [ ]  접근 제어자의 종류엔 어떤게 있는지 설명하시오(접근제어).  

---
### **6-1) ARC (Swift)**
- [ ]  ARC란 무엇인지 설명하시오.
- [ ]  Retain Count 방식에 대해 설명하시오.
- [ ]  Strong 과 Weak 참조 방식에 대해 설명하시오.
- [ ]  순환 참조에 대하여 설명하시오.
- [ ]  강한 순환 참조 (Strong Reference Cycle) 는 어떤 경우에 발생하는지 설명하시오.   

---
### 6-2) MRC
- [ ]  ARC 대신 Manual Reference Count 방식으로 구현할 때 꼭 사용해야 하는 메서드들을 쓰고 역할을 설명하시오.
- [ ]  retain 과 assign 의 차이점을 설명하시오.
- [ ]  특정 객체를 autorelease 하기 위해 필요한 사항과 과정을 설명하시오.
- [ ]  Autorelease Pool을 사용해야 하는 상황을 두 가지 이상 예로 들어 설명하시오.
- [ ]  다음 코드를 실행하면 어떤 일이 발생할까 추측해서 설명하시오. Ball *ball = [[[[Ball alloc] init] autorelease] autorelease];   

---
### **6-3) 데이터 저장 (Swift)**
- [ ]  앱의 콘텐츠나 데이터 자체를 저장/보관하는 특별한 객체를 무엇이라고 하는가? (데이터저장)
- [ ]  Core Data와 Sqlite 같은 데이터 베이스의 차이점을 설명하시오.(데이터저장)

---
### **6-4) Functional Programming (Swift)**
- [ ]  함수형 프로그래밍이 무엇인지 설명하시오.
- [ ]  고차 함수가 무엇인지 설명하시오.
- [ ]  Swift Standard Library의 map, filter, reduce, compactMap, flatMap에 대하여 설명하시오.   

---
### **7-1)  App LifeCycle (iOS)**
- [ ]  앱이 foreground에 있을 때와 background에 있을 때 어떤 제약사항이 있나요? (App LifeCycle)
- [ ]  앱이 In-Active 상태가 되는 시나리오를 설명하시오. (App LifeCycle)
- [ ]  App의 Not running, Inactive, Active, Background, Suspended에 대해 설명하시오. (App LifeCycle)   

---
### 7-2) **AppDelegate, SceneDelegate (iOS)**
⁉️ **메서드 호출 순서**   
일반적인 사이클이라면 앱이 켜질 때 이런 순서로 메서드가 호출될 것 같다.   
`willEnterForegroundNotification`를 `post`하여 관심 있는 인스턴스가 전환에 응답할 수 있도록 제공한다.   
<br>

`willEnterForeground` - **Foreground** 상태로 들어감을 알리는 메서드   
`willDidBecomeActive` - `willEnterForeground` 통해 호출돼 **Active** 상태에 들어왔음을 알리는 메서드.  
<br>

`willResignActive` - 앱이 곧 **InActive** 상태가 될 것을 알리는 메서드.  
<br>

`DidEnterBackground` - 백그라운드에 진입했음을 알리는 메서드.  
`beginBackgroundTask(expirationHandler:)` - **Background** 진입 전 작업이 완료되지 않았는데 제한 시간 `5초` 보다 더 걸릴 경우 추가시간을 요청하는 메서드  (이건 App Lifecycle 정리할 때 공식 문서 읽기)   
💡 시스템에서 추가시간을 요청받을 때 시간이 필요하기 때문에 최대한 빨리 요청해야 한다.   
<br>
<br>

✅ **문제 & 답변**   
#### 상태 변화에 따라 다른 동작을 처리하기 위한 AppDelegate 메서드들을 설명하시오. (AppDelegate)
- iOS 버전에 따라 메서드들이 호출되는 곳의 차이는 있을 수 있다. (iOS 13 버전 미만은 AppDelegate, 이상은 SceneDelegate)
<br>

- `willEnterForeground`: **Foreground** 에 들어감을 알리는 메서드   
- `didBecomeActive`: 앱이 **Active** 상태가 되었음을 알림. App이 **Active** 상태로 전환된 직후 호출
    - 이 메서드를 호출하여 앱이 비활성 상태에서 활성 상태로 이동했음을 알린다.!  (**InActive** 상태에서 중지되었던 일들을 다시 시작한다.)
    - 출처 : [applicationDidBecomeActive(_:)](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622956-applicationdidbecomeactive)   
- `willResignActive`: 앱이 곧 **InActive** 상태가 될 것을 알림. App이 InActive 상태로 전환되기 직전에 호출 (interrupt 또는 앱을 종료하여 **Background**로 가기 전에 **InActive** 상태가 된다. )   
- `didEnterBackground`: App이 **Background** 상태로 전환된 직후 호출, **Background** 상태가 되었음을 알리는 메서드.  
        - 이 메서드를 사용하여 공유 리소스를 해제, 타이머 무효화, 앱이 (Foreground 상태의 앱의 메모리 부족, 앱을 사용자가 종료)상황에 대비해 앱을 현재 상태로 복원하는데 충분한 상태 정보를 저장. (메모 작성 중이었다면 메모 저장 같은 작업을 여기서 한다.)   
 <br>
 <br>
 
 🐣 **파생된 질문**   
 - `willEnterForeground`의 메서드가 `willDidBecomeActive` 메서드에 대한 호출로 이어지기 때문에 `willEnterForeground`에서의 상태는 비활성 상태 라고 추측되는데 맞을까? (런치 스크린 뜨고 있을 때일까?)
 - 처음 앱을 켤 때 한정 지으면 `willEnterForeground`를 통해 **InActive** 상태로 들어가고 **Active** 상태가 되었을 때 `willDidBecomeActive`가 호출된다.
 - 따라서 `willEnterForeground`를 **InActive**라고 생각하는 게 아닌 **Active** 상태가 되기 위해 **InActive** 상태를 거치는 상태라고 보면 될 것 같다.   
<br>
<br>

⭐ **새로 알게 된 내용**    ([applicationDidEnterBackground(_:)](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622997-applicationdidenterbackground) 문서 내용)
- 포어그라운드에서 메일 전송 같은 작업을 실행시키고 바로 백그라운드로 왔을 때 **Background**에서 메일 전송과 같은 네트워크와 통신해야 하는 작업이 진행 중일 텐데 애플에서는 악성코드를 예방하기 위해서 5초의 시간만 준다고 한다.
- 5초 안에 만약에 작업이 끝나지 않으면 (**1.** `beginBackgroundTask(expirationHandler:)`
에서 추가시간을 요청하는 방법도 있다 하지만 시스템에서 추가시간을 요청받을 때 시간이 필요하기 때문에 최대한 빨리 요청해야 한다. ) **2.** 보내던 메일을 임시저장 한다든지, 파일 업로드에 실패했다는 얼럿을 띄운다는 것과 같은 마지막 하나의 함수를 호출하고 **Not Running** 상태로 돌아간다. (2번에 대한 공식 문서를 아직 못 찾음)   
<br>

📝 **참고**   
- [UIApplicationDelegate](https://developer.apple.com/documentation/uikit/uiapplicationdelegate)    
- [applicationWillEnterForeground(_:)](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1623076-applicationwillenterforeground)
- [applicationDidBecomeActive(_:)](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622956-applicationdidbecomeactive)
- [applicationWillResignActive(_:)](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622950-applicationwillresignactive)
- [applicationDidEnterBackground(_:)](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622997-applicationdidenterbackground)
<br>
<br>

####  scene delegate에 대해 설명하시오. (SceneDelegate)
**scene delegate**   
- iPad에서 multi window를 지원하기 위해서 생겨난 개념으로 AppDelegate에서 관리하던 UI Lifecycle을 관리하는 책임을 가지고 있다.   
- 화면에 표시되는 내용(Windows 또는 Scenes)을 처리하고 앱이 표시되는 방식을 관리한다.   
<br>

**scene 이란?**   
- app의 UI를 나타내는 개체, scene 에는 ui 하나의 인스턴스를 나타내는 windows와 viewcontroller가 들어있다.
<br>

⁉️ **해결하지 못한 질문들**
#### 앱이 시작할 때 main.c 에 있는 UIApplicationMain 함수에 의해서 생성되는 객체는 무엇인가? (AppDelegate)
- UIApplication 싱글턴 객체가 생성된다. 
- `delegateClassName: String?` 인걸로 보아 델리게이트 객체는 생성이 될 수도 있고 안될 수도 있는 것 같다.  [UIApplicationMain(_:_:_:_:)](https://developer.apple.com/documentation/uikit/1622933-uiapplicationmain)
- `main.c` : 프레임워크 깊은 곳에서 실행되는 메인 함수 정도로 이해하였다.
<br>

#### UIApplication 객체의 컨트롤러 역할은 어디에 구현해야 하는가? (AppDelegate)
정확히 질문의 의미를 파악하지 못하였음.   
AppDelegate나, 그 안에 상태변화 메서드에 구현해야 할까?   

---
### **7-3) Autolayout (iOS)**
✅ **문제 & 답변**   
#### Intrinsic Content Size에 대해서 설명하시오.
 - 고유의 콘텐츠 크기를 뜻하며 `UISwitch`나 `UIButton`, `UILabel`, `UITextfield`) 처럼 자신의 content를 기반으로 뷰의 사이즈를 정할 수 있는 것. (`위치=좌표`는 지정해 줘야 한다.)    
 - `UISwitch`처럼 아예 너비, 높이의 기본 사이즈가 정해져 있거나, UIButton의 TitleLabel을 통해 너비와 높이를 유추할 수 있다는 개념이다.     
<br>

#### hugging, resistance에 대해서 설명하시오.
`Content Hugging`
- `Intrinsic Content Size`에 맞게 줄어들려고 하는 힘
- 늘어나지 않으려고 하는 힘
- 컨텐츠보다 더 늘어나지 않으려고 하는 힘.   
<br>

`Compression-Resistance` 
- 외부에서 뷰를 찍어누를 때 버티는 힘 (가로, 세로가 각각 있다.)
- 줄어들지 않으려고 버티는 힘 (늘어나려고 하는 힘은 아님)
- 자신의 컨텐츠를 지키려고 하는 힘    
<br>

**정리**
- `CHCR`은 서로 반대되는 개념이 아닌 다른 관점에서의 개념이다. 
- 둘의 기준이 되는 것은 `Intrinsic Content Size`
- `Priority` 우선도를 통해 결정됨 (`Priority`가 같다면 충돌이 일어난다.)   
<br>

뷰에 `UI`들을 올려놓았을 때 수평이나 수직에 대해 늘어나지 않았으면 좋겠는 객체들에 대해서 `Content Hugging`의 `Priority`를 높여주고, 상황에 따라서 객체들의 사이즈가 달라질 때 화면에서 가장 사라지지 않았으면 하는 객체에 `Compression-Resistance`의 `Priority`를 높여주면 되겠다고 생각하였다.    
<br>

#### 오토 레이아웃을 코드로 작성하는 방법은 무엇인가? (3가지)
`Layout Anchors` ,`NSLayoutConstraint Class` ,`Visual Format Language`
<br>

`Layout Anchors`    
- 읽기 쉽고 간결한 형식으로 제약 조건을 만들 수 있다.   
- 주로 어떤 `객체`의 어느 `Anchor(Attribute)`에 어떤 `Constaint(Relationship, Multiplier, Constant)` 를 줄 것인지 지정해 주고 `isActive` 시켜준다.   
- 💡 `Horizontal - 수평`에 대한 `Constraint`를 설정하는데 `Vertical - 수직`에 대한 `Constraint`를 설정해 주면 자동으로 컴파일 에러를 뱉어준다. (`Generic` 기능을 사용했기 때문 (제네릭과 에러를 뱉어주는 것과 무슨 연관이 있을까?)     
- [[Generic Class] NSLayoutAnchor](https://developer.apple.com/documentation/appkit/nslayoutanchor)
<br>

`NSLayoutConstraint Class`   
- `init(item:attribute:relatedBy:toItem:attribute:multiplier:constant:)`메서드를 사용하여 제약 조건을 만들 수 있는데 `Layout Anchors` 방식보다 가독성이 떨어진다.   
- `NSLayoutAnchor`가 `iOS 9` 버전부터 지원되기 때문에 `NSLayoutAnchor`로 설정해 줄 수 없는 제약사항(한계점)을 설정해야 할 때나 `iOS 8` 이전 버전을 지원해야 하는 경우에 사용할 것 같다.   
- 단점은 수평과 수직에 대한 잘못된 제약을 주었을 때 오류를 검출 안 해준다.   
<br>

`Visual Format Language`
- 제약 조건을 시각적으로 표현한 언어
<br>

장점
- `Auto Layout`은 `Visual Format Language`를 사용하여 콘솔에 메시지를 프린트한다.   
    - 따라서 `Auto Layout`관련 오류가 났을 때 `Visual Format Language`를 알면 더 쉽게 문제 인식과 해결이 가능하다.   
- `Visual Format Language`를 사용하면 매우 간단한 표현식을 사용하여 한 번에 여러 제약 조건을 만들 수 있다.
- `Visual Format Language`를 사용하면 유효한 제약 조건(₩이게 정확히 무슨 말을 뜻하는 거지?`) 만 만들 수 있습니다.
- [Visual Format Language](https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/AutolayoutPG/VisualFormatLanguage.html#//apple_ref/doc/uid/TP40010853-CH27-SW1) 잘 이해 안감 한번 살펴보고 글로 정리할 필요를 느낌   
<br>

#### 스토리보드를 이용했을 때의 장단점을 설명하시오.
`장점`   
- 앱의 흐름이 시각화되어 있기 때문에 보기 편하고 개발자가 아닌 디자이너와 같은 화면을 보며 쉽게 이야기가 가능하다.
- 프리뷰 기능을 통해 빌드 하지 않고 화면 확인 가능하다.   
<br>

`단점`   
- 스토리보드 파일의 포멧이 XML로 되어있어 읽기도 어렵고, 여러 명이 작업을 한다면 Merge Conflict 처리 비용이 크기 때문에 협업에서 사용하는데 어렵다. 
- 스토리보드로 할 수 없는 작업(뷰 계층 구조에 대한 일부 동적 변경 사항)을 해줄 수 있다. (예시는?)   
- 코드로 뷰를 만들면 재사용에 용이한데 스토리보드는 그렇지 않다.    
<br>

#### Safearea에 대해서 설명하시오.
- `StatusBar`, `NavigationBar`, `ToolBar`, `TabBar`등 을 사용하면 화면의 특정 부분을 우선적으로 차지하게 되는데 그런 영역들을 제외한 컨텐츠가 안전하게 보일 수 있음을 보장하는 영역    
<br>

#### Left Constraint 와 Leading Constraint의 차이점을 설명하시오.
- 대부분의 언어는 왼쪽에서 오른쪽으로 읽지만 대표적으로 아랍권은 오른쪽에서 왼쪽으로 읽는다.    
    - `Leading and Trailing Constraint`은 국가의 레이아웃이 읽기 방향에 따라 조정되는 제약사항이다.   
- `Left and Right Constraint`은 객체나 화면의 절대적인 방향 왼쪽, 오른쪽을 뜻한다.     
<br>

- 💡 `Auto Layout Guide`에 따르면 `Left and Right Constraint` 사용을 지양하고 `Leading and Trailing Constraint`을 사용할 것을 권장한다.    
<br>
<br>

🐣 **파생된 질문**    
#### `Layout Anchors`는 `Horizontal - 수평`에 대한 `Constraint`를 설정하는데 `Vertical - 수직`에 대한 `Constraint`를 설정해 주면 자동으로 컴파일 에러를 뱉어준다. 
#### 이것이 `Generic` 기능을 사용했기 때문이라는데 `Generic`이 정확히 어떤 역할을 했기에 가능한 것일까??   
- 답변: ?
<br>

#### `NSLayoutConstraint Class`로 설정해주어야 하는 `NSLayoutAnchor`로는 설정해 줄수 없는 제약사항(한계점)은 어떤 것들이 있을까??
- 답변: ?
<br>
<br>

⭐ **새로 알게된 내용**   
#### `TextView`는 스크롤이 가능하냐 아니냐에 따라 `Intrinsic Content Size`를 가질 수도 있고 아닐 수도 있다.      
- `TextView`의 스크롤 기능이 **꺼져**있다면 텍스트의 길이에 따라서 Intrinsic Content Size가 정해지고,   
- `TextView`의 스크롤 기능이 **켜져**있다면 Intrinsic Content Size가 정해질 수 없다.   
<br>

#### Intrinsic Content Size 활용 방법
`Storyboard` > `Size inspector` > `Instrinsic Size` > `Placeholder`를 이용하면 임시적인 높이와 너비 사이즈를 지정해 줄 수 있다.   
스토리보드에서만 적용 가능하고 실제 실행 중에는 역할을 하지 않는다. (스토리보드에서 대략적으로 위치를 놓아볼 때 활용해보면 좋을듯하다.)   
<br>

`@IBDesignable`, Custom Class의 `intrinsicContentSize` 프로퍼티를 이용해 기본 너비, 높이 설정 가능. (`@IBDesignable`에 대해 나중에 글로 정리해 보기 아래 링크도 참고하기)     
- [intrinsicContentSize 관련 참고해보면 좋을 글](https://ios-development.tistory.com/233)
- [invalidateIntrinsicContentSize() 관련 글](https://magi82.github.io/ios-intrinsicContentSize/)
<br>

📝 **참고**   
- [Auto Layout Guide (마지막 업데이트 날 짜 - 2016-03-21)](https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/AutolayoutPG/ProgrammaticallyCreatingConstraints.html#//apple_ref/doc/uid/TP40010853-CH16-SW1)
- [[야곰닷넷] 오토레이아웃 정복하기👍](https://yagom.net/courses/autolayout/)   

---
### **8-1) Design Pattern 1**

- [ ]  Singleton 패턴을 활용하는 경우를 예를 들어 설명하시오. (Design Pattern)
- [ ]  KVO 동작 방식에 대해 설명하시오. (Design Pattern)
- [ ]  NotificationCenter 동작 방식과 활용 방안에 대해 설명하시오. (NotificationCenter)

### **8-2) Design Pattern 2**

- [ ]  Delegate란 무언인가 설명하고, retain 되는지 안되는지 그 이유를 함께 설명하시오. (Delegation)
- [ ]  Delegate 패턴을 활용하는 경우를 예를 들어 설명하시오. (Design Pattern)
- [ ]  Delegates와 Notification 방식의 차이점에 대해 설명하시오. (Design Pattern)
- [ ]  의존성 주입에 대하여 설명하시오. (Dependency Injection)

### **8-3) Architecture**

- [ ]  MVVM, MVC, Ribs, VIP 등 자신이 알고있는 아키텍쳐를 설명하시오. (Architecture)
- [ ]  MVC 구조에 대해 블록 그림을 그리고, 각 역할과 흐름을 설명하시오.(Architecture)

---

### **9-1) Framework**

- [ ]  iOS 앱을 만들고, User Interface를 구성하는 데 필수적인 프레임워크 이름은 무엇인가? (UIKit)
- [ ]  Foundation Kit은 무엇이고 포함되어 있는 클래스들은 어떤 것이 있는지 설명하시오. (Foundation)
- [ ]  Foundation 과 Core Foundation 프레임워크의 차이점을 설명하시오. (Foundation)

### 9-2) App

- [ ]  실제 디바이스가 없을 경우 개발 환경에서 할 수 있는 것과 없는 것을 설명하시오. (Etc)
- [ ]  App Bundle의 구조와 역할에 대해 설명하시오. (Etc)
- [ ]  App thinning에 대해서 설명하시오.(etc)
- [ ]  Plist 파일 구조와 Plist 파일에 저장된 데이터를 다루기 적합한 클래스를 설명하시오. (Etc)

### 9-3) ETC

- [ ]  Responder Chain 구조에 대해 설명하고, First Responder 역할에 대해 설명하시오. (UIResponder)
- [ ]  Push Notification 방식에 대해 설명하시오. (User Notification)
- [ ]  NSCoder 클래스는 어떤 상황에서 어떻게 써야 하는지 설명하시오.(Keyed Archivers)
- [ ]  Fast Enumeration 이란 무엇인지 설명하시오.(Object-C) **이건 Obj-C 관련 내용인것 같아서 빼도 될지 공부를 안해봐서 판단이 안되네요**
- [ ]  Reactive Programming이 무엇인지 설명하시오.(Reactive Programming)

---
### 참고
- [From: https://github.com/JeaSungLEE/iOSInterviewquestions](https://github.com/JeaSungLEE/iOSInterviewquestions)
- [족보 저장소: https://github.com/ios-study-boost/iOSInterviewquestions](https://github.com/ios-study-boost/iOSInterviewquestions)
