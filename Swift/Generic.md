# Generic
### 글 쓰게 된 이유
공부 중 `Generic` 함수, 타입 구현의 필요성을 느꼈고, 앞으로 이와 비슷한 상황이 수없이 발생할 것 같아   
어떤 방향이 더 좋을지 이유를 찾고 시야를 넓히기 위해 글을 정리하게 되었습니다.   
[SwiftProgrammingLanguage](https://docs.swift.org/swift-book/LanguageGuide/Generics.html), `야곰의 SWIFT 프로그래밍 3판` 의 내용을 정리하는 수준의 글입니다.   

***
### Generic Functions
`Generic`을 이용하면 유연하고 재사용 가능한 코드를 작성할 수 있습니다.   
Swift 표준 라이브러리의 대부분이 `Generic`으로 구성되어 있어서 우리가 알게 모르게 제네릭을 사용하고 있었다고 한다.   

간단하게 제네릭의 유연성, 재사용성 등을 체감할 수 있는 공식 문서의 예제를 살펴봅시다.    
```swift
// 두 정수 값을 바꿔주는 함수
func swapTwoInts(_ a: inout Int, _ b: inout Int) {
    let temporaryA = a
    a = b
    b = temporaryA
}

var someInt = 3
var anotherInt = 107
// inout 매개변수에 값을 넘길때에는 &표시를 붙여주어야 합니다.
swapTwoInts(&someInt, &anotherInt)
print("someInt is now \(someInt), and anotherInt is now \(anotherInt)")
// Prints "someInt is now 107, and anotherInt is now 3"
```   
위의 `swapTwoInts` 함수는 두 정숫값만을 바꿔줄 수 있다.   
정수 이외에 부동 소수점 숫자나 문자열 등 같은 기능을 타입이 다르다면? 어떻게 할 수 있을까?   
아마 아래와 같이 `swapTwoStrings`, `swapTwoDoubles`과 같은 함수를 많이 만들 것이다.   
```swift
func swapTwoStrings(_ a: inout String, _ b: inout String) {
    let temporaryA = a
    a = b
    b = temporaryA
}

func swapTwoDoubles(_ a: inout Double, _ b: inout Double) {
    let temporaryA = a
    a = b
    b = temporaryA
}
```   
<br>

기능은 같지만 허용하는 값 타입만 다를 뿐이다.   
이 경우 `Generic`을 이용하면 Swift의 특성인 `Type-Safe` 에 위배되지도 않고 코드의 중복성 제거 및 유연한 함수를 정의할 수 있다.    
`Generic` 적용 함수는 아래와 같다.   
```swift
func swapTwoValues<T>(_ a: inout T, _ b: inout T) {
    let temporaryA = a
    a = b
    b = temporaryA
}
```   
우리가 앞서 `Int`, `String`, `Double` 등 특정 타입을 넣어준 자리에 Type Parameters를 뜻하는 `T`를 넣어준다.    
💡 a와 b는 `T` 타입과 반드시 동일해야 한다. 그 이유는 Swift가 `Type-Safe` 한 언어이기 때문에 다른 타입 간에 서로 값 교환을 할 수 없기 때문이다.   
- `Generic` 함수는 함수의 이름 옆에 `<T>`를 써줘야 하며 Swift에게 함수 정의 내의 placeholder type 이름임을 알려준다.
- `<T>`를 통해 제네릭을 이용한 함수임을 정의했다고 Swift에게 알리는 정도의 의미라고 이해하였고, 실제로도 Swift가 `T`라는 타입을 찾지는 않는다고 한다.
- `Generic` 함수의 타입 `T - Type`은 `Generic` 함수가 호출될 때마다 결정된다.   
<br>

```swift
var someInt = 3
var anotherInt = 107
swapTwoValues(&someInt, &anotherInt)
// someInt is now 107, and anotherInt is now 3

var someString = "hello"
var anotherString = "world"
swapTwoValues(&someString, &anotherString)
// someString is now "world", and anotherString is now "hello"
```   
`Generic` 함수 사용 예를 살펴보면 정말 매력적이라는 걸 알 수 있고, 호출 시 Swift의 `Type Inference` 특성에 의해 알맞은 `T`로 추론된다.   

---
### Type Parameters
제네릭 함수는 주로 `func methodname<TypeParameter>(parameter: TypeParameter)` 와 같은 형식으로 쓰이는데 여기서 `<T>`처럼 `<>`안에 써 주는 것은 큰 의미가 있다기보다는 placeholder의 역할을 한다고 이해했고, `<>`의 네이밍도 중요하겠지만 `<>`자체가 더 중요한 의미라고 생각됐다.   
`<>`안에 하나 이상의 `Type Parameter`를 넣어줄 때는 `,`를 통해 구분해 주면 된다.   
<br>

네이밍에 대해서도 언급해 주네요 살펴보자아.   
보통 `Dictionary<Key, Value>`, `Array<Element>` 와 같이 `Type Parameter` 와 `Genric Type` or `Generic function` 과의 관계를 알려주는 네이밍을 해주는 게 좋다고 한다.   
하지만 서로 간에 설명하기에 적합한 네이밍이 없을 경우에는 `T`, `U`, `V` 와 같은 하나의 문자를 쓴다고 한다.   
💡 `Type Parameter`의 이름은 `Upper Camel Case` 로 지어주고 이 이름은 `Value`가 아니라 `Type`을 의미해야 한다.   

❔ `T`, `U`, `V` 가 어떤 단어의 축약 문자인지, 쓰임새에 따라 다른 단어를 쓰는지?는 알아내지 못했다. 😤    

---
### Generic Types
Swift에서는 `Generic function` 이외에도 `Generic Type`을 직접 정의할 수 있다.   
`Generic`으로 정의된 `Array`, `Dictionary` 같이 모든 타입에서 작동할 수 있도록 `Class`, `Struct`, `Enum` 형태로 정의할 수 있다.    

`Generic Type`을 설명하는 코드 예시로는 `Stack` 구조를 만드는 작업에 대해 보여준다.   
`Stack` 은 한 쪽 끝에서만 자료를 넣고 뺄 수 있는  `Last In First Out` 형식의 자료구조이다.   
```swift
// Generic을 사용하지 않고 Int 값을 넣고 빼는 Stack을 구현한 코드
struct IntStack {
    var items = [Int]()
    mutating func push(_ item: Int) {
        items.append(item)
    }
    mutating func pop() -> Int {
        return items.removeLast()
    }
}
```   
위의 코드도 훌륭하게 작동하는 코드이지만 `Generic Function`과 같이 모든 타입의 값을 넣고 빼는 `Stack` 구조를 정의하는 방법에는 `Type` 자체를 `Generic Type`으로 정의해 주는 방법이 있다.   
```swift
struct Stack<Element> {
    var items = [Element]()
    mutating func push(_ item: Element) {
        items.append(item)
    }
    mutating func pop() -> Element {
        return items.removeLast()
    }
}
```   
`Generic Type`으로 정의해 주는 방법은 타입 이름 옆에 `<Element>`와 같이 관계를 알려줄 수 있는 알맞은 네이밍으로 명시해 준다.   
`Generic`을 쓰지 않고 구현한 코드와 기능적으론 똑같은 역할을 하지만 언제든 원하는 타입으로  `Stack`을 생성하고 값을 `push`, `pop` 할 수 있다.   
<br>

#### Extending a Generic Type
`Generic Type`을 확장할 때 `Type Parameter list` (예시에서는 `Element`)를 제공하지 않아도 된다.   
따로 명시하지 않아도 extesion 구문 안에서 `Type Parameter list` 를 사용할 수 있다.   

```swift
extension Stack {
    var topItem: Element? {
        return items.isEmpty ? nil : items[items.count - 1]
    }
}
```   
<br>

#### Type Constraints
`Generic Function`과 `Generic Type`은 모든 타입을 허용할 수 있도록 해주지만 `Type Constraints`를 적용해 주는 것이 유용한 경우도 있다.   
그 이유는 모든 타입이 아닌 특정 역할을 할 수 있는 타입에게만 해당 기능을 적용할 수 있기 때문이다.   
예를 들면 `Decoding`을 할 수 있는 `Decodable` 프로토콜을 채택한 타입들만을 위한 `Function`, `Type` 을 정의해 줄 수도 있을 것이다.   
위와 같이 **특정 프로토콜을 준수하는 타입**이거나 **특정 클래스로부터 상속되는 타입**들만을 위한 정의를 하는 경우 `Type Constraint`를 해주면 된다.   
```swift
// T -> SomeClass로 부터 상속되는 타입, U -> SomeProtocole을 준수하는 타입
func someFunction<T: SomeClass, U: SomeProtocol>(someT: T, someU: U) {
    // function body goes here
}
```   

---
### Associated Types
프로토콜을 정의할 때 연관 타입 `Associated Type`을 함께 정의하면 유용할 때가 있다.   
`Associated Type`은 프로토콜에서 사용할 수 있는 placeholder 이름이라고 한다.   
`Struct`, `Class`, `Eunm`에서 `<T>`와 같은 역할로 볼 수 있는것 같다.   
```swift
protocol Container {
    associatedtype Item
    mutating func append(_ item: Item)
    var count: Int { get }
    subscript(i: Int) -> Item { get }
}
```   
Container 라는 프로토콜을 정의하는데 `associatedtype`으로 Item을 정의한 것을 볼 수 있다.   
Item은 placeholder 이기 때문에 이 프로토콜과의 관계에 따라 Item 이라는 이름으로 써 준것 같다. (associatedtype T 로 해도 상관없는듯 하다.)   
Item이라는 타입은 존재하지 않는 타입으로 실제로 사용하게 될 특정한 하나의 타입을 의미한다.  
- Container 타입으 새로운 Item을 append 메서드를 통해 추가할 수 있어야 한다.   
- Item의 개수를 확인할 수 있도록 Int 타입의 count 프로퍼티를 구현해야 한다.   
- Int 타입의 index 값으로 특정 index에 해당하는 아이템을 가져올 수 있는 서브스크립트를 구현해야 한다.   
여기서 중요한 것은 Item이 어떤 특정타입이 아닌 모든 타입이 될 수 있다는 것이다. (단, 코드 내부의 Item 타입들은 하나의 동일한 타입이여야 한다.).  
```swift
// 제네릭 타입이 아닌 Int Stack에 Container 프로토콜 채택
struct IntStack: Container {
    // original IntStack implementation
    var items: [Int] = []
    mutating func push(_ item: Int) {
        items.append(item)
    }
    mutating func pop() -> Int {
        return items.removeLast()
    }
    
    // conformance to the Container protocol
    typealias Item = Int
    mutating func append(_ item: Item) {
        self.push(item)
    }
    var count: Int {
        return items.count
    }
    subscript(i: Int) -> Item {
        return items[i]
    }
}

// 제네릭 타입인 Stack에 Container 프로토콜 채택
struct Stack<Element>: Container {
    // original Stack<Element> implementation
    var items: [Element] = []
    mutating func push(_ item: Element) {
        items.append(item)
    }
    mutating func pop() -> Element {
        return items.removeLast()
    }
    // conformance to the Container protocol
    mutating func append(_ item: Element) {
        self.push(item)
    }
    var count: Int {
        return items.count
    }
    subscript(i: Int) -> Element {
        return items[i]
    }
}
```    

Extending an Existing Type to Specify an Associated Type 아래 내용 보기   

---
### 마무리 글
`Generic`을 사용하면 같은 기능을 하는 코드를 👉 모든 타입을 허용하는 하나의 `Type`, `Function`으로 정의해 줄 수 있다.   
`Generic`에 대해 정리하게 돼서 좋았고, 글을 정리하면서 즐겁게 할 수 있었던 이유는 내가 정리했던 기본 개념들이 이 개념을 살펴볼 때 떠올랐고, 그래서 근거 있는 추론을 할 수 있게 되었고, 100%란 수치는 존재할 수 없겠지만 이전의 내가 `Generic`을 50%를 이해할 수 있었다면 여러 가지 개념들을 살펴보고 정리하는 나의 노력 덕분에 60%를 이해할 수 있었다고 체감되었기 때문이다.   
다시 한번 `TIL`과 `회고`의 중요성을 느낄 수 있는 하루였고 꾸준한 내가 되었으면 좋겠다. 💪   
<br>

💧 다음 회고할 때는 `Hashable`, `Equatable`에 대해서 정리 후 다시 문서를 읽어보는 방향으로 진행하는 것이 좋을것 같다.   
***
### 참고
- [SwiftProgrammingLanguage](https://docs.swift.org/swift-book/LanguageGuide/Generics.html)
- `야곰의 SWIFT 프로그래밍 3판`
- [Type Safety and Type Inference 정리 글](https://github.com/zziro95/zzipository/blob/main/Swift/Type%20Safety%20and%20Type%20Inference.md)
- [Associated Types 볼 때 같이 보기](https://kka7.tistory.com/128)
