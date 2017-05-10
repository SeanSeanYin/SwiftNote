* #### 讓背景播放影片的做法

```
import AVFoundation
    
class LoginViewController: UIViewController {    
    var avPlayer:AVPlayer!
    var avPlayerLayer:AVPlayerLayer!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        let videoUrl = Bundle.main.url(forResource: "mina_knockknock", withExtension: "MP4")
        avPlayer = AVPlayer(url: videoUrl!)
        avPlayerLayer = AVPlayerLayer(player: avPlayer)
        avPlayerLayer.videoGravity = AVLayerVideoGravityResizeAspectFill
        avPlayer.volume = 0.0
        avPlayer.actionAtItemEnd = AVPlayerActionAtItemEnd.none
        
        avPlayerLayer.frame = view.layer.bounds
        view.backgroundColor = UIColor.clear
        view.layer.insertSublayer(avPlayerLayer, at: 0)
        
        NotificationCenter.default.addObserver(self, selector: #selector(playerItemDidReachEnd(notification:)), name: NSNotification.Name(rawValue: "AVPlayerItemDidPlayToEndTimeNotification"), object: avPlayer.currentItem)
        
        logoImage.isHidden = true
        self.navigationController?.navigationBar.isHidden = true
    }

    func playerItemDidReachEnd(notification:Notification) {
        let playerItem = notification.object as! AVPlayerItem
        playerItem.seek(to: kCMTimeZero)
        avPlayer.play()
    }
}
```



