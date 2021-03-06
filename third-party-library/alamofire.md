# Alamofire

* **Google Doc的下載連結格式**
  * 先取得檔案的共享連結，格式為 `https://docs.google.com/document/d/FILE_ID/edit?usp=sharing`
  * 改成此格式，及為下載連結 `http://docs.google.com/document/d/FILE_ID/export?format=pdf`
* **偵測網路狀態**

  ```text
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
  ```

  * 因為上面程式是放在`AppDelegate.swift`內，所以自行先創造一個`Window`，然後才能產生`AlertController`

* **在httpbody內送出string的方式**

```text
let url = "http://xxx.com.tw/api/"

let string = "\"{\\\"para1\\\":\\\"1317\\\", \\\"para2\\\":\\\"\\\", \\\"para3\\\":\\\"\\\", \\\"para4\\\":\\\"10\\\"}\""
print("jsonString:\(string)")

var request = URLRequest(url: URL(string: url)!)
request.httpMethod = "POST"
request.setValue("application/json", forHTTPHeaderField: "Content-Type")

// 將string轉成data，然後再塞到body內
let data = string.data(using: String.Encoding.utf8)!
request.httpBody = data

Alamofire.request(request).responseJSON { responseObject in
```

* **得到"JSON could not be serialized because of error: The data couldn’t be read because it isn’t in the correct format."的原因**
  * 在request內忘記加上`encoding:JSONEncoding.defaul`會導致Server端回傳String格式  
* **讓Alamofire可以和 Self signed certificate的Server溝通的方法**

```text
class NetworkManager {

    static let share = NetworkManager()

    let defaultManager: Alamofire.SessionManager = {
        let serverTrustPolicies: [String: ServerTrustPolicy] = [
            "apistage2.aisleconnect.us": .disableEvaluation
        ]

        let configuration = URLSessionConfiguration.default
        configuration.httpAdditionalHeaders = Alamofire.SessionManager.defaultHTTPHeaders

        return Alamofire.SessionManager(
            configuration: configuration,
            serverTrustPolicyManager: ServerTrustPolicyManager(policies: serverTrustPolicies)
        )
    }()
}

之後要調用，呼叫 NetworkManager.share.defaultManager.request() 即可
```

