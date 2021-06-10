# Closure
### 글 쓰게 된 이유
Swift 5.0부터 사용할 수 있는 `Result`에 대해 정리하던 도중 탈출 클로저에 대한 온전한 이해가 필요해서 정리를 하게 되었습니다.   
우선적으로 필요한 부분만 쏙 빼먹고 나중에 다시 돌아와 추가적으로 정리를 해보려 했는데 [Swift Language Guide](https://docs.swift.org/swift-book/LanguageGuide/Closures.html)를 슥 살펴보니 Swift를 다루는데 Closure에 대해 잘 모른다는 게 치명적일 거란 생각이 들어 늦었지만 전체적으로 살펴봐야겠군용.   
역시 배움에는 지름길은 없다 😅   
기본을 더 충실히 💪   

***
### Closure
클로저는 간단하게 보자면 코드 블럭이다.    
`C`와 `Objective-C`의 `블럭(blocks)`과 다른 언어의 `람다(lambdas)`와 비슷하다고 합니다.   
클로저는 어떤 상수나 변수의 참조를 캡쳐해 저장할 수 있다고 합니다. (캡쳐에 대한 내용은 잘 모르겠으나 획득?이라는 표현에 가까운 것 같다. [Swift Language Guide](https://docs.swift.org/swift-book/LanguageGuide/Closures.html) 문서의 아랫부분에서 다뤄 준다고 한다.).  
<br>

클로저는 일정 기능을 하는 코드를 하나의 블록으로 모아놓은 것!이라고 합니다. (`야곰`의 설명은 정말 잘 와닿게 표현해 준다.)   
그러니 함수도 클로저의 한 형태라고 볼 수 있습니다.   
전역 함수(global functions), 중첩 함수(nested function)도 클로저의 특별한 경우라고 합니다.   
<br>

클로저는 다음 세 가지 형태 중 하나를 가집니다.   
- 전역 함수: 이름이 있고 어떤 값도 획득하지 않는 형태
- 중첩 함수: 이름이 있고 관련한 함수로부터 값을 획득할 수 있는 클로저
- 클로저 표현: 이름이 없고 관련된 문맥으로부터 값을 획득할 수 있는 축약 문법으로 작성된 형태.  
<br>

클로저의 문법은 상황에 따라 축약도 많이 되고, 문맥을 통해 타입의 유추도 가능하기 때문에 여러 형식으로 작성된다.   
Swift에서 클로저가 중요한 만큼 클로저로 표현된 코드를 제대로 해석할 줄 모른다면 개발에 많은 어려움이 있을 것이다.   
<br>

Swift의 `Closure` 표현식은 간단하고 깔끔한 구문을 장려하기에 장려하는 표현 스타일을 살펴보자.   
- 문맥을 통해 `parameter type`, `return type`을 유추할 수 있기에 생략이 가능하다.
- 클로저에 한 줄의 표현만 들어있을 경우 암시적으로 이를 반환 값으로 취급한다.
- 축약된 전달인자 이름을 사용할 수 있다.
- 후행 클로저 (Trailing Closure) 문법을 사용할 수 있다.   
<br>

문서의 시작 부분부터 머리가 얼얼하다.   
❄️ focus,,       
<br>

클로저의 표현 방법은 클로저의 위치를 기준으로 기본 클로저 표현, 후행 클로저 표현으로 나눌 수 있다.   
기본 클로저 부터 예시 코드와 함께 살펴보자.   
```swift
// 정렬에 사용될 배열
let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]

/* 
알파벳에서 >의 의미는 알파벳순으로 뒤에 있다는 것을 의미한다.
따라서 backward는 영단어가 들어있는 배열을 역순으로 만들수 있게 해준다.
*/
func backward(_ s1: String, _ s2: String) -> Bool {
    return s1 > s2
}
var reversedNames = names.sorted(by: backward)
// reversedNames is equal to ["Ewa", "Daniella", "Chris", "Barry", "Alex"]
```   
> 함수를 메서드의 전달인자로 보낸다, 함수형 프로그래밍 패러다임에서는 아주 당연한 일   
<br>

클로저의 표현에 대해 살펴보고 표현을 통해 코드를 조금 더 간결하게 표현해보자.   
```swift
// 클로저의 표현
{ (paremeters) -> return type in
    statements (실행 코드들)
}

// sorted(by: )에 전달인자로 클로저를 직접 전달하는 방식
reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in
    return s1 > s2
})
```   
클로저의 매개변수와 반환 타입은 위의 backward 함수의 선언과 같다.   
`names.sorted(by: backward)` 이렇게 코드를 작성하는 경우는 반복해서 같은 기능을 사용하는 경우에 용이할 것이고.   
`sorted(by: )`의 전달인자로 클로저를 전달하는 경우에는 직관적이고 `backword`라는 함수가 어떻게 구현되어 있는지 찾아다니는 수고를 하지 않아도 된다는 장점이 있다.   
<br>

#### 좀 더 간결한 축약 표현
**Inferring Type From Context (문맥에서 타입 추론)**   
Swift 라이브러리의 `sorted(by:)`를 살펴보면 `public func sorted(by areInIncreasingOrder: (Element, Element) -> Bool) -> [Element]` 와 같이 구현되어 있다.   
매개변수에 문맥상 같은 타입의 두 전달인자가 들어오고 이것을 비교한 뒤 `Bool` 타입으로 반환한다는 것을 알고 있다.   
따라서 타입 추론이 가능하므로 타입을 생략한 표현이 가능하다.   
하지만 코드의 모호성이 생길 수 있으므로 타입을 명시해 주는 것은 각자의 기준에 따라 달라질 것 같다.      
```swift
// 문맥을 통한 타입 추론이 가능하기 때문에 더 간결해진 클로저 표현
reversedNames = names.sorted(by: { s1, s2 in return s1 > s2 } )

// 단일 클로저 표현에서 return 키워드 생략 가능
reversedNames = names.sorted(by: { s1, s2 in s1 > s2 } )

/* 
인자 이름 축약 (인자 값은 순서대로 $0, $1, $2와 같이 표현 가능)
축약 인자 이름을 사용하면 인자 값과 그 인자로 처리할 때 사용하는 인자가 같다는 것을 알기 때문에  ㅑㅜ zldnjem todfir rksmd
*/
reversedNames = names.sorted(by: { $0 > $1 } )

// 연산자 메서드를 통해 더 줄일 수 있다고 합니다.
reversedNames = names.sorted(by: >)
```   

***
### Trailing Closure


***
### 소제목
~~

***
### 소제목
~~

***
### 소제목
~~

***
### Escaping Closure
비동기 작업으로 함수가 종료되고 난 후 호출할 필요가 있는 클로저를 사용해야 할 때 필요한 개념이 `Escaping Closure (탈출 클로저)`이다.    
클로저를 매개변수로 갖는 함수를 선언할 때 (매개변수 이름: 뒤에 `@escaping` 키워드를 사용하여 클로저가 탈출하는 것을 허용한다고 명시해 줄 수 있다.   
비동기 작업을 하는 경우 비동기 함수가 종료된 후 데이터를 사용해야 하기 때문에 탈출 클로저가 유용하게 쓰인다.   

***
### 소제목
~~

***
### 마무리 글
~~

***
### 참고
- 야곰 - Swift Programming 3판
- [Swift Language Guide](https://docs.swift.org/swift-book/LanguageGuide/Closures.html)
- []()
- []()
