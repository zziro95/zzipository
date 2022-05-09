# UIViewRepresentable
### 글 쓰게 된 이유
`SwiftUI` 만으로 개발을 하기엔 구현하기 어려운 부분들이 아직 많다.    
`SwiftUI`의 시대가 올 것이라고 생각하지만 아직은 `UIKit`과 함께 사용할 수밖에 없는 현실이지 않을까?   
요런건 나중에 생각하고 공부부터 합시당   
공식 문서 토대로 정보를 정리하고 알게 된 내용을 정리한 글입니다.   

***
### UIViewRepresentable
[공식문서](https://developer.apple.com/documentation/swiftui/uiviewrepresentable)를 살펴보면 `UIKit`를 `SwiftUI` 뷰 계층에 통합시키기(integrate) 위해 사용하는 `UIKit` 뷰를 위한 래퍼라고 설명되어 있다.   
간단하게 말하자면 `SwiftUI`시스템 환경에서 `UIKit`의 뷰들을 사용하고 싶을 때 이 프로토콜을 채택하여 `UIKit` 뷰를 한 번 감싼 새로운 타입을 만들어서 사용하면 된다.    
<br>

프로토콜을 채택하여 만든 `UIView`는 생성, 업데이트 프로세스가 `SwiftUI` 뷰와 유사하게 동작하며, `SwiftUI`가 그렇듯 (선언적) 앱의 현재 상태 정보로 뷰를 구성한다.   
<br>

💡**이 부분은 아직 온전하게 이해하지 못한 부분이다 미래의 나에게 질문을 던져놓자**.  
> Use the teardown process to remove your view cleanly from your SwiftUI. For example, you might use the teardown process to notify other objects that the view is disappearing.   
`teardown process`를 사용하여 `SwiftUI`에서 뷰를 깔끔하게 제거하라고 한다.   
예를 들어 `teardown process`를 사용하여 뷰가 사라지고 있음을 다른 객체에 알릴 수 있다고 한다.    
<br>

💡`teardown process`  무언가를 완료하고 정리하는 작업을 의미하는 teardown, 이 글이 말하는 건 시스템 내부적으로 돌아가는 teardown 프로세스를 뜻하는 걸까?? teardown을 사용해서 뷰를 깔끔하게 제거하라는 말의 의미가 뭘까?!   
<br>

**UIViewRepresentable 를 통해서 만들어준 뷰는 시스템에 의해 적절한 시간에 뷰를 만들고 업데이트 해준다고 한다**   
⭐ 그 시스템은 뷰에서 발생하는 변경 사항을 SwiftUI Interface의 다른 부분에 자동으로 전달하지 않는다.   
→ 만들어준 뷰가 다른 SwiftUI 뷰들과 상호작용을 용이하게 하기 위해서는 `Coordinator`라는 인스턴스를 제공해야 한다. (`must`)   
`Coordinator`를 사용해서 `target-action`을 전달하고 모든 `SwiftUI` 뷰로 메시지를 위임한다.   
`Coordinator`에 대해서는 `UIViewRepresentable`의 필수 구현 메서드부터 살펴보고 알아보자!   
<br>

***
### Creating and Updating the View
#### makeUIView(context:)
- [makeUIView(context:)](https://developer.apple.com/documentation/swiftui/uiviewrepresentable/makeuiview(context:))메서드는 뷰 개체를 만들기 위해 필수로 구현해야 하는 메서드이고 뷰 개체를 만들고 초기 상태를 구성하는 메서드이다.    
- 시스템은 뷰를 처음 생성할 때 이 메서드를 **한 번만** 호출한다.
- ⭐ 만들어진 이후의 모든 후속 업데이트에 대해서 시스템은  [updateUIView(_:context:)](https://developer.apple.com/documentation/swiftui/uiviewrepresentable/updateuiview(_:context:))를 호출한다.
<br>

파라미터와 반환 타입도 살펴보자.      
파라미터로는 `context: Self.Context`라는 Type Alias 타입을 받고 `UIViewType`이라는 타입으로 반환한다.    
파라미터로 받는 `context`는 시스템의 현재 상태에 대한 정보를 포함하는 컨텍스트 구조이다.   
반환 타입은 `UIViewType`은 `associatedtype`으로
<br>


***
### 소제목
~~

***
### 마무리 글
~~

***
### 참고
- [UIViewRepresentable](https://developer.apple.com/documentation/swiftui/uiviewrepresentable)
- [makeUIView(context:)](https://developer.apple.com/documentation/swiftui/uiviewrepresentable/makeuiview(context:))
