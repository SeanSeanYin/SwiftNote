* #### 使用圖片快取

  * 先在ViewController內宣告  `var imageCache = NSCache<AnyObject,AnyObject>()`

  * 然後使用 imageCache.object\(forKey: id as AnyObject\)來判斷獲取照片Url是否成功，不成功就需要下載

  * 在imageCache.setObject\(response.destinationURL! as AnyObject, forKey: id as AnyObject\)時，第一個參數請存Url

```
            let id = self.newsArray[indexPath.row].id
            // 先取抓快取裡面的圖，沒有的話再下載
            if let imageUrl = imageCache.object(forKey: id as AnyObject) as? URL {
                
                cell.imageview.image = UIImage(contentsOfFile: imageUrl.path)
            } else {
                
                if let imageUrl = self.newsArray[indexPath.row].imagePath {
                    let destination: DownloadRequest.DownloadFileDestination = { _, _ in
                        let documentsURL = FileManager.default.urls(for: .documentDirectory, in: .userDomainMask).first
                        let fileURL = documentsURL?.appendingPathComponent(id!)
                        return (fileURL!, [.removePreviousFile, .createIntermediateDirectories])
                    }
                    Alamofire.download(imageUrl, to: destination).response { response in
                        if response.error == nil, let imagePath = response.destinationURL?.path {
                            OperationQueue.main.addOperation () {
                                let image = UIImage(contentsOfFile: imagePath)
                                cell.imageview.image = image
                                //
                                self.imageCache.setObject(response.destinationURL! as AnyObject, forKey: id as AnyObject)
                            }
                        }
                    }
                }
                cell.timeLabel.text = "日期：\(self.newsArray[indexPath.row].createDate!)"
                cell.titleLabel.text = self.newsArray[indexPath.row].title!
                cell.authorLabel.text = "作者：\(self.newsArray[indexPath.row].author!)"
            }
```



