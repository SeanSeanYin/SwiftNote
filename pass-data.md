####在Swift內，有ViewController之間，有幾種方式可以傳遞資料

 * Segue：適合用在有上下頁關係的ViewController之間相互傳遞資料
 * Delegate：適合一對一，一個ViewController送，另外一個ViewController收
 * Notification：適合一對多，一個ViewController傳遞（post）
，其他ViewContoller收（addObserver）
 * Singleton：任意ViewController都可以讀寫，但是要注意到Singleton的life cycle

#### Segue
