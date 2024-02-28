오늘 해결해야 할 문제는 자동으로 dimiss 되는 sheet 뷰 문제.

```swift
var body: some View {
    let _ = Self._printChanges()
    VStack {
        ...
    }
}
```
let _ = Self._printChanges()을 바디에 입력하면 
