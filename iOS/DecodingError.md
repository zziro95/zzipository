# DecodingError
### 글 쓰게 된 이유
디코딩 함수의 오류 처리를 위해 공부   

***
### DecodingError
[DecodingError](https://developer.apple.com/documentation/swift/decodingerror)를 살펴보자.   
<br>

`DecodingError` - 값을 디코딩 하는 동안 발생하는 오류를 나타내는 열거형
- `dataCorrupted(DecodingError.Context)`: 데이터가 손상되었거나 유효하지 않음을 나타내는 케이스 
    - (ex. JSON 데이터의 문법적인 오류가 있을 경우)
- `KeyNotFound(CodingKey, DecodingError.Context)`: 키가 있는 디코딩 컨테이너가 주어진 키에 대한 항목을 요청했지만 포함되어 있지 않았을 때의 케이스 
    - (ex. 정의한 타입의 프로퍼티명(key값)이 JSON 데이터의 키값에 없을 경우)   
```swift
// zziro라는 키값이 JSON 데이터에는 존재하지 않음
// 정의한 타입
struct ZZiro: Decodable {
    let zziro: String?
    let name: String?
    let age: Int?
}

// JSON 데이터
{
    "name" : "ZZIRO",
    "age" : 100
}
```   
- `typeMismatch(Any.Type, DecodingError.Context)`: 인코딩 된 payload에서 찾은 타입과 일치하지 않아 주어진 유형의 타입으로 디코딩 할 수 없을 때의 케이스
- `valueNotFound(Any.Type, DecodingError.Context)`: 주어진 타입의 값이 옵셔널이 아닌 값이 예상됐지만, null 이 발견 되었을 때의 케이스
    - (ex. 정의한 프로퍼티 타입이 `optional`이 아닌 타입일 때 `null` 값이 들어오는 경우) 
    - 정의한 프로퍼티의 타입에 `optional`을 선언해 주면 JSON 데이터를 통해 `null` 값이 들어와도 valueNotFound로 걸러지지 않는다.
<br>
<br>

에러 내용을 좀 더 자세하게 표현하고 싶다면 `DecondingError.Context`의 프로퍼티를 사용하면 된다.    
`DecondingError.Context` (Struct)의 프로퍼티.  
- codingPath: [CodingKey] - 디코딩 호출이 실패한 지점에 도달하기 위해 사용된 코딩 키의 경로 (어느 코딩 키에서 오류가 났는지 알려준다.)
- debugDescription: String - 디버깅 목적으로 무엇이 잘못되었는지에 대한 설명
- underlyingError: Error? - 이 오류를 발생시킨 근본적인 오류(있다면)   

***
### Decoding 시 오류 처리에 방법에 대한 고민
JSON Decoding 상황에서 오류 처리하는 과정에서 생긴 의문이다.   
<br>

💡 **첫 번째 고민**
간단하게 얘기해보자면 두 가지 방법 중 어떤 게 더 좋은 방법일까에 대한 고민이었다.   
1. LocalizedError를 이용한 에러 처리
    - 나와 팀원들이 오류가 발생했을 때 debugprint()를 통해 보다 쉽게 어떤 오류인지 인지할 수 있다. (한국어!)
    - 조금 더 이유 있는 코드 같아 보인다.   
2. NSError의 localizedDescription 프로퍼티를 이용하는 방법
    - 장점: 코드가 매우 간결하다.!   
코드 예시는 이러하다.   
```swift
// 첫번째의 경우는 제가 따로 JSONDecodingError을 만들어주어서 에러처리를 하는 방법입니다.

enum JSONDecodingError: Error {
    case dataCorrupted
    case keyNotFound
    case typeMismatch
    case valueNotFound
    case unknown
}

extension JSONDecodingError: LocalizedError {
    var errorDescription: String {
        switch self {
        case .dataCorrupted:
            return "데이터가 손상되었거나 유효하지 않습니다."
        case .keyNotFound:
            return "주어진 키를 찾을수 없습니다."
        case .typeMismatch:
            return "주어진 타입과 일치하지 않습니다."
        case .valueNotFound:
            return "예상하지 않은 null 값이 발견되었습니다."
        case .unknown:
            return "알 수 없는 에러가 발생했습니다."
        }
    }
}

// decoding시 에러 처리하는 메서드
func decoding(data: Data) throws -> T {
    let jsonDecoder = JSONDecoder()
    let decodingResult: T
    do {
        decodingResult = try jsonDecoder.decode(T.self, from: data)
        return decodingResult
    } catch DecodingError.dataCorrupted {
        debugPrint(JSONDecodingError.dataCorrupted.errorDescription!)
        throw  JSONDecodingError.dataCorrupted
    } catch DecodingError.keyNotFound {
        debugPrint(JSONDecodingError.keyNotFound.errorDescription!)
        throw  JSONDecodingError.keyNotFound
    } catch DecodingError.typeMismatch {
        debugPrint(JSONDecodingError.typeMismatch.errorDescription!)
        throw  JSONDecodingError.typeMismatch
    } catch DecodingError.valueNotFound {
        debugPrint(JSONDecodingError.valueNotFound.errorDescription!)
        throw  JSONDecodingError.valueNotFound
    } catch {
        debugPrint(JSONDecodingError.unknown.errorDescription!)
        throw  JSONDecodingError.unknown
    }
}
```   
이렇게 하면 원하는 데로 다양한 상황에서 어떤 오류인지 상황을 분리해서 보다 자세하게 확인이 가능해서 좋았다.   
그런데 다른. 방법도 있다는 것을 알게 되었다.   
<br>

```swift
// 그리고 두번째는 NSError의 localizedDescription을 이용하는것 인데
do {
  self.sampleData = try jsonDecoder.decode([SampleData].self, from: dataAsset.data)
} catch let error {
  debugPrint("\(error.localizedDescription)")
}
```   
두 경우 모두 `debugPrint`를 하였을 때 각 에러 상황에 맞는 문자열을 출력해 주는데 차이점이라면 `LocalizedError` 프로토콜을 이용하는 경우는 한국어로 로그를 볼 수 있어서 나와 팀원들이 어떤 오류가 발생했는지 좀 더 알기 쉽다는 점이 있지만..   
그 장점밖에 느껴지지 않아서 두 방법 중 어떤 방법이 좋은 방법일까 or 더 좋은 에러 처리 방식도 있을까?? 고민을 하게 되었다.   
<br>

💡 **두 번째 고민**
`NSError`의 `localizedDescription`을 사용하는 경우는 어떤 경우가 있을까?
얼럿으로 사용자에게 알리는 것과 같은 (콘솔 창이 아닌 화면에 띄워야 하는 오류) 여러 국가?에서 지역에 맞는 오류 문구를 표현해 주기 위해 사용하는 게 적합하다는 생각이 들었다.   
<br>

어느 정도 결론을 내리긴 했는데 다른 사람의 의견을 듣고 싶어서 캠퍼 동기 `태태`에게 도움을 청해 의견을 물어봤다. (고마워요 `태태` 🙇)   
<br>

📝 **정리**   
질문하기 위해 정리하면서 `LocalizedError`를 사용하는 쪽이 더 이유 있어 보인다고 생각했고 `태태`도 나와 비슷하게 생각한다고 이야기해 주었다.     
정리해 보면 `LocalizedError`를 사용하는 방식이 어떤 오류가 발생했는지 좀 더 알기 쉽고, 그에 따라 대응하기에도 더 수월할 것이다.   
어느 정도 정리는 됐지만 긴가민가하기도 했고, 확실히 결론 내리지 못한 고민이었다.   
동료와 함께 이야기 나누기 위해 정리하고 이야기도 나눔으로써 나의 생각을 정리할 수 있어 좋았고, 이 고민을 통해 평소에 생각하지 못할 `NSError의 localizedDescription을 언제 사용하는 게 좋을까?`와 같은 질문을 스스로에게 던질 수 있어서 좋았다.   
***
### 소제목
~~

***
### 마무리 글
~~

***
### 참고
- [[Enum] DecodingError](https://developer.apple.com/documentation/swift/decodingerror)
- [[Struct] DecodingError.Context](https://developer.apple.com/documentation/swift/decodingerror/context)
- [[Protocol] LocalizedError](https://developer.apple.com/documentation/foundation/localizederror)
- [NSError > localizedDescription](https://developer.apple.com/documentation/foundation/nserror/1414418-localizeddescription)
