# Firebase

* #### 呼叫API的時候，收到`An invalid API Key was supplied in the request.`的處理方式

  * 重新去`Firebase的專案->設定->下載GoogleService-Info.plist，然後覆蓋在現在專案內的GoogleService-Info.plist`
  * 原因：`GoogleService-Info.plist`內，沒有`API_KEY`這欄位
* #### 在使用FBSDK登入的時候收到error code:304

  * 原因：使用者在切換到FB登入時，做了切換帳號的動作，用不同於先前登入過的新帳號來登入，導致token沒有更新
  * 解法： 在`FBSDKLoginManager().logIn()`之前，先登出`FBSDKLoginManager().logOut()`
* #### 透過Firebase利用FB登入，[參考這篇](http://appcoda.com.tw/firebase-facebook-login/)
* #### Google Login 時，畫面空白的原因和解法

  * 原因：因為我把Google SignIn放在獨立的.swift內，所以在 `sign(_ signIn:GIDSignIn!, present viewController: UIViewController!)`  這個delegate的function內，我的 top ViewController不是當下的真正的top viewController，而是NavigationController，因此在呼叫出Google Login的SFSafariViewController時，會產生 `whose view is not in the window hierarchy` 的錯誤，進而造成畫面空白。
  * 解法，使用下面這個function來獲取 top ViewController，來確保可以獲得top viewController而不是NavigationController

  ```
      class func getTopViewController () -> UIViewController? {
        
          if var topController = UIApplication.shared.keyWindow?.rootViewController {
            
              while let presentedViewController = topController.presentedViewController {
                  topController = presentedViewController
              }
            
              return topController
          }
        
          return nil
      }
  ```
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

                          // 確定沒有Error
                          guard error == nil else {
                              print("GIDAuthentication refreshTokens failed")
                              return
                          }

                          // 更新成功
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
* #### Google SignIn的Delegate若是不在AppDelegate內的做法

  * dismiss和present這兩個function要從topViewController來dismiss或present

```
    func sign(_ signIn: GIDSignIn!, dismiss viewController: UIViewController!) {
        let topViewController = UIApplication.topViewController()
        topViewController.dismiss(animated: true, completion: nil)
    }

    func sign(_ signIn: GIDSignIn!, present viewController: UIViewController!) {
        let topViewController = UIApplication.topViewController()
        topViewController.present(viewController, animated: true, completion: nil)
    }

    extension UIApplication {
        class func topViewController(base:UIViewController? = UIApplication.shared.keyWindow?.rootViewController) -> UIViewController {
            if let navigationVC = base as? UINavigationController {
                return navigationVC
            }
            if let tabBarVC = base as? UITabBarController {
                if let selectedVC = tabBarVC.selectedViewController {
                    return topViewController(base:selectedVC)
                }
            }
            if let presentedVC = base?.presentedViewController {
                return topViewController(base:presentedVC)
            }
            return base!
        }
    }
```

#### 



