* 使用方式
 * Target -> Build Phase -> + CoreLocation.framework
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
            self.displayLocationInfo(pm)
        } else {
            println("Problem with the data received from geocoder")
        }
})}
func locationManager(manager: CLLocationManager!, didFailWithError error: NSError!) { }
```
 * 