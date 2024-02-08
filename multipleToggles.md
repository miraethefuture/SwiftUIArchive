```swift
enum Food: String, CaseIterable {
    case apple = "Apple"
    case strawberry = "Strawberry"
    case tomato = "Tomato"
    case spinach = "Spinach"
    case carrot = "Carrot"
    case port = "Pork"
}
```
- 'Food' enum은 4개의 case를 가지고 있습니다.

```swift
@State var selection = Set<Food>()
```
selection은 Food 타입의 요소를 가집니다. custom binding이 이 selection에 값이 있는지 없는지를 판단하여, 있을때는 true를 없을 때는 false를 반환합니다. 
```swift
    func typeList(type: FoodType) -> some View {
        ForEach(type.foodItem, id: \.foodItem) { item in
            HStack {
                var isOn = Binding<Bool>( // <-- Here 1!
                    Binding(get: {
                        return selection.contains(item.foodItem)
                    }, set: { value in
                        if selection.contains(item.foodItem) {
                            selection.remove(item.foodItem)
                        } else {
                            selection.insert(item.foodItem)
                        }
                    })
                )
                Toggle(isOn: isOn ?? .constant(false)) { <-- Here 2!
                    Text(item.title)
                        .fontStyle(color: .red, size: 15, weight: .regular)
                }
                .tint(.red)
                .padding(.vertical, 6.5)
            }
        }
    }
```
- 각각의 토글은 각자의 Binding<Bool> 값을 가지고 있어합니다. (하나의 Binding bool 값을 가지고 있다면 모든 토글이 동시에 on/off 됩니다.)
- CustomBinding을 생성하여 여러개의 @Binding 변수를 만들지 않고 각 토글에게 다른 binding bool 값을 주겠습니다.
- Here 1 이라고 표시된 부분이 custom binding을 생성한 부분입니다.
- toggle하여 isOn의 값이 변경되면, selection 안에 해당되는 item이 존재하는지 확인하여 없는 경우 insert, 있는 경우 remove 합니다.
- custom binding의 get: { } 에서는 해당 값이 selection 안에 존재하는 경우 true를, 반대의 경우 false를 반환합니다.  
