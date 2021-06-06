# setUp tearDown
### 글 쓰게 된 이유
TDD에 대해 복습 정리 중이다.   
복습 도중 setUp과 tearDown에 대해서 정리해야겠다고 느껴져 의식의 흐름대로 먼저 정리해보려 한다.   
XCTest에 대해 살펴보면 될 것 같다. 가볍게 살펴보자.   
***
### XCTest
[XCTest](https://developer.apple.com/documentation/xctest/xctest)는 테스트를 생성, 관리 및 실행하기 위한 추상 클래스이다.   
XCTest를 상속받는 XCTestCase, XCTestSuite 클래스를 이용해 테스트를 주로 하는 것 같다.   
Test를 새로 만들면 XCTestCase를 상속받는 클래스가 생성돼있는 걸 확인할 수 있다.   
이 글의 중점은 setUp과 tearDown이지만 XCTestCase, XCTestSuite도 가볍게 살펴보자.   

---
### XCTestCase
- 테스트 케이스, 테스트 메서드, 성능 테스트 정의를 위한 주요 클래스이다.   
- 테스트 실행 전후에 optional setup, teardown 테스트 메서드들 관련 그룹이다.   
<br>

XCTestCase를 통해 `Customizing Test Setup and Teardown` 이 외에도 `Handling Test Case Failure`, `Measuring Performance`, `Creating Asynchronous Test Expectations`, `Waiting for Expectations`, `Monitoring UI Interruptions`, `Creating Tests Programmatically` 과 같은 여러 작업을 할 수 있다.   
나중에 이 토픽들에 대해서도 다뤄보는 것도 좋을 것 같다.   
<br>

자세한 내용은 [Defining Test Cases and Test Methods](https://developer.apple.com/documentation/xctest/defining_test_cases_and_test_methods)를 참고하라고 한다.   

#### Defining Test Cases and Test Methods
문서를 살펴보면 프로젝트에 테스트를 추가하려면   
- test target 안에 `XCTestCase`를 상속받는 새 클래스를 만들어준다.
- test case에 하나 이상의 test method를 만들어 준다.
- test method에 하나 이상의 test assertion을 만들어 준다.   
<br>

**Test Method**   
- `no parameters`, `no return value`이고 `test`로 네이밍이 시작하는 XCTestCase를 상속받은 클래스의 인스턴스 메서드이다.   
- `XCTest` Framework에 의해 자동으로 감지된다고 한다.   
- 네이밍은 테스트 케이스의 테스트를 요약하는 이름을 지정한다.
- 주로 `test_하려고_하는_테스트`의 형식으로 메서드의 이름을 지어주는 것 같다.   
<br>

#### Test Assertions
`XCTest` Framework를 통해 `Test Method`가 예상대로 동작하는지 확인할 수 있다.   
정말 많은 Test Assertion이 있고 많이 쓸 거 같은 메서드들만 정리해 봤다.   
그 외에도 어떤 것들을 확인할 수 있는지 간략하게 살펴보고 정리했다.   

- Boolean Assertions: true / false 결과를 생성하는 조건을 테스트한다.
  - XCTAssert(): 식이 True 임을 확인한다.
  - XCTAssertTrue(): 식이 True 임을 확인한다.
  - XCTAssertFalse(): 식이 False 임을 확인한다.
- Nil and Non-Nil Assertions: 테스트 조건이 nil 인지 nil 이 아닌지 확인한다.
  - XCTAssertNil() - 표현식이 nil 임을 확인한다.
  - XCTAssertNotNil() - 표현식이 nil 이 아님을 확인한다.
  - XCTUnwrap - 언래핑을 해야 하는 상황에서 쓰는 언래핑 함수
- Equality and Inequaltiy Assertions: 두 값이 같은지 아닌지 확인한다.
  - XCTAssertEqual() - 두 값이 같음을 확인한다.
  - XCTAssertNotEqual() - 두 값이 다름을 확인한다.
- Comparable Value Assertions: 두 값을 비교해 어느 값이 큰지 작은지 확인한다.
- Error Assertions: 함수에서 오류가 발생하는지 그렇지 않은지 확인한다.
    - XCTAssertNoThrow() - 표현식이 오류를 발생시키지 않음을 확인한다.
    - XCTAssertThrowsError() - 표현식에서 오류가 발생함을 확인한다.
- Unconditional Test Failures: 즉시, 무조건 실패를 생성한다.
- Methods for Skipping Tests: 명시한 조건을 마주하면 테스트를 스킵 한다.   
<br>

💡 고민 사항   
오류가 발생했을 때 그렇지 않았을 때 모든 상황에 대해 테스트 코드를 작성하고 싶다.   
JSON Data 디코딩으로 예를 들어보면 올바른 값이 들어와 디코딩에 성공한다면 `XCTAssertNoThrow()`를 이용하여 오류가 발생하지 않고 디코딩에 성공하는 테스트 코드는 테스트에 성공한다.   
하지만 오류 발생한 상황에 대해 작성한 테스트 코드는 실패한다.   
같은 시점에 발생할 수 없는 `성공/ 실패`에 대한 모든 테스트를 서로 독립적으로 테스트할 수 있을까??   
`Mock`객체를 통해 해결할 수 있을까 고민해 보자!   

⁉️ 해결 방안
1. 첫번째 드는 생각은 조금 단순했다. 테스트 하고자 하는 기능에 `input`이 존재할 테니 `성공/ 실패` 각 경우에 맞는 `input`, 예상되는 결과에 알맞는 `Test Assertions`을 이용해 테스트하면 될 것 같다.   
2. `Mock`, `Stub` 등 `Test Double`에 대한 공부후 다시 고민할 필요.   
***
### XCTestSuite
일반적으로, `Xcode`는 자동으로 Test Suite를 관리한다고 한다.   
사용자 정의 Test Suite를 정의해야 하는 경우에만 사용한다고 한다.   

***
### setUp tearDown
setUp tearDown 관련 [[Article] Understanding Setup and Teardown for Test Methods](https://developer.apple.com/documentation/xctest/xctestcase/understanding_setup_and_teardown_for_test_methods)가 있어서 문서를 토대로 정리해보았다.   
<br>

테스트를 할 때 실행하기 전 초기 상태를 준비하는 작업 `setUp` 과 테스트가 완료된 후 정리하는 작업. `tearDown` 이 필요하다.   
**여러 가지 방법**으로 테스트 상태의 setUp, tearDown을 사용자 정의할 수 있다.   
- setUp() `Class method`를 override 하여 **모든** 테스트 메서드들의 초기 상태를 설정한다.
- setUpWithError() `Instance method`를 override 하여 **각** 테스트 메서드가 실행되기 전에 초기 상태를 설정하고 관련 오류를 처리한다.
- setUp() `Instance method`를 override 하여 **각** 테스트 메서드가 실행되기 전에 초기 상태를 설정한다.
- 테스트 메서드가 실행되는 동안 addTeardownBlock(_:) 메서드를 사용하여 **자체** 포함된 분해 코드를 등록한다.
- tearDown() `Instance method`를 override 하여 **각** 테스트 메서드가 완료된 후 tearDown을 수행한다.
- tearDownWithError() `Instance method`를 override 하여 **각** 테스트 메서드가 완료된 후 관련 오류를 처리한다.
- tearDown() `Class method`를 override 하여 **모든** 테스트 메서드가 완료된 후 최종적으로 tearDown을 수행한다.   
<br>

> setUp(), tearDown() `Class method` 들은 `XCTestCase`에 정의되어 있지만, setUp(), setUPWithError(), tearDown(), tearDownWithError() `Instance method` 들은 `XCTest` 클래스에 정의되어 있다.   
<br>

#### Test Case의 실행 순서
Test Case의 실행 순서를 살펴보기 위해서 공식 문서의 예제 코드와 이미지를 가져왔다.   
```swift
class SetUpAndTearDownExampleTestCase: XCTestCase {
    override class func setUp() { // 1.
        // This is the setUp() class method.
        // It is called before the first test method begins.
        // Set up any overall initial state here.
    }
    
    override func setUpWithError() throws { // 2.
        // This is the setUpWithError() instance method.
        // It is called before each test method begins.
        // Set up any per-test state here.
    }
    
    override func setUp() { // 3.
        // This is the setUp() instance method.
        // It is called before each test method begins.
        // Use setUpWithError() to set up any per-test state,
        // unless you have legacy tests using setUp().
    }
    
    func testMethod1() throws { // 4.
        // This is the first test method.
        // Your testing code goes here.
        addTeardownBlock { // 5.
            // Called when testMethod1() ends.
        }
    }
    
    func testMethod2() throws { // 6.
        // This is the second test method.
        // Your testing code goes here.
        addTeardownBlock { // 7.
            // Called when testMethod2() ends.
        }
        addTeardownBlock { // 8.
            // Called when testMethod2() ends.
        }
    }
    
    override func tearDown() { // 9.
        // This is the tearDown() instance method.
        // It is called after each test method completes.
        // Use tearDownWithError() for any per-test cleanup,
        // unless you have legacy tests using tearDown().
    }
    
    override func tearDownWithError() throws { // 10.
        // This is the tearDownWithError() instance method.
        // It is called after each test method completes.
        // Perform any per-test cleanup here.
    }
    
    override class func tearDown() { // 11.
        // This is the tearDown() class method.
        // It is called after all test methods complete.
        // Perform any overall cleanup here.
    }
}
```   
<br>

<img src="https://github.com/zziro95/zzipository/blob/main/images/OrderOfExecutionForExampleTestCase.png" width="70%" height="70%" title="OrderOfExecutionForExampleTestCase" alt="OrderOfExecutionForExampleTestCaseImg"></img>  
<br>

예제 코드와 도식화된 이미지를 보니 이해에 도움이 되었다.   
💡 여기서 중요한 포인트는 `XCTest`가 `LIFO` (후입선출) 순서로 teardown block들을 실행하기 때문에 `addTeardownBlock`을 사용하여 실행되는 블록의 순서는 8번 teardown block, 7번 teardown block이다.   
<br>

**addTeardownBlcok**   
또한 이해가 잘되지 않았던 `addTeardownBlock`은 테스트를 하면서 생성된 파일을 삭제하는 거와 같은 각 테스트 메서드 안에서 **각 테스트 메서드가 끝날 때 호출되고** 실행한 작업을 tearDown 해주는 역할을 한다고 이해하였다.   
<br>

> 추가로 setUp(), setUPWithError(), tearDown(), tearDownWithError() `Instance method` 들에는 Test Assertion들이 포함될 수 있지만, 모든 테스트 메서드 실행의 일부로 평가된다고 한다.  
> setUp(), tearDown() `Class method` 들에서는 Test Assertion이 포함할 수 없다.   
> Test Assertion은 클래스 메서드 범위 내에 존재하지 않는 `Test Class Instance`가 필요하다.   
   
---
### setUp, tearDown
Xcode 11.4 이전 버전에서 테스트를 만들면 setUp과 tearDown 메서드가 기본적으로 있었는데,   
Xcode 11.4 이후 버전에서 테스트를 만들면 setUpWithError, tearDownWithError가 기본적으로 있다.   
<br>

**setUp()**   
- 클래스 안에 속하는 `테스트 메서드들이 호출되기 전` 한 번 호출된다.
- 테스트 클래스에서 진행되는 테스트 케이스에서 공통으로 필요로 하는 행위들을 정의
- ex. 객체 인스턴스 만들기, db 초기화 등   
<br>

**tearDown()**
- `모든 테스트 케이스 메서드들이 종료된 후`  한 번 호출된다.
- setUp에서 생성되고 테스트에서 사용된 것들을 해체할 내용들을 작성해 준다.
- ex. 파일 닫기, 연결, 새로 만든 항목 제거 등   
<br>

**setUpWithError()**, **tearDownWith**는 각각 setUp, tearDown과 비슷한 역할을 하지만 발생하는 에러를 던져주는 메서드이다.   
💡 만약 **setUpWithError()** 에서 초기 작업을 해주는데 이 초기 작업에서 에러가 날 경우에는 관련 테스트가 `Skip` 된다고 한다.   

---

### 고민 사항 (super, class, instance method)
`Override`를 하기 때문에 super를 호출해야 하는데 다음과 같은 코드 위치에 선언해 주어야 한다고 한다.   
super에 대한 지식이 부족하기 때문에 회고하면서 살펴보았으면 좋겠어서 글을 남겨 본다.   
```swift
override func setUp() {
    super.setUp()
    // Put setup code here. This method is called before the invocation of each test method in the class.
}

override func tearDown() {
    // Put teardown code here. This method is called after the invocation of each test method in the class.
    super.tearDown()
}
```   
<br>

#### super 해줘야 하는 이유? 
- super가 없으면 비정상적인 동작을 할 수도 있다..?
- super에 로직들이 포함되어 있을 수 있다.?   
더 알아보고 수정하러 오자~   
<br>

#### 공부 후 다시 생각해 볼 것들
setUp()과 tearDown() 메서드 /  class method와 instance method의 차이
XCTest의 setUp tearDown, XCTestCase의 setUp tearDown의 차이가 있을까??   
override와 super에 대해서도 좀 더 확실히 알아야 겠지..?   

***
### 마무리 글
setUp과 tearDown을 다룰 때 `Class method`와 `Instance method`라는 용어가 계속적으로 나왔는데 `Override` 개념과 함께 나와서 이해를 해도 조금 찝찝한 느낌이 있다..   
내가 지금까지 이해한 바로는 `Class method`는 Unit Test를 하기 위해서 만든 클래스가 `XCTestCase`를 상속받기 때문에 사용할 수 있는 클래스의 메서드이고, `Instance method`는 그 클래스 안에서 정의한 메서드인데 setUp(), setUPWithError(), tearDown(), tearDownWithError() 메서드들은 `XCTestCase`의 슈퍼클래스인 XCTest에 정의된 메서드이기 때문에 `Override`해서 사용하는 것이라고 정리해 보았다.   
확신을 위해 `Class method`와 `Instance method`, `Override`에 대해 더 공부가 필요한 것 같고 캠퍼들과 이야기해보는 것도 좋을 것 같다!   

***
### 참고
- [[Framework] XCTest](https://developer.apple.com/documentation/xctest)
- [[Class] XCTest](https://developer.apple.com/documentation/xctest/xctest)
- [XCTestCase](https://developer.apple.com/documentation/xctest/xctestcase)
- [Defining Test Cases and Test Methods](https://developer.apple.com/documentation/xctest/defining_test_cases_and_test_methods)
- [XCTestSuite](https://developer.apple.com/documentation/xctest/xctestsuite)
- [Understanding Setup and Teardown for Test Methods](https://developer.apple.com/documentation/xctest/xctestcase/understanding_setup_and_teardown_for_test_methods)
- [XCTestCase]()
- [Zedd님 블로그 setUpWithError tearDownWithError](https://zeddios.tistory.com/991)
- [Zedd님 블로그 Unit Test](https://zeddios.tistory.com/48)
- [Getting Started With Unit Testing | XCTest | Swift](https://www.youtube.com/watch?v=P-Zow2yVx4o&t=1481s)
