# Property
### 글 쓰게 된 이유
구조체, 클래스, 열거형에서 타입과 연관된 값들을 표현할 때 프로퍼티라는 걸 사용한다.   
연산 프로퍼티와 지연 저장 프로퍼티 등 자세하게 알지 못하는 부분이 꽤 있다.   
스위프트 문법은 여러 번 살펴보며 익혀야 한다.   
오늘은 전체적으로 슥 보고 다음은 전체적으로 회고를 할 테고 그다음은 그전보다 넓고 다른 관점으로 회고하길 바라며 글을 시작한다.   

***
### 저장 프로퍼티 `Stored Properties` & 지연 저장 프로퍼티 `Lazy Stored Properties` 
프로퍼티의 종류는 네 가지가 있다. 이 중 저장 프로퍼티와, 지연 저장 프로퍼티부터 살펴보자.    
- 저장 프로퍼티 `Stored Properties`
- 지연 저장 프로퍼티 `Lazy Stored Properties`
- 연산 프로퍼티 `Computed Properties`
- 타입 프로퍼티 `Type Properties`
<br>

✅ 저장 프로퍼티 `Stored Properties`   
클래스, 구조체의 인스턴스와 연관된 값을 저장하는 가장 단순한 개념이다.   
저장 프로퍼티에는 변수(`var`), 상수(`let`) 키워드가 있다.        
- `var` : 변수 저장 프로퍼티 (value가 변경될 수 있음을 뜻한다.)
- `let` : 상수 저장 프로퍼티 (상수로 선언하면 휴먼 오류나 예기치 못한 상황에서 value 바뀌는 것을 예방할 수 있다. )   
<br>

✅ 지연 저장 프로퍼티 `Lazy Stored Properties`   
지연 저장 프로퍼티는 호출이 있어야 값을 초기화하며 `lazy` 키워드를 사용한다.   
`let` 상수는 인스턴스가 완전히 생성되기 전에 초기화해야 하기 때문에 필요할 때 값을 할당하는 지연 저장 프로퍼티와는 맞지 않는다.   
따라서 `var` 변수 키워드를 사용하여 변수로 정의한다.   
<br>

**사용 예시**   
- 복잡한 클래스나 구조체를 구현할 때 많이 사용된다.
- 클래스의 인스턴스의 저장 프로퍼티로 다른 클래스, 구조체 인스턴스를 할당해야 할 때가 있다.
- ⭐ 코드로 오토 레이아웃할 때 사용했었는데 찾아보기.  
<br>

지연 저장 프로퍼티를 잘 사용하면 불필요한 성능 저하나 공간 낭비를 줄일 수 있다.   
> 다중 스레드 환경에서 지연 저장 프로퍼티에 동시다발적으로 접근할 때는 한 번만 초기화된다는 보장이 없다.   
> 생성되지 않은 지연 저장 프로퍼티에 많은 스레드가 비슷한 시점에 접근한다면, 여러 번 초기화될 수 있다는 단점이 있다.   
---
### 연산 프로퍼티 `Computed Properties`
✅ 연산 프로퍼티 `Computed Properties`    
값을 저장한 것이 아니라 특정 연산을 실행한 결괏값을 의미한다.   
실제로 값을 저장하는 `저장 프로퍼티`와는 조금 다른 의미로 특정 상태에 따른 값을 `연산하는 프로퍼티`이다.    
인스턴스 `내/외부`의 값을 연산하여 적절한 값을 돌려주는 접근자(`getter`)의 역할이나 은닉화된 내부의 프로퍼티 값을 간접적으로 설정하는 설정자(`setter`)의 역할을 할 수도 있다.   
<br>

**메서드와 연산프로퍼티**   
🤔 굳이 메서드를 두고 왜 연산 프로퍼티를 쓸까????   
- 인스턴스 외부에서 메서드를 통해 인스턴스 내부 값에 접근하려면 메서드를 두 개 (접근자, 설정자) 구현해야 한다.   
    - `연산 프로퍼티는 이 두 가지를 한 번에 수행해낼 수 있다.`   
- 이를 감수하고 메서드로 구현한다 해도 두 메서드가 분산 구현되어 코드의 가독성이 나빠질 위험이 있다.   
<br>

💡 연산 프로퍼티의 한계점.  
- 연산 프로퍼티는 접근자인 `get`만 구현해둔것처럼 읽기 전용 상태로 구현하기 쉽지만, 쓰기 전용 상태로 구현할 수 없다는 단점이 있다. 
- 메서드로는 설정자(setter) 메서드만 구현하여 쓰기 전용 상태로 구현할 수 있지만 연산 프로퍼티는 그것이 불가능하다.   
<br>

#### get, set 
- get
- set    
나눠서 다시 정리하기!   
회고시 수정이 필요한 부분!   
연산 프로퍼티는 간단한 값을 리턴해줄 때 메서드로 구현하는 것보단 연산 프로퍼티로 구현하는 게 가독성에 좋다
접근자(`getter`)만 필요한 경우 = 읽기 전용으로 구현할 경우 > 메서드보단 연산 프로퍼티가 적합?! (지금 생각은 ⭕)
<br>

읽기 전용으로만 구현하려면 `get` 메서드만 사용한다.
get만 사용할 경우 `get` 키워드 생략 가능
<br>

연산 프로퍼티 get, set 야곰 202p 보고 공부
연산 프로퍼티의 `get`은  `내/외부`의 값을 연산하여 적절한 갑 돌려준다.  
`set`은  외부의 값을 받아와 연산하여 내부의 값을 바꿔준다.    
`set` 의 매개변수로 원하는 이름을 소괄호 안에 명시해 주면 `set` 메서드 내부에서 전달받은 전달인자 사용 가능하다.   
관용적인 표현으로 newValue로 매개변수 이름을 대신할 수 있다. > 그럴 경우 소괄호로 따로 명시해 주면 안 된다.     

---
### 타입 프로퍼티 `Type Properties`
✅ 타입 프로퍼티 `Type Properties`   
- 특정 타입에 사용되는 프로퍼티이다.   
- 각각의 인스턴스가 아닌 타입 자체에 속하는 프로퍼티를 뜻한다.   
- 인스턴스의 생성 여부와 상관없이 타입 프로퍼티의 값은 하나이다.   
- 타입의 모든 인스턴스가 공통으로 사용하는 값을 담고 있으며, 모든 인스턴스에서 공용으로 접근하고 값을 변경하게 할 수도 있다. (`static var`, `static let`)   
<br>

**두 가지 형태**     
- 저장 타입 프로퍼티 (변수 또는 상수로 선언 가능, 반드시 초깃값을 설정해야 하며 지연 연산된다.)
    - `lazy` 지연 저장 프로퍼티와는 다르게 다중 스레드 환경이라고 하더라도 단 한 번만 초기화된다는 보장을 받는다.
- 연산 타입 프로퍼티 (변수로만 선언 가능)   

***
### 프로퍼티 감시자 (Property Observers)
- 프로퍼티의 값이 변하는 것을 감시한다
- 프로퍼티 감시자는 프로퍼티의 값이 변할 때 값의 변화에 따른 특정 작업을 실행한다.
- 프로퍼티 감시자는 저장 프로퍼티에 적용할 수 있으며 부모클래스로부터 상속받을 수 있다.
- 💡 프로퍼티의 값이 새로 할당될 때 마다 호출하는데, 변경되는 값이 현재의 값과 같더라도 호출한다.
<br>

**`willSet`**
- 프로퍼티의 값이 변경되기 직전에 호출한다. 
- `willSet`에 전달되는 전달인자는 프로퍼티가 변경될 값이다.
<br>

**`didSet`**
- 메서드와 프로퍼티의 값이 변경된 직후에 호출한다.  
- `didSet`에 전달되는 전달인자는 프로퍼티가 변경되기 전의 값이다.   
<br>

두 메서드 모두 매개변수 이름을 따로 지정하지 않으면 `willSet`에는 `newValue`, `didSet`에는 `oldValue` 라는 매개변수 이름이 자동으로 지정된다.   

---
### 상속받은 연산 프로퍼티의 프로퍼티 감시자구현
~~


***
### 전역변수와 지역변수
~~

***

### 키 경로

---
### 마무리 글
~~

***
### 참고
- 야곰 - Swift Programming 3판
- [Swift Language Guide](https://docs.swift.org/swift-book/LanguageGuide/Properties.html)
- [Swift - 프로퍼티](https://www.youtube.com/watch?v=aVGgy29-gOY)
- [Swift - 프로퍼티 감시자](https://www.youtube.com/watch?v=X7oreJGRuaU)
- [회고 시 제드님 블로그도 읽어보기](https://zeddios.tistory.com/245)
