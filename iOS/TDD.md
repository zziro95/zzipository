# TDD
### 글 쓰게 된 이유
`TDD`에 대해 배워보고 적용을 해보긴 했지만 진짜 그냥 체험.? 해보기만 한 정도였다.   
다시 해보고 싶은데 그때보단 좀 더 체계적으로 진행해보고 싶고, 좋은 방향으로 진행해보고 싶어서 복습과 함께 정리해보고자 합니다!   
💡 `Xcode`에서 테스트를 할 때 필요한 개념인 [setUp tearDown](https://github.com/zziro95/zzipository/blob/main/iOS/setUp%20tearDown.md)에 대해서 정리도 하였습니다.   

***
### TDD
`TDD (Test Driven Development)` : 테스트 주도 개발을 뜻한다.   

#### TDD Cycle
<img src="https://github.com/zziro95/zzipository/blob/main/images/TDDCycle.png" width="70%" height="70%" title="TDDCycle" alt="TDDCycleImg"></img>   
<br>

위와 같은 매우 짧은 개발 사이클을 반복하는 소프트웨어 개발 프로세스 중 하나이다.   
1. 개발자가 먼저 요구 사항을 검증하는 테스트케이스 작성   
2. 테스트 케이스를 통과하는 최소한의 코드 생성     
3. 작성한 코드를 표준에 맞도록 리팩토링   
<br>

이와 같이 `1 -> 2 -> 3 -> 1 -> 2 -> 3` 계속 반복하며 개발을 하고 각 단계를 `RED`, `GREEN`, `REFACTOR`라 칭한다.   
<br>

- `RED`: 구현을 하기 전 실패 테스트 코드 작성 (실패하는 테스트를 작성하는 단계)
- `GREEN`: 테스트를 통과하는 최소한의 코드 구현 
- `REFACTOR`: 최소한의 코드를 작성했기 때문에 완전한 코드라고 볼 수 없는 코드를 위해 리팩토링하는 단계 (이 단계에서 **without changing the behavior** 기존 동작이 변경되어선 안된다.)
<br>

간단하게 말해서 무엇을 테스트할지 설계하고, 테스트에 통과할 코드를 만드는 방법이 TDD 이다.   
<br>

---
#### 장단점
**장점**   
- 큰 단위의 문제를 작은 단위로 나누게 된다.
- 지속적인 피드백을 통해 목표 개선 (빠르게 실패하고 피드백을 받고 개선하는 것)
- 코드 복잡도가 떨어진다.
- 유지 보수 비용이 낮아진다.
- 결함이 줄어든다. (버그를 줄일 수 있다.)
- 자동화된 테스트 코드가 있다면 수정에 용이하다.   
<br>

> 테스트는 훌륭한 스펙 정의 문서가 된다. 
> 어떤 인풋에 어떤 아웃풋이 나오는지 자연스럽게 생각하게 되고 표현하게 된다.
<br>

**단점**   
- 개발 시간이 늘어난다.
- 단위 테스트에 집착하면 모든 프로젝트에 비슷한 규칙으로 테스트하게 될 수 있다.
- TDD로만 모든 코드를 작성하려 할 수 있다.   

> 추가로 `붱이`가 개발뿐만 아니라 인생을 살아갈 때도 너무 완벽하게 성공을 향해 가려다 실패를 마주해 무너지는 것보다 많은 실패를 겪으며 받아들이고 피드백을 통해 성장하는 사고를 가지는 것도 중요하다고 말해주었다.👍     
<br>

---
#### Test
`TDD`에 의하면 `TestCase`는 가장 먼저 작성된다.   
`Test`를 나중에 하면 안 될까? 개발 이전에 하는 게 어떤 점에서 좋은지 살펴보자.   
- 테스트를 고려하는 코드(테스트가 가능한 코드)를 작성하게 되게 때문
  - 개발 끝내고 테스트 코드를 넣으려고 하면 테스트가 너무 어려울 때가 있을 수 있다.
- 테스트에 대한 구체적인 이해를 가진 채로 개발하게 된다.(ex. input ouput 타입에 대한 고려)
- 빠른 피드백과 빠른 반응
<br>

위와 같은 여러 근거에 의해 `Test`를 먼저 작성하는 게 옳아 보인다.   
그럼 어떤 식으로 진행해야 할까?   
**개발을 할 때도 마찬가지지만 `Test` 또한 코드부터 작성하는 것을 가장 피해야 한다.**      
- 프로젝트의 스펙을 구체적으로 생각, 표현하기
    - 내가 어떤 작업을 하고 있고 작업의 결과는 어떻게 되어야 한다.
    - 어떤 `input`에 어떤 `output`이 나올 것이다를 생각하기.   
- 명확하고 구체적인 목표, 기준을 가지고 작은 단위부터 진행.   

---
#### 올바른 테스트란?
**FIRST**   
- `Fast` - 테스트는 빠르게 동작해야 한다.
- `Independent` - 테스트는 각 각의 다른 테스트들과 독립적이어야 한다.
    - 테스트를 한 객체가 독립적이지 않을 경우 테스트가 실패했을 때 어디서 실패했는지 알아내기 힘들다.   
- `Repeatable` - 테스트는 실행할 때마다 같은 결과를 만들어야 한다. (재반복이 가능한 테스트를 만들어야 한다.)
- `Self-validating` - 스스로 검증이 가능해야 한다 (리턴 값이 없으면 테스트를 검증할 방법이 없다.)
    - 명확하게 테스트를 확인할 수 있는 `output` 같은 장치를 두기 위한 노력, 고민 필요   
- `Timely` - 단위 테스트를 즉시 작성해야 이상적인 코드가 나온다.
<br>

**Right - BICEP**
- `Right` 결과가 올바른가
- `Boundary` - 모든 경계 조건이 Correct 한가?
    - ex) 나눗셈 테스트할 때 피연산자 0이면 안 되니깐 엄밀하게 테스트해야 한다.
- `Inverse` - 역 관계를 확인할 수 있나?
- `Cross-check` - 다른 수단을 사용해서 결과를 교차 확인할 수 있나?
- `Error condition` - 에러 조건을 강제로 만들 수 있나?
    - ex) 메모리, 디스크가 가득 찬 경우, 네트워크 오류
- `Performance` - 성능 특성이 한도 내에 있나?
<br>

올바른 테스트를 작성하기 위해서 고려해야 될 것들이 참 많다.   
모든 조건을 다 생각하며 테스트를 진행하는 것도 좋겠지만 경험을 통해서 각 기능의 특수성에 맞게 어떤 것이 더 우선적으로 생각되어야 하는지 판별할 수 있어야 할 것이다.   

---
### 독립적인 Test가 중요한 이유
테스트를 고려하지 않고 코드를 작성했을 때 **유닛, 모듈이 분리가 돼 독립적으로 분리가 되지 않아서** 테스트가 어려워진다고 한다.   
<br>

테스트를 할 때 내가 `A`에 관해 테스트하려고 했는데 `A`와 관련된 `B`때문에 테스트가 실패 될 수도 있다.   
이런 경우에는 테스트 결과만 보고 잘못된 판단을 내릴 수도 있고 빠른 피드백을 얻기에 좋은 테스트가 아니다.   
이에 대비해 무조건 성공하는 or 실패하는 `Mock` 데이터를 만들어서 테스트를 한다면 해결하는 데 도움이 된다.   
<br>

`B`에 대해 무조건 성공, 실패하는 `Mock` 객체를 두면 `A`에 관한 독립적인 테스트가 가능해진다. (`Mock` 객체를 두는 이유)   
> 이것 때문에 `프로토콜`, `추상화` 개념이 중요하다고 하셨다. << 이 얘기는 프로토콜과 추상화에 대해 좀 더 공부를 하고 난 다면 이해할 수 있을까?   
<br>

이 내용과 관련돼서 `붱이`가 보여준 테스트를 고려하지 않은 코드의 예시를 첨부했다.   
```swift
// 케이블을 생성함에 있어서 전기공급자를 입력으로 받고 있다.
sut = 케이블(입력단자: Mock전기공급자())

// 테스트를 고려하지 않은 코드의 예시
// 입력단자를 밖에서 부터 주입 받는게 아니라 안에서 생성해주는 형태
// 이렇게 되면 케이블에 대해 테스트를 하는데 어덥터 때문에 테스트가 실패할 수 있고 심지어 아울렛 때문에 테스트가 실패할 수도 있다.
struct 케이블: 전기공급자 {
    private let 입력단자: 어덥터 = 어덥터(입력단자: 아울렛())
}

// 단위 테스트를 정상적으로 하기위해선 모듈을 뜯어내 독립적인 테스트가 필요하다.
// 좋은 테스트를 하기 위해선 좋은 구조를 만들어야 하겠구나...
```

💡 리팩토링 과정이나 테스트시 테스트를 실패했을 때 어디서 문제가 생겼는지 파악하기 위해선 독립적인 테스트를 하는 것이 얼마나 중요한지 알 수 있다.   

---
### private func에 대한 테스트?
> public한 메서드를 테스트하는데 리팩토링 과정에서 기능 분리를 위해 private func 이 생길 수도 있다.   
> 그럼 이 private func에 대한 테스트는 할 수 없는가?   
캠퍼 `이니`가 질문해 준 내용이다.   
그에 대한 `붱이`의 답변은   
> "테스트에서는 public 한 코드밖에 테스트할 수밖에 없고, public 한 코드를 수정하는 과정에 private 한 코드들이 생겼다 해도 TDD Cycle에 의해 다시 테스트하는 과정에서 기존에 만들어 놓은 테스트 메서드들에 대해 다시 테스트가 되고, 테스트가 `실패한다면 수정하고 있는 코드 범위가 테스트 실패의 원인이 되겠고 개선하여 테스트 성공하게 리팩토링` 해야 한다" 였다.   

**private 메서드는 만들기 전에 테스트되고 있어야 한다**는 이야기를 넌지시 들었던 것 같은데 이 내용이 아닐까 싶다.   
회고하는 과정에서 꼭 다시 생각해 봤으면 좋겠기에 기록하였다.   
***
### 마무리 글
야곰 아카데미에서 `TDD` 관련 수업을 할 때 `붱이`가 설명해 준 내용들이 글의 대부분을 차지하고 있다.   
배우는 과정에서 다른 분들의 도움을 많이 받고 있음을 다시 한번 느낀다. 🙇   
<br>

작성하다 보니 조금 반복적으로 쓰게 되는 단어들이 있었다.   
스펙을 `구체적`으로 표현하기, 빠른 `피드백`, 테스트를 진행할 때 머릿속에 데리고 다녀야겠다.   
<br>

아직 UITest는 iOS에서 실질적으로 쉽지 않다고 들었다.   
UnitTest에 대해서라도 많은 경험을 하고, 좋은 개발을 하고 싶은 마음이다.   
***
### 참고
- 야곰 아카데미 (with. `붱이`)

---
### TodoList
- [Let`s TDD - 전수열님 영상도 보기!](https://www.youtube.com/watch?v=meTnd09Pf_M)
- 관련 WWDC도 찾아보기
- override super()
- mock stub 등 등 살펴보고 정리하기
