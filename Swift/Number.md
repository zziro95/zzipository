# Number
### 글 쓰게 된 이유
모델 타입을 구현할 때 프로퍼티들 중에서도 Number에 관한 프로퍼티들의 타입을 정해주는데 혼란을 겪었다.   
그 이유가 정확한 기준이 없기 때문이라고 생각하여 Swift의 여러 Number 관련 타입들을 살펴보며 나만의 기준을 정해보자   
<br>

:bulb: 글을 읽기 전 `Type Safety and Type Inference`에 대한 이해가 필요하므로 [간단하게 정리한 글](https://github.com/zziro95/zzipository/blob/main/Swift/Type%20Safety%20and%20Type%20Inference.md)이 있으니 살펴보고 아래 글을 보면 좋을 것 같다.   

***
### Integers
Integers는 부호가 있는 정수 `signed` (양수, 0, 음수), 부호가 없는 정수 `unsigned` (양수, 0) 가 있다.   
Swift는 8, 16, 32, 64 bit의 `signed`, `unsigned` 정수를 지원한다.   
<br>

**Int**   
*the same size as the current platform’s native word size*   
Swift는 현재 플랫폼 네이티브 사이즈와 같은 Int인 정수 타입을 제공한다고 한다.   
- 32-bit 플랫폼에서 Int는 Int32와 같은 사이즈를 가짐 (범위 -2,147,483,648 ~ 2,147,483,647 )
- 64-bit 플랫폼에서 Int는 Int64와 같은 사이즈를 가짐 (범위 -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807 )     
<br>

요즘 애플은 64-bit이면서 32-bit를 지원하는 형태라고 한다. 나는 64-bit!   
<br>

> Unless you need to work with a specific size of integer, always use Int for integer values in your code.   
[SwiftLanguageGuide](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html)에 따르면 특정 크기의 정수로 작업해야 하는 경우가 아니라면 항상 `Int`를 사용할 것을 권장하고 있다.   
<br>

**UInt**   
Swift에서는 `UnsignedInt`도 지원하고 있다.   
<img src="https://github.com/zziro95/zzipository/blob/main/images/UInt.png" width="70%" height="70%" title="UInt" alt="UIntImg"></img>
<br>

부호가 없는 정수 타입이 필요한 경우에만 사용할 것을 권장한다.   
밑줄 친 부분을 보면 **저장될 값이 음수가 아니더라도 `Int`를 사용하는 것을 선호한다**고 말한다.    

<br>

***
### 소제목
~~

***
### 소제목
~~

***
### 마무리 글
~~

***
### 참고
- [SwiftLanguageGuide](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html)
- [한국어 번역본](https://bbiguduk.gitbook.io/swift/language-guide-1/the-basics)

