```swift
func calculateRemainingTime() {
    let now = Date()
    let calendar = Calendar.current
    let midnight = calendar.startOfDay(for: now).addingTimeInterval(24 * 60 * 60)
    timeRemaining = midnight.timeIntervalSince(now)
}
    
func formattedTime(_ time: TimeInterval) -> String {
    let formatter = DateComponentsFormatter()
    formatter.allowedUnits = [.hour, .minute, .second]
    formatter.unitsStyle = .positional
    return formatter.string(from: time) ?? "0:00:00"
}


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
```

