# ProgrammersLevel1
### 정리하면서 만드는 TO-DO List
- Swift의 Collection Type들을 다시 살펴보고 정리하기 ([참고하기](https://jusung.gitbook.io/the-swift-language-guide/language-guide/04-collection-types))   
- IteratorProtocol ([IteratorProtocol](https://developer.apple.com/documentation/swift/iteratorprotocol))   
- Swift Sequence Collection ([참고하기](https://academy.realm.io/kr/posts/try-swift-soroush-khanlou-sequence-collection/))   
<br>

### x만큼 간격이 있는 n개의 숫자

***

### 직사각형 별찍기
- 나의 풀이
```swift
let asterisk: String = "*"

private func printAsteriskSquare() {
    for _ in 1...b {
        print(String(repeating: asterisk, count: a))
    }
}

printAsteriskSquare()
```   
<br>

코드만 보면 아주 무난하게 푼듯 하지만 그렇지 않지이   
아래의 코드를 먼저 작성하고, 아주 별로라(중첩 for 문도 아님 ㅋㅋㅋ) 다른 방법을 찾아보고 위의 코드가 나왔다   
위의 코드도 좋다고 생각이 들진 않지만 아래 코드보단,,.   
코딩테스트가 필요없단 생각도 있었고, 하기 싫었지만.. 컴퓨터적 사고?를 하는데 은근 도움이 되는것 같다    
그리고 이쪽으로 내가 많이 부족함을 느낀다💪     
아래 코드는 박제   

```swift
var asterisk: String = ""
private func printAsteriskSquare1() {
    for _ in 1...a {
        asterisk += "*"
    }
    
    for _ in 1...b {
        print(asterisk)
    }
}
```   
- 알게 된 내용   
`String` [init(repeating: count)](https://developer.apple.com/documentation/swift/string/2427723-init)   
어려운 내용도 아니고 써봤던 이니셜라이저이지만 생각이 나지 않았으니 몰랐던걸로 하자   
겸사 겸사 다른 타입의 비슷한 이니셜라이저를 찾아보자   
<br>

`Array` [init(repeating: count:)](https://developer.apple.com/documentation/swift/array/1641692-init)   
`Array`에도 비슷한 이니셜라이저가 있다.   
`init(repeating repeatedValue: Element, count: Int)` 이니셜라이저를 보면 `String`의 경우 `repeatedValue: String`인데 `Element`라고 되어있다.   
[Element](https://developer.apple.com/documentation/swift/sequence/2908099-element)는 `associatedtype`으로 `Element`는 플레이스홀더로 타입 정의시 구체적인 타입을 지정하면 되고, 문서를 보면 나와있겠지만 `where Self.Element == Self.Iterator.Element` 타입 제약이 걸려있다.   
💡 **`Element`가 순회할수 있어야 한다는 제약인가 (확실하게 이해하지 못해 `IteratorProtocol`과 컬렉션 타입에 대한 공부가 필요해보인다!)**   

- 다른 사람들의 풀이   
주로 중첩 포문에 `print("*", terminator: "")`를 많이 사용하였군   
<br>

음 간결한 문제 풀이도 중요하지만 다음 문제 풀이에는 읽기 좋은 코드를 짜는 부분도 생각하며 풀어보자.     
***
