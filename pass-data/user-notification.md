#### Local user notification
##### 所有要用到推播的檔案，都要`import UserNotifications`
* 獲得使用者的允許
 * 在AppDelegate內的`didFinishLaunchingWithOptions`新增
 ```
 UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .sound], completionHandler: { success, error in
        guard (error == nil) else {
            print("錯誤：\(error?.localizedDescription)")
            return 
        }
            
        guard success else {
            print("為什麼不同意")
            return
        }
        print("感謝大大的同意")
    })
 ```
