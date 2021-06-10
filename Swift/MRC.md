# MRC
### 글 쓰게 된 이유
솔직히 말하자면 캠퍼들과 스터디를 준비하는 과정에서  `MRC`에 대해 공부를 해야 하기 때문에 글을 작성하게 되었다.   
지금은 Swift가 제공해주는 `ARC`를 통해 메모리가 자동으로 관리되지만 그 이전에는 `MRC`라고 수동으로 `Reference Count`를 계산하는 방식으로 메모리를 관리했다고 한다.   
`Objective-C`의 영역이라고 생각되지만 어짜피 살펴봐야되게 된 이상 조금이라도 정성스럽게 보기 위해 글을 쓰기로 했다.   
깊숙히 보단 얇게 보며 대략적인 내용을 정리하게 될 것 같다.   
참고하는 글들에 `Objective-C` 들이 있지만 제대로 알고 있지 않고 문맥상 이해하는 코드들이기 때문에 코드는 가져오지 않았습니다.   

---
### MRC
`Automatic Reference Counting - ARC` 와 달리 개발자가 직접 수동관리하는 `MRC` 방식은 `Manual Reference Counting`이라 불린다.   
`Manual Retain Release - MRR`이라고 불리기도 하는데 편의상 `MRC`라고 부르겠다.    
`RC`는 Reference Count (참조 횟수)를 뜻하는데 `MRC`에서 정확하게는 Retain Count라고 부른다고 한다.   
참조 횟수라고 생각하면 될 듯 하다.   
<br>

`Objective-C`에서는 인스턴스를 새로 생성할 때 메서드가 `alloc`, `new`, `copy`, `mutableCopy`가 있다고 한다.   
인스턴스를 생성과 동시에 할당을 한다면 참조 횟수(Retain Count)가 1이 된다고 한다. (`ARC`와 같네요).  
**새로 인스턴스를 생성할 경우에만** 참조 횟수가 1로 자동으로 증가한다.   

#### Retain Release
RC를 수동으로 증가(Retain), 감소(Release) 시킬 때 사용하는 메서드이다.   
<br>

Retain에 대해서 알아보자.   
새로 인스턴스가 생성될 경우에는 자동으로 참조 횟수가 1로 증가한다는 걸 알고있다.   
따라서 우리는 위와 같은 경우에는 Retain을 써줄 필요가 없다, 써서는 안된다가 더 맞는 표현인 것 같다.    
그럼 이. **만들어진 인스턴스를 참조할 때** Retain을 써줘야 한다가 된다.   
**인스턴스의 주소값을 할당받은 경우**, **인스턴스에 대한 소유권을 가진 경우**라는 표현도 같은 표현이다.    
<br>

이제 Release다.   
기존 인스턴스를 참조하던 인스턴스를 더이상 사용하지 않을거라 `nil`을 대입할때 `ARC`는 자동으로 참조 횟수가 줄어든다.   
하지만 `MRC`의 경우는 개발자가 인스턴스간의 관계를 인지하고 있어야 하며 위와 같이 더이상 사용하지 않을 인스턴스에 대해 Release라는 메서드를 호출해 주어 수동으로 참조 횟수를 1 줄여주어야 한다.   

#### autorelease
autorelease pool 블록 내에서 생성한 객체들을 적절한 시점에 한 번에 해제할 수 있도록 해주는 방법   

---
### 면접 대비 문제 & 답변
- [ ]  ARC 대신 Manual Reference Count 방식으로 구현할 때 꼭 사용해야 하는 메서드들을 쓰고 역할을 설명하시오.
    - `Retian Count`를 수동으로 증가시키는 Retain과 감소시키는 Release 메서드가 있고, RC를 autorelease pool block 끝에서 줄여주는 autorelease가 있다.
    - `Objective-C`에서는 `참조 타입` 인스턴스를 새로 생성할 때 Retain 메서드를 사용해 주어야 하나요?
        - `Objective-C`에서 사용하는 `alloc`, `new`, `copy`, `mutableCopy` 메서드를 통해 인스턴스를 최초로 생성해주었을 때에는 자동으로 참조 횟수가 1로 증가하기 때문에 Retain 메서드를 사용하지 않아도 된다.   
<br>

- [ ]  retain 과 assign 의 차이점을 설명하시오.
    - retain은 Retain Count 증가와 동시에 객체를 참조할 포인터 값을 설정
    - assign은 Retain Count를 증가시키지 않고 객체를 참조할 포인터 값을 설정. weak와 비슷한 개념으로 보인다.   
<br>

- [ ]  특정 객체를 autorelease 하기 위해 필요한 사항과 과정을 설명하시오.
    - autorelease pool은 pool 자체가 draining 될 때 메시지를 보내는 개체를 저장한다고 한다,
    - lazy 한 방법같은데 이해가 잘 안된다..   
<br>

- [ ]  Autorelease Pool을 사용해야 하는 상황을 두 가지 이상 예로 들어 설명하시오.
    - Foundation 전용 프로그램을 작성할 때
    - 스레드를 분리하는 경우
        - 애플리케이션 또는 스레드가 오래 지속되고 잠재적으로 많은 autoreleased objects들을 생성하는 경우 Autorelease Pool을 사용해야 한다고 한다.
        - AppKit과 UIKit이 메인 스레드에서 수행되는 것 처럼 autoreleased objects들을 생성할 때 Autorelease Pool을 사용해야 한다는 이야기 인것 같다.
        - Autorelease Pool을 사용하지 않으면 autoreleased objects들이 누적되고 메모리 사용량이 증가한다고 한다.   
<br>

- [ ]  다음 코드를 실행하면 어떤 일이 발생할까 추측해서 설명하시오. Ball *ball = [[[[Ball alloc] init] autorelease] autorelease];
    - `[[Ball alloc] init]`까지는 Ball이라는 타입을 생성 초기화 하여 ball 인스턴스에 할당
    - autorelase는 중첩이 가능하다고 한다. 따라서  autoreleasepool 블록이 중첩되어 있는 구조로 보인다. 
    - 그러나 위의 코드에 대해서는 어떤 일이 발생할지 잘 모르겠다...   
<br>

***
### 참고
- [Memory Management Policy](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/MemoryMgmt/Articles/mmRules.html#//apple_ref/doc/uid/20000994-BAJHFBGH)
- [Using Autorelease Pool Blocks](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/MemoryMgmt/Articles/mmAutoreleasePools.html#//apple_ref/doc/uid/20000047-CJBFBEDI)
- [NSAutoreleasePool](https://developer.apple.com/documentation/foundation/nsautoreleasepool)
