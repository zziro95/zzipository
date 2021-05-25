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
- test target 안에 XCTestCase를 상속받는 새 클래스를 만들어준다.
- test case에 하나 이상의 test method를 만들어 준다.
- test method에 하나 이상의 test assertion을 만들어 준다.   
<br>

**Test Method**   
- `no parameters`, `no return value`이고 `test`로 네이밍이 시작하는 XCTestCase를 상속받은 클래스의 인스턴스 메서드이다.   
- XCTest Framework에 의해 자동으로 감지된다고 한다.   
- 네이밍은 테스트 케이스의 테스트를 요약하는 이름을 지정한다.
- 주로 `test_하려고_하는_테스트`의 형식으로 메서드의 이름을 지어주는 것 같다.   
<br>

#### Test Assertions
XCTest Framework를 통해 `Test Method`가 예상대로 동작하는지 확인할 수 있다.   
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
- Unconditional Test Failures: 즉시, 무조건 실패를 생성한다.
- Methods for Skipping Tests: 명시한 조건을 마주하면 테스트를 스킵 한다.   

***
### XCTestSuite
~~

***
### setUp tearDown
XCTest의 setUp tearDown, XCTestCase의 setUp tearDown의 차이가 있을까??   
override와 super에 대해서도 좀 더 확실히 알아야 겠지..?

***

### 마무리 글
~~

***
### 참고
- [[Framework] XCTest](https://developer.apple.com/documentation/xctest)
- [[Class] XCTest](https://developer.apple.com/documentation/xctest/xctest)
- [XCTestCase](https://developer.apple.com/documentation/xctest/xctestcase)
- [Defining Test Cases and Test Methods](https://developer.apple.com/documentation/xctest/defining_test_cases_and_test_methods)
