* ### plist所有取用限制列表
 * [Apple文件](https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html)
 * 相片：NSPhotoLibraryUsageDescription
 * 相機：NSCameraUsageDescription
 
* ### 存取http的url
 * 先新增 `App Transport Security Settings`
 * 再剛剛建立完成的```App Transport Security Settings```下，再新增```Allow Arbitrary Loads```，並將`boolen`值設定為`Yes`
