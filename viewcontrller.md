# ViewContrller

* #### 新增背景圖片

  * `self.view.backgroundColor = UIColor(patternImage: UIImage(named: "background.png"))`
* #### 用Label畫直線

  ```
  let lineView = UIView(frame: CGRect(x: 0, 
            y: label.bounds.size.height / 2,
            width: label.bounds.size.width,
            height: 1)) 
     lineView.backgroundColor = UIColor.blackColor();
     label.addSubview(lineView)
  ```
* #### 新增Spinner

  * 先宣告 @IBOutlet var spinner:UIActivityIndicatorView!
  * 在要顯示的地方新增
    \`\`\`
    self.spinner.hidesWhenStopped = true
    self.spinner.center = self.view.center
    view.addSubview\(spinner\)
    spinner.startAnimating\(\)\`\`\`
  * 在要停止的地方新增
    \`\`\` 
    OperationQueue.main.addOperation {
       self.spinner.stopAnimating\(\)
    }\`\`\`
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
* #### 出現`whose view is not in the window hierarchy!`的解法

  * 在 `viewDidAppear` 呼叫就能避免現象，說是在 `viewDidLoad` 時沒有 `Window Hierarchy`資訊
* #### Popover for iPad

  * Button

    ```
    actionSheet.popoverPresentationController?.sourceView = button
    actionSheet.popoverPresentationController?.sourceRect = button.bounds;
    actionSheet.popoverPresentationController?.permittedArrowDirections = UIPopoverArrowDirection.Left;
    ```

  * BarButtonItem

    ```
    actionSheet.popoverPresentationController?.barButtonItem = button
    actionSheet.popoverPresentationController?.permittedArrowDirections = UIPopoverArrowDirection.Up;
    ```
* #### 在ViewController內新增TableView，然後能控制TableView內的Component的方式

  * 先創造`UITableCell的SubClass`，然後將Table的Cell的Class指定為剛剛建立的SubClass，並且讓`ViewController多繼承UITableViewDelegate, UITableViewDataSource`，並且在ViewController的viewDidLoad函式內，新增`table.delegate = self & table.dataSource = self`，最後是在ViewController的Class內實作`tableView(_: didSelectRowAt:) & tableView(_: cellForRowAt:) & numberOfSectionsInTableView` 這三個函式
  * 然後要取用Table內的元件，可以這樣調用`let cell = tableView.dequeueReusableCellWithIdentifier("MyCustomTableViewCell", forIndexPath: indexPath) as! MyCustomTableViewCell`，之後再用`cell.MyLabel.text = someString`賦予值
* #### Segue用法

  * 呼叫特定的Segue

    `performSegue(withIdentifier: "showPopover", sender: sender )`

  * 然後實作要傳遞到下一個Scene的資料

    ```
    override func prepare(for segue: UIStoryboardSegue, sender: Any!) {

       if segue.identifier == "showPopover" {

           let viewController = segue.destination as! UITableViewController

           if let popoverController = viewController.popoverPresentationController {

               popoverController.delegate = self
           }
       }
    }
    ```

* ### 隱藏鍵盤

* * 使用[Extension Class](http://stackoverflow.com/questions/24126678/close-ios-keyboard-by-touching-anywhere-using-swift)的方式來擴充隱藏鍵盤功能，可支援任意個ViewContrller。



