* ### plist所有取用限制列表

  * [Apple文件](https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html)
  * 相片：NSPhotoLibraryUsageDescription
  * 相機：NSCameraUsageDescription
* ### 存取http的url

  * 先新增 `App Transport Security Settings`
  * 再剛剛建立完成的`App Transport Security Settings`下，再新增`Allow Arbitrary Loads`，並將`boolen`值設定為`Yes`
* ### 送Request給self signed certificate的Server

  * 先新增 `App Transport Security Settings`

  * 在底下新增 `Exception Domains`的Dictionary，之後再新增下面三項Boolean的項目

  * `NSExceptionAllowsInsecureHTTPLoads`的值為`YES`

  * `NSExceptionRequiresForwardSecrecy`的值為`NO`

  * `NSIncludesSubdomains`的值為`YES`

![](/assets/螢幕快照 2017-07-05 下午3.45.32.png)

* 要讓系統方面（像是App Name或要求Location的字串）顯示做到多國語言的做法
  * 先在整個專案建立"InfoPlist.strings"這檔案（名字一定要是InfoPlist）



