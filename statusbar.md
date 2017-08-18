* #### 要遮住StatusBar的做法

```
// 用Label擋住
let statusBarLabel = UILabel(frame: CGRect(x: 0, y: 0, width: self.screenWidth(), height: 20.0))
statusBarLabel.backgroundColor = CommonUtility().COLOR_navigationBar
self.view.addSubview(statusBarLabel)
```



