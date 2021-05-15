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
    
 > Notation은 표기법이라는 뜻으로 JSON을 언어라고 보는 건 맞지 않고, 데이터를 주고받기 위해 규칙을 정해 놓은 표기법이라고 이해하는 것이 더 좋은 접근이라고 생각한다.   
    
기본 자료형 (Value)
- String
- Number
- Object
- Array
- Boolean (true, false)
- null   

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
   
`JSON`은 컴퓨터가 서로 데이터를 주고받을 때 사람이 컴퓨터가 어떤 데이터를 읽고 쓰는지 편하게 보기 위해서 규칙을 가지고 만든 포맷이다.   
사실 `JSON` 이전에 방시인 `XML`을 사용하거나 기계어를 전달하는 방식이 더 빠르고 기계 친화적인 방법이지만 `JSON`을 쓰는 이유는 사람이 읽기 편하고 널리 표준화 되어 있기 때문이다.    

 ---
 ### JSON Parsing
 프로젝트를 경험하며 나름 `JSON`과 친해졌다고 생각했는데 `JSON`과 함께 자주 등장하는 이 용어 `Parsing`은 무슨 뜻인가..   
 지금부터 알아보자!   
 `Parsing` : 사전적 의미로는 구문 분석이고, 데이터를 조립해 원하는 데이터를 빼내는 것이라고도 할 수 있다. (어떤 데이터를 원하는 폼으로 만드는것)    
 위 예시의  `JSON` 데이터를 그대로 Swift에서 사용할 수 없으니 사용할 수 있게끔 가공하는 작업이라고 보면 될 것 같다.   
    
> `Parser` 란 `Parsing` 을 수행하는 프로그램을 지칭한다.   

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
 - 야곰 아카데미 수업
 - [json.org](http://www.json.org/json-ko.html)
 - [JSON 위키백과](https://ko.wikipedia.org/wiki/JSON)
 - [Zedd님 블로그 JSON 관련 글들](https://zeddios.tistory.com/)
 

