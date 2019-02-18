# UIImagePickerController

* **實作UIImagePickerController**
  * 在要使用的viewController的class內，要宣告`UIImagePickerControllerDelegate, UINavigationControllerDelegate`這兩個delegate
  * 在class內宣告`let imagePicker = UIImagePickerController()`
  * 在`viewDidLoad`內宣告`imagePicker.delegate = self`
  * 實作`func imagePickerController(_ picker: UIImagePickerController, didFinishPickingMediaWithInfo info: [String : Any])`

    ```text
    func imagePickerController(_ picker: UIImagePickerController, didFinishPickingMediaWithInfo info: [String : Any]) {

        if let pickedImage = info[UIImagePickerControllerOriginalImage] as? UIImage {
            imageData = NSData(data: UIImageJPEGRepresentation(pickedImage, 1.0)!)

            let file = FileInfo(name: "selected.jpg", size: imageData?.length, portrait: 0)
            let json:JSON = ["action": "file_upload", "filename": "selected.jpg", "size": file.size, "portrait": file.portrait]

            SSWebSocket.sharedSocket.requestUpload(json)

            let url = FileManager.default.urls(for: .documentDirectory, in: .userDomainMask).first
            let directoryURL = NSURL.fileURL(withPath: (url?.path)!+"/images/1.jpg")
            imageData?.write(to: directoryURL, atomically: true)
        }

        dismiss(animated: true)
    }
    ```

  * 產生ActionSheet讓User選擇相簿或是拍照

    ```text
    @IBAction func chooseImage () {

        let alert = UIAlertController(title: nil, message: nil, preferredStyle: .actionSheet)
        let cameraAction = UIAlertAction(title: "拍照", style: .default, handler:{ void in
            self.imagePicker.allowsEditing = true
            self.imagePicker.sourceType = .camera

            self.present(self.imagePicker, animated: true, completion: nil)
        } )
        let albumAction = UIAlertAction(title: "從相簿中選擇", style: .default, handler:{ void in
            self.imagePicker.allowsEditing = true
            self.imagePicker.sourceType = .photoLibrary

            self.present(self.imagePicker, animated: true, completion: nil)
        })
        let cancelAction = UIAlertAction(title: "取消", style: .cancel, handler: nil)

        alert.addAction(cameraAction)
        alert.addAction(albumAction)
        alert.addAction(cancelAction)

        self.present(alert, animated: true, completion: nil)
    }
    ```
* 讓ImagePickerController的顏色可以變成客製化的顏色

  * 在呼叫ImagePickerController的時候設定下面幾行

  ```text
  self.imagePicker.navigationBar.isTranslucent = true
  self.imagePicker.navigationBar.barTintColor = UIColor.navigation
  self.imagePicker.delegate = self
  ```

