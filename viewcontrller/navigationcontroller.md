* #### 替換Navigation Bar Title的方式

  * 建立一個Label，然後塞進去Title的View

```
let titleLabel = UILabel(frame: CGRect(x:0, y:0, width:200, height:40))
self.title = self.titleString
titleLabel.text  = self.titleString
titleLabel.textColor = UIColor.black
titleLabel.sizeToFit()
self.navigationItem.titleView = titleLabel
```



