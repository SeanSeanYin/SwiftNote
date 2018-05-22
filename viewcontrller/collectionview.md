* 讓CollectionView的Cell可以在計算完Cell的寬度後再重新畫Cell並且不會block的方法

```
    func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
        // 先宣告Cell
        if let cell = collectionView.dequeueReusableCell(withReuseIdentifier: "BookCollectionCell", for: indexPath) as? BookCollectionCell {
        
            // 設定cell和coverImageView的背景色
            cell.backgroundColor = UIColor.clear
            cell.coverImageView.backgroundColor = UIColor.white

            // 確保獲得資料，否則直接回覆一個空的Cell
            guard let book = (self.recommendList[collectionView.tag].books?[indexPath.item]) else {
                return UICollectionViewCell()
            }

            // 獲得下載圖片的url，否則直接給預設圖片
            if let imageUrl = book.bookDetails.imageUrl {

                DispatchQueue.global().async {
                    NetworkManager.shared.downloadImage(withImageUrl: imageUrl, completion: { [weak self] image in
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
                        } else {
                            DispatchQueue.main.async {
                                cell.coverImageView.image = UIImage(named: "default_book")
                            }
                        }
                    })
                }
            } else {
                cell.coverImageView.image = UIImage(named: "default_book")
            }

            if (book.bookDetails.stores == nil) || (book.bookDetails.stores!.count == 0) {

                DispatchQueue.main.async {
                    cell.stockLabel.text = NSLocalizedString("SeeStaff", comment: "")
                    cell.stockLabel.textColor = UIColor.hex("F5A623")
                    _ = cell.coverImageView.setBorder(with: UIColor.hex("F5A623").cgColor)
                }
            } else {
                cell.stockLabel.text = NSLocalizedString("SeeStaff", comment: "")
                cell.stockLabel.textColor = UIColor.hex("F5A623")
                _ = cell.coverImageView.setBorder(with: UIColor.hex("F5A623").cgColor)

                for store in (book.bookDetails.stores)! {
                    if store.inStock == nil { continue }
                    if (store.id)! == self.store.id && ((store.inStock)! > 0) {
                        cell.stockLabel.text = NSLocalizedString("InStore", comment: "")
                        cell.stockLabel.textColor = UIColor.hex("00A0E9")
                        _ = cell.coverImageView.setBorder(with: UIColor.hex("00A0E9").cgColor)
                        break
                    }
                }
            }

            return cell
        }

        return UICollectionViewCell()
    }
```



