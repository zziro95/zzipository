# Functions
### 글 쓰게 된 이유
[Closure](https://github.com/zziro95/zzipository/blob/main/Swift/Closure.md)의 Capturing Values 부분 정리 중 함수 객체를 반환하는 내용이 나왔고 관련 내용을 먼저 살펴보고 오기 위해 Function에 대해 정리하는 글을 쓰게 되었습니다.   

***
### 소제목
~~

***
### Function Types as Return Types
함수 유형을 다른 함수의 `Return Type`으로 사용할 수 있다.   
리턴 화살표 `->` 뒤에 함수 유형을 적어 주면 된다.   
예제 코드와 함께 이해해보자.   
```swift
// input 값에 +1을 더한 값, 1을 뺀 값을 리턴해주는 stepForward, stepBackward 함수가 있다. 

func stepForward(_ input: Int) -> Int {
    return input + 1
}
func stepBackward(_ input: Int) -> Int {
    return input - 1
}

// 반환 유형이 (Int) -> Int인 chooseStepFunction 이 있다.
// backward: Bool 값이 True, False 냐에 따라 stepBackward, stepForward 메서드가 반환된다.
func chooseStepFunction(backward: Bool) -> (Int) -> Int {
    return backward ? stepBackward : stepForward
}

// chooseStepFunction의 리턴 함수 설정과, 적절한 조건식을 사용하여 어떤 값이든 0에 가까워진다.
var currentValue = 3
let moveNearerToZero = chooseStepFunction(backward: currentValue > 0)
```   
위의 `chooseStepFunction`과 같은 함수 유형을 반환하는 함수를 이용하여 원하는 구현을 할 수 있다.   
<br>

😅 반환 타입으로 함수 유형을 써본 기억이 딱히 떠오르지 않는다.   
함수를 정의할 때 반환 타입에 대해서 생각을 많이 하게 되는데 함수 유형을 어떻게 활용할 수 있을지에 대해서도 자주 생각해 보자.   

***
### 소제목
~~

***
### 마무리 글
~~

***
### 참고
- [Swift Language Guide](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID177)
- []()
- []()
