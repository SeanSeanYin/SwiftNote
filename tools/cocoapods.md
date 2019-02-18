# CocoaPods

[使用CocoaPods安裝套件教學](https://jay10447.gitbooks.io/book20160316/content/kai_shi_shi_yong_cocoapods_guan_li_di_san_fang_kai.html)

* **升級到OSX 10.12.2後，pod install失敗（**[**參考這篇**](https://gold.xitu.io/entry/58620f628d6d810065f940d3)**）**
  * 原因是帳戶對文件的權限被Apple改掉，檢查以下的權限

    `ls -al /usr/local`

    要是使用者和Group不是目前的設定，請利用下面指令更改

    `sudo chown -R $(whoami):admin /usr/local`

    然後還有個資料夾的權限也要注意 /Usrs/$\(whoami\)/.rbenv/  
    要是也不是當前使用者的權限，利用下列指令更改

    `sudo chown -R $(whoami):admin /Usrs/$(whoami)/.rbenv/`

    之後就可以利用 `pod install` 安裝囉
* **當顯示以下的錯誤的解決方式：``[!] The XCloud [Release] target overrides the ALWAYS_EMBED_SWIFT_STANDARD_LIBRARIES build setting defined in `Pods/Target Support Files/Pods-XCloud/Pods-VCloud.release.xcconfig'. This can lead to problems with the CocoaPods installation``**

  -`Use the $(inherited) flag, or`

  -`Remove the build settings from the target.`

  * 直接刪除build settings：選擇專案的`project.xcodeproj`，用`xcode以外`的文字編輯器打開，直接把 `ALWAYS_EMBED_SWIFT_STANDARD_LIBRARIES`給刪除，再次`pod install`

* **Unable to find a specification for \`xxxxx \(~&gt; 1.x.x\)\` depended upon by Podfile.**
  * `pod repo remove master`
  * `pod setup`
* **在更新Xcode之後下`pod install`會卡在`Installing`的解決方法**
  * `pod remove repo master`
  * `pod setup`
  * `pod install`
  * **執行pod setup 太久的原因：master有519MB大！直接到目錄底下從github上clone比較快**
  * `cd ~/.cocoapods/repos` 
  * `git clone --depth 1 https://github.com/CocoaPods/Specs.git master`
* **Podfile範例**

```text
// 設定source和ios的最低版
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '9.0'

// 要使用workspace方式
use_frameworks!
// 各個需要的pod
def pods
   pod 'GoogleSignIn'
end

// 用來限定Swift 版本
post_install do |installer|
  installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
      config.build_settings['SWIFT_VERSION'] = '3.2'
    end
  end
end

// 有幾個Target需要使用上面的pod
target 'BookMaster' do
   pods
end
```

