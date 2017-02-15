### Firebase

* ####呼叫API的時候，收到`An invalid API Key was supplied in the request.`的處理方式
 * 重新去`Firebase的專案->設定->下載GoogleService-Info.plist，然後覆蓋在現在專案內的GoogleService-Info.plist`
 * 原因：`GoogleService-Info.plist`內，沒有`API_KEY`這欄位