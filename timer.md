```
// 宣告
var timer:Timer!

// 設定Timer
timer = Timer.scheduledTimer(timeInterval: TimeInterval.init(60), 
                             target: self, 
                             selector: #selector(self.refreshToken), 
                             userInfo: nil, 
                             repeats: true)
// 讓Timer不再運作
timer.invalidate()
```



