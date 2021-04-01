### Core Animation
<img src="https://github.com/zziro95/zzipository/blob/main/images/CoreAnimation.png" width="70%" height="70%" title="CoreAnimation" alt="CoreAnimationimg"></img>
<br>


#### Core Animation
CALayer란 -   <br>
뷰에는 하나의 레이어만 구성되어 있다. 대신 서브레이어는 여러개 소유할 수 있다. <br>
레이어는 뷰의 draw(rect:)로 그려진 뒤에 표시된다. 서브뷰는 이 레이어 위에 얹혀진다. <br>
<br>


#### CAAnimationGroup
여러개의 애니메이션을 묶어서 관리하고 싶을때 사용한다.
<br>


#### CATransaction
`CATransaction.begin()`, `CATransaction.commit()`
begin과 commit사이에 애니메이션을 처리해달라! <br>
중첩적으로 적용가능, begin-commit 세트로 써야하는 것 같다. <br>
<br>


#### CAProperty Animation
가장 많이 쓰이는 추상 클래스 <br>
실질적으로 사용하게 될 concreat class 는 `CABasicAnimation`, `CAKeyframeAnimation`이다. <br>
레이어에 있는 프로퍼티들의 값 변경에 따라 자동으로 애니메이션 변경을 도와주는 클래스 <br>
<br>


#### CABasicAnimation
CAProperty Animation 추상클래스를 상속받아서 사용 <br>
```swift
// keyPath 스트링으로 집어넣으면 휴먼에러가 발생할 수도 있어서 따로 만들어 준다.
// 옛날 문법들에서 파생되었기 때문에 아직도 이런예시가 남아 있음
private struct CAKeyPath {
    struct Position {
        static let x = "position.x"
        static let backgroundColor = "backgroundColor"
    }
}

//keyPath - 변경해줄 Layer의 프로퍼티 (Layer의 어떤 속성을 건드려서 Animation을 만들어 줄 것인가.)
let animation = CABasicAnimation(CAKeyPath.Position.x)
//opacity 란 프로퍼티를 0에서 1로 변경시켜달라
animation.fromValue = 0
animation.toValue = 1

// background Property  red -> blue
let animation = CABasicAnimation(CAKeyPath.Position.backgroundColor)
animation.fromValue = NSColor.red.cgColor
animation.toValue = NSColor.blue.cgColor
```
프로퍼티 값만 바꿔주면 알아서 애니메이션을 만들어준다! <br>
fromValue, toValue말고 byValue도 있다. <br>
`from`, `to`, `by` 3개의 아이템을 가지고 2개씩 짝을지어 쓴다.!(`from-to`, `by-to`, `by-from`) <br>
`from-to` 절대적인 값의 변화를 의미한다! <br>
`from-by` 상대적인 값의 변화를 의미한다.  `ex) from1 0 by 5 -> from에서 5만큼 더한거 15로 가는 효과를 연출`  <br>
`by-to` toValue에서 byValue를 뺀다 `ex) toValue 20 byValue 15면 20까지(to) 15(by)만큼  애니메이션 진행 결과적으로 5-20 효과`
<br>


#### CAKeyframeAnimation
CABasicAnimation보다 조금 더 세밀한 애니메이션을 만들어 줄 수 있다. <br>
```swift
// 마찬가지로 keyPath에 애니메이션하는 키 경로를 지정
let colorKeyframeAnimation = CAKeyframeAnimation(CAKeyPath.Position.backgroundColor)

// 변화될 값들
colorKeyframeAnimation.values = [UIColor.red.cgColor,
                                 UIColor.green.cgColor,
                                 UIColor.blue.cgColor]
// 애니메이션들이 실행될 시간들 0~1까지가 애니메이션의 길이
// duration의 길이와 상관없이 0부터 1값을 가지게된다, duration이 100초라면 0초에 빨간색, 50초부터 그린, 100초에는 파란색이 될것이다.
colorKeyframeAnimation.keyTimes = [0, 0.5, 1]
colorKeyframeAnimation.duration = 2
```
<br>


#### CATransition
레이어 상태간에 애니메이션 전환을 제공하는 개체 <br>
Transition Types - fade, moveIn, push, reveal <br>
<br>
뷰간의 전환때 애니메이션옵션들을 줄 수 있다. <br>
`UIViewController` > `transition(from, to, duration, options, animations, completion)`
조금더 복잡하게 하려면 다른 방법도 있다. 따로 찾아보자
살펴볼 문서  Hint: 프로토콜을 가진 클래스를 구현해주면 된다
https://developer.apple.com/documentation/uikit/uiviewcontrolleranimatedtransitioning
<br>


#### CASpring Animation
용수철같은 애니메이션 효과들이 있다.
<br>
 
 
#### 참고
- [CABasicanimation](https://developer.apple.com/documentation/quartzcore/cabasicanimation, "apple")
- [CAKeyframeAnimation](https://developer.apple.com/documentation/quartzcore/capropertyanimation, "apple")
- [CAPropertyAnimation](https://developer.apple.com/documentation/quartzcore/cakeyframeanimation, "apple")
다음에 정리할 때 추가로 보면 좋을 문서
- <https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreAnimation_guide/Introduction/Introduction.html>
- <https://www.objc.io/issues/12-animations/animations-explained/>
