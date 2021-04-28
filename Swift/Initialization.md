#  Instance / Initialization
### 글 쓰게 된 이유, 목적
타입을 만들고 생성하는 과정에서 초기값을 설정해주어야 할 때가 있다. <br>
`Initialization`를 만들어주지 않아도 되는 상황도 있고, 다양하게 만들어서 여러 상황에 대처할 수도 있도록 해줘야 하는 경우들도 있었다. <br>
`init`에 대해 살펴보고 적절히 활용해보자! <br>
***
### Instance (인스턴스)
인스턴스는 `Class`, `Struct`, `Enum`를 실제로 사용하기 위해서 생성된 객체를 뜻한다. <br>
객체라는 표현을 주로 써서 인스턴스란 표현이 잘 입에 붙지 않는데 <br>
선언한 타입을 사용하기 위해 `초기화` 과정을 거쳐 생성된 객체가 인스턴스라고 이해하였다. <br>

인스턴스는 생성된 객체이니 당연히 생성하는 과정이 있어야 겠죠? 그 과정이 초기화라고 보면 될 것 같다. <br>
```swift
/* 
struct로 선언된 Dog라는 타입을 미리 간단하게 선언해 두었고,
이 타입이 이 글의 예시가 되어줄 것이다. 
*/
struct Dog {
    var name: String
    var age: Int
    let breed: String
}
```
<br>
### Initialization (초기화)
`Initialization`이란 사용할 `Class`, `Struct`, `Enum`의 인스턴스를 준비하는 프로세스이다. <br>

타입에 init메서드를 선언해준다. 파라미터에 기본값을 넣어줄수도있고ㅡ 경우가 엄청 많네




초기화하는 작업에는 모든 프로퍼티에 유효한 값을 할당해주어야 한다.

String타입인데 Int를 넣어주면 안된다는것이다. 


 - 인스턴스
인스턴스의 생성
```swift
이런식으로 생성을 하고 내가 자주 썻던 ()는 초기화작업이였음을 알수있따.
위의 코드는 초기값을 아무것도 주지 않은것이고 아래코드는 초기값을 각각 설정해준것이다
```

프로세스,,,

#### 참고
- [Swift Language Guide](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html, "swift")
- [Swift - 인스턴스의 생성과 소멸](https://www.youtube.com/watch?v=E2Yy3gp9_Nk, "Instance")
- 스위프트 프로그래밍 3판 - yagom


