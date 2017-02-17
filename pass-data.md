###在Swift內，有ViewController之間，有幾種方式可以傳遞資料

 * ##### Segue：適合用在有上下頁關係的ViewController之間相互傳遞資料
 * ##### Delegate：適合一對一，一個ViewController送，另外一個ViewController收
 * ##### Notification：適合一對多，一個ViewController傳遞（post），其他ViewContoller收（addObserver）
 * ##### Singleton：任意ViewController都可以讀寫，但是要注意到Singleton的life cycle
-------------------------------------------------
* #### Segue的使用方式

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
* #### 使用Segue傳遞到有Navigation Bar的Viewcontroller時，Navigation Bar會顯示失敗的處理方式

  ```
  let nav = segue.destinationViewController as! UINavigationController
  let myViewController = nav.topViewController as! MyViewController
  ```
* #### Unwind無效的情況

  * 現在有三個ViewController：`MainViewController`、`SecondViewController`、`ThirdViewController`，在 `ThirdViewController` 建立 `unwindToMain` 和`unwindToSecond`的`Unwind Segue`，然後 `MainViewController`是`Initial ViewController`
  * 一開始從`MainViewController`直接跳到`ThirdViewController`後，因為沒有載入過`SecondViewController`，執行`unwindToSecond`的`unwind segue`會無效，但是執行`unwindToMain`的會正常跳轉頁面
  * 推測原因是因為沒讀取過`SecondViewController`，所以程式不知道要跳到哪一頁
* #### Unwind Sugue的使用方式

  * 在想要返回的目的`ViewController`內，建立收到`unwind segue`後的處理函式，參數的類型為`UIStoryboardSegue`，這很重要！

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

  * 在發送`unwind segue`的`ViewController`內，透過`Main.storyboard`建立`unwind segue`，先選取`ViewController`，然後點選此`ViewController 的 Home icon`，以Ctrl-Drag的方式拉到右邊的`Exit icon`上再放掉，剛剛建立的unwind處理函式（在這個例子是`backToCafeDetail`）會出現在下拉式選單內，然後選取`backToCafeDetail`，完成建立`Unwind Segue`。

  ![](/assets/螢幕快照 2017-01-01 11.44.10.png)

  * 然後在`ViewController`內選取該`Unwind Segue`，將`Identifier`欄位填上`backToCafeDetail`（名字一樣比較不容易搞混）
  * 最後是在函式內利用`self.performSegue(withIdentifier: "backToCafeDetail", sender: self)`的方式呼叫`Unwind Segue`
-------------------------------------------------
* #### Custom Delegate的使用方式（[參考這篇](http://eddychang.me/blog/swift/66-delegation-example.html)）

  假設我們有兩個Class：Class1 & Class2，我們想要把Class1的某些事情委託給Class2做，我們需要如下的實作方式

  * Class1.swift

  ```
  // 制定Protocol
  protocol Class1Delegate: class {
    // 制定代理方法內，要實作的function
    func getCellTitle(_ index:Int!) -> String?
  }
  class Class1: UITableViewCell {
    // 宣告protocol的變數
    weak var delegate:Class1Delegate?

    // 使用protocl變數:delegate來呼叫function
    let title = delegate?.getCellTitle(0) ?? "No Title"
  }
  ```

  * Class2.swift

  ```
  class Class2: UITableViewController, Class1Delegate {
     //宣告要代理的Class1的實體
     var cell:Class1!

     override func viewDidLoad () {
         super.viewDidLoad()
         // 指定要實作代理方法的對象為self(自己)
         self.cell.delegate = self
     }

     // 實作代理的function
     func getCellTitle(_ index:Int!) -> String? {         
         if (cell != nil) { return cell.title }
         return nil
     }
  } 
  ```

  * `protocol Class1Delegate: class`後面加上`:class`，是為了讓在`Class1`內宣告`delegate`的時候，可以使用`weak`屬性，避免`Retain cycles`。由於`struct和enum`都是`value type`，所以都只能用`strong`。
  * `let title = delegate?.getCellTitle(0) ?? "No Title"` 當`delegate?.getCellTitle(0)`回傳`nil`時，會因為`??`的關係，給`title`一個預設值`"No title"`


* #### 在AppDelegate創造custom delegate去呼叫某個ViewController
 * 會失敗，因為在`ViewController`內宣告的`AppDelegate`的`Instance`，根本不會被`init`，所以`AppDelegate class`內的`delegate is always nil`
 * 改用`Notification`
-------------------------------------------------
* #### Notification的使用方式

 * 在送