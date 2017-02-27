# UIPickerView

* #### 出現`hild view controller:<UICompatibilityInputViewController: 0x14f9c6850> should have parent view controller:<CCCreateActionController: 0x14e9c8c00> but requested parent is:<UIInputWindowController: 0x14e912200>'`錯誤的處理方式
 * 原因：在`IB建立此UIPickerView`並也建立`@IBOutlet`到某個`UIViewController`，之後又`Assign`給`Textfield`作為`inputview`，導致要呼叫`UIPickerView`時，不知道才是真的`Parent`
 * 解決方式：不要建立`@IBOutlet`，在`viewDidLoad`內使用`let picker = UIPickerView()`產生物件