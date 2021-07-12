# Result
### 회고시 고칠점
- 글 전체적으로 정돈
- 다 살펴보지 못한 참고 사이트 읽어보기
- 실제로 Result를 사용한 내 사례 코드 넣어보기

***
### 개요
작업(Task) 중에는 실패할 수 있는 작업이 있습니다.   
디스크에 파일을 쓰거나, API를 호출해 네트워크를 통해 데이터를 가져온다거나, 특정 URL에 있는 데이터를 불러오는 작업이 이 경우에 해당합니다.    
이런 실패 가능한 작업을 처리하기 위해 Swift에서는(4.2 이하 버전) `do`,`try`, `catch`,`throws` 문법을 제공했습니다.   
<br>

이 방법은 에러를 런타임에 동기로 자동으로 처리할 수 있게 해주었습니다.    
하지만 이 방법으로는 발생 가능한 여러 가지 예외 상황에 대해 대처하기 어려운 단점이 있었습니다.   
Swift5에서는(SE-0235) 이런 점을 보완해 에러를 보다 유연하게 처리할 수 있는 Result<Value, Error>문법을 지원합니다.   

즉 에러를 비동기로 처리하기가 어렵다.

```swift
func load(then handler: @escaping (Data?, Error?) -> Void) {
    //...
}

load { (data, error) in
    guard error == nil else { handleError(error!) }
    
    guard let data = data else { return } // 이런 경우도 발생할까? 🤔
    // 요청도중에 데이터가 손실되는 경우가 아닐까?
    
    handleData(data)
}
```
하나는 런타임에 error가 nil이라고 할지라도 data가 반드시 존재한다는 보장이 없습니다. 즉, error, data 모두가 nil일 수 있습니다.

다른 하나는 우리가 실제로 에러를 처리하기 위해 필요한 상태(state)보다 더 많은 상태가 생겨 불필요한 상태를 추가로 처리해야 한다는 것입니다. 저희가 처리하고자 하는 실행 결과의 상태는 성공(Success)과 실패(Failure) 딱 두가지 입니다.

하지만 위 경우는 다음과 같이 총 네 가지 발생할 수 있습니다.

Data, Error : True, False
Data, Error : True, True
Data, Error : False, True
Data, Error : False, False
저희가 처리하고 싶은 경우는 1번과 3번 두 가지이지만 실제로는 2, 4와 같은 모호한 상태가 추가되는 것이죠. Result타입을 사용하면 이런 에러 처리를 명확하게 할 수 있습니다.

---
### 상태의 분리 (Separate states)
다음은 Swift5에서 Result 타입의 정의입니다.
```swift
enum Result<Success, Failure: Error> {
    case success(Success)
    case failure(Failure)
}

// 앞의 예제를 Result를 이용해 바꿔보겠습니다.

func load(then handler: @escaping (Result<Data>) -> Void) {
    //...
}

load { result in
    switch result {
    case .success(let data):
        // load된 data 처리
    case .failure(let error):
        // error 처리
    }
}
```
Result를 사용하면 모호한 상태의 처리가 필요 없고 꼭 필요한 상태만 처리하면 되니 보다 명시적이고 간결하게 에러처리를 할 수 있음을 확인할 수 있습니다. Result는 기본적인 사용법 외에 다음과 같이 다양하게 사용할 수 있습니다.



---

### Result의 다양한 사용법
1. 타입 에러 (Typed errors)
앞의 예제 코드에서 error는 Swift의 Error프로토콜을 따르는 모든 형태의 에러가 될 수 있는데, 이 경우 발생한 에러가 어떤 에러인지 정확하기 파악하기 어려운 점이 있습니다. 이 에러를 더 안전하고 정확하게 처리하기 위해 연관된 에러(associated error)를 정의해 사용할 수 있습니다.

앞의 예제 코드에서 error를 정의해 사용해 보겠습니다. Swift의 Error를 따르는(Conform) 열거형 LoadingError 를 선언합니다.
```swift
enum LoadingError: Error {
    case networkUnavailable
    case timedOut
    case invalidStatusCode(Int)
}

```
```swift
typealias Handler = (Result<Data, LoadingError>) -> Void
```
생성한 Handler를 이용해 load 함수를 선언합니다.

```swift
func load(then handler: @escaping Handler) {
        //...
}
```
load 함수의 성공, 실패 처리는 다음과 같이 할 수 있습니다. 에러 발생시 저희가 정의한 에러의 종류에 따라 처리할 수 있습니다.


```swift
load { [weak self] result in
    switch result {
    case .success(let data):
        self?.handle(data)
    case .failure(let error):
        switch error {
        case .networkUnavailable:
            self?.showErrorView(withMessage: .unavailable)
        case .timedOut:
            self?.showErrorView(withMessage: .timedOut)
        case .invalidStatusCode(let code):
            self?.showErrorView(withMessage: .statusCode(code))
        }
    }
}
```
2. Throw 처리
때에 따라서는 작업 결과의 처리를 Switch에서 하지 않고 try, do, catch 에서 직접 결과값을 받아서 처리하고 싶을 때가 있습니다. 이런 경우 성공시 결과값을 반환하고 실패시 throw를 뱉도록 처리도 가능합니다.

```swift
extension Result {
    func process() throws -> Success {
        switch self {
        case .success(let value)
            return value
        case .failure(let error)
            throw error
        }
    }
}

do {
    let result = try value?.process()
    handleValue(result)
}
catch {
    handleError(error)
}
```

3. 지연 처리 (Delayed Handling)
어떤 경우에는 에러처리를 바로 하지 않고 나중에 하고 싶을 때가 있습니다. 다음은 이런 경우에 대해 Result를 사용하지 않고 기존의 방식으로 코딩한 (예) 입니다.


```swift
var configString: String?
var configError: Error?

do {
    configString = try String(contentsOfFile: "myfile.data")
} catch {
    configError = error
}

func doSomethingWithConfig() {
    guard let configString = self.configString else {
        handle(configError)
    }
}
```
이 코드를 Result를 이용하면 클로저를 초기화 파라미터로 사용해 코드를 더 간결히 작성할 수 있습니다.

```swift
let configuration = Result { try String(contentsOfFile: "myfile.data") }

func doSomethingWithCongifg() {
    switch configuration {
    case .success(let success)
        handleSuccess(success)
    case .failure(let error)
        handlError(error)
    }
}
```
4. Result 변형 (Transforming Result)
Result는 map(), flatMap(), mapError(), flatMapError() 함수를 지원합니다. 다음은 Result에서 map()을 사용한 (예) 입니다.

```swift
func generateRandomNumber(maximum: Int) -> Result<Int, Error> {
    //...
}

let result = generateRandomNumber(maximum: 7)
let number = result.map { "Generated Random number is : \($0)" }

// 정의는 다음과 같다.
public func map<NewSuccess>(_ transform: (Success) -> NewSuccess) -> Result<NewSuccess, Failure> { }

public func mapError<NewFailure>(_ transform: (Failure) -> NewFailure) -> Result<Success, NewFailure> { }

public func flatMap<NewSuccess>(_ transform: (Success) -> Result<NewSuccess, Failure>) -> Result<NewSuccess, Failure> { }

public func flatMapError<NewFailure>(_ transform: (Failure) -> Result<Success, NewFailure>
) -> Result<Success, NewFailure> { }
```
***
### 마무리 글
~~

***
### 참고
- [swift-evolution](https://github.com/apple/swift-evolution/blob/master/proposals/0235-add-result.md)
- [참고 블로그!](https://jusung.github.io/Result-%ED%83%80%EC%9E%85/)
- [How to use Result in Swift](https://www.hackingwithswift.com/articles/161/how-to-use-result-in-swift)
- [👍 The power of Result types in Swift](https://www.swiftbysundell.com/articles/the-power-of-result-types-in-swift/)
- [What's new in Swift 5.0?](https://www.youtube.com/watch?v=_Iw4zf8gtqs)
- [Result](https://developer.apple.com/documentation/swift/result)
- [Swift 5 Released](https://swift.org/blog/swift-5-released/)



