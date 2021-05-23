# Type Safety and Type Inference
### 글 쓰게 된 이유
[Number]() 글을 정리 중에 이해해야 할 개념이라 먼저 살펴보고 정리하기로 하였다..   
레고.   

***
### Type Safety and Type Inference
[Type Safety and Type Inference](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html#ID322)를 토대로 정리해 보았다.   
<br>

#### Type Safety
Swift는 Type Safety (형식이 안전한?) 언어라고 한다. 
코드에 `String`이 필요한 곳에 실수로라도 `Int`, `Double` 등 과 같은 다른 타입을 전달할 수 없고,  코드에서 사용할 수 있는 값 유형에 대해 명확하게 알려준다.   
<br>

Swift는 `Type Safety`한 언어이기 때문에 코드를 컴파일 할 때 type check를 수행하고, 일치하지 않는 타입을 에러로 표시한다.   
이를 통해 개발 프로세스에서 빠르게 오류를 포착하고 수정할 수 있게 지원해주는 역할을 한다.   
<br>

그러나 상수와 변수에 type을 지정하지 않은 경우에는 Swift가 `Type Inference`(Type 추론)을 사용하여 적절한 type을 찾는다.   
<br>

#### Type Inference
컴파일러는 사용자가 작성한 코드를 컴파일할 때, `Type Inference` 기능을 통해 특정한 표현식에 담긴 값을 자세히 살펴봄으로써 해당 값의 타입을 자동으로 추론한다.   
`Type Inference` 덕분에 Swift는 C 또는 Objective-C 언어 보다 타입 선언의 필요성이 적다.   
상수 또는 변수인지는 명확하게 표현해야 하지만 타입에 대해서는 명시하지 않은 경우 자동으로 추론한다.   
<br>

내가 Xcode를 통해 상수 또는 변수를 선언할 때 type을 명시하지 않은 경우가 꾀 있었는데, 초기값(initial value)를 제공했기 때문에 자동으로 type이 추론되었던 것이였다.   
<br>

예시 코드를 살펴보자.   
```swift
let meaningOfLife = 42
// meaningOfLife is inferred to be of type Int

let pi = 3.14159
// pi is inferred to be of type Double

let anotherPi = 3 + 0.14159
// anotherPi is also inferred to be of type Double
```   
코드로 살펴볼 수 있듯이 type을 명시해 주지 않아도 컴파일시 알맞은 유형으로 `Type Inference`가 됨을 알 수 있다.   

---
### 마무리 글
Type Inference 개념에 대해 살펴볼 때 `literal`, `literal value`라는 개념이 나왔는데 문맥상 **코드를 작성할 때 사용자가 직접 입력하는 값** 정도로 이해했고 따로 정리가 필요할 것 같다.   
잊지 말고 정리하도록 하자!    

***
### 참고
- [Type Safety and Type Inference](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html#ID322)
