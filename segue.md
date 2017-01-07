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
  
