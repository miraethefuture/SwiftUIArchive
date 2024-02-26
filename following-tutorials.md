🥨
```swift
.frame(maxWidth: .infinity, alignment: .leading)
```
- .frame modifier는 보이지 않는 프레임 속에 뷰를 담는다.
- maxWidth를 .infinity로 지정하면 프레임의 width가 가능한 범위에서 가장 넓게 늘어난다.
- alignment: .leading은 프레임 속 뷰가 왼쪽으로 정렬되도록 한다.

🥨
- modifier를 적용할때마다 새로운 뷰를 만들어내는 것이기 때문에, modifier의 순서는 중요하다.
