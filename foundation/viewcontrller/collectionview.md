# CollectionView

* 讓CollectionView的Cell可以在計算完Cell的寬度後再重新畫Cell並且不會block的方法

```text
    func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
        // 先宣告Cell
        if let cell = collectionView.dequeueReusableCell(withReuseIdentifier: "BookCollectionCell", for: indexPath) as? BookCollectionCell {

            // 設定cell和coverImageView的背景色
            cell.backgroundColor = UIColor.clear
            cell.coverImageView.backgroundColor = UIColor.white

            // 確保獲得資料，否則直接返回一個空的Cell
            guard let book = (self.recommendList[collectionView.tag].books?[indexPath.item]) else {
                return UICollectionViewCell()
            }

            // 獲得下載圖片的url，否則直接給預設圖片
            if let imageUrl = book.bookDetails.imageUrl {

                // 將下載的工作塞到global queue內，不要block到main queuq
                DispatchQueue.global().async {
                    NetworkManager.shared.downloadImage(withImageUrl: imageUrl, completion: { [weak self] image in
                        // 如果下載成功，塞到Main queue去更新圖片，然後重新reloadItems來畫新的Width
                        if image != nil {
                            DispatchQueue.main.async {
                                let calWidth:CGFloat = Common.countImageWidth(img: image!, fixedHeight: 130 * (self?.getScreenScale(with: .height))!)
                                (self?.recommendList[collectionView.tag].books![indexPath.item])?.imageWidth = calWidth
                                cell.coverImageView.image = image
                                _ = cell.coverImageView.setShadow(withOpacity: 0.5, offset: CGSize(width: 2, height: 2))
                                if let index = collectionView.indexPath(for: cell) {
                                    if ((self?.recommendList[collectionView.tag].books![indexPath.item])?.hasReload == false) {
                                        collectionView.reloadItems(at: [index])
                                        (self?.recommendList[collectionView.tag].books![indexPath.item])?.hasReload = true
                                    }
                                }
                            }
                        } else { // 下載失敗，直接給預設圖片
                            DispatchQueue.main.async {
                                cell.coverImageView.image = UIImage(named: "default_book")
                            }
                        }
                    })
                }
            } else {
                cell.coverImageView.image = UIImage(named: "default_book")
            }
            // 將Cell返回
            return cell
        }
        // 返回空的Cell
        return UICollectionViewCell()
    }
```

* 讓Cell內的圖片依照Cell順序下載顯示的方法

```text
// 先宣告一個Serial的Queue
fileprivate let serialQueue = DispatchQueue.init(label: "queue1", qos: .userInitiated)

// 然後在呼叫下載圖片的API時使用
self.serialQueue.async {
    // Download image...
}
```

