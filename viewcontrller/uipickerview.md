# UIPickerView

* #### UIPickerView+UITextfield的使用方法

  * ##### 實作`UIPickerViewDelegate, UIPickerViewDataSource`

    ```
    extension customViewController:UIPickerViewDelegate, UIPickerViewDataSource {

        func numberOfComponents(in pickerView: UIPickerView) -> Int { 
            // 回傳要有幾行
            return 1 
        }

        func pickerView(_ pickerView: UIPickerView, numberOfRowsInComponent component: Int) -> Int {
            // 每行要有幾列
            switch (component) {
                case 0:
                    return agesArray.count
                default:
                    return 0
            }
        }

        func pickerView(_ pickerView: UIPickerView, titleForRow row: Int, forComponent component: Int) -> String? {
            // 每列的Title    
            switch (component) {
            case 0:
                return agesArray[row]
            default:
                return ""
            }
        }

        func pickerView(_ pickerView: UIPickerView, didSelectRow row: Int, inComponent component: Int) {
            // 當選擇
            self.ageTextField.text = agesArray[row]
            self.sendButton.isEnabled = true
         }
    }
    ```
  * ##### 實作UITextfield

    ```
    @IBOutlet weak var ageTextField:UITextField!
    override func viewDidLoad() {
         // 指定點擊textfiled後要出現的鍵盤為pickerview
         ageTextField.inputView = agePickerView
    }
    ```
  * ##### 點擊UIPickerView以外的地方取消UIPickerView

    ```
    override func viewDidLoad() {
        // 新增手勢，點擊時觸發FullfillUserInfoViewController.hideKeyboard(tapG:)
        let tap = UITapGestureRecognizer(target: self, action: #selector(FullfillUserInfoViewController.hideKeyboard(tapG:)))
        tap.cancelsTouchesInView = false
    } 
    func hideKeyboard(tapG:UITapGestureRecognizer){
        self.view.endEditing(true)
    }
    ```
* #### 用程式新增PickerView的Done按鈕
* ```
  // 先做出按鈕 
  let doneButton = UIBarButtonItem(title: "確認", style: UIBarButtonItemStyle.plain, target: self, action: #selector(donePicker))

  // 新增ToolBar，並且把按鈕加到ToolBar的Items內
  let toolBar = UIToolbar()
  toolBar.barStyle = UIBarStyle.default
  toolBar.isTranslucent = true
  toolBar.tintColor = UIColor.black
  toolBar.sizeToFit()
  toolBar.setItems([doneButton], animated: false)
  toolBar.isUserInteractionEnabled = true

  // 指定inputAccessoryView為ToolBar
  customerNameTextField.inputAccessoryView = toolBar
  ```
* #### 出現`hild view controller:<UICompatibilityInputViewController: 0x14f9c6850> should have parent view controller:<CCCreateActionController: 0x14e9c8c00> but requested parent is:<UIInputWindowController: 0x14e912200>'`錯誤的處理方式

  * 原因：在`IB建立此UIPickerView`並也建立`@IBOutlet`到某個`UIViewController`，之後又`Assign`給`Textfield`作為`inputview`，導致要呼叫`UIPickerView`時，不知道才是真的`Parent`
  * 解決方式：不要建立`@IBOutlet`，在`viewDidLoad`內使用`let picker = UIPickerView()`產生物件



