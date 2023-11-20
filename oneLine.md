
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


🥐 
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
