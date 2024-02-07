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
- 'Food' enum은 4개의 case를 가지고 있음
- 각 case는 토글의 label name이 될 string raw value를 가지고 있음

```swift
struct FoodItemModel: Identifiable {
    var id: NotificationItem { self.foodItem }
    var foodItem: Food
    var title: String { self.foodItem.rawValue } // 토글 라벨 텍스트로 사용
}
```
```swift
enum FoodType: String, CaseIterable {
    case Fruit = "Fruit"
    case Vegetable = "Vegetable"
    case Meat = "Meat"
    
    var notiItem: [NotificationItemModel] {
        switch self {
        case .Fruit:
            return [
                FoodItemModel(foodItem: .apple),
                FoodItemModel(foodItem: .strawberry),
                FoodItemModel(foodItem: .tomato)]
        case .Vegetable:
            return [
                FoodItemModel(foodItem: .spinach),
                FoodItemModel(foodItem: .carrot)]
        case .Meat:
            return [
                FoodItemModel(foodItem: .pork)]
        }
    }
}
```
```swift
@State var selection = Set<Food>()
    func typeList(type: FoodType) -> some View {
        ForEach(type.foodItem, id: \.foodItem) { item in
            HStack {
                var isOn = Binding<Bool>(
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
                Toggle(isOn: isOn ?? .constant(false)) {
                    Text(item.title)
                        .fontStyle(color: .red, size: 15, weight: .regular)
                }
                .tint(.red)
                .padding(.vertical, 6.5)
            }
        }
    }
```
