# ViewContrller

* 新增背景圖片
  * ```self.view.backgroundColor = UIColor(patternImage: UIImage(named: "background.png"))```
* 用Label畫直線
```
let lineView = UIView(frame: CGRect(x: 0, 
            y: label.bounds.size.height / 2,
            width: label.bounds.size.width,
            height: 1)) 
     lineView.backgroundColor = UIColor.blackColor();
     label.addSubview(lineView)
```
* 新增Spinner
  * 先宣告 @IBOutlet var spinner:UIActivityIndicatorView!
  * 在要顯示的地方新增
  ```
    self.spinner.hidesWhenStopped = true
    self.spinner.center = self.view.center
    view.addSubview(spinner)
    spinner.startAnimating()```
  * 在要停止的地方新增
  ``` 
    OperationQueue.main.addOperation {
       self.spinner.stopAnimating()
    }```
* popover 要能顯示在多種Size的螢幕上
  * 先讓viewcontroller follow protocol：```UIPopoverPresentationControllerDelegate```
  * 再新增該function
  ``` 
    func adaptivePresentationStyle(for controller: UIPresentationController) -> UIModalPresentationStyle {
        return .none
    }
    ```
* popover要能正確切齊顯示在anchor下方
  * 使用下面方法
  ``` 
  let vc = segue.destination
  if let controller = vc.popoverPresentationController {
        controller.delegate = self
        controller.sourceView = self.view
        controller.sourceRect = (self.navigationItem.rightBarButtonItem?.accessibilityFrame)!
  }
    ```
* 出現```whose view is not in the window hierarchy!```的解法

  * 
在 ```viewDidAppear``` 呼叫就能避免現象，說是在 ```viewDidLoad``` 時沒有 ```Window Hierarchy ```資訊。

* PopOver on iPad

 * Button:actionSheet.popoverPresentationController?.sourceView = button
actionSheet.popoverPresentationController?.sourceRect = button.bounds;
actionSheet.popoverPresentationController?.permittedArrowDirections = UIPopoverArrowDirecti * BarButtonItem: