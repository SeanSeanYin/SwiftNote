* #### 使用Xib的方式來建立UIView（[參考這篇](https://medium.com/@brianclouser/swift-3-creating-a-custom-view-from-a-xib-ecdfe5b3a960)）

  * 先New一個View的File（myView.xib），然後在裡面拉Layout

  * 再New一個myView.swift的File來控制這個xib，內容一定要有

    * @IBOutlet var contentView: UIView! 用來控制myView.xib內預設的UIView

    * 提供兩種UIView的init方式，並且呼叫設定myView的Frame的函式

    * commonInit用來註冊這個xib，並且設定frame和上下左右的邊界

  * ```
    class CalendarUIView: UIView {

        @IBOutlet var contentView: UIView!
        @IBOutlet weak var monthLabel:UILabel!
        @IBOutlet weak var dayLabel:UILabel!
        @IBOutlet weak var weekDayLabel:UILabel!
        @IBOutlet weak var storeDayLabel:UILabel!
        @IBOutlet weak var titleDayLabel:UILabel!
        @IBOutlet weak var subTitleLabel:UILabel!
        @IBOutlet weak var dateLabel:UILabel!
        @IBOutlet weak var priceLabel:UILabel!

        override init(frame: CGRect) {
            super.init(frame:frame)
            commonInit()

        }

        required init?(coder aDecoder: NSCoder) {
            super.init(coder: aDecoder)
            commonInit()
        }

        private func commonInit() {
            Bundle.main.loadNibNamed("CalendarUIView", owner: self, options: nil)
            addSubview(contentView)
            contentView.frame = self.bounds
            contentView.autoresizingMask = [.flexibleWidth, .flexibleHeight]
        }
    }
    ```
  * 選擇myView.xib的Identity Inspector，在Class欄位，填入myView這個class name

  * 將class內的IBOutlet的元件，跟xib內的component做連結



