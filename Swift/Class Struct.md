# Class / Struct
### 글 쓰게 된 이유, 목적
프로젝트를 진행하면서 모델 설계를 해야 하고, 객체를 만드는 것이 시작인데 어떤 형태, 타입, 
`Struct` 또는 `Class`로 만들어야하는지 <br>
`Struct` 또는 `Class`를 선택했다면 그 타당한 근거와 이유는 무엇인지 나에게 납득시키고 남에게 설명하기 위해서 글을 정리하게 됬습니다.! <br>
***
구조체와 클래스는 비슷하다고 느껴지지만 다르다고 알고 있고 이 부분부터 정리해나가 보자

### 어떤 점에서 `구조체`와 `클래스`가 비슷하다고 느껴졌는가?
`Person`이라는 타입을 만든다고 했을 때  `Struct`, `Class` 무엇으로 만들어도 상관없다. ~(상황에 따라 그렇지 않겠지만 이 상황에서만 바라보자면)~ <br>
`구조체`와 `클래스`는 객체를 만들 때 만드려는 객체의 공통된, 일반화된 특성과 행위를 담아줄 수 있고, 서로 다른 타입을 담을 수 있다.  <br>
예를 드는게 좀 더 편할것 같다.  <br>
<img src="https://github.com/zziro95/zzipository/blob/main/images/Object.png" width="70%" height="70%" title="object" alt="objectImg"></img>
> 객체에 대한 글을 정리했었지만,, 이 글을 써내려가면서 아직도 정확히 정리되어있지 않았음 느낀다. <br>
> 지금 내가 들었던 고민은 만약 `Person`이라는 타입에 `name`, `age`, `country` 프로퍼티들이 있다면 그것들도 객체인가,,,,이런 고민을 했다... <br>
> 프로퍼티라는 용어를 쓰면서도 이런 생각이 들었다니,..,.  <br>
<br>
다시 정리 해보자면 `Person`은 사람이지만 `찌로`같은 특정한 사람이 아닌 나의 기준에서 일반화한 사람이라는 객체이고, 객체의 특성과 행위를 `Property`와 `Method`로 정의해 놓았다.
<br>
일반화라는것은 서로 다른 개체들로부터 공통된 개념을 추출하는 것이다. <br>
여기서 첫 질문에 대한 답을 쓸 수 있게 된것같다. <br>
`구조체`와 `클래스`는 객체를 일반화 한다는 점에서 비슷한 역할을 한다. <br>

#### Todo
조금은 본격적인 구조체와 클래스의 차이.. init부터,, 어디까지.? 정리해야할까? <br>
싱글턴은 클래스로 만들어야함 // 싱글턴도 정리해야함 <br>
결론적으로 보면 글을 한번에 쓰긴 어려울것 같고.! 쓰면서 등장하는 개념들을 정리하며 완성시키자!! <br>

### 구조체
- 값 타입 (call by value)

### 클래스
- 참조 타입 (call by reference)
<br>
모델을 만들때 가장먼저 고민하는부분 , , 값복사,참조.
wwdc swift퍼포먼스도 제데로 봐보자!

#### 참고
- 야곰 아카데미 수업



글쓰면서 봐야할것 아직안본거임

https://medium.com/macoclock/reference-vs-value-types-in-swift-c1ece75b8a55





타이븡ㄹ 실체화 한것을 인스턴스라고 부른다. 클래스의 인스턴스를 객체라고 한다.

객체글 관련  https://docs.swift.org/swift-book/LanguageGuide/ClassesAndStructures.html

![image-20210418011426460](/Users/jinhochoi/Library/Application Support/typora-user-images/image-20210418011426460.png)

밤 - Swift 문서에 보니까 객체라는 표현을 사용하는 대신에 더 일반화된 표현인 Instance를 사용한다고 나와있네요. 아마도 Instance가 우리말로 개체인거 같습니다..



Bam - 아까 struct, class 관련해서 다시 해봤는데요. struct의 프로퍼티가 struct이고, private(set)이면 스크린샷처럼 에러가 발생합니다.  반면에 프로퍼티가 class이면 private(set)이라도 메서드 접근이 가능합니다.

![image-20210418011851142](/Users/jinhochoi/Library/Application Support/typora-user-images/image-20210418011851142.png)

ㅎㅎ 맞아요~ class는 참조타입이니까 



Jake - class와 struct의 차이에 대해서 좀 더 자세하게 알고싶으면 보는 것을 추천드려요!! 코드리뷰어 분들이 추천해줬어요~~~

https://developer.apple.com/videos/play/wwdc2016/416/

야곰 - ㅎㅎ 저거 꽤 어려워요 20%만 이해해도 좋아요

다 이해하면 더 좋지만 다 못해도 괜찮아요

현업 주니어들도 반이상은 저거 이해하기 어려울거예요



상어블로그 https://shark-sea.kr/m/entry/Swift-%EA%B5%AC%EC%A1%B0%EC%B2%B4%EC%99%80-%ED%81%B4%EB%9E%98%EC%8A%A4-%EC%B0%A8%EC%9D%B4-struct-vs-class

공식문서 https://developer.apple.com/documentation/swift/choosing_between_structures_and_classes



클래스 공부하고 클래스의 상속 클라썸강의 #272보기





스위프트 기본 타입으로는 Int String Struct Class 등이 있다 . false

- Int, String은 기본타입이 맞는데 Struct Class는 객체를 만드를 작업이기때문에 기본타입이 아니라고 알고있다.
- Int, String은 이미 주어진 타입
- Struct Class는 타입을 정의하기 위한 방식이다.
- 
