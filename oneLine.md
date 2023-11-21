
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

