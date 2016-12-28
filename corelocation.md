* 使用方式
 * Target -> Build Phase -> + CoreLocation.framework
 * 在要使用的檔案內， `import CoreLocation`
 * 在要使用的Class內，新增代理 `CLLocationManagerDelegate`
 * 宣告 `let locationManager = CLLocationManager()`