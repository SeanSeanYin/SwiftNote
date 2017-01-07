* #### Segue用法

  * 呼叫特定的Segue
  `performSegue(withIdentifier: "showPopover", sender: sender )`

  * 然後實作要傳遞到下一個Scene的資料
```
override func prepare(for segue: UIStoryboardSegue, sender: Any!) {
       if segue.identifier == "showPopover" {
           let viewController = segue.destination as! UITableViewController
           if let popoverController = viewController.popoverPresentationController {
              popoverController.delegate = self
           }
       }
}
```
  
* #### Unwind無效的情況

 * 現在有三個ViewController：`MainViewController`、`SecondViewController`、`ThirdViewController`，在 `ThirdViewController` 建立 `unwindToMain` 和`unwindToSecond`的`Unwind Segue`，然後 `MainViewController`是`Initial ViewController`
 * 一開始從`MainViewController`直接跳到`ThirdViewController`後，因為沒有載入過`SecondViewController`，執行`unwindToSecond`的`unwind segue`會無效，但是執行`unwindToMain`的會正常跳轉頁面
 * 推測原因是因為沒讀取過`SecondViewController`，所以程式不知道要跳到哪一頁

* #### Unwind的使用方式

  * 在想要返回的目的ViewController內，建立收到unwind後的處理函式，參數的類型為`UIStoryboardSegue`，這很重要！

    ```
    @IBAction func backToCafeDetail (_ segue:UIStoryboardSegue) {

        let sourceController = segue.source as! SortTableViewController
        self.sortItem = sourceController.sortItem

        if (self.cafes != nil){
            self.sortedCafes = sort(with: self.cafes, and: self.sortItem)
        }
        self.cafeDetailTable.reloadData()
    }
    ```

  * 在發送unwind segue的ViewController內，透過Main.storyboard建立unwind segue，先選取ViewController，然後點選此ViewController的icon，以Ctrl-Drag的方式拉到右邊的Exit icon上再放掉，剛剛建立的unwind處理函式（在這個例子是backToCafeDetail）會出現在下拉式選單內，然後選取backToCafeDetail，完成建立Unwind Segue。

  ![](/assets/螢幕快照 2017-01-01 11.44.10.png)

 * 然後在ViewController內選取該Unwind Segue，將Identifier欄位填上backToCafeDetail（名字一樣比較不容易搞混）
 * 最後是在函式內利用`self.performSegue(withIdentifier: "backToCafeDetail", sender: self)`的方式呼叫Unwind Segue
