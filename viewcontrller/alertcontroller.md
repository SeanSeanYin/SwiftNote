* #### AlertSheet
```
@IBAction func showSortSheet(sender: AnyObject) {

    let sortMenu = UIAlertController(title: nil, message: "Sort by", preferredStyle: .ActionSheet)

    let wifiAction = UIAlertAction(title: "Wifi", style: .Default, handler: nil)
    let cheapAction = UIAlertAction(title: "Cheap", style: .Default, handler: nil)
  
    sortMenu.addAction(wifiAction)
    sortMenu.addAction(cheapAction)
    self.presentViewController(sortMenu, animated: true, completion: nil)
  }
```

* #### popover 要能顯示在多種Size的螢幕上

  * 先讓viewcontroller follow protocol：`UIPopoverPresentationControllerDelegate`

  * 再新增該function

  ```
  // 注意：Swift 2.2和3的此function name不一樣
  func adaptivePresentationStyle(for controller: UIPresentationController) -> UIModalPresentationStyle {
      return .none
  }
  ```
* #### popover要能正確切齊顯示在anchor下方

  * 使用下面方法

  ```
  let vc = segue.destination
  if let controller = vc.popoverPresentationController {
      controller.delegate = self
      controller.sourceView = self.view
      controller.sourceRect = (self.navigationItem.rightBarButtonItem?.accessibilityFrame)!
  }
  ```
