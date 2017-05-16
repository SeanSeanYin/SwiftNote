* #### 要用Singleton並且又保證不會被多執行緒同時存取

```
// 創立一個序列化的queue
private let arrayQueue = dispatch_queue_create("arrayQueue", DISPATCH_QUEUE_SERIAL)

// func doSomething(){

    // 用同步式的方法，將block內的事情，加入到arrayQueue內
    dispatch_sync(arrayQueue, {() in
        
        //do anything you want
    })
}
```

* #### 洩漏陷阱

  * 使用struct或有實作NSCopying協定的class來建構singleton

  * 可使用decorator來限制

* #### 共用檔案陷阱

  * 將Singleton的class獨立寫在一個swift檔案內，並且用private關鍵字保護



