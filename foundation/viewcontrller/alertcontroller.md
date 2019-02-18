# AlertController

* **AlertSheet**

  ```text
  @IBAction func showSortSheet(sender: AnyObject) {

    let sortMenu = UIAlertController(title: nil, message: "Sort by", preferredStyle: .ActionSheet)

    let wifiAction = UIAlertAction(title: "Wifi", style: .Default, handler: nil)
    let cheapAction = UIAlertAction(title: "Cheap", style: .Default, handler: nil)

    sortMenu.addAction(wifiAction)
    sortMenu.addAction(cheapAction)
    self.presentViewController(sortMenu, animated: true, completion: nil)
  }
  ```

* **popover 要能顯示在多種Size的螢幕上**

  * 先讓viewcontroller follow protocol：`UIPopoverPresentationControllerDelegate`
  * 再新增該function

  ```text
  // 注意：Swift 2.2和3的此function name不一樣
  func adaptivePresentationStyle(for controller: UIPresentationController) -> UIModalPresentationStyle {
      return .none
  }
  ```

* **實作帶有Textfield的alertview**

```text
    // 建立AlertView
    let alert = UIAlertController(title: "\(NSLocalizedString("forgotPassword", comment: ""))?", message: NSLocalizedString("enterYourEmailAddressToReceiveDirectionsToResetYourPassword", comment: ""), preferredStyle: .alert)

    // 增加textField和設定placeholder
    alert.addTextField(configurationHandler: { textfield in
        textfield.placeholder = NSLocalizedString("email", comment: "")
        textfield.keyboardType = .emailAddress
    })

    //設定cancel和send的按鈕
    let cancel = UIAlertAction(title: NSLocalizedString("cancel", comment: ""), style: .cancel, handler: nil)
    let send = UIAlertAction(title: NSLocalizedString("send", comment: ""), style: .default, handler: { action in

        if (alert.textFields?.first?.text?.isEmail)! {
            self.forgotPassword(with: (alert.textFields?.first?.text)!)
        } else {
            self.showMessage(title: NSLocalizedString("invalidEmailFormat", comment: ""), message: NSLocalizedString("emailAddressFormatInvalid", comment: ""), action: nil)
        }
    })

    // 增加cancel和send按鈕到AlertView上
    alert.addAction(send)
    alert.addAction(cancel)
    self.present(alert, animated: true, completion: nil)
```

* **popover要能正確切齊顯示在anchor下方**

  * 使用下面方法

  ```text
  let vc = segue.destination
  if let controller = vc.popoverPresentationController {
      controller.delegate = self
      controller.sourceView = self.view
      controller.sourceRect = (self.navigationItem.rightBarButtonItem?.accessibilityFrame)!
  }
  ```

* **popover 出現在NavigationBarButtonItem下方的做法**

  * 先建立一個TableViewController，這個TableVC的內容，就會是後來popover出來的選單內容，建議是用靜態Table做就好，因為選單的選項都是已知且固定的
  * 在viewWillAppear做一些設定

  ```text
  // 設定讓呈現出來的選單不要是圓角
  self.view.superview?.layer.cornerRadius = 0.0
  // 設定出來的選單大小
  self.preferredContentSize = CGSize(width: 80, height: 130)
  ```

  * 再回到要呈現選單的ViewController內，讓此VC遵循`UIPopoverPresentationControllerDelegate,UIAdaptivePresentationControllerDelegate`
  * 在storyboard內，從呈現選單的ViewController，拉一個segue到TableViewController，選擇「Present As Popover」，然後將Anchor設定到BarButtonItem內的Button上
  * 實作

  ```text
  func adaptivePresentationStyle(for controller: UIPresentationController) -> UIModalPresentationStyle { 
      // 讓選單TableViewController的格式為none
      return .none 
  }
  ```

  * 實作 prepare\(for segue, sender\)

  ```text
      override func prepare(for segue: UIStoryboardSegue, sender: Any!) {

          if (segue.identifier == "showOptions") {

              let destinationVC = segue.destination as! OptionsTableViewController
              if let popoverController = destinationVC.popoverPresentationController {
                  popoverController.delegate = self
                  popoverController.sourceView = (sender as! UIButton)
                  popoverController.sourceRect = (sender as! UIButton).bounds
              }
          }
      }
  ```

