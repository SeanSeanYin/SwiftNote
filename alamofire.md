# Alamofire

* #### Google Doc的下載連結格式

  * 先取得檔案的共享連結，格式為 `https://docs.google.com/document/d/FILE_ID/edit?usp=sharing`
  * 改成此格式，及為下載連結 `http://docs.google.com/document/d/FILE_ID/export?format=pdf`

* #### 偵測網路狀態

        let net = NetworkReachabilityManager()
        net?.startListening()
        
        net?.listener = {status in
            
            if  net?.isReachable ?? false {
                
                if ((net?.isReachableOnEthernetOrWiFi) != nil) {
                    print("Wifi Mode")
                }else if(net?.isReachableOnWWAN)! {
                    print("WAN Mode")
                }
            }
            else {
                let topWindow: UIWindow = UIWindow(frame: UIScreen.main.bounds)
                topWindow.rootViewController = UIViewController()
                topWindow.windowLevel = UIWindowLevelAlert + 1
                
                let alert = UIAlertController(title: "無網路服務", message: "請檢查網路狀態", preferredStyle: .alert)
                let doAction = UIAlertAction(title: "確定", style: .default, handler: { (action: UIAlertAction) -> Void in
                    topWindow.isHidden = true
                })

                topWindow.makeKeyAndVisible()
                alert.addAction(doAction)
                topWindow.rootViewController?.present(alert, animated: true, completion: nil)
                print("No network")
            }
        }