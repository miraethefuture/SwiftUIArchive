오늘 해결해야 할 문제는 자동으로 dimiss 되는 sheet 뷰 문제.

```swift
var body: some View {
    let _ = Self._printChanges()
    VStack {
        ...
    }
}
```
let _ = Self._printChanges()을 바디에 입력하면 어떤 것들에 변경이 일어났는지 찍어볼 수 있음.
하지만, 변경된 것들을 모두 제거해도 같은 문제가 발생.

NavigationView가 iOS 16.0 버전에서 deprecated 된 것이 원인일 수 있다고 하여
```swift
NavigationView { 
  ...
}
.navigationViewStyle(.stack)
```
위 코드처럼 .navigationViewStyle(.stack)을 기존의 NavigationView { }에 추가해주어야 한다고 함.
Navigation view 없이 단도으로 뷰를 올려보니 sheet가 내려가지 않음!

