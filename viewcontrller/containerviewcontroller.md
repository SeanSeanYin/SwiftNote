* #### 實作ContainerView的方法

  * 先在Storyboard上的ViewController拉一個Container View
  * 然後ViewController內宣告 `@IBOutletweakvar containView: UIView!`  並跟Container View做Binding
  * 然後宣告Container View內的ViewController

  ```
      // 用Lazy是有需要用到在初始化，此為第一個ViewController
      private lazy var infoViewController: StoreDetailInfoViewController = {
          let storyboard = UIStoryboard(name: "Main", bundle: .main)
          var viewController = storyboard.instantiateViewController(withIdentifier: "StoreDetailInfoViewController") as! StoreDetailInfoViewController
          viewController.store = self.store
          self.add(asChildViewController: viewController)
          return viewController
      } ()
    
      // 此為二個ViewController
      private lazy var featuredViewController: StoreDetailFeaturedViewController = {
          let storyboard = UIStoryboard(name: "Main", bundle: .main)
          var viewController = storyboard.instantiateViewController(withIdentifier: "StoreDetailFeaturedViewController") as! StoreDetailFeaturedViewController
          viewController.store = self.store
          self.add(asChildViewController: viewController)
          return viewController
      } ()
  ```

  * 



