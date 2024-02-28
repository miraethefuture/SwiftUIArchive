```swift
import SwiftUI
import Combine

struct AdaptsToKeyboard: ViewModifier {
    @State var currentHeight: CGFloat = 0
    
    func body(content: Content) -> some View {
        GeometryReader { geometry in
            content
                .padding(.bottom, self.currentHeight)
                .onAppear(perform: {
                    NotificationCenter.Publisher(center: NotificationCenter.default, name: UIResponder.keyboardWillShowNotification)
                        .merge(with: NotificationCenter.Publisher(center: NotificationCenter.default, name: UIResponder.keyboardWillChangeFrameNotification))
                        .compactMap { notification in
                            withAnimation(.easeInOut(duration: 0.16)) {
                                notification.userInfo?[UIResponder.keyboardFrameEndUserInfoKey] as? CGRect
                            }
                    }
                    .map { rect in
                        rect.height - geometry.safeAreaInsets.bottom
                    }
                    .subscribe(Subscribers.Assign(object: self, keyPath: \.currentHeight))
                    
                    NotificationCenter.Publisher(center: NotificationCenter.default, name: UIResponder.keyboardWillHideNotification)
                        .compactMap { notification in
                            CGFloat.zero
                    }
                    .subscribe(Subscribers.Assign(object: self, keyPath: \.currentHeight))
                })
        }
    }
}

extension View {
    func adaptsToKeyboard() -> some View {
        return modifier(AdaptsToKeyboard())
    }
}
```
- NotificationCenter는 어떤 이벤트나 상태 변경이 발생했을 때 옵저버 객체들에게 알림을 전달하는 메커니즘
- 각각의 실행중인 앱은 'default' notification center를 가짐. (목적에 따라, notication center를 생성할 수 있음)
- NotificationCenter는 Combine 프레임워크의 publisher를 사용하여, 키보드가 나타날때 발생하는 notification 값을 나타냄.
- .merge(with:)는 두 개의 Publisher를 병합하여 하나의 Publisher로 만듦. 위 코드에서는 키보드가 나타날때와 키보드의 프레임이 변경될 때의 notification을 모두 처리하기 위해 사용됨.
