# ZZIROTDD
### 글의 목적
TDD를 실제로 적용하면서 느낀점과 팁, 여러가지 생각들을 정리하는 글.   
한 번에 작성될 글이 아니며 개발하면서 계속 회고할 글.   
나중 회고를 위해 이상적인 작업 순서가 아닌, 실제로 진행, 생각한 순서로 쓴 글입니다.   

***
### JSON 관련 테스트
캠프기간 이후 TDD를 공부한 후 실제 적용해보는 첫번째 시도이다.   
잘 할거라고 생각했는데 이거 처음부터 머리가 하얘진다.   
❗**어떤 테스트 코드를 작성해야 하는지**가 가장 큰 고민이다.   
<br>

예전의 나라면 우선 `JSON Parsing` 하는 타입과 메서드를 구현하고 테스트 코드를 작성했을텐데 반대로 하려다 보니 자연스럽게 `input` 과 `output`에 대해 고려하게 되었다.   
지금 내 `Xcode`는 길을 잃었다. 😂   
```swift
// 현재 상태.. 이런 테스트들을 하고 싶다 헤쳐나가 보자

func test_JSON_샘플데이터_item_디코딩_성공() {
//        (JSONParser.decode(T),T)
}

func test_JSON_샘플데이터_item_디코딩_실패() {
//        (JSONParser.decode(T),T)
}
```
진행속도도 더디고, 머리가 잘 정리가 안되서 글을 써보면서 머릿속을 정리하고 다시 테스트 코드를 작성해보고자 한다.   
<br>

- 구현하려는 스펙
    - **최종적**으로는 서버 `API` 통신을 통해 받아오는 `JSON` 데이터 디코딩
    - **현재**는 서버 통신 없이 import 한  Sample Data를 디코딩 해야함
    - `item`, `items` 즉 `Product` 하나하나 가져올 수도 있어야 하고 배열로도 가져올 수 있어야 한다.   
- 테스트 해야 할 가장 작은 단위는?
    - JSONParser.docode를 하기 위해 데이터 가져오기?
    - JSONParser.docode를 제네릭 타입으로 구현하는것은 TDD Cycle을 통해 `Refactor` 과정에서 해야하는걸까?
    - 그렇다면 최소한의 코드인 JSONParser.docode를 테스트 하려면 어떻게 해야할까?   
- 결론
    - `JSONDecoder`의 `func decode<T>(_ type: T.Type, from data: Data) throws -> T where T : Decodable` 메서드를 사용할 것이기 때문에 Type은 선언한상태이지만 디코딩할 데이터 = `DataAsset`을 가져오는 작업부터 테스트 코드를 작성해보자.
    - ❓ `JSONParser`라는 타입에 메서드로 구현하려 했는데 `단일책임원칙(SRP)`을 따르지 못하는 것 같아서 새로운 타입 `DataAsset`을 구현하고 싶었지만 분리하기가 어려워서 실패하였다.  (나중에 회고할 때는 이 작업을 충분히 해낼 수 있을까? 미래에 나에게 질문을 던져주자)
```swift
// 테스트 코드
func test_DataAsset_객체가_유효한지() {
    var dataAssetName: String = "item"
    XCTAssertNoThrow(try jsonParser.fetchData(fileName: dataAssetName))
    
    dataAssetName = "items"
    XCTAssertNoThrow(try jsonParser.fetchData(fileName: dataAssetName))
    
}

func test_DataAsset_유효하지_않은_이름이_할당되었을때(){
    let dataAssetName: String = "DataAsset이름이변경될수도있어"
    let expectedError: DataAssetError = .invalidDataAssetName
    var error: DataAssetError?

    XCTAssertThrowsError(try jsonParser.fetchData(fileName: dataAssetName)) { thrownError in
        error = thrownError as? DataAssetError
    }
    
    XCTAssertEqual(expectedError, error)
}

// 생성한 타입
struct JSONParser {
    func fetchData(fileName: String) throws -> Data {
        guard let dataAsset: NSDataAsset = NSDataAsset.init(name: fileName) else {
            throw DataAssetError.invalidDataAssetName
        }
        return dataAsset.data
    }
}

// 에러
enum DataAssetError: Error {
    case invalidDataAssetName
    case unknown
}

extension DataAssetError: LocalizedError {
    var errorDescription: String? {
        switch self {
        case .invalidDataAssetName:
            return "유효하지 않은 DataAsset 이름입니다."
        case .unknown:
            return "알 수 없는 에러가 발생했습니다."
        }
    }
}
```   
테스트를 먼저 작성하고 코드를 작성하고 싶었는데 익숙치 않은지 같이 작성하게 되었다.   
처음부터 완벽하게 하려하지말고 조금씩 `TDD Cycle`에 익숙해져 가보자.   

#### 💡 addTeardownBlock
흠 이건 바로 해결할 고민은 아니지만 적어놓기로 하였다.   
`addTeardownBlock`에 대해 공부를 했을 때 예를 들어 테스트를 진행하면서 생성 된 파일을 삭제해주는것과 비슷한 작업을 이 블록안에서 tearDown 해준다고 이해하였다.   
`func test_DataAsset_객체가_유효한지()`의 코드로 예를 들면 변수 `dataAssetName`에 값들을 할당하며 테스트 하고 있다.   
- 고민사항
    - `addTeardownBlock`에  `dataAssetName = nil`과 같은 코드를 넣어주어야 하는가?
- 왜 이런 생각이 들었는가?
    - 테스트 할 주요 오브젝트에 대해서는 setUp, tearDown 메서드를 통해 초기 상태 설정, 분해 작업을 해주는데 테스트메서드의 변수, 상수에 대해서도 해주어야 하나?
- 현재 생각
    - 클로저에 대한 공부가 부족해서 생긴 고민! -> 클로저에 대해 공부후 다시 돌아와서 볼 필요가 있
    - 테스트 메서드 안에 변수 상수들은 지역 상수, 변수의 개념으로 전역적으로 선언된 것이 아니기 떄문에 `ARC`에 의해 자동으로 메모리에서 해제된다??
    - 현재 생각에 대한 근거가 명확하지 않아,, 씁쓸하다.,갈길이 멀구만 차근차근 화이팅   

***



### 소제목
유닛 테스트를 한다면 테스트할 주제와 대상 클래스를 정하고, 대상 클래스가 사용하는 의존성(패키지일 수도 있고 특정 함수일 수도 있겠지요)들은 Mock이나 Stub으로 만든다. (Mock과 Stub이란?) Mocking을 어떻게 하는지는 사용하는 언어마다 주로 사용하는 테스팅 프레임워크의 레퍼런스를 참고하라. 그러고 나면 자신이 의존성을 잘 정리했는지 살펴보기 좋아지고, 이어서 테스트하기 좋은 형태가 눈에 들어오기 시작한다.

무엇을 테스트할지 정하기 어렵다면? 
단위 테스트를 예로 들면 자신이 만든 클래스나 모듈, 함수 등의 기능이 정상적으로 동작하는지 확인하기 위해 테스트를 작성한다고 생각해보라.

Swift mock stub
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
- [Getting Started With Unit Testing | XCTest | Swift](https://www.youtube.com/watch?v=P-Zow2yVx4o&t=1481s)
- []()
