* #### 獲取用戶大頭像的URL
 * 
 ```
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