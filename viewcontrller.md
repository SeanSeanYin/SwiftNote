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
     label.addSubview(lineView) ```
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
  * 
* 
