# Date
先獲取現在時間

```let now = NSDate()```

再轉成unix時間since1970

```let timeInterval:TimeInterval = now.timeIntervalSince1970```

再用Int轉成10位數

```let timeStamp = Int(timeInterval)```

轉成人類看得懂的格式

```let dformatter = DateFormatter()```
```dformatter.dateFormat = "yyyy年MM月dd日 HH:mm:ss"```

列印出來結果

```print("目前日期時間：\(dformatter.string(from: now as Date))")```



