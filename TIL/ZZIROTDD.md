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

#### decode 함수 - Generic or Result ??
샘플 데이터를 decoding 해주어야 한다.   
Product와 ProductList 타입 모두를 전달 받을 수 있는 함수, 타입을 만들어 주어야 한다고 생각한다.   
머리도 복잡하니 한 번에 도착점에 가려고 하지 말고 `TDDCycle`을 통해 가장 최소한의 단위부터 실패하며 가보자.   
우선은 하나의 타입만을 디코딩 할 수 있는 메서드를 만들어 보겠다.   
```swift
// Test 코드 기능 별로 단위를 나누니 내 예상보다 테스트 코드가 복잡했다.
// 이런 형식으로 테스트를 진행하는게 맞는걸까?
func test_JSON_샘플데이터_item만을_디코딩() throws {
    let dataAssetName: String = "item"
    
    do {
        let dataToDecode = try jsonParser.fetchData(fileName: dataAssetName)
        XCTAssertNoThrow(try jsonParser.decoding(data: dataToDecode))
    } catch {
        throw DataAssetError.unknown
    }
}
```   
이 고민에 대해서 `야곰아카데미` 커뮤니티를 통해 질문을 하였고 `올라프`님의 답변을 받을 수 있엇다.   
아직 답변을 100% 이해하지 못한 상태라 일단은 내가 생각한 방법으로 진행해보았다. (답변을 정확하게 이해하려면 공부 해야할게 너무 많아서,.. 조금 미뤘다)   
조급해지면 안되니깐.. 일단 내가 정한 일의 우선순위에 따라 진행해보자~!    
<br>

#### Generic
JSONParser 타입에 데이터를 매개변수로 받아 Product와 ProductList를 반환해주는 두 함수를 만들었다.    
```swift
func decodingProduct(data: Data) throws -> Product {
        let jsonDecoder = JSONDecoder()
        let decodingResult: Product
        do {
            decodingResult = try jsonDecoder.decode(Product.self, from: data)
            return decodingResult
        } catch {
            throw  JSONError.decodingError
        }
    }

    func decodingProductList(data: Data) throws -> ProductList {
        let jsonDecoder = JSONDecoder()
        let decodingResult: ProductList
        do {
            decodingResult = try jsonDecoder.decode(ProductList.self, from: data)
            return decodingResult
        } catch {
            throw  JSONError.decodingError
        }
    }
```   
코드를 보면 느낄 수 있듯이 같은 구조의 코드이고 들어올 데이터와 반환할 타입만 다르다.   
Generic과 Result를 통해 리팩토링을 진행 할 수 있을거라고 생각했다.   
우선 [Generic](https://github.com/zziro95/zzipository/blob/main/Swift/Generic.md)에 대해 정리해보았고 Generic Type을 이용해 리팩토링 한 코드는 아래와 같다.   
<br>

```swift
struct JSONParser<T: Decodable> {
    func decoding(data: Data) throws -> T {
        let jsonDecoder = JSONDecoder()
        let decodingResult: T
        do {
            decodingResult = try jsonDecoder.decode(T.self, from: data)
            return decodingResult
        } catch {
            throw  JSONError.decodingError
        }
    }
}
```   
나중에 encoding을 한다면 Codable을 준수하는 타입들을 허용할 수 있게 리팩토링을 하게 될 가능성이 있고, 현재는 Decodable 한 타입에 대한 Generic Type인 상태이다.   
<br>

#### Result
이제 Result에 대해 살펴보고 어느 쪽이 더 좋은 방안 일지 생각해보자!   

***
### Test method Naming
test 메서드를 보다 명확하게 하기 위해서 좀 더 직관적인 한글로 메서드 이름을 지어줬다.   
메서드 네이밍에 관해서 그렇게 고민을 많이 하진 않았었는데 캠퍼 동기 `Joons`와 서류 스터디 시간에 `TDD`에 대한 이야기를 나눌 때 `Joons`는 어떤 객체에 어떤 작업을 테스트하는 건지 메서드 네이밍을 통해 좀 더 직관적으로 알리려고 했다고 한다.   
코드 예시를 봤을 때도 어떤 객체에 어떤 작업을 테스트하는지 명확히 나타나 있어서 구분 짓기도 좋아 보였고 가독성에도 좋게 느껴졌다.   
앞으로 테스트 메서드 네이밍을 할 때는 당분간 이 방법을 채택해서 진행해보고 더 나은 방법이 있나 나만의 방법도 고려해보자.    
***


### Test Double에 대해 공부하기
유닛 테스트를 한다면 테스트할 주제와 대상 클래스를 정하고, 대상 클래스가 사용하는 의존성(패키지일 수도 있고 특정 함수일 수도 있겠지요)들은 Mock이나 Stub으로 만든다. (Mock과 Stub이란?) Mocking을 어떻게 하는지는 사용하는 언어마다 주로 사용하는 테스팅 프레임워크의 레퍼런스를 참고하라. 그러고 나면 자신이 의존성을 잘 정리했는지 살펴보기 좋아지고, 이어서 테스트하기 좋은 형태가 눈에 들어오기 시작한다.

무엇을 테스트할지 정하기 어렵다면? 
단위 테스트를 예로 들면 자신이 만든 클래스나 모듈, 함수 등의 기능이 정상적으로 동작하는지 확인하기 위해 테스트를 작성한다고 생각해보라.

Swift mock stub
***
### 개발하면서 했던 질문 & 답변
`TDD`에 대한 내용을 이론으로 정리했지만 실제로 테스트 코드를 작성하면서 시간도 너무 오래 걸리고 내 코드에 기준과 이유가 부족함을 느꼈다.   
그리하여 `야곰아카데미` 채널에 질문을 하게 되었다! (소통을 할 커뮤니티가 있다는건..👍)   
<br>

내가 한 질문은 아래와 같다.   
1. 테스트를 위해서 메서드의 `output(리턴 값)`을 꼭 주어야 하는가?    
- 보다 명확한 테스트를 위해 필요하다. 
- `output`이 있어야 메서드의 `결괏값 = 성공한 결과 or 에러`를 통해 메서드의 성공 실패, 또는 결과를 테스트할 수 있다.
-  `output`이 없다면 테스트가 불가능한 것인가?   
<br>

2. 테스트 코드를 잘 짜는 법? / 테스트 코드의 의존관계   
제가 테스트 주도 개발을 하면서 겪은 상황입니다. 
- 하나의 메서드(기능) 마다 input, output을 설정해 주었습니다.
- 그리고 기능마다 Test를 통해 검증하는 식으로 진행하고 있는데 기능 별로 단위를 나누니 제 예상보다 테스트 코드가 복잡했습니다. 
- 예를 들면 `test_JSON_샘플데이터_item만을_디코딩()`에 디코딩 테스트를 위해 `fetchData()`를 해야 해서 do - catch 문을 써야 했습니다. 
- 디코딩 테스트 메서드에 디코딩 할 데이터를 가져오는(**다른 기능**) 함수가 들어오게 됬습니다.    
<br>

해당 코드입니다.   
```swift
func test_JSON_샘플데이터_item만을_디코딩() throws {
    let dataAssetName: String = "item"
    
    do {
        let dataToDecode = try jsonParser.fetchData(fileName: dataAssetName)
        XCTAssertNoThrow(try jsonParser.decoding(data: dataToDecode))
    } catch {
        throw DataAssetError.unknown
    }
}
```   
- decoding을 테스트하기 위해 테스트 구문에 디코딩 할 데이터를 가져오는 메서드 `fetchData`를 넣어줘야 하는데 `fetchData`가 성공해야 `decoding`을 테스트할 수 있습니다.   
- 이러한 방식은 `게시글 작성이 성공`되어야 `게시글 삭제 테스트` 할 수 있는 것처럼 의존관계가 설정되는 경우라고 할 수 있을까요?
- **만약 그렇다면 어떤 식으로 리팩토링을 진행해야 할까요??**   
<br>
<br>

마음먹고 2번 내용을 질문을 하려고 정리하다 보니 새로운 생각이 떠올라서 이 내용도 첨부하였다.   
질문을 위해 정리하는 과정, 내가 가진 의문에 대해서 정리해보는 과정의 중요함을 다시 한 번 느낀다.   
- 온전히 디코딩만을 테스트하려면 디코딩 테스트를 위해 Data 타입의 인스턴스를 생성해 주고 `setUp`에서 JSON 샘플 데이터를 할당해 줍니다.
- 이 샘플 데이터 값이 할당된 Data 타입의 인스턴스를 이용해 온전히 디코딩만을 위한 테스트를 진행합니다. 
이 방법에 대한 의견과 더 좋은 방안이 있을까요?   

---
답변에 대해 100퍼센트 이해하지 못하여 곱씹고 이해해보고 정리해보기 위해 글에 남겼다. (정리가 다 된다면 올라프님의 답변 내용은 지우기!)      
이유는 프로토콜에 대한 개념 부족 때문이라고 진단해보았다.    
<br>

올라프님의 답변      
1번 질문을 "반환값이 없는 메소드는 어떻게 테스트하면 좋을까?" 로 이해해도 될까요? 그렇다면 제 생각은 다음과 같아요.   
```swift
protocol MessageOutputable {
    func show(_ message: String)
}

class A {
    
    private let messageOutputUnit: MessageOutputable
    
    init(messageOutputUnit: MessageOutputable) {
        self.messageOutputUnit = messageOutputUnit
    }
    
    func show(_ message: String) {
        messageOutputUnit.show(message)
    }
}

class MessageOutputUnit: MessageOutputable {
    
    func show(_ message: String) {
        print(message)
    }
}
```   

보통 이런 경우는 의존성이 있는 객체의 메소드를 실행시킬 때라고 생각이됩니다.    
A라는 객체가 MessageOutputUnit이라는 객체에 의존성을 가지고 있습니다.    
난 A라는 객체의 show(_:) 메소드를 테스트하고 싶은데 반환값이 없으니까 테스트를 어떻게 해야할지 모르겠어요.   
이런 경우에 저는 동작을 테스트하곤 합니다.    
<br>

A의 역할은 매개변수를 받아서 MessageOutputUnit의 show(_:) 메소드를 호출해 전달하는 것입니다. 따라서 해당 동작을 제대로 수행하는지를 테스트하면 되겠군요! 
<br>

```swift
import XCTest

class MockMessageOutputUnit: MessageOutputable {
    
    private var show_message: String?
    private var show_callCount: Int = 0
    
    override func show(_ message: String) {
        show_message = message
        show_callCount += 1
    }
    
    func show_validate(message: String, callCount: Int) {
        XCTAssertEqual(message, show_message)
        XCTAssertEqual(show_callCount, callCount)
    }
}
```   
따라서 테스트할 때 위와 같이 Mock 클래스를 만들고 A에게 주입을 해줍니다.   
그리고 when 절에서 A의 show(_:) 메소드를 호출하고, then 절에서는 주입된 MockMessageOutputUnit 클래스의 show_validate(message:callCount) 메소드를 통해 내가 전달한 값이 제대로 전달되었는지, 그리고 원하는만큼 불렀는지를 테스트하면 되지 않을까요?   
<br>

2번 질문에 대해서는 1번에 어느정도 답이 있다고 생각하는데, test_JSON_샘플데이터_item만을_디코딩() 메소드의 역할은 Json을 잘 디코딩 하는가? 까지 검증하는 것이라고 생각이 됩니다.   
따라서 fetchData(fileName:) 메소드의 성공, 실패 여부는 테스트하지 않아도 될 것 같아요.   
Json을 디코딩 하려면, 무조건 Json 이 있어야하니까요.   
이런건 then절에 넣어두면 될 것 같습니다.   

***
### 마무리 글
~~

***
### 참고
- [Getting Started With Unit Testing | XCTest | Swift](https://www.youtube.com/watch?v=P-Zow2yVx4o&t=1481s)
- []()
