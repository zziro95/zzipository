# CustomTextField   

### 방법
이 [문서](https://www.fivestars.blog/articles/how-to-customize-textfields/)를 주로 참조하였고, 여러 방법에 대해 자세히 정리되어 있다.    
1. ViewModifier를 이용하는 형식
2. TextFieldStyle를 채택하는 방식
3. UIViewRepresentable를 이용한 UITextField 사용
4. [SwiftUI-Introspect](https://github.com/siteline/SwiftUI-Introspect) 라이브러리 사용 
<br>
***

### ViewModifier를 이용하는 형식
#### 직접 타입을 만들어 적용하는 형식   
아래 코드는 [문서](https://www.fivestars.blog/articles/how-to-customize-textfields/)에 있는 코드를 그대로 옮긴 코드이다.   
주석을 자세히 적어준 덕분에 `.accentColor()`를 이용하여 커서의 색상도 변경해 줄 수 있음을 알게 되었다.   
이러한 형태의 장점은 변경하고 싶은 부분이 생길 경우 이 타입 자체만 변경해주기 때문에 독립적인 구분되어 있다는 점이 장점일 것 같다.   
```swift
public struct FSTextField: View {
  var titleKey: LocalizedStringKey
  @Binding var text: String

  /// Whether the user is focused on this `TextField`.
  @State private var isEditing: Bool = false

  public init(_ titleKey: LocalizedStringKey, text: Binding<String>) {
    self.titleKey = titleKey
    self._text = text
  }

  public var body: some View {
    TextField(titleKey, text: $text, onEditingChanged: { isEditing = $0 })
      // Make sure no other style is mistakenly applied.
      .textFieldStyle(PlainTextFieldStyle())
      // Text alignment.
      .multilineTextAlignment(.leading)
      // Cursor color.
      .accentColor(.pink)
      // Text color.
      .foregroundColor(.blue)
      // Text/placeholder font.
      .font(.title.weight(.semibold))
      // TextField spacing.
      .padding(.vertical, 12)
      .padding(.horizontal, 16)
      // TextField border.
      .background(border)
  }

  var border: some View {
    RoundedRectangle(cornerRadius: 16)
      .strokeBorder(
        LinearGradient(
          gradient: .init(
            colors: [
              Color(red: 163 / 255.0, green: 243 / 255.0, blue: 7 / 255.0),
              Color(red: 226 / 255.0, green: 247 / 255.0, blue: 5 / 255.0)
            ]
          ),
          startPoint: .topLeading,
          endPoint: .bottomTrailing
        ),
        lineWidth: isEditing ? 4 : 2
      )
  }
}
```   
<br>
#### ViewModifier를 구현해주는 방식   
같은 역할을 하지만 ViewModifier로 묵어서 적용해 주었다고 이해하면 좋을 것 같다.   
이러한 형태는 같은 다른 건 다 같은데 backgroundColor만 다르게 표현해 준다던지 padding 값의 차이를 둔다던지 예외 케이스를 처리해 주기에 용이할 것 이다.   
개인적으로는 위의 방식보단 ViewModifier로 구현하는 방식이 유연하게 대처할 수 있으므로 좋다고 생각한다.   
예를 들어 `Case1TextField`, `Case2TextField`의 스타일이 약간의 차이가 있고, 타입을 각각 구현해주고 싶다면 두 구체타입을 만들되 하나의 `SearchTextFieldModifier`만 사용하면 구현이 가능할 것이다.   
이는 코드의 재사용을 통해 중복코드를 없애준다.   
하지만 `Case1TextField`, `Case2TextField`의 다른 스타일이 `SearchTextFieldModifier`로만 제어하기 힘들다면(완전히 다른 스타일의 경우) **직접 타입을 만들어 적용하는 형식**이 더 효과적이다.      
```swift
struct SearchTextFieldModifier: ViewModifier {

    let verticalPadding: CGFloat
    let horizontalPadding: CGFloat
    let backgroundColor: Color
    let cornerRadius: CGFloat

    init(verticalPadding: CGFloat = 10,
         horizontalPadding: CGFloat = 16,
         backgroundColor: Color = Color.gray,
         cornerRadius: CGFloat = 20) {
        self.verticalPadding = verticalPadding
        self.horizontalPadding = horizontalPadding
        self.backgroundColor = backgroundColor
        self.cornerRadius = cornerRadius
    }

    func body(content: Content) -> some View {
        content
            .padding(.vertical, verticalPadding)
            .padding(.horizontal, horizontalPadding)
            .background(backgroundColor)
            .cornerRadius(cornerRadius)
    }
}

// 사용 예시 코드
TextField("Search...", text: $text)
    .modifier(SearchTextFieldModifier())
```   
<br>
***

### TextFieldStyle를 채택하는 방식  
생각보다 단순했다.   
`TextFieldStyle`를 채택해주고 이 스타일도 `init()`을 이용하여 각 스타일에 맞게 재사용 가능하도록 하였다.    
```swift
struct SearchTextFieldStyle: TextFieldStyle {

    let verticalPadding: CGFloat
    let horizontalPadding: CGFloat
    let backgroundColor: Color
    let cornerRadius: CGFloat

    init(verticalPadding: CGFloat = 10,
         horizontalPadding: CGFloat = 16,
         backgroundColor: Color = Color.gray,
         cornerRadius: CGFloat = 20) {
        self.verticalPadding = verticalPadding
        self.horizontalPadding = horizontalPadding
        self.backgroundColor = backgroundColor
        self.cornerRadius = cornerRadius
    }

    func _body(configuration: TextField<Self._Label>) -> some View {
        configuration
            .padding(.vertical, verticalPadding)
            .padding(.horizontal, horizontalPadding)
            .background(backgroundColor)
            .cornerRadius(cornerRadius)
    }
}

// 사용 예시 코드
TextField("Search...", text: $text)
    .textFieldStyle(SearchTextFieldStyleTest())
```   

💡다만 이 방식에는 유의할점이 있다. `func _body(configuration: TextField<Self._Label>) -> some View {}`     
이 메서드의 _(underScore)의 의미를 몰라 알아보니 hiddenMethod를 의미한다고 한다.   
이 방식은 비공개 API를 사용하므로 사용하기에 안전하지 않다.   
API가 업데이트 되어 변경되거나 사라질 경우 컴파일 에러가 발생할 여지가 다분하다.   
이런식으로 비공개 메서드가 존재하는 이유는 모르겠지만 SwiftUI가 TextFieldStyle 을 커스텀화하는걸 원하지 않는다거나 아직 불안정하여 공식적인 메서드를 지원하지 않음을 의미한다고 생각한다.   
다른 예시로는 버튼을 커스텀할때 사용되는 [ButtonStyle.makeBody(configuration:)](https://developer.apple.com/documentation/swiftui/buttonstyle/makebody(configuration:) )와 같이 공식적인 메서드를 이용하는 방법이 가장 안전하다.    
```swift
// Xcode에서 TextFieldStyle 정의를 살펴보면 아래와 같이 나오는데
@available(iOS 13.0, macOS 10.15, tvOS 13.0, watchOS 6.0, *)
public protocol TextFieldStyle {}

// 어떻게 접근하여 확인하는지는 모르겠지만 아래 형태로 hidden 메서드가 정의되어 있는 것으로 보인다.
public protocol TextFieldStyle {
  associatedtype _Body: View
  @ViewBuilder func _body(configuration: TextField<Self._Label>) -> Self._Body
  typealias _Label = _TextFieldStyleLabel
}
```   
<br>
***

### UIViewRepresentable를 이용한 UITextField 사용
~  
<br>
***

### SwiftUI-Introspect 사용
~   
<br>
***

### 마무리 글   
TextField를 SwiftUI에서 어떻게 커스텀하는지 여러 방법을 알게 되었고, hidden 메서드라는 개념에 대해서도 알게되어 좋았다.   
우선순위가 높지 않아 UIKit을 이용하는 방법과 SwiftUI-Introspect 라이브러리 사용에 대해 연습해보지 않았지만, 추후 해보게 된다면 이 문서를 업데이트 하게 될 것이다.   
<br>
***

### 참고
- [문서](https://www.fivestars.blog/articles/how-to-customize-textfields/)
- [SwiftUI-Introspect](https://github.com/siteline/SwiftUI-Introspect)
