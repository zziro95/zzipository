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
- didEnterBackground: App이 **Background** 상태로 전환된 직후 호출, **Background** 상태가 되었음을 알리는 메서드.  
        - 이 메서드를 사용하여 공유 리소스를 해제, 타이머 무효화, 앱이 (Foreground 상태의 앱의 메모리 부족, 앱을 사용자가 종료)상황에 대비해 앱을 현재 상태로 복원하는데 충분한 상태 정보를 저장. (메모 작성 중이었다면 메모 저장 같은 작업을 여기서 한다.)   
 <br>
 <br>
 
 **파생된 질문**
 - `willEnterForeground`의 메서드가 `willDidBecomeActive` 메서드에 대한 호출로 이어지기 때문에 `willEnterForeground`에서의 상태는 비활성 상태 라고 추측되는데 맞을까? (런치 스크린 뜨고 있을 때일까?)
 - 처음 앱을 켤 때 한정 지으면 `willEnterForeground`를 통해 **InActive** 상태로 들어가고 **Active** 상태가 되었을 때 `willDidBecomeActive`가 호출된다.
 - 따라서 `willEnterForeground`를 **InActive**라고 생각하는 게 아닌 **Active** 상태가 되기 위해 **InActive** 상태를 거치는 상태라고 보면 될 것 같다.   
<br>
<br>

**새로 알게 된 내용** (applicationDidEnterBackground(_:) 문서 내용)
- 포어그라운드에서 메일 전송 같은 작업을 실행시키고 바로 백그라운드로 왔을 때 **Background**에서 메일 전송과 같은 네트워크와 통신해야 하는 작업이 진행 중일 텐데 애플에서는 악성코드를 예방하기 위해서 5초의 시간만 준다고 한다.
- 5초 안에 만약에 작업이 끝나지 않으면 (**1.** beginBackgroundTask(expirationHandler:)
에서 추가시간을 요청하는 방법도 있다 하지만 시스템에서 추가시간을 요청받을 때 시간이 필요하기 때문에 최대한 빨리 요청해야 한다. ) **2.** 보내던 메일을 임시저장 한다든지, 파일 업로드에 실패했다는 얼럿을 띄운다는 것과 같은 마지막 하나의 함수를 호출하고 **Not Running** 상태로 돌아간다. (2번에 대한 공식 문서를 아직 못 찾음)   
<br>
    
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

- [ ]  오토레이아웃을 코드로 작성하는 방법은 무엇인가? (3가지)
- [ ]  hugging, resistance에 대해서 설명하시오.
- [ ]  Intrinsic Size에 대해서 설명하시오.
- [ ]  스토리보드를 이용했을때의 장단점을 설명하시오.
- [ ]  Safearea에 대해서 설명하시오.
- [ ]  Left Constraint 와 Leading Constraint 의 차이점을 설명하시오.

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
