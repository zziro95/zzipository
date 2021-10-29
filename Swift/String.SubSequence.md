# String.SubSequence
### 글 쓰게 된 이유
최근 들어 공부 내용을 정리하지 않고 있다.    
노션에 더미 데이터 마냥 지저분하게 쌓여있기만 하고, 글을 정리하지 않았다.   
맞다 이것은 반성의 글이다 ㅎㅎ   
꾸준하다는 것은 정말 어렵지만 꾸준함이 무너졌을 때 놓지 않고 꾸준히 하려는 마음가짐도 중요하다고 위안하며 다시 글을 써보려 한다.   
<br>

요즘 들어 `String`과 `Array`를 잘 다루지 못하는 것이 나의 발목을 자주 잡곤 했다.   
그러다가 결국 `String.SubSequence`가 뭐지?에서 이 글을 쓰게 되었다.   
`String`에 대해 공부할 내용은 많겠지만 조각을 작게 나눠 부분 부분 알아가자!   

---
### String.SubSequence
사실 요 타입은 내가 `.split()` 메서드를 접하게 된 타입이다.   
애플 문서 [String.SubSequence](https://developer.apple.com/documentation/swift/string/subsequence)로 살펴보니 `typealias` 였고 `Substring` 타입임을 알게 되었다.   
<br>

`typealias`란 이미 존재하는 데이터 타입에 별칭을 붙일 때 사용하는 키워드이다.   
굳이 키워드까지 써가며 별칭을 붙이는 이유는 이해하기 쉽게 좋은 가독성의 코드를 만들기 위함도 있을 것이다.   

---
### SubString
다시 돌아와서, 그렇다면 이제 어렵지 않다 `SubString`에 대해 살펴보겠다.   
`SubString`은 문자열의 조각으로  `.split()`, `.prefix()`와 같은 메서드의 반환 타입이기 때문에 자주 만난다.  
`String`에서 쓸 수 있는 메서드들의 대부분을 가지고 있기 때문에 불편함 없이 사용할 수 있다.   
<br>

항상 이해하기 어려운 것들은 노란 박스에 담겨있지만 살펴보자.   
> Important
> Don’t store substrings longer than you need them to perform a specific operation.A substring holds a reference to the entire storage of the string it comes from, not just to the portion it presents, even when there is no other reference to the original string. Storing substrings may, therefore, prolong the lifetime of string data that is no longer otherwise accessible, which can appear to be memory leakage.   
<br>

작업을 수행하는 데 필요한 것보다 더 긴 부분의 문자열을 저장하지 말라는 내용이다.    
내가 이해한 바로는 원래 문자열이 있고, 어떠한 조건으로 자른 문자열이 있을 것이다.    
그러나 그 조건에 의해 잘린 `substring`은 원래 문자열의 부분이 아닌 전체 저장소에 대한 참조를 보유한다.   
`substring`을 저장하면 더 이상 접근할 수 없는 문자열 데이터의 수명도 연장되어 메모리 누수가 생길 수 있다는 의미이다.   
<br>

어느 정도 이해는 가지만 완벽히 이해 가지는 않는 문구이다.   
메모리에 대해서도 많은 공부가 필요해 보인다.ㅠ.   
<br>

살펴보던 와중 이해가 부족했던 부분이 [도미닉의 글](https://appleceo.github.io/2019/06/20/substring/)을 보고 확실히 이해되었다.   
이렇게 몰래 도움을 받아 버렸다~🙇   

---
### 마무리 글
결과적으로 내가 궁금해했던 `String.SubSequence`은 `SubString`의 `typealias` 였다는 것을 알게 되었고, 새로운 것들을 알게 되었다.  
<br>

```
let rawInput = "126 a.b 22219 zzzzzz"
var numericPrefix = rawInput.prefix(while: { "0"..."9" ~= $0 })
// numericPrefix is the substring "126"

numericPrefix = rawInput.prefix(while: { "0"..."3" ~= $0 })
// numericPrefix is the substring "12"
```   
그리고 애플 문서를 보다가 재미난 코드를 보았다.   
`numericPrefix`는 0~9를 포함하는 `Substring`을 반환한다.   
정연 팀장님을 통해 접한 `~=` 키워드를 봐서 반갑기도 했고, 코드를 읽어 보면 별거 아닌 것 같아 보여도 이것을 어떻게 활용하느냐에 따라 코드의 가치는 커질 것이다.   
그렇다는 건 많은 메서드를 사용해 보고, 접해보고 여러 방향으로 생각해 보는 것이 중요하겠다.   
<br>

간단하지만 간만에 글을 정리해서 기분이 좋았고, `numericPrefix` 아주 명확한 네이밍에 박수를 치며 글을 마친다.   

---
### 참고
- 야곰 - Swift Programming 3판
- [Dominic`s  Blog 🍎CEO](https://appleceo.github.io/2019/06/20/substring/)
- [[Apple] String.SubSequence](https://developer.apple.com/documentation/swift/string/subsequence)
- [[Apple] Substring](https://developer.apple.com/documentation/swift/substring)
