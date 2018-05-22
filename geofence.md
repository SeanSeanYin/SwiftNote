* 要使用GeoFence記得先跟使用者要求Location的授權
* 註冊GeoFences

```
    func addRegion(of store:BookStore) -> Bool {

        // 先確保有經緯度的資料
        guard let latitude = store.location?.latitude, let longitude = store.location?.longitude , let id = store.id, let name = store.name else {
            print("Failed to create region.")
            return false
        }

        // 設定identifier
        let identifier = String(id) + "_" + name
        // 獲得radius
        guard let radius = store.layout?.radius else {
            print("Failed to get radius.")
            return false
        }
        // 先用經緯度設定要觀測的點位置，再用此點給定要觀測的半徑和唯一的識別字串
        let geofenceRegionCenter = CLLocationCoordinate2D(latitude: CLLocationDegrees(latitude), longitude: CLLocationDegrees(longitude))
        let geofenceRegion = CLCircularRegion(center: geofenceRegionCenter, radius: Double(radius), identifier: identifier)

        // 設定是進入點的範圍和離開時是否要通知
        geofenceRegion.notifyOnEntry = true
        geofenceRegion.notifyOnExit = true

        // 開始觀測此點
        locationManager.startMonitoring(for: geofenceRegion)

        return true
    }
```

* 最後是實作delegate

```
    // 當進入觀測點的範圍內要做的事
    func locationManager(_ manager: CLLocationManager, didEnterRegion region: CLRegion) {
        
        if region is CLCircularRegion {
            print("Enter region:\(region.identifier)")
            self.notifyEnterStore(of: region)
        }
    }
    
    // 當離開觀測點的範圍時要做的事    
    func locationManager(_ manager: CLLocationManager, didExitRegion region: CLRegion) {

        if region is CLCircularRegion {
            print("Exit region:\(region.identifier)")
        }
    }

    // 當開始觀測點時要做的事
    func locationManager(_ manager: CLLocationManager, didStartMonitoringFor region: CLRegion) {
        
        print("didStartMonitoringFor region:\(region)")
    }
```



