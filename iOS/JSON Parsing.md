 # JSON Parsing
 ### 글 쓰게 된 이유
 `REST API`를 통해 데이터를 주고받을 경우 `JSON` 데이터 형식을 이용하여 주고받는 경우가 많습니다.   
 프로젝트를 진행하며 자주 다뤘던 `JSON`에 대해 알아보고 고민점들을 글로 정리하여 구체화하고 해결 방안을 찾아보기 위해 글을 쓰게 되었습니다. 

 ***
 ### JSON
 JSON (JavaScript Object Notation)   
 - `Key-Value`로 이루어진 데이터 객체를 전달하기 위해 인간이 읽을 수 있는 텍스트를 사용하는 개방형 표준 포맷
 - 비동기 브라우저/서버 통신(AJAX)을 위해 넓게는 XML을 대체하는 주요 데이터 포맷이다.
 - 인터넷에서 자료를 주고받을 때 그 자료를 표현하는 방법
 - 자바스크립트 언어로부터 파생되어 자바스크립트의 구문 형식을 따르지만 언어 독립형 데이터 포맷이다.   
<br>

 > Notation은 표기법이라는 뜻으로 JSON을 언어라고 보는 건 맞지 않고, 데이터를 주고받기 위해 규칙을 정해 놓은 표기법이라고 이해하는 것이 더 좋은 접근이라고 생각한다.   
 <br>
 
기본 자료형 (Value)
- String
- Number
- Object
- Array
- Boolean (true, false)
- null   
<br>

❗Key 값은 모두 String으로 표기해야 되기 때문에 `""` 로 묶어 줘야 한다.   
```JSON
// Object
{ 
    // Array
    "persons" : [ 
        {
            "name": "zziro",
            "age": 100,
            "marital_status": false,
            "motto": null
        },
        {
            "name": "zziroro",
            "age": 30,
            "marital_status":  true,
            "motto": null
        }
    ]
}
```    
<br>

`JSON`은 컴퓨터가 서로 데이터를 주고받을 때 사람이 컴퓨터가 어떤 데이터를 읽고 쓰는지 편하게 보기 위해서 규칙을 가지고 만든 포맷이다.   
사실 `JSON` 이전에 방시인 `XML`을 사용하거나 기계어를 전달하는 방식이 더 빠르고 기계 친화적인 방법이지만 `JSON`을 쓰는 이유는 사람이 읽기 편하고 널리 표준화 되어 있기 때문이다.    

 ---
 ### JSON Parsing
 프로젝트를 경험하며 나름 `JSON`과 친해졌다고 생각했는데 `JSON`과 함께 자주 등장하는 이 용어 `Parsing`은 무슨 뜻인가..   
 지금부터 알아보자!   
 `Parsing` : 사전적 의미로는 구문 분석이고, 데이터를 조립해 원하는 데이터를 빼내는 것이라고도 할 수 있다. (어떤 데이터를 원하는 폼으로 만드는것)    
 위 예시의  `JSON` 데이터를 그대로 Swift에서 사용할 수 없으니 사용할 수 있게끔 가공하는 작업이라고 보면 될 것 같다.   
<br>

> `Parser` 란 `Parsing` 을 수행하는 프로그램을 지칭한다.   
<br>

**JSON을 파싱에는 `JSONSerialization` 과 `Codable` 을 이용하는 두가지 방식이 있는걸로 보인다.**    
하나씩 살펴보도록 하자!   
 ***
 
 ### JSONSerialization
 `JSONSerialization` 을 먼저 설명하는 이유는 알아보는 과정에서 아마도 `Codable` 보다 먼저 사용됐던 방식으로 확인했기 때문이다.   
 `Codable`이 Swift4에서 나왔다고 하는데 이 전에는 `JSONSerialization`을 사용하여 파싱 하였다고 한다.   
 `Codable`밖에 안 써봐서 감사함을 몰랐지만 왜 다들 더 편해하고 두 팔 벌려 환영해 주었는지 느끼게 되는 것 같다 얼른 시작해보자.   
 <br>
 
[JSONSerialization](https://developer.apple.com/documentation/foundation/jsonserialization) 공식문서를 살펴보면 JSONSerialization 클래스를 사용하여 JSON <-> Foundation 개체간에 변환해줄 수 있다.   
JSON 개체를 Foundation 개체로 변환하려면 다음과 같은 조건이 충족되어야 한다.   
- top level object 는 NSArray이거나 NSDictionary 이여야 한다.
- 모든 Object값은 String, Number, Array, Dictionary, Null 이여야 한다.
- 모든 Key값은 String 이여야 한다.
- Number는 NaN 이나 infinity 면 안된다.   
이 외에도 다른 규칙이 적용될 수도 있으니 개체를 JSON 데이터로 변환 할 수 있는지 여부를 [isValidJSONObject(_:)](https://developer.apple.com/documentation/foundation/jsonserialization/1418461-isvalidjsonobject) 메서드를 통해 확인하는 습관을 가지는게 좋을듯 하다.   

실질적으로 JSON 데이터를 Foundation 개체로 변환하는 작업은 [jsonObject(with:options:)](https://developer.apple.com/documentation/foundation/jsonserialization/1415493-jsonobject) 메서드가 해준다.   
반대 작업(Foundation -> JSON)은 [data(withJSONObject:options:)](https://developer.apple.com/documentation/foundation/jsonserialization/1413636-data) 메서드가 해주는걸로 보인다.   
[Zedd님 블로그](https://zeddios.tistory.com/148)를 보고 코드를 따라 치므로써 파싱 과정에 대해 좀 더 이해할 수 있었다.   
```swift
let dataPath: String = "/Users/jinhochoi/Desktop/zziroJSON/zziroData.json"

// 로컬 경로를 통해 JSON 데이터 가져오기
if let data = try? String(contentsOfFile: dataPath).data(using: .utf8) {
    // JSONSerialization.jsonObject 메서드를 이용하여 Foundation 개체로 변환한다.
    let json = try? JSONSerialization.jsonObject(with: data, options: []) as! [String : Any]
    print(json)
}
```
<br>

주석을 이용하여 정리를 해보았고 글에서도 언급해주시듯이 json 파일 형식에 맞게 `as` 뒤에 타입을 선언해주어야 변환이 가능하다는 주의점이 있다.   
지금 까지의 작업은 데이터를 가져와 Foundation 개체로 변환시켜 준 것이고, 이제 그 데이터를 사용할 수 있도록 파싱을 해줘야 한다. (위에 데이터를 가져오는 작업이 파싱인 줄 알았지만 그냥 데이터의 틀을 가져왔다 정도로 이해했다.)   
```swift
// 각 타입에 맞게 파싱한 데이터를 저장할 배열 선언
var nameArray = [String]()
var ageArray = [Int]()
var maritalStatusArray = [Bool]()
var mottoArray = [String?]()

// 가져온 데이터를 키값을 가지고 분류해 배열에 담아주기
if let persons =  json["persons"] as? [[String: Any]]{
    for index in persons {
        nameArray.append(index["name"] as! String)
        ageArray.append(index["age"] as! Int)
        maritalStatusArray.append(index["marital_status"] as! Bool)
        mottoArray.append(index["marital_status"] as? String)
    }
}

/*
각 배열 출력 결과
["zziro", "zziroro"]
[100, 30]
[false, true]
[nil, nil]
*/
```
<br>

`Codable`을 먼저 써보고 이 방법을 써보니 조금 이해하기도 어려웠고 원하는 정보에 접근하는 작업이 더 불편하다고 느껴졌다.   
`Codable`은 데이터를 가져오고 디코딩을 하기 위해 JSON 형식에 맞게 타입을 선언해주기 때문에 키 값에 맞춰 데이터들이 할당되어 데이터 사용에 편리 효율적입니다.   
이런 방식이 있구나 알아두고 `Codable`을 쓰자...   

 ---
 
 ### Codable
 [Codable](https://developer.apple.com/documentation/swift/codable)도 공식문서를 살펴보면 자신을 외부 표현으로 변환하거나 외부 표현으로 변환 할 수 있게 하는 프로토콜임을 알 수 있다.    (자신(type) <-> 외부표현(ex. JSON))   
 또한 `Encodable` & `Decodable` 프로토콜의 typealias 이므로 인코딩과 디코딩을 모두 가능하도록 지원해주는 프로토콜이다.     
 하지만 정의하는 타입이 인코딩을 하지 않을 경우에는 `Decodable` 만 채택하는 방식이 더 이유있는 코드에 가깝다고 생각한다.    
 <br>
 
 `Decodable`은 외부 표현에서 자신의 형식으로 변환 해주는 프로토콜이고 (Parsing), `Encodable`은 자신을 외부 표현으로 변환 해주는 프로토콜이다.   
 **<Struct, Class, Enum 전부 채택 가능>>**    
 
 ---
 
 ### CodingKey
JSON 형태의 데이터로 변환하고자 하면, 기본적으로 JSON 타입의 키(Key)와 사용자가 정의한 프로퍼티가 일치해야 한다.   
Key와 프로퍼티의 이름을 다르게 사용하고 싶다면, 타입 내부에 CodingKeys 라는 String 타입의 열거형을 선언 (why:question: `JSON의 키값은 String 타입이니까`) , CodingKey 프로토콜을 채택하면 된다.   
<br>

나는 `CodingKey`를 JSON의 키 값이 스네이크케이스로 되어있던 부분을 카멜케이스로 변환해주기 위해 사용하였는데, **축약된 표현이나 타입의 프로퍼티로서 모호한 네이밍을 좀 더 명확하게 바꿔줄 수 있다**는 장점이 있다.   

***
 ### 마무리 글
 JSON 데이터의 내용을 로컬을 통해 가져오거나, API를 통해 받아온다
 <br>

 1. JSONSerialization.jsonObject 메서드를 이용하여 Foundation 개체로 변환 후 Key값을 통해 값을 불러와 인스턴스 프로퍼티에 할당해준다.
 2. Decodable을 이용하는 경우 가져올 데이터의 형식에 맞춰 선언한 타입에 Decodable 프로토콜을 채택해주고 JSONDecoder를 통해서 Key값과 매칭되는 프로퍼티에 값을 할당해준다.
 <br>

 JSONSerialization에서 JSON을 Foundation 개체로 변환 후 원하는 값을 뽑아내는 작업을 Codable을 이용하면 좀 더 편리하게 사용할 수 있다라는 장점이 있다.!

 ***
 ### 참고
 - 야곰 아카데미 수업
 - [json.org](http://www.json.org/json-ko.html)
 - [JSON 위키백과](https://ko.wikipedia.org/wiki/JSON)
 - [Zedd님 블로그 JSON 관련 글들](https://zeddios.tistory.com/)
 - [JSONSerialization](https://developer.apple.com/documentation/foundation/jsonserialization)
 - [Codable](https://developer.apple.com/documentation/swift/codable)
 - [Encoding and Decoding Custom Types
](https://developer.apple.com/documentation/foundation/archives_and_serialization/encoding_and_decoding_custom_types)
- [CodingKey](https://developer.apple.com/documentation/swift/codingkey)
- [Naverboostcourse](https://www.boostcourse.org/mo326/lecture/18732) 
