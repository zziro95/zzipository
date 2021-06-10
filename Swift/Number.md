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
값의 범위는 0 ~ 18,446,744,073,709,551,615 이다. (64-bit 기준)   
<img src="https://github.com/zziro95/zzipository/blob/main/images/UInt.png" width="70%" height="70%" title="UInt" alt="UIntImg"></img>
<br>

부호가 없는 정수 타입이 필요한 경우에만 사용할 것을 권장한다.   
밑줄 친 부분을 보면 **저장될 값이 음수가 아니더라도 `Int`를 사용하는 것을 선호한다**고 말한다.    
- 정수값에 `Int`를 일관되게 사용하면 코드 interoperability(상호 운용성)을 돕는다.
- `Type Safety and Type Inference`에 설명된 대로 서로 다른 Number Type 간에 변환할 필요가 없다.
- `Int` 타입을 사용함으로써 정수형 타입의 추론에도 도움이 된다.   

***
### Floating-Point Numbers
Floating-Point Numbers(부동 소수점 숫자)는 분수 성분을 가진 숫자를 뜻한다.   
정수 타입의 값 범위보다 더 넓은 범위의 표현이 가능하다.   
- `Double` 은 64-bit 부동 소수점 숫자를 표기
- `Float` 는 32-bit 부동 소수점 숫자를 표기   
>  `Double`은 최소 15자리의 소수점 정확도를 가지고 있고, `Float`는 6자리의 소수점 정확도를 가지고 있다.   
> 코드에서 작업해야 하는 값의 특성과 범위에 따라 적절한 타입을 골라야 하지만 `Double`이 더 선호 된다고 한다.   
<br>

***
### 정리
1. 우선 다뤄야 하는 값의 특성과 범위를 고려해야 한다.   
2. 그 근거에 따라 `Integers`와 `Floating-Point Numbers` 중 어느 숫자 형식을 쓸 건지 정한다.   
3. `Integers`의 경우 음수가 아닌 0과 정수만을 표현할 때 `UInt`를 쓰지만, `코드 상호 운용성` 과 `Type Safety and Type Inference`가 가지는 이점이 더 크기에 저장될 값이 음수가 아니더라도 `Int` 사용을 권장한다.
4. `Floating-Point Numbers`를 사용할 경우 어느 정도의 소수점 정확도가 필요한지에 따라 `Double`과 `Float` 중에서 선택해 줄 수 있지만 `Double`이 더 선호된다.   
<br>

확실히 정리를 하고 나니 `Number`와 관련된 Property의 Type을 어떤 기준으로 선언할지 기준이 잡히게 되었다.   
지금이라도 기준이 생기게 돼서 기분이 좋다.   
다른 주제들도 좀 더 깊게 생각하는 계기가 될 것 같다.   

***
### 참고
- [Swift Language Guide](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html)
- [한국어 번역본](https://bbiguduk.gitbook.io/swift/language-guide-1/the-basics)
