* #### 使用方式

  * Target -&gt; Build Phase -&gt; + CoreLocation.framework
  * 在要使用的檔案內， `import CoreLocation`
  * 在要使用的Class內，新增代理協定 `CLLocationManagerDelegate`
  * 宣告實體 `let locationManager = CLLocationManager()`
  * 設定實體的屬性
    ```
    locationManager.delegate = self //先設定 代理為自己
    locationManager.desiredAccuracy = kCLLocationAccuracyBest //準確度要最好
    locationManager.requestWhenInUseAuthorization() //詢問使用者是否願意在使用App時，允許使用定位服務
    locationManager.startUpdatingLocation() //開始定位
    ```
  * 實作下面兩個 function

    ```
    func locationManager(manager: CLLocationManager!, didUpdateLocations locations: [AnyObject]!) {CLGeocoder().reverseGeocodeLocation(manager.location, completionHandler: {(placemarks, error)-> Void in
        if error {
            println("Reverse geocoder failed with error" + error.localizedDescription)
            return
        }

        if placemarks.count != 0 {
            let pm = placemarks[0] as CLPlacemark
            if pm != nil {
                //stop updating location to save battery life
                locationManager.stopUpdatingLocation()
                print(pm.locality ? placemark.locality : "")
                print(pm.postalCode ? placemark.postalCode : "")
                print(pm.administrativeArea ? pm.administrativeArea : "")
                print(pm.country ? pm.country : "")
            }
        } else {
            print("Problem with the data received from geocoder")
        }
    })}

    func locationManager(manager: CLLocationManager!, didFailWithError error: NSError!) {
        print("Error while updating location " + error.localizedDescription)
    }
    ```

  * 很重要！在plist內新增詢問使用者是否允許給予定位權限的字串

    * `NSLocationAlwaysUsageDescription` -&gt; 是否允許永遠使用定位
    * `NSLocationWhenInUseUsageDescription` -&gt; 是否允許使用中使用定位
* #### 使用simulator測試位置
* #### 顯示縣市

```
placemark.locality
```



