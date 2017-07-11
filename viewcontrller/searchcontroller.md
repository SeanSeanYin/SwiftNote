#### 在有NavigationBar的ViewController上，做出可隱藏的SearchBar

* 先讓ViewController遵守 `UISearchResultsUpdating & UISearchControllerDelegate`這兩個協定
* 在ViewController內宣告  `let searchController = UISearchController(searchResultsController:nil)`
* 在viewDidLoad內先設定 searchController

```
   searchController.searchResultsUpdater = self
   searchController.delegate = self
   searchController.hidesNavigationBarDuringPresentation = false
   searchController.dimsBackgroundDuringPresentation = false
```

* 然後點擊search的icon後執行

```
    @IBAction func startSearch (_ sender:UIBarButtonItem) {

        self.definesPresentationContext = true
        // 隱藏左右兩邊的Button Item
        self.navigationItem.leftBarButtonItem = nil
        self.navigationItem.rightBarButtonItem = nil
        // 將titleView的內容設定成searchBar
        self.navigationItem.titleView = searchController.searchBar
        searchController.isActive = true
    }
```

* 接著設定當searchBar消失時的動作

```
    func didDismissSearchController(_ searchController: UISearchController) {

        self.navigationItem.titleView = nil
        self.title = "視訊"
        self.navigationItem.leftBarButtonItem = self.searchBarItem
        self.navigationItem.rightBarButtonItem = self.createLiveBarItem
    }
```

* 最後是讓searchBar一顯示的時候，自動彈出keyboard

```
    func didPresentSearchController(_ searchController: UISearchController) {

        DispatchQueue.main.async {
            searchController.searchBar.becomeFirstResponder()
        }
    }
```

讓Search Bar的取消鍵有作用

```
func searchBarCancelButtonClicked(searchBar: UISearchBar) {
    self.searchBar.showCancelButton = false
}
```



