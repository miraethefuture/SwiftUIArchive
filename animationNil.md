🥐

애니메이션 nil 처리 
```swift
.transaction { transaction in
    transaction.animation = nil
}

.animation(nil) // 15에서 사라지는 modifier라 위 modifier 사용
```
