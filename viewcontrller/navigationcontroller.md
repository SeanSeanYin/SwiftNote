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

* #### 更改BackBarItem的Title

  * 在要隱藏的viewController內的viewDidLoad呼叫

  ```
  self.navigationController?.navigationBar.topItem?.title = ""
  ```

  * 但是會造成前一頁的title不見，所以要在前一頁的viewDidLoad內呼叫

```
self.navigationController?.navigationBar.topItem?.title = "Title"
```

* 移除特定的ViewController

```
// 移除全部
self.navigationController!.viewControllers.removeAll()
// 移除第一個
self.navigationController?.viewControllers.removeFirst
// 移除最後一個
self.navigationController?.viewControllers.removeLast
// 移除特定個
self.navigationController?.viewControllers.remove(at: "insert here a number")
```



