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
* #### Label or Button 顯示圓角

  ```
  myLabel.layer.masksToBounds = true
  myLabel.layer.cornerRadius = 5
  ```
* #### 新增Spinner

  * 先宣告 `@IBOutlet var spinner:UIActivityIndicatorView!`
  * 在要顯示的地方新增

    ```
    self.spinner.hidesWhenStopped = true
    self.spinner.center = self.view.center
    view.addSubview\(spinner\)  
    spinner.startAnimating
    ```

  * 在要停止的地方新增

    `OperationQueue.main.addOperation {                                  
     self.spinner.stopAnimating() }`
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
* #### Popover 出現的 View 不要圓角，改回直角的方法

  * ```
    override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(animated)
        self.view.superview?.layer.cornerRadius = 0.0
    }
    ```
* #### 在ViewController內新增TableView，然後能控制TableView內的Component的方式

  * 先創造`UITableCell的SubClass`，然後將Table的Cell的Class指定為剛剛建立的SubClass，並且讓`ViewController多繼承UITableViewDelegate, UITableViewDataSource`，並且在ViewController的viewDidLoad函式內，新增`table.delegate = self & table.dataSource = self`，最後是在ViewController的Class內實作`tableView(_: didSelectRowAt:) & tableView(_: cellForRowAt:) & numberOfSectionsInTableView` 這三個函式

  * 然後要取用Table內的元件，可以這樣調用`let cell = tableView.dequeueReusableCellWithIdentifier("MyCustomTableViewCell", forIndexPath: indexPath) as! MyCustomTableViewCell`，之後再用`cell.MyLabel.text = someString`賦予值
* #### Slider用法

  * 設定maximumValue & minimumValue & value
    ```
    self.slider.maximumValue = 10
    self.slider.minimumValue = 1
    self.slider.setValue(1, animated: true)
    ```
  * 設定滑動事件
    ```
    @IBAction func sliderValueChanged (sender: UISlider){
      self.currentPage = Int(sender.value)
      self.changePage(currentPage: self.currentPage)
    }
    ```
* #### Navigation Bar換顏色

  * `navigationController.navigationBar.barTintColor = UIColor.greenColor()`
* #### Navigation Bar設定Title

  * `self.myButton.setTitle(titleString, for: .normal)`，字串一定會顯示完整
  * 使用`self.myButton.titleLabel?.text = titleString`的話，會有字串顯示不完全的問題
* #### 使用RGB的顏色

  * `cell.backgroundColor = UIColor(red: 0.5, green: 0.5, blue: 0.5, alpha: 1.0)`
* #### 隱藏鍵盤

  * 使用[Extension Class](http://stackoverflow.com/questions/24126678/close-ios-keyboard-by-touching-anywhere-using-swift)的方式來擴充隱藏鍵盤功能，可支援任意個ViewContrller。
* #### 做xib的注意事項

  * `xib最底下那層View是UIView類別`
* #### 要把SearchBar固定在不是TableHaed和Navigation Bar的方法

  * 先建立一個UIView
  * 再把Search Bar新增到剛剛的UIView
* #### 取消當前的View

  * `dismiss(animated: true, completion: nil)`
* #### PickerView改變選項的字型和顏色的方法

  ```
  func pickerView(pickerView: UIPickerView, viewForRow row: Int, forComponent component: Int, reusingView view: UIView!) -> UIView
  {
    var pickerLabel = UILabel()
    pickerLabel.textColor = UIColor.blackColor()
    pickerLabel.text = "PickerView Cell Title"
    pickerLabel.font = UIFont(name: "Arial-BoldMT", size: 15) 
    pickerLabel.textAlignment = NSTextAlignment.Center

    return pickerLabel
  }
  ```
* #### 取消Table的Cell之間的線

  `sel.tableView.separatorStyle= .none`

* #### 更換button的文字和圖片

  ```
  self.mapButton.setTitle("Map", for: .normal)
  self.sortButton.setImage(UIImage(named: "btn_sort_n"), for: .normal)
  ```
* #### 想要每次返回ViewController的時候重新load data

  * 寫在viewWillAppear內，viewDidLoad不會重新再被call到
* #### TextView的鍵盤要收起來

  * 讓viewController實作 `UITextViewDelegate`

  * ```
    func textView(_ textView: UITextView, shouldChangeTextIn range: NSRange, replacementText text: String) -> Bool {
        if (text == "\n") {
            textView.resignFirstResponder()
            return false
        }
        return true
    }
    ```

* #### 用程式添加UIBarButtonItem

```
        let image = UIImage(named: "icon_save_resize")
        let saveItem = UIBarButtonItem(image: image, style: UIBarButtonItemStyle.plain, target: self, action: #selector(saveNote))
        self.navigationItem.setRightBarButton(saveItem, animated: true)
```



