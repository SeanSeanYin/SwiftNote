#### Local user notification
##### 所有要用到推播的檔案，都要`import UserNotifications`
* 獲得使用者的允許
 * 在AppDelegate內的`didFinishLaunchingWithOptions`新增
 ```
 UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .sound, .carPlay], completionHandler: { success, error in
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
--------------
* 發送Notification
    
 ```
 @IBAction func sendNotification(_ sender: AnyObject){
     // 設定傳送的資訊
     let content = UNMutableNotificationContent()
     content.title = "聽說這是主題"
     content.subtitle = "聽說這是副主題"
     content.body = "聽說這才是本體"
     content.badge = 1
     content.sound = UNNotificationSound.default()
     
     // 設定觸發條件->產生request->觸發
     let trigger = UNTimeIntervalNotificationTrigger(timeInterval: 5, repeats: false)
     let request = UNNotificationRequest(identifier: "notification", content: content, trigger: trigger)
     UNUserNotificationCenter.current().add(request, withCompletionHandler: nil)
 }
 ```
 * 觸發條件其實有這幾種
   * `UNTimeIntervalNotificationTrigger：`幾秒後觸發
   * `UNCalendarNotificationTrigger：`特定時間觸發
   * `UNLocationNotificationTrigger：`特定位置觸發
   * `UNPushNotificationTrigger：`從APNS觸發
 * 要取消`request`的方法
   * `open func removePendingNotificationRequests(withIdentifiers identifiers: [String])`
   * `open func removeAllPendingNotificationRequests()`
   * `open func removeDeliveredNotifications(withIdentifiers identifiers: [String])`
   * `open func removeAllDeliveredNotifications()`
--------------
* 允許在App在前景時，收Notification
 * 先讓`AppDelegate`實作`UNUserNotificationCenterDelegate的willPresent`這個函式
 ```
 extension AppDelegate: UNUserNotificationCenterDelegate {
        func userNotificationCenter(_ center: UNUserNotificationCenter, willPresent notification: UNNotification, withCompletionHandler completionHandler: @escaping (UNNotificationPresentationOptions) -> Void) {
            completionHandler([.carPlay, .badge, .sound, .alert])
        }
 }
 ```
 * 再讓`didFinishLaunchingWithOptions`代理
 
   `UNUserNotificationCenter.current().delegate = self`