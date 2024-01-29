
🥐 애니메이션 nil 처리 
```swift
.transaction { transaction in
    transaction.animation = nil
}

.animation(nil) // 15에서 사라지는 modifier라 위 modifier 사용
```

  
🥐 .strikethrough()
```swift
.strikethrough(item.soldOut, color: Color(.red))
```

<s>strikethrough</s> 를 bool 조건에 따라 나타나도록 함. 


🥐 HStack 안에 있는 subviews에 height 일치시키기
```swift
HStack {
    
    Button {
    } label: {
    }
    
    Text("1")
        .frame(maxHeight: .infinity)
    
    Button {
    } label: {
    }
}
.fixedSize(horizontal: false, vertical: true)
```
subview height를 parent height 에 맞추기  
더 높은 height에 맞춰짐


🥐 VStack과 ScrollView 함께 사용 시 나타나는 여백 없애기 
```swift
ScrollView(showsIndicators: false) {
    VStack(spacing: 0) {

    }
}
```
위와 같이 스크롤 뷰를 꼭 VStack 바깥쪽에 놓아야 함.
안쪽에 놓으면 흰 여백이 생김.

🥐 opacity를 부모뷰에만 적용하기

[How to apply SwiftUI opacity to the parent View only?](https://stackoverflow.com/questions/72402274/how-to-apply-swiftui-opacity-to-the-parent-view-only)

```swift
HStack {
    VStack {
        Circle()
        ...
    }
    Image()
        .overlay {
            Text() // opacity를 적용하고 싶지 않은 뷰
        }
}
.compositingGroup()
.opacity(isSoldOut ? 0.5 : 1)
```
.compositingGroup()
그룹이 적용된 뷰 계층 중 최상위 뷰에만 opacity가 적용됨.

🥐 링크 주소가 파란색으로 나타날때
```swift
Text(verbatim: "https://www.instagram.com")
```
위와 같이 Text(verbatim: ) 을 사용하면 적용한 컬러로 나타남

🥐 optional 타입의 파라미터 하나를 가진 함수 작성 
```swift
func displayInfo(of artist: Artist? = nil) {
    // ...
}

displayInfo()
displayInfo(of: artist)
```
와 같이 사용할 수 있음

🥐 Optional binding 
```swift
struct SomeView: View {
    var title: String
    @Binding var showModal: Bool?
}
```
위 스트럭처를 사용 시 showModal을 사용하고 싶지 않을때도 showModal 값을 입력하라는 에러가 남
```swift
var showPassword: Binding<Bool>?
```
위 형태로 작성하면
```swift
showModal?.wrappedValue = false 
```
처럼 사용하면서 필요하지 않을 때는 값을 보내지 않을 수 있음



