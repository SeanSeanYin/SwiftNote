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
 * 一開始從`MainViewController`直接跳到`ThirdViewController`後，因為沒有載入過SecondViewController，

