* ### 實作UIImagePickerController

  * 在要使用的viewController的class內，要宣告`UIImagePickerControllerDelegate, UINavigationControllerDelegate`這兩個delegate
  * 在class內宣告`let imagePicker = UIImagePickerController\(\)`
  * 在`viewDidLoad\(\)`內宣告`imagePicker.delegate = self`
  * 實作`func imagePickerController(_ picker: UIImagePickerController, didFinishPickingMediaWithInfo info: [String : Any])`


