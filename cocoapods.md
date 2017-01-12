# CocoaPods

[使用CocoaPods安裝套件教學](https://jay10447.gitbooks.io/book20160316/content/kai_shi_shi_yong_cocoapods_guan_li_di_san_fang_kai.html)

* ### 升級到OSX 10.12.2後，pod install失敗（[參考這篇](https://gold.xitu.io/entry/58620f628d6d810065f940d3)）

  * 原因是帳戶對文件的權限被Apple改掉，檢查以下的權限

    `ls -al /usr/local`

    要是使用者和Group不是目前的設定，請利用下面指令更改

    `sudo chown -R $(whoami):admin /usr/local`

    然後還有個資料夾的權限也要注意 /Usrs/$\(whoami\)/.rbenv/  
    要是也不是當前使用者的權限，利用下列指令更改

    `sudo chown -R $(whoami):admin /Usrs/$(whoami)/.rbenv/`

    之後就可以利用 `pod install` 安裝囉
* #### 當顯示以下的錯誤時：``[!] The VCloud [Release] target overrides the ALWAYS_EMBED_SWIFT_STANDARD_LIBRARIES build setting defined in `Pods/Target Support Files/Pods-VCloud/Pods-VCloud.release.xcconfig'. This can lead to problems with the CocoaPods installation``

   `Use the $(inherited) flag, or`
   `Remove the build settings from the target.`



