# Firebase

* #### 呼叫API的時候，收到`An invalid API Key was supplied in the request.`的處理方式

  * 重新去`Firebase的專案->設定->下載GoogleService-Info.plist，然後覆蓋在現在專案內的GoogleService-Info.plist`
  * 原因：`GoogleService-Info.plist`內，沒有`API_KEY`這欄位

* #### 在使用FBSDK登入的時候收到error code:304

  * 原因：使用者在切換到FB登入時，做了切換帳號的動作，用不同於先前登入過的新帳號來登入，導致token沒有更新
  * 解法： 在`FBSDKLoginManager().logIn()`之前，先登出`FBSDKLoginManager().logOut()`
* #### 透過Firebase利用FB登入，[參考這篇](http://appcoda.com.tw/firebase-facebook-login/)

* #### Google SingIn的refresh token方式

  * 因為每次User開啟App一定都會先去Google拿一次accessToken，所以一定會呼叫sign\(\)這個delegate內的function，不管是有 GIDSignIn\(\).sharedInstance\(\).hasAuthInKeychain\(\)的情況下用signInSilently\(\)，或是直接使用sign\(\)做登入



