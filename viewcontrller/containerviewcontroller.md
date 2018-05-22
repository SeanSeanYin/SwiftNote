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

      // 此為第二個ViewController
      private lazy var featuredViewController: StoreDetailFeaturedViewController = {
          let storyboard = UIStoryboard(name: "Main", bundle: .main)
          var viewController = storyboard.instantiateViewController(withIdentifier: "StoreDetailFeaturedViewController") as! StoreDetailFeaturedViewController
          viewController.store = self.store
          self.add(asChildViewController: viewController)
          return viewController
      } ()
  ```

  * 然後寫顯示和移除ViewController的函式

  ```
      // 顯示ViewController
      fileprivate func add(asChildViewController viewController: UIViewController) {

          // 新增viewController成原本viewcontroller的子viewcontroller
          self.addChildViewController(viewController)

          // 新增viewController的view 成 原本viewcontroller的view的subview
          self.containView.addSubview(viewController.view)

          // 設定 viewController的view的座標位置跟原本viewcontroller的containView的座標位置一致
          viewController.view.frame.origin = self.containView.bounds.origin

          // 設定 viewController的view的Frame跟原本viewcontroller的containView的大小一樣
          viewController.view.frame.size = self.containView.frame.size

          // 將子viewcontroller移到父viewcontroller的位置
          viewController.didMove(toParentViewController: self)
      }

      // 移除ViewController
      fileprivate func remove(asChildViewController viewController: UIViewController) {

          // 在調用removeFromParentViewController要先調用willMovetoParanetViewController
          // 
          viewController.willMove(toParentViewController: nil)
        
          // 將子viewController的view從父viewController的view移除
          viewController.view.removeFromSuperview()
        
          // 正式將子viewController從父viewController移除
          viewController.removeFromParentViewController()
      }
  ```

  * 



