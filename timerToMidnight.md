```swift

@State private var timeRemaining = TimeInterval()

let timer = Timer.publish(every: 1, on: .main, in: .common).autoconnect()

VStack {
  // 최상단
}
.onAppear {
    calculateRemainingTime()
}
.onReceive(timer) { _ in
    calculateRemainingTime()
}



// 현재 시간 - 저녁 12시까지의 time interval을 구함
func calculateRemainingTime() {
    let now = Date()
    let calendar = Calendar.current
    let midnight = calendar.startOfDay(for: now).addingTimeInterval(24 * 60 * 60)
    timeRemaining = midnight.timeIntervalSince(now)
}

// hh:mm:ss 의 형태로 포맷팅
func formattedTime(_ time: TimeInterval) -> String {
    let formatter = DateComponentsFormatter()
    formatter.allowedUnits = [.hour, .minute, .second]
    formatter.unitsStyle = .positional
    return formatter.string(from: time) ?? "0:00:00"
}
```

