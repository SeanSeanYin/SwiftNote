# Firebase

* #### 呼叫API的時候，收到`An invalid API Key was supplied in the request.`的處理方式

  * 重新去`Firebase的專案->設定->下載GoogleService-Info.plist，然後覆蓋在現在專案內的GoogleService-Info.plist`
  * 原因：`GoogleService-Info.plist`內，沒有`API_KEY`這欄位
* #### 在使用FBSDK登入的時候收到error code:304

  * 原因：使用者在切換到FB登入時，做了切換帳號的動作，用不同於先前登入過的新帳號來登入，導致token沒有更新
  * 解法： 在`FBSDKLoginManager().logIn()`之前，先登出`FBSDKLoginManager().logOut()`
* #### 透過Firebase利用FB登入，[參考這篇](http://appcoda.com.tw/firebase-facebook-login/)
* #### Google SingIn的refresh token方式

  * 因為每次User開啟App一定都會先去Google拿一次accessToken，不管是GIDSignIn\(\).sharedInstance\(\).hasAuthInKeychain\(\)的情況下用signInSilently\(\)，或是直接使用sign\(\)做登入，一定會呼叫delegate內的sign\(\)這個function，。
  * 只要Google登入成功後，呼叫Timer程式，來在固定的時間內確認accessToken

  ```
      var refreshTimer = Timer()
      let timeIntervalOfRepeats = TimeInterval(600) // 10 mintues
      let timeIntervalOfRefresh = TimeInterval(-540) // 9 minutes

      func startRepeatlyRefreshToken(){
          if User.shared.loginType == .google {
              refreshTimer = Timer.scheduledTimer(timeInterval: self.timeIntervalOfRepeats, target: self, selector: #selector(self.refreshToken), userInfo: nil, repeats: true)
          }
      }
  ```

  * 實作refreshToken的函式

  ```
      func refreshToken(){
          // 先確保有網路
          guard ReachabilityManager.shared.isNetworkAvailable else {
              print("Netwrok is not available so failed to refresh accessToken.")
              return
          }

          // 如果已登入，才要更新，沒登入是要更新什麼....
          if GIDSignIn.sharedInstance().hasAuthInKeychain() {

              // 先獲得accessToken的過期時間
              if let expirationTime = GIDSignIn.sharedInstance().currentUser.authentication.accessTokenExpirationDate {
                  let remainderTime = Date().timeIntervalSince(expirationTime)
                  print("Remainder:\(remainderTime) > timeIntervalOfRefresh:\(self.timeIntervalOfRefresh) is \((remainderTime > self.timeIntervalOfRefresh) ? true : false )")
                  // 如果剩餘時間大於規定的更新時間（-540秒，也就是9分鐘），就去更新
                  if remainderTime > self.timeIntervalOfRefresh {
                      GIDSignIn.sharedInstance().currentUser.authentication.refreshTokens { (response, error) in

                          guard error == nil else {
                              print("GIDAuthentication refreshTokens failed")
                              return
                          }

                          if let auth = response {
                              print("New accessToken expiration time:\(auth.accessTokenExpirationDate!)")
                          }
                      }
                  }
              }
          } else {
              print("GIDSignIn.sharedInstance().hasAuthInKeychain():\(GIDSignIn.sharedInstance().hasAuthInKeychain())")
          }
      }
  ```

  * 最後是登出時，取消Timer

  ```
      fileprivate func stopRepeatlyRefreshToken(){
          refreshTimer.invalidate()
      }
  ```

  * 



