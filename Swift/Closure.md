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
클로저가 길어지거나 가동성이 떨어진다고 느낄 때 `Trailing Closure (후행 클로저)`를 사용하면 좋다.   
💡 Swift에서 여러 클로저를 전달인자로 전달할 수 있지만 맨 마지막 전달인자로 전달되는 클로저에만 후행 클로저를 적용할 수 있다.    
예시 코드를 보며 살펴보자.    
```swift
// 하나의 클로저만을 전달인자로 가지는 함수
func someFunctionThatTakesAClosure(closure: () -> Void) {
    // function body goes here
}

// 후행 클로저를 사용하지 않고 함수를 호출하는 경우
someFunctionThatTakesAClosure(closure: {
    // closure's body goes here
})

// 후행 클로저를 사용하여 함수를 호출하는 경우
someFunctionThatTakesAClosure() {
    // trailing closure's body goes here
}
```   
간단한 코드지만 확실히 후행 클로저를 사용할 때 가동성이 좋아짐을 느낄 수 있다.   
`map`, `filter`와 같은 고차 함수를 사용할 때에도 자주 등장한다.    
```swift
// numbers라는 int배열을 String 배열로 변환하는 코드를 보자.

let digitNames = [
    0: "Zero", 1: "One", 2: "Two",   3: "Three", 4: "Four",
    5: "Five", 6: "Six", 7: "Seven", 8: "Eight", 9: "Nine"
]
let numbers = [16, 58, 510]

let strings = numbers.map { (number) -> String in
    var number = number
    var output = ""
    repeat {
        output = digitNames[number % 10]! + output
        number /= 10
    } while number > 0
    return output
}
// strings is inferred to be of type [String]
// its value is ["OneSix", "FiveEight", "FiveOneZero"]
```   
<br>

또한 비동기 처리에서도 많이 사용되는데 비동기 작업이 완료된 후 그에 대한 결괏값을 가지고 다른 처리를 해야 할 때 유용하다.   
```swift
// 서버로 부터 사진 다운로드가 성공되면 completion 클로저가, 그렇지 않은 경우 onFailure 클로저가 실행된다. 
func loadPicture(from server: Server, completion: (Picture) -> Void, onFailure: () -> Void) {
    if let picture = download("photo.jpg", from: server) {
        completion(picture)
    } else {
        onFailure()
    }
}

loadPicture(from: someServer) { picture in
    someView.currentPicture = picture
} onFailure: {
    print("Couldn't download the next picture.")
}
```   
위와 같은 코드를 사용한다면 `성공 / 실패` 두 상황을 모두 처리하는 하나의 클로저를 사용하는 대신 두 상황을 분리하여 상황에 맞게 코드를 명확하게 분리할 수 있는 장점이 있다.   

***
### Capturing Values
글의 초반부에서 나왔던 클로저는 어떤 상수나 변수의 참조를 캡쳐해 저장할 수 있다는 값 획득에 대해서 살펴보겠습니다.   
> The closure can then refer to and modify the values of those constants and variables from within its body, even if the original scope that defined the constants and variables no longer exists.   
"클로저는 상수와 변수를 정의한 original scope이 더 이상 존재하지 않더라도, 자신 내부에서 해당 상수 및 변수의 값을 참조하고 수정할 수 있다." 라고 한다.     
`Capturing Values`의 핵심 문구라고 생각되는 위 문구가 확실히 이해가 가진 않지만 문서의 설명을 천천히 살펴보며 이해해 보자!    
비동기 작업에서 이 개념이 중요하다고 하고, 중첩 함수가 Swift에서 값을 획득하는 가장 단순한 형태라고 한다.   
💡 원본 값이 사라져도 그 값을 캡쳐(획득)? 했기 때문에 클로저의 내부에서 그 값을 사용할 수 있다는 이야긴 것 같은데  잘 이해해 보자.   
```swift
// 중첩 함수란 함수의 내부에서 다른 함수를 호출하는 형태로 된 함수. makeIncrementer()함수 내에서 incrementer()를 호출

// makeIncrementer의 반환 타입은 () -> Int로 Int형의 클로저를 반환한다는 의미이다
func makeIncrementer(forIncrement amount: Int) -> () -> Int {
    var runningTotal = 0
    func incrementer() -> Int {
        runningTotal += amount
        return runningTotal
    }
    return incrementer
}

func incrementer() -> Int {
    runningTotal += amount
    return runningTotal
}
```   
`incrementer` 함수만 따로 보면 `runningTotal`, `amount`라는 프로퍼티가 정의되어 있지 않아 동작할 수 없지만 `makeIncrementer`안에서 처럼 주변에 `runningTotal`, `amount` 변수가 있다면 `incrementer` 함수는 두 변수의 참조를 획득할 수 있다.   
<br>

❓ `incrementer` 함수가 `makeIncrementer` 함수 영역 안에 있고 `makeIncrementer` 영역 안에는 `runningTotal`, `amount` 변수가 있기 때문에 **Swift에 의해서?** `incrementer` 함수가 변수들을 참조할 수 있게 된다.
<br>

incrementer 함수가 두 변수의 참조를 획득하면 makeIncrementer 함수의 실행이 끝나도 사라지지 않는다.   
게다가 incrementer가 호출될 때마다 계속해서 사용할 수 있다.!   
```swift
let incrementByTen = makeIncrementer(forIncrement: 10)

incrementByTen()
// returns a value of 10
incrementByTen()
// returns a value of 20
incrementByTen()
// returns a value of 30
```   
함수는 각각 실행되지만 `runningTotal`과 `amount`가 캡쳐 돼서 변수를 공유하기 때문에 누적된 결과를 확인할 수 있다.
```swift
let incrementBySeven = makeIncrementer(forIncrement: 7)
incrementBySeven()
// returns a value of 7
```   
 `let incrementByTen: () -> Int` , `let incrementBySeven: () -> Int` 타입을 확실히 알고 싶어서 확인해 보았더니 `() -> Int` 로 나온다.   
이것은 상수 클로저? 라고 생각하면 될까? 익숙해질 필요가 있어 보인다.   
같은 중첩 함수를 이용하지만 새로운 클로저를 생성해 주었기 때문에 초깃값이 다름을 알 수 있다.   
💡 결론적으로 봤을 때 `incrementByTen` 과  `incrementBySeven` 함수는 `makeIncrementer`라는 같은 중첩 함수를 이용한다는 것은 동일하지만 서로 할당된 메모리가 다르기 때문에 그 공간에서 공유하는 `runningTotal`과 `amount`의 값은 공유하지 않음을 의미한다.   
<br>

> 만약 클래스 인스턴스의 프로퍼티로 클로저를 할당하고, 그 클로저가 인스턴스 또는 멤버를 참조하여 캡쳐하는 경우 클로저와 인스턴스 사이에 강한 순환 참조가 발생한다고 한다.   
> 강한 참조 순환을 끊기 위해 `Capture lists`라는 개념이 있다.   
<br>

***
### Closures Are Reference Types
오 위에서 살짝 의아하게 느꼈던 부분에 대해서 바로 나왔다.   
`let incrementByTen = makeIncrementer(forIncrement: 10)` 과 같이 상수 클로저를 생성하였고, 클로저를 호출 함으로 `runningTotal`의 값이 계속 변했다.   
그 이유가 함수와 클로저는 참조 타입이기 때문이다.   
<br>

```swift
let alsoIncrementByTen = incrementByTen
alsoIncrementByTen()
// returns a value of 40

incrementByTen()
// returns a value of 50
```   
따라서 위에서 `incrementByTen`을 세 번 호출하여 `runningTotal`의 값은 30 이였다.   
그리고 위 코드와 같이 `alsoIncrementByTen`에 `incrementByTen`을 할당해 주었다.   
이렇게 된다면 클로저는 참조 타입이기 때문에 `alsoIncrementByTen`오 `incrementByTen`는 같은 클로저를 가리킨다는 것이다.   
그러므로 `incrementByTen`이 이미 캡쳐하여 사용하고 있던 `runningTotal`의 값은 30인 상태이고, 위 코드처럼 `alsoIncrementByTen()`, `incrementByTen()`를 순차적으로 실행했을 때 같은 `runningTotal`을 통해 값이 누적되어 40, 50 값이 출력됨을 확인할 수 있다.   

***
### Escaping Closure
비동기 작업으로 함수가 종료되고 난 후 호출할 필요가 있는 클로저를 사용해야 할 때 필요한 개념이 `Escaping Closure (탈출 클로저)`이다.    
클로저를 매개변수로 갖는 함수를 선언할 때 (매개변수 이름: 뒤에 `@escaping` 키워드를 사용하여 클로저가 탈출하는 것을 허용한다고 명시해 줄 수 있다.   
비동기 작업을 하는 경우 비동기 함수가 종료된 후 데이터를 사용해야 하기 때문에 탈출 클로저가 유용하게 쓰인다.   
```swift
// 전달인자로 전달받은 클로저 completionHandler가 함수 외부 completionHandlers 변수에 저장될 수 있다. 

var completionHandlers: [() -> Void] = []
func someFunctionWithEscapingClosure(completionHandler: @escaping () -> Void) {
    completionHandlers.append(completionHandler)
}
```   
<br>

타입 내부 메서드의 매개변수 클로저에 `@escaping` 키워드를 통해 탈출 클로저임을 명시했다면, 클로저 내부에서 해당 타입의 프로퍼티나 메서드 등에 접근하려면 `self` 키워드를 명시적으로 사용해야 한다.   
그 이유는 위와 같이 프로퍼티가 외부의 것인지 아니면 내부의 프로퍼티인지 구분할 수 없기 때문임으로 보인다.   
```swift 
func someFunctionWithNonescapingClosure(closure: () -> Void) {
    closure()
}

class SomeClass {
    var x = 10
    func doSomething() {
        someFunctionWithEscapingClosure { self.x = 100 }
        someFunctionWithNonescapingClosure { x = 200 }
    }
}

let instance = SomeClass()
instance.doSomething()
print(instance.x)
// Prints "200"

completionHandlers.first?()
print(instance.x)
// Prints "100"
```

***
### Autoclosures
~~

***
### 마무리 글
Escaping Closure 부분에서 `self`에 대한 명시에 대한 내용이 나오는데 끝부분까지 집중력 있게 보지 못했다.   
그래서 정리하지 못한 내용이 있는데 계속 끌고 가는 것보다는 다음에 다시 보고 정리하는 방법을 택하기로 했다.   
***
### 참고
- 야곰 - Swift Programming 3판
- [Swift Language Guide](https://docs.swift.org/swift-book/LanguageGuide/Closures.html)
- [Swift Language Guide 번역 자료](https://jusung.gitbook.io/the-swift-language-guide/language-guide/07-closures)
- [[회고할 때 보기]Strong Reference Cycles for Closures](https://docs.swift.org/swift-book/LanguageGuide/AutomaticReferenceCounting.html#ID56)
