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

* #### 要讓系統方面（像是App Name或要求Location時的字串）顯示做到多國語言的做法

  * 先在整個專案建立"InfoPlist.strings"這字串檔（名字一定要是InfoPlist）
  * 然後確認想要顯示多國語言的Key值
  * ```
    // 像是第一個是名字
    "CFBundleDisplayName" = "BookGuru";
    "NSCalendarsUsageDescription" = "This allows you to add Book Store Events to your default Calendar.";
    "NSCameraUsageDescription" = "This allows you to scan Book barcodes to see their details, as well as taking your Profile picture.";
    "NSLocationWhenInUseUsageDescription" = "Turning on Location Services will help us determine your proximity to stores.";
    "NSLocationUsageDescription" = "Turning on Location Services will help us determine your proximity to stores.";
    "NSLocationAlwaysAndWhenInUseUsageDescription" = "Turning on Location Services will help us determine your proximity to stores.";
    "NSLocationAlwaysUsageDescription" = "Turning on Location Services will help us determine your proximity to stores.";
    "NSPhotoLibraryUsageDescription" = "This allows you to access your photo library to choose a Profile Picture.";
    "NSPhotoLibraryAddUsageDescription" = "This allows you to access your photo library to choose a Profile Picture.";
    ```



