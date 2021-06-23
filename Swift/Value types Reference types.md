# Value types Reference types
맞춤법 검사하기
### 글 쓰게 된 이유
[야곰닷넷](https://yagom.net/courses/reference-and-value-types-in-swift/)에 좋은 강의가 올라와서 완강과 함께 `Value types` 과 `Reference types`에 대해 다시 한번 정리해보는 시간을 가져보고자 합니다.   
[야곰닷넷 강의](https://yagom.net/courses/reference-and-value-types-in-swift/)의 내용을 정리하는 글입니다.   
강의 적극 추천 (`지니`, `코리` 👍👍)   

***
### 값 타입(Value types)과 참조 타입(Reference types)
#### **Value types**
값 타입은 메모리의 스택(Stack) 영역에 저장되는 타입이다.   
메모리에 할당된 값 타입의 데이터를 다른 변수 또는 상수에 복사하면, 각각의 인스턴스는 데이터의 유일한 복사 값을 가진다.   
그렇기 때문에 복사된 인스턴스의 값을 수정해도 기존 인스턴스에는 영향을 주지 않는다.   
<br>

Swift 타입 중 Value types 인 것   
- `struct`, `enum`
- `Int`, `Double`, `String`과 같은 기초 타입 (Fundamental types)
- `Array`, `Set`, `Dictionary`와 같은 컬렉션 타입 (Collection types)
- Value types으로 구성된 `tuple`   
💡 Swift 표준 라이브러리의 값 타입은 `enum`을 제외한 모든 타입이 `struct` 로 구현되어 있다.   
<br>
<br>

#### **Reference types**
참조 타입의 데이터는 메모리의 힙(Heap) 영역에 저장되고, 이 데이터를 가리키는 주소 값은 스택(Stack) 영역에 저장된다.   
데이터를 참조하여 사용하기 때문에 값 타입과 달리 데이터를 할당하거나 전달할 때 값 복사가 아닌 참조 값을 사용한다.   
<br>

Swift 타입 중 Reference types 인 것 
- `class`
- `closure`

***
### 메모리 할당을 고려하여 타입 선택하기
타입을 만들 때 값 타입과 참조 타입 중 어느 타입으로 정의해 주는지도 중요한 요소이다.    
두 타입 사이에 어떠한 성능의 차이가 있는지 알아보자.   
<br>

스택 할당(`Stack allocation`)과 힙 할당(`Heap allocation`)에는 구조적인 차이가 있다.   
`Stack`은 한 방향으로만 데이터를 넣고 빼는 단순한 구조이기 때문에 스택 포인터를 사용하여 빠르게 접근할 수 있다. (`Stack` 구조할 때 그 `Stack`이 메모리에서도 같은 의미의 용어인지 오늘 처음 알았다..ㅎ🙈)   
`Heap`은 할당할 때마다 적절한 메모리 공간이 있는지 확인한 후에 할당을 처리하는 동적인 구조이다.   

`스택 할당`은 많은 시간을 필요로 하지 않지만 그에 비해 `힙 할당`은 보다 복잡한 과정을 가지고 있기 때문에 더 많은 `Overhead`가 발생한다.   
따라서 일반적으로 더 좋은 성능의 코드를 위해선 값 타입을 사용하는 것이 더 좋다.    
<br>

처음에 Swift를 배울 때 웬만하면 Struct를 사용해서 타입을 정의해라라는 말을 들었었는데 이에 대한 좋은 답변인 것 같다.    
<br>
<br>

#### String
Swift에서 `String`은 값 타입으로 분류된다.   
하지만 `String`을 구성하는 문자들은 `Character` 타입으로, 힙 영역에 간접적으로 저장된다고 한다.   
💡그래서 `String`은 값 타입이지만 힙 할당이 발생한다.   
<br>

#### 힙 할당 피하기
힙 할당을 피하여 성능을 개선하는 예시이다.    
```swift
enum Emotion { case happy, sad, angry }
enum Species { case human, bear, dragon }

var cachedEmoji = [String: UIImage]()

func generateEmoji(_ emotion: Emotion, _ species: Species) -> UIImage {
    let key = "\(emotion):\(species)"
    if let image = cachedEmoji[key] {
        return image
    }
    ...
}
```   
위 코드는 `let key = "\(emotion):\(species)"` `String`타입의 `key` 상수를 딕셔너리의 키값으로 사용하고 있다.   
앞서 말했듯이 String은 값 타입이지만 힙 할당이 발생하므로 성능 개선을 위해 `String` 대신 `Struct`를 이용해 새로운 타입을 만들어 힙 할당을 피할 수 있다고 한다.   
<br>

```swift
struct Attributes: Hashable {
    var emotion: Emotion
    var species: Species
}
```   
`Attributes`라는 타입은 `struct`로 선언되었으므로 값 타입이고, 프로퍼티들의 타입들 `Emotion`, `Species` 또한 `enum` 타입이기 때문에 이 구조체의 인스턴스를 생성할 때에는 힙 할당이 아닌 오로지 스택 할당만 발생한다.   

```swift
타입을 [String: UIImage] -> [Attributes: UIImage]로 바꿔 주었다.

var cachedEmoji = [Attributes: UIImage]()

func generateEmoji(_ emotion: Emotion, _ species: Species) -> UIImage {
    let key = Attributes(emotion: emotion, species: species)
    if let image = cachedEmoji[key] {
        return image
    }
    ...
}
```   
이와 같은 코드를 작성하여 `Character` 처럼 힙 할당이 발생하는 타입을 피하고, 오로지 스택 할당만 발생해 이전 보다 성능이 개선되었다고 볼 수 있다.   
<br>

💡 Hashable 은 사용자 정의 타입을 컬렉션에 사용하기 위해 필요한 프로토콜이라고 한다.   
예시에서는 딕셔너리가 컬렉션 타입이기 때문에 딕셔너리의 키값으로 사용하기 위해 채택한 경우이다.   
Hashable에 대한 정리도 필요하다고 느꼈다.   

***
### Copy-on-Write in Swift
값 타입을 복사하면 각각의 인스턴스는 유일한 복사 값을 가지지만 항상 그렇지는 않다.   
Swift에서는 효율적으로 자원을 관리하기 위해 `Copy-on-Write`라는 기술을 사용하여 인스턴스의 불필요한 복사를 줄인다. 알아보자.   
<br>

`Copy-on-Write`는 인스턴스를 복사할 때 먼저 참조를 통해 불필요한 복사를 줄이고, 수정이 발생하는 경우에만 실제로 복사하는 방식?이라고 한다.   
Swift에서는 기본적으로 Collection 타입(`Array`, `Set`, `Dictionary`)에 COW가 구현되어 있으며 타입에 직접 구현할 수도 있다.    
설명이 잘 이해가 안가지만 예시 코드를 보면 이해할 수 있을 것 같다.   
```swift
var array1: [Int] = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
print(UnsafeRawPointer(array1)) // 0x0000000100704210

var array2 = array1
print(UnsafeRawPointer(array2)) // 0x0000000100704210

array2.removeLast() // Copy-on-Write
print(UnsafeRawPointer(array1)) // 0x0000000100704210
print(UnsafeRawPointer(array2)) // 0x0000000100404e70
```   
우리는 array가 값 타입임을 알고 있다.   
따라서 `var array2 = array1`를 해준다 해도 각각의 인스턴스는 유일한 복사 값을 가지고 있다.   
하지만 이 시점에 `UnsafeRawPointer`를 이용해서 실제 메모리 할당 주소를 확인해 보면 두 인스턴스는 같은 주소를 공유하고 있음을 확인할 수 있다.   
이는 값 복사는 하였지만 그 안에 데이터가 변화되지 않았기 때문에 미리 불필요하게 새로운 메모리를 할당하지 않은 것이라고 이해했다.   
`array2.removeLast()`와 같이 데이터의 변화가 발생하면 참조를 끊고 그때서야 다른 메모리 공간을 할당한다.   
값 타입을 할당하더라도 데이터가 수정되지 않고 서로 같은 값을 가지고 있는 상황이라면 새로운 메모리를 차지하는 게 비효율적이므로 이러한 기술이 생긴 것 같다.👍   

---
### 값 타입과 참조 타입의 혼합 사용
#### **값 타입 안의 참조 타입**
예시 코드   
```swift
// 값 타입인 Student 구조체가 참조 타입인 HighSchool 타입의 프로퍼티를 포함하는 코드

class HighSchool: CustomStringConvertible {
    var description: String {
        return "\(name) High School"
    }

    var name: String

    init(name: String) {
        self.name = name
    }
}

struct Student {
    var highSchool: HighSchool
}

let swiftHighSchool = HighSchool(name: "Swift")

let student1 = Student(highSchool: swiftHighSchool)
let student2 = Student(highSchool: swiftHighSchool)

student2.highSchool.name = "Next"

print(student1.highSchool) // Next High School
print(student2.highSchool) // Next High School
```   
하나의 참조 타입 인스턴스를 생성하고 각각의 값 타입 인스턴스의 프로퍼티로 할당해 준다.   
`student2`를 통해서 프로퍼티의 이름에 대한 값을 변경했음에도 변경한 프로퍼티가 참조 타입의 프로퍼티이기 때문에 변경된 값이 공유 됨을 확인할 수 있다.    
<br>

#### **참조 타입 안의 값 타입**
예시 코드
```swift
// 참조 타입인 Product 클래스가 값 타입인 Company 타입의 프로퍼티를 포함하는 코드

struct Company {
    var name: String
}

class Product {
    var name: String
    var company: Company

    init(name: String, company: Company) {
        self.name = name
        self.company = company
    }
}

let apple = Company(name: "Apple")

let iPhone = Product(name: "iPhone12", company: apple)
let macbookAir = Product(name: "Macbook Air", company: apple)

macbookAir.company.name = "Microsoft"

print(iPhone.company.name)     // Apple
print(macbookAir.company.name) // Microsoft
```   
값 타입의 인스턴스를 생성, 값 할당을 해주었다.   
그 후 각각의 참조 타입 인스턴스를 생성해 주고 company 프로퍼티에 값 타입 인스턴스인 apple을 할당해 주었다.     
이후 macbookAir의 company 프로퍼티를 변경해 준 뒤 두 참조 타입 인스턴스 iPhone, macbookAir를 비교해봤을 때 company 프로퍼티는 값 타입이기 때문에 참조하지 않고 새로운 메모리를 할당받아 변경된 데이터 값을 가지고 있음을 확인할 수 있다.   
<br>

---
### 마무리 글
애플은 일반적으로 구조체를 선호하고 필요에 따라 클래스를 사용하도록 권장한다.   
그러나 구조체의 성능이 반드시 우수한 게 아니기 때문에 상황에 맞게 고려해 봐야 한다는 점이 가장 중요한 내용이었던 것 같다.   
<br>

어찌 보면 가장 기본적인 내용이지만 강의를 들으면서 몰랐던 내용들이 참 많았구나 새삼 느꼈다.   
아주 보람찬 시간이었고, 좋은 강의를 만들어준 야곰닷넷과 `지니`, `코리`에게 감사하다.   
🍀  회고 때 다시 보기 - COW 직접 구현하기 부분.   

***
### 참고
- [야곰닷넷 강의](https://yagom.net/courses/reference-and-value-types-in-swift/)
