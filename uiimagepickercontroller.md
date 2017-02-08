* ### 實作UIImagePickerController

  * 在要使用的viewController的class內，要宣告`UIImagePickerControllerDelegate, UINavigationControllerDelegate`這兩個delegate
  * 在class內宣告`let imagePicker = UIImagePickerController\(\)`
  * 在`viewDidLoad\(\)`內宣告`imagePicker.delegate = self`
  * 實作`func imagePickerController(_ picker: UIImagePickerController, didFinishPickingMediaWithInfo info: [String : Any])`
```
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

