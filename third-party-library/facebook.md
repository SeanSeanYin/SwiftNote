# Facebook

* **獲取用戶大頭像的URL**
  * ```text
    let parameters = ["fields":"id, name, picture"]
    let request = FBSDKGraphRequest(graphPath: "me", parameters: parameters, httpMethod: "GET")
    let _ = request?.start(completionHandler: { (connection, result, error) in

        guard connection != nil else {
            print("Failed to get connection")
            return
        }

        guard error == nil else {
            print ("Error : \(error?.localizedDescription)")
            return
        }

        guard let result = result as? NSDictionary else {
            print("Failed to get result")
            return
        }

        guard let userId = result.value(forKey: "id") as? String,
              let userName = result.value(forKey: "name") as? String,
              let userPhotoURL = ((result.value(forKey: "picture") as AnyObject).value(forKey: "data") as AnyObject).value(forKey: "url") as? String else {
            print("Failed to get result data")
            return
        }

        UserInfo.shared.name = userName
        UserInfo.shared.id = userId
        UserInfo.shared.photoURL = userPhotoURL
    })
    ```
* **審查時壓縮模擬器**
  * 壓縮模擬器組建的指令

    ```text
    ditto -ck --sequesterRsrc --keepParent  ~/Library/Developer/Xcode/DerivedData/Agora-bnknhtabkdzfnrfokeasiwvixasp/Build/Products/Debug-iphonesimulator/Agora.app/  ~/Desktop/AgoraLive.zip
    ```

  * 查詢模擬器型別

    ```text
    ios-sim showdevicetypes
    ```

  * 驗證模擬器組建

    ```text
    ios-sim launch --devicetypeid="iPhone-5, 10.0" ~/Desktop/Agora.app/
    ```

  * 參數 --devicetypeid是用來選擇模擬器要run在哪種型號跟os
* **要求權限**
  * ```text
    func getUserFacebookProfile(token:FBSDKAccessToken){

        let parameters = ["fields":"id, name"]
        let request = FBSDKGraphRequest(graphPath: "me", parameters: parameters, httpMethod: "GET")
        let _ = request?.start(completionHandler: { (connection, result, error) in

            guard connection != nil else {
                print("Failed to get connection")
                return
            }
            guard error == nil else {
                print ("Error : \(error?.localizedDescription)")
                return
            }
            guard let result = result as? NSDictionary else {
                print("Failed to get result")
                return
            }

            guard let userId = result.value(forKey: "id") as? String,
                let userName = result.value(forKey: "name") as? String else {

                    print("Failed to get result data:\(result)")
                    return
            }

            self.user = UserInfo(id: userId, name: userName, token: token.tokenString)
            self.performSegue(withIdentifier: "goToMainPage", sender: self)
        })
    }
    ```
* **利用shareButton分享照片到facebook**
  * 這方法是透過已安裝的FB App或是Safari內的FB 帳號來分享，所以不用額外要求publish\_actions權限
  * `import FBSDKShareKit`
  * 在`imagePickerController:didFinishPickingMediaWithInfo`這function內

    ```text
    func imagePickerController(_ picker: UIImagePickerController, didFinishPickingMediaWithInfo info: [String : Any]) {

        if let pickedImage = info[UIImagePickerControllerOriginalImage] as? UIImage {
            // 設定照片
            let photo = FBSDKSharePhoto()
            photo.image = pickedImage
            photo.isUserGenerated = true
            // 設定分享內容
            let content = FBSDKSharePhotoContent()
            content.photos = [photo]
            // 建立fb專用的分享按鈕
            let shareButton = FBSDKShareButton()
            shareButton.center = self.view.center
            shareButton.shareContent = content
            self.view.addSubview(shareButton)
        }        
        dismiss(animated: true)
    }
    ```
* **呼叫Graph API時，要抓取result的值的方式**

```text
        let request = FBSDKGraphRequest(graphPath: "/me/live_videos", parameters: nil, httpMethod: "POST")
        request?.start(completionHandler: { connection, result, error in

            guard error == nil else {
                print("error:\(error?.localizedDescription)")
                return
            }

            if (connection != nil) {
                print("connection:\(connection)")
            }

            guard let data = result as? Dictionary<String, Any>, let streamId = data["id"], let streamUrl = data["stream_url"] else {
                return
            }
        })
```

