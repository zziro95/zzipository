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

---
✅ **문제 & 답변**   
#### ▶️ 상태 변화에 따라 다른 동작을 처리하기 위한 AppDelegate 메서드들을 설명하시오. (AppDelegate)
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
 #### ▶️ `willEnterForeground`의 메서드가 `willDidBecomeActive` 메서드에 대한 호출로 이어지기 때문에 `willEnterForeground`에서의 상태는 비활성 상태 라고 추측되는데 맞을까? (런치 스크린 뜨고 있을 때일까?)
 - 처음 앱을 켤 때 한정 지으면 `willEnterForeground`를 통해 **InActive** 상태로 들어가고 **Active** 상태가 되었을 때 `willDidBecomeActive`가 호출된다.
 - 따라서 `willEnterForeground`를 **InActive**라고 생각하는 게 아닌 **Active** 상태가 되기 위해 **InActive** 상태를 거치는 상태라고 보면 될 것 같다.   
<br>
<br>

---
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

---
#### ▶️ scene delegate에 대해 설명하시오. (SceneDelegate)
**scene delegate**   
- iPad에서 multi window를 지원하기 위해서 생겨난 개념으로 AppDelegate에서 관리하던 UI Lifecycle을 관리하는 책임을 가지고 있다.   
- 화면에 표시되는 내용(Windows 또는 Scenes)을 처리하고 앱이 표시되는 방식을 관리한다.   
<br>

**scene 이란?**   
- app의 UI를 나타내는 개체, scene 에는 ui 하나의 인스턴스를 나타내는 windows와 viewcontroller가 들어있다.
<br>

---
⁉️ **해결하지 못한 질문들**
#### ▶️ 앱이 시작할 때 main.c 에 있는 UIApplicationMain 함수에 의해서 생성되는 객체는 무엇인가? (AppDelegate)
- UIApplication 싱글턴 객체가 생성된다. 
- `delegateClassName: String?` 인걸로 보아 델리게이트 객체는 생성이 될 수도 있고 안될 수도 있는 것 같다.  [UIApplicationMain(_:_:_:_:)](https://developer.apple.com/documentation/uikit/1622933-uiapplicationmain)
- `main.c` : 프레임워크 깊은 곳에서 실행되는 메인 함수 정도로 이해하였다.
<br>

#### ▶️ UIApplication 객체의 컨트롤러 역할은 어디에 구현해야 하는가? (AppDelegate)
정확히 질문의 의미를 파악하지 못하였음.   
AppDelegate나, 그 안에 상태변화 메서드에 구현해야 할까?   

---
---
### **7-3) Autolayout (iOS)**
✅ **문제 & 답변**   
#### ▶️ Intrinsic Content Size에 대해서 설명하시오.
 - 고유의 콘텐츠 크기를 뜻하며 (`UISwitch`나 `UIButton`, `UILabel`, `UITextfield`) 처럼 자신의 content를 기반으로 뷰의 사이즈를 정할 수 있는 것. (`위치=좌표`는 지정해 줘야 한다.)    
 - `UISwitch`처럼 아예 너비, 높이의 기본 사이즈가 정해져 있거나, UIButton의 TitleLabel을 통해 너비와 높이를 유추할 수 있다는 개념이다.     
<br>

🐣 **파생된 질문**    
#### ▶️ 런타임 시 `Button`의 `TitleText`가 바뀌면 `Intrinsic Content Size` 가 자동으로 조절되는 걸까??
- 해당 버튼에 `Top`, `Leading Constraint`만 설정되어 있다면 `TitleText`가 변경될 시 `Intrinsic Content Size`가 자동으로 바뀔 거 같고,   
- `Top`, `Leading`, `Trailing`, `Bottom Constraint` (즉 너비, 높이) 모두 설정되어 있다면 `TitleText`가 변경되더라도 `Intrinsic Content Size`는 변하지 않을 것 같다.   
정확하다기보다는 추측에 가깝고 공식 문서나 정확한 근거를 찾아보자.   
<br>

---
#### ▶️ hugging, resistance에 대해서 설명하시오.
`Content Hugging`
- `Intrinsic Content Size`에 맞게 줄어들려고 하는 힘
- 늘어나지 않으려고 하는 힘
- 컨텐츠보다 더 늘어나지 않으려고 하는 힘. (최대 크기에 대한 제약?)    
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

---
#### ▶️ 오토 레이아웃을 코드로 작성하는 방법은 무엇인가? (3가지)
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

🐣 **파생된 질문**    
#### ▶️ `Layout Anchors`는 `Horizontal - 수평`에 대한 `Constraint`를 설정하는데 `Vertical - 수직`에 대한 `Constraint`를 설정해 주면 자동으로 컴파일 에러를 뱉어준다. 
#### 이것이 `Generic` 기능을 사용했기 때문이라는데 `Generic`이 정확히 어떤 역할을 했기에 가능한 것일까??   
<img src="https://github.com/zziro95/zzipository/blob/main/images/NSLayoutAnchor<AnchorType>.png" width="70%" height="70%" title="NSLayoutAnchor<AnchorType>" alt="NSLayoutAnchor<AnchorType>Img"></img>    

- `Generic`로 만들어진 코드의 `T - Type Parameter`는 동일한 타입이어야 한다.    
- 위의 `NSLayoutAnchor` 정의 코드를 보면 `<AnchorType>`에 수평이면 수평, 수직이면 수직 하나의 타입만 들어올 수 있고, 따라서 수평과 수직 타입이 같이 접근하게 되면 `T`가 동일하지 않기 때문에 올바른 제약이 아님을 확인하고 오류를 검출할 수 있다.       
<br>
<img src="https://github.com/zziro95/zzipository/blob/main/images/[Apple] NSLayoutAnchor.png" width="70%" height="70%" title="[Apple] NSLayoutAnchor" alt="[Apple] NSLayoutAnchorImg"></img>    

- [NSLayoutAnchor 공식 문서](https://developer.apple.com/documentation/uikit/nslayoutanchor)를 보면 유효하지 않은 제약 조건이 생성될 수 있으나 이러한 제약 조건들은 런타임 시에 충돌을 일으킨다고 한다.   
<br>

#### ▶️ `NSLayoutConstraint Class`로 설정해주어야 하는 `NSLayoutAnchor`로는 설정해 줄수 없는 제약사항(한계점)은 어떤 것들이 있을까??
- 답변: 아직 답을 찾지 못함.   
<br>

---
#### ▶️ 스토리보드를 이용했을 때의 장단점을 설명하시오.
`장점`   
- 앱의 흐름이 시각화되어 있기 때문에 보기 편하고 개발자가 아닌 디자이너와 같은 화면을 보며 쉽게 이야기가 가능하다.
- 프리뷰 기능을 통해 빌드 하지 않고 화면 확인 가능하다.   
- 프로젝트가 커질수록, 스토리보드 안에 내용이 많을수록 로딩이 느려진다. (재사용성 과도 연관되는 이야기 일듯)
<br>

`단점`   
- 스토리보드 파일의 포멧이 XML로 되어있어 읽기도 어렵고, 여러 명이 작업을 한다면 Merge Conflict 처리 비용이 크기 때문에 협업에서 사용하는데 어렵다. 
- 스토리보드로 할 수 없는 작업(뷰 계층 구조에 대한 일부 동적 변경 사항)을 해줄 수 있다. (예시는?)   
- 코드로 뷰를 만들면 재사용에 용이한데 스토리보드는 그렇지 않다.    
<br>

🐣 **파생된 질문**    
#### ▶️ 코드나 스토리보드로 오토 레이아웃을 잡았는데 제대로 잡혔는지 어디 잘못 설정돼있는데 곳이 없는지 확인하는 방법을 알고 있나요?
- 런타임 시에 접근할 수 있는 `Debug View Hierarchy`에 접근해 보라색, 노란색, 빨간색 오류들이 있는지 없는지 확인해보기.   
<br>

---
#### ▶️ Safearea에 대해서 설명하시오.
- `StatusBar`, `NavigationBar`, `ToolBar`, `TabBar`등 을 사용하면 화면의 특정 부분을 우선적으로 차지하게 되는데 그런 영역들을 제외한 컨텐츠가 안전하게 보일 수 있음을 보장하는 영역   
> 아이폰 10 이후로 등장한 개념!    
> 홈 버튼 유무, 가로 세로 모드에 따라 영역이 다르다.      
> 나중에 좀 더 자세히 알아보자. [참고하면 좋을 블로그](https://babbab2.tistory.com/134).   
<br>

---
#### ▶️ Left Constraint 와 Leading Constraint의 차이점을 설명하시오.
- 대부분의 언어는 왼쪽에서 오른쪽으로 읽지만 대표적으로 아랍권은 오른쪽에서 왼쪽으로 읽는다.    
    - `Leading and Trailing Constraint`은 국가의 레이아웃이 읽기 방향에 따라 조정되는 제약사항이다.   
- `Left and Right Constraint`은 객체나 화면의 절대적인 방향 왼쪽, 오른쪽을 뜻한다.     
<br>

- 💡 `Auto Layout Guide`에 따르면 `Left and Right Constraint` 사용을 지양하고 `Leading and Trailing Constraint`을 사용할 것을 권장한다.    
- 개발자가 앱의 사용 환경, 상황을 고려하여 읽는 방법에 따라 달라져야 할 제약조건이라면 `Leading and Trailing Constraint`를 고정적, 절대적으로 좌측, 우측에 대한 제약조건을 주어야 한다면 `Left and Right Constraint`를 사용하게 될 것 같다.   
<br>
<br>

---
⭐ **새로 알게 된 내용**   
#### ▶️ `TextView`는 스크롤이 가능하냐 아니냐에 따라 `Intrinsic Content Size`를 가질 수도 있고 아닐 수도 있다.      
- `TextView`의 스크롤 기능이 **꺼져**있다면 텍스트의 길이에 따라서 `Intrinsic Content Size`가 정해지고, (다른 건 고려하지 않고 텍스트의 크기로만 결정된다.)   
- `TextView`의 스크롤 기능이 **켜져**있다면 Intrinsic Content Size가 정해질 수 없다.   
<br>

#### ▶️ `ImageView`의 `Intrinsic Content Size`
- 이미지가 없는 경우는 `Intrinsic Content Size`가 정해질 수 없고,
- 이미지를 있는 경우는 `Intrinsic Content Size`가 이미지의 크기로 설정된다.   
<br>

#### ▶️ Intrinsic Content Size 활용 방법
`Storyboard` > `Size inspector` > `Instrinsic Size` > `Placeholder`를 이용하면 임시적인 높이와 너비 사이즈를 지정해 줄 수 있다.   
스토리보드에서만 적용 가능하고 실제 실행 중에는 역할을 하지 않는다. (스토리보드에서 대략적으로 위치를 놓아볼 때 활용해보면 좋을듯하다.)   
<br>

`@IBDesignable`, Custom Class의 `intrinsicContentSize` 프로퍼티를 이용해 기본 너비, 높이 설정 가능. (`@IBDesignable`에 대해 나중에 글로 정리해 보기 아래 링크도 참고하기)     
- [intrinsicContentSize 관련 참고해보면 좋을 글](https://ios-development.tistory.com/233)
- [invalidateIntrinsicContentSize() 관련 글](https://magi82.github.io/ios-intrinsicContentSize/)
<br>

---
📝 **참고**   
- [Auto Layout Guide (마지막 업데이트 날 짜 - 2016-03-21)](https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/AutolayoutPG/ProgrammaticallyCreatingConstraints.html#//apple_ref/doc/uid/TP40010853-CH16-SW1)
- [[야곰닷넷] 오토레이아웃 정복하기👍](https://yagom.net/courses/autolayout/)   

---
---
### **8-1) Design Pattern 1**
✅ **문제 & 답변**    
#### ▶️ `Singleton Pattern` 을 활용하는 경우를 예를 들어 설명하시오. (Design Pattern)   
`Singleton Pattern`   
- 싱글턴 패턴은 타입을 인스턴스화 시키는 과정을 디자인한 패턴으로 공유하고 싶은 인스턴스를 유일하게 만들 수 있다.   
- `Type Property`를 이용해서 인스턴스를 생성해 주고, `init mehtod`에 접근 제한자를 설정하여 타입 내부에서만 인스턴스화 할 수 있고, 외부에서는 접근할 수 없기 때문에 유일한 인스턴스가 된다.   
- 특정 클래스의 인스턴스가 오직 하나임을 보장 (데이터 공유, 메모리 절약)
<br>

`Singleton Pattern` 을 활용하는 경우   
- 파일시스템, 데이터베이스, 코어데이터 등 디스크 저장소를 공유해서 사용하고 싶을 때 (ex. `FileManager`, `UserDefaults`)
- 네트워크 요청을 그룹화하는 `URLSession`
- 앱의 비동기 작업에 우선순위를 지정하고 순서를 지정, 예약하는 `OpertaionQueue`   
- 현재 실행 중인 응용 프로그램에 대한 접근 `UIApplication`   
<br>

- 싱글턴을 사용하는 코드는 테스트하기 어렵거나 불가능하다. (이외 여러 단점이 있음) 상태값이 글로벌하게 바뀌다 보니까. 싱글턴에 의존하는 코드를
- 📮 그렇다면 올바른 해결 방법은? `dependency injection` 의존성 주입이라는데.. 프로토콜에 대해 정리 후 볼 필요가 있어 보인다. 
- 아래 글에 **"싱글턴 패턴을 사용하지 말고 dependency injection을 사용하여 항상 문제를 해결할 수 있으며 해결해야 합니다."** 라는 의견도 있음.   
[싱글턴 의존성 주입 관련 글](https://matteomanferdini.com/swift-singleton/)   
<br>

🐣 **파생된 질문**     
#### ▶️ 타입 프로퍼티 `static`, `class`  키워드의 차이는?
- 답변: 상속을 할 수 있느냐 없느냐 (상속과 관련) < 근거 문서와 좀 더 자세히 확실한 답변 알아보기

<br>

싱글턴 사용시 주의점?
싱글턴은 어디서든 접근이 가능하다. 멀티 스레딩에서는 스레드 세잎하지 않음 그걸 주의해 줘야한다.   


싱글턴이 처음 사용될 때 메모리가 올라가는데 ARC에 대해서 메모리가 내려갈까? 
ARC가 해주지않을까 했는데 싱글턴은 스태틱으로 하니깐 한번 생성이 되면 앱 자체가 메모리 해제될 때 까지 해제되지 않는걸로 보인다.
static 프로퍼티에 대해서 알아야 해결 가능할 듯

---
#### ▶️ KVO 동작 방식에 대해 설명하시오. (Design Pattern)
- `Key`를 가지고 `Key`에 해당하는 `Value`를 지켜본다
- 특정 프로퍼티의 변화를 실시간으로 감지, 반응하기 위해 옵저빙을 하는 것이다. 
- `addObserver`를 이용해 관찰할 수 있고 `forKeyPath`에는 지켜볼 프로퍼티를 넣어준다. 
- 이전의 값을 지켜보려면 `old`, 변화된 값을 보고 싶으면 `new` 키워드를 사용하면 된다.   
- 하나의 인스턴스의 프로퍼티를 여러 인스턴스에서 지켜볼 수 있다.    
<br>

동작 방식
프로퍼티를 옵저빙하겠다고 마킹
추적할 클래스는 클래스 자체가 nsobject 의 상속을 받아야하기 때문에(클래스 타입만 가능) nsobject 상속하고 
objc dynamic?

스위프트 값타입을 지향하는데 구조체는  KVO를 못하나?
KVO Didset willset

🐣 **파생된 질문**     
#### ▶️ `KVO`와 `NotificationCenter`의 공통점과 차이점은??
**공통점**    
- 인스턴스끼리 서로 알지 않아도 정보를 전달받을 수 있는 방법   
<br>

**차이점**     
의존의 차이라고 말할 수 있을까??   
- `KVO`는 `Key`를 통해서 지켜보겠다 등록을 하면 `Value`가 변했을 때 바로 파악할 수 있는데 
- `NotificationCenter`는 옵저버로 등록을 해도 `NotificationCenter`에서 `post`를 해줘야만 전달받을 수 있다.   
<br>

---
#### ▶️ `NotificationCenter` 동작 방식과 활용 방안에 대해 설명하시오. (NotificationCenter)
**동작 방식**   
- `NotificationCenter`의 `addObserver(_:selector:name:object:) or addObserver(forName:object:queue:using:)`메서드를 이용해서 옵저버로 등록하고, 알림을 받았을 때 실행할 클로저를 선언해 준다.   
- 특정 이벤트 발생 시 `post`메서드를 통해 이벤트를 알린다.   
- post를 통해 전달받으면 우리가 addObserver 메서드의 탈출 클로저에 선언한 작업이 진행된다.   
<br>

**활용방안**   
- 인스턴스 간에 정보를 전달 받고 싶을 때 (구체적인 사례는 잘 생각 안 남)
- ex. 데이터나 이벤트 전달 시 타입 간에 의존성을 줄일 때
- ex. 대용량 파일을 다운로드하는 스레드를 생성하고 다른 페이지에서 다른 작업으로 넘어가도 다운로드 완료 알림 팝업을 띄우기 < [좋은 예 같아서 긁어옴...출처](https://www.notion.so/NotificationCenter-bcb6e10495fb42c1b2c51de6f6936995)
- 객체의 상태가 변한 걸 알고 싶을 때? 그 변한 걸 가지고 작업(Alert을 띄우거나 데이터를 받아와서 처리하거나)을 해주고 싶을 때?
<br>

🐣 **파생된 질문**    
#### ▶️ `removeObserver()`의 올바른 사용법??
- 답변: 사용을 많이 못 해봐서 잘 모르겠다 ㅠㅠㅠ   
<br>

#### ▶️ `addObserver(_:selector:name:object:)`,  `addObserver(forName:object:queue:using:)` 차이??
- 답변: `selector`는 `obj-c` 의 방식이기 때문에 `@objc` 어노테이션이 필요하고, 후자는 스위프트의 탈출 클로저를 이용하는 방식?   
<br>

이기능을 위해서 델리게이션이나 KVO를쓸수잇는데 왜 노티피케이션을 썻나요?
- 노티피케이션은 방송국 처럼 다수의 옵저버들에게 한번에 노티해줄수있다 장점 (간단한 기능에는 안어울린다. )
- Delegate Pattern은 1대1 관계로만 주고 받을 수 있다. 여러곳에서 사용할려면 각각 delegate를 지정해줘야함   NotificationCenter  1대 다에 유리하다.


⭐ **새로 알게 된 내용**   
- `NotificationCenter` `post`시 등록된 `observer` 목록을 검색하므로 앱 속도가 느려질 수 있다고 한다.
- 하나 이상의 `NotificationCenter`를 사용하면 `post` 마다 수행되는 작업이 줄어들어 (작업과 옵저버가 분산되므로?) 앱 전체의 성능이 향상된다.   
[NotificationCenter.default](https://developer.apple.com/documentation/foundation/notificationcenter/1414169-default)   
<br>

---
---
### **8-2) Design Pattern 2**
✅ **문제 & 답변**   
#### ▶️   
🐣 **파생된 질문**    
⭐ **새로 알게 된 내용**   
📝 **참고**   
Protocol - 기능의 요구사항, 청사진, 네이밍은 주로 ~할 수 있다 (형용사) ~able
Type에 프로토콜을 채택하면 프로토콜에 명시된 기능을 정의해야하고, 그것은 타입이 그 기능을 할 수 있음을 의미한다.
Walkable라는 Protocol에 walk라는 func을 명시해놓으면 그 프로토콜을 채택한 타입은 walk()라는 메서드를 구현해야한다.
그런데 Walkable을 채택하지 않고 그냥 walk라는 메서드를 구현하면 되는데 굳이 왜 프로토콜을 만들고 채택을 해주어 사용하는 걸까????
- ㅏㅏㅏ 프로토콜을 명세를 해놓으면 기능을 까먹지 않고 구현할 수 있으니까?? 공통된 기능을 공유하기 위해서?ㄴㄴ이건 아님 (세부 구현은 다름 뒤뚱뒤뚱 걷거나 이롱이롱 걷거나)
- 야곰왈 주스메이커, 커피메이커가 있다고 보자. Makable을 만들어 놓으면 

이 프로토콜을 따르고있다, 채택하고 있다 이 인스턴스는 ~한 기능을 보장해요!

프로토콜이 아닌 쥬스메이커로 샵 타입을 만들면 다 바꿔줘야한다.

프로토콜을 이용하여 타입을 설계하면 프로토콜을 따르는 타입이라면 누구든 역할을 할 수 있게되고
프로토콜을 채택한 타입과 그 타입을 사용하는 타입은 서로의 존재에 대해 모르더라도 문제가 없음. (프로토콜이라는 추상적인 개념으로 연결이 됨) 정의된 타입 내부를 전혀 건들지 않고 새로운 작업을 할 수 있음. 결합도가 낮아짐

프로토콜을 이용하면 타입간의 결합도가 없다.


Delegation Design Pattern
프로토콜이라는 개념을 가지고 응용한 것이 Delegation Design Pattern
사장 - 비서      일을 위임한다.
일을 시키려면 job description 같은 명세서가 필요함

Delegate 패턴을 활용하는 경우의 예
사진앨범, 사장님
화면에 사진앨범을 보여준다.
개발자=우리는 비서역할의 코드들을 구현한다.
마음에 드는 사진을 고르면 -> 새로운 화면에 띄워준다? 같은

아래 코드 이전에 뷰컨에 tavleviewdelegate 채택해줘야함
tableview.delegate = self(뷰컨) 테이블뷰에 발생하는 이벤트들에 대한 처리를 뷰컨에다가 구현해서 처리해주겠음?!

애플은 딜리게이트라는 프로퍼티를 구현
프로그램마다 실행해야할 동작들이 무수히 많고 다르기 때문에 딜리게이트 프로토콜을 구현만 해놓고 내부 구현은 개발자에게 맡김

노티피케이션과 차이점
델리게이트는 1대1 상황 (비서와 사장)1대1의 상황이라고 볼 수 있다.

프로토콜과 딜리게이트 안이어지는 느낌
프로토콜을 채택했을 때 구현하란 경고 메세지가 없다 이런건 어떤 경울까??
- 프로토콜 옵셔널 선택요구사항 , optional func 이였기 때문 쓸꺼면 쓰고 말꺼면 말아라 굳이 구현 안해도된다
- 꼭 구현해야하는건 옵셔널로 하면 안됨 (테이블뷰의 셀수 그런거)
- 스위프트에서는 활용할 수 없다  프로토콜위에 @objc 어노테이션을 붙여줘야 optional func을 명세해줄 수 있다.




#### ▶️ Delegate란 무언인가 설명하고, retain 되는지 안되는지 그 이유를 함께 설명하시오. (Delegation)
 retain 사이클이 발생
 weak으로 하면 안생기지않나

#### ▶️ Delegate 패턴을 활용하는 경우를 예를 들어 설명하시오. (Design Pattern)
뷰를 표시하는 경우 
주로 뷰를 표시하고 그 뷰에 발생하는 여러 상황 이벤트들을 처리하기 위해서 

#### ▶️ Delegates와 Notification 방식의 차이점에 대해 설명하시오. (Design Pattern)
딜리게이트 - 하나만 프로퍼티  1대1로만? 관계가 가능하다 종류마다. 
노티피케이션 - 1대 다 

#### ▶️ 의존성 주입에 대하여 설명하시오. (Dependency Injection)
- 객체를 외부에서 생성해서 초기화를 해주는것
- 런타임때 교체해주기 위해서
- 외부에서 객체를 생성해서 넣어준다?




### **8-3) Architecture**
✅ **문제 & 답변**   
#### ▶️
🐣 **파생된 질문**    
⭐ **새로 알게 된 내용**   
📝 **참고**   
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
