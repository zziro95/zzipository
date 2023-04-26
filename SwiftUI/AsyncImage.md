# AsyncImage   

iOS 15+ 부터 사용가능한 [AsyncImage](https://developer.apple.com/documentation/swiftui/asyncimage)에 대해서 살펴보자.   
핵심부터 말하자면 비동기로 이미지를 불러오고 보여주는 역할을 하는 타입이다.   
iOS 15이하에서 [SDWebImageSwiftUI](https://github.com/SDWebImage/SDWebImageSwiftUI.git)를 사용한 경험이 있는데 `svg` 파일 확장자에 대한 이미지가 잘 표시되지 않았던 경우가 있었다.   
AsyncImage에 대해 알아보고 사용해보며 이미지 처리에 대한 선택폭을 넓혀보자.   
<br>   
***   

### Overview   
정의를 살펴보면 `struct AsyncImage<Content> where Content : View`이러하고 보면 이 뷰는 `URLSession`을 이용하여 지정된 url에서 이미지를 불러오고, 표시한다.
이미지가 로드될 때까지 placeholder를 표시하고, 이 placeholder의 기본형태는 옅은 회색이며 원하는 형태의 뷰로도 표현이 가능하다.      
이미지 로드에 성공하면 이미지를 사이즈에 맞게 보여주지만, 잘못된 url이거나 네트워크 오류 발생과 같은 실패할 경우도 존재한다.   
실패한 경우는 placeholder가 계속 보여지게 된다.   
<br>   

#### init   
어떤형태로 사용할 수 있는지 init에 대해 살펴보자.   
```swift
    
    /// - Parameters:
    ///   - url: The URL of the image to display.
    ///   - scale: The scale to use for the image. The default is `1`.
     Set a different value when loading images designed for higher resolution displays. 
     For example, set a value of `2` for an image that you would name with the `@2x` suffix if stored in a file on disk.
     
     When the load operation completes successfully, SwiftUI  updates the view to show content that you specify, which you create using the loaded image. 
    For example, you can show a green placeholder, followed by a tiled version of the loaded image:

AsyncImage(url: URL(string: "https://example.com/icon.png")) { image in
    image.resizable(resizingMode: .tile)
} placeholder: {
    Color.green
}

    ///
    /// If the load operation fails, SwiftUI continues to display the
    /// placeholder. To be able to display a different view on a load error,
    /// use the ``init(url:scale:transaction:content:)`` initializer instead.
    ///
    /// - Parameters:
    ///   - url: The URL of the image to display.
    ///   - scale: The scale to use for the image. The default is `1`. Set a
    ///     different value when loading images designed for higher resolution
    ///     displays. For example, set a value of `2` for an image that you
    ///     would name with the `@2x` suffix if stored in a file on disk.
    ///   - content: A closure that takes the loaded image as an input, and
    ///     returns the view to show. You can return the image directly, or
    ///     modify it as needed before returning it.
    ///   - placeholder: A closure that returns the view to show until the
    ///     load operation completes successfully.
    public init<I, P>(url: URL?, scale: CGFloat = 1, @ViewBuilder content: @escaping (Image) -> I, @ViewBuilder placeholder: @escaping () -> P) where Content == _ConditionalContent<I, P>, I : View, P : View

    /// Loads and displays a modifiable image from the specified URL in phases.
    ///
    /// If you set the asynchronous image's URL to `nil`, or after you set the
    /// URL to a value but before the load operation completes, the phase is
    /// ``AsyncImagePhase/empty``. After the operation completes, the phase
    /// becomes either ``AsyncImagePhase/failure(_:)`` or
    /// ``AsyncImagePhase/success(_:)``. In the first case, the phase's
    /// ``AsyncImagePhase/error`` value indicates the reason for failure.
    /// In the second case, the phase's ``AsyncImagePhase/image`` property
    /// contains the loaded image. Use the phase to drive the output of the
    /// `content` closure, which defines the view's appearance:
    ///
    ///     AsyncImage(url: URL(string: "https://example.com/icon.png")) { phase in
    ///         if let image = phase.image {
    ///             image // Displays the loaded image.
    ///         } else if phase.error != nil {
    ///             Color.red // Indicates an error.
    ///         } else {
    ///             Color.blue // Acts as a placeholder.
    ///         }
    ///     }
    ///
    /// To add transitions when you change the URL, apply an identifier to the
    /// ``AsyncImage``.
    ///
    /// - Parameters:
    ///   - url: The URL of the image to display.
    ///   - scale: The scale to use for the image. The default is `1`. Set a
    ///     different value when loading images designed for higher resolution
    ///     displays. For example, set a value of `2` for an image that you
    ///     would name with the `@2x` suffix if stored in a file on disk.
    ///   - transaction: The transaction to use when the phase changes.
    ///   - content: A closure that takes the load phase as an input, and
    ///     returns the view to display for the specified phase.
    public init(url: URL?, scale: CGFloat = 1, transaction: Transaction = Transaction(), @ViewBuilder content: @escaping (AsyncImagePhase) -> Content)
```   

💡 살펴보면서 image에 대한 [ResizingMode](https://developer.apple.com/documentation/swiftui/image/resizingmode)에 대해 처음 알게되서 좋았다.   


```swift
// 
AsyncImage(url: URL(string: "https://example.com/icon.png"))
    .frame(width: 200, height: 200)
```   

### AsyncImagePhase

### 마무리 글   
~   
<br>
***

### 참고
- [AsyncImage](https://developer.apple.com/documentation/swiftui/asyncimage)
