* 先宣告下列變數來準備使用

```
    let captureSession = AVCaptureSession()
    var captureDevice:AVCaptureDevice?
    var captureLayer:AVCaptureVideoPreviewLayer?
    var metadata:AVCaptureMetadataOutput? = nil
```

* 先  `import AVFoundation`  
* 在 `viewDidLoad()` 先創造 `Capture Session`

```
     func setupCaptureSession(){
        // 先設定deive和video的種類
        self.captureDevice = AVCaptureDevice.defaultDevice(withMediaType: AVMediaTypeVideo)
        let deviceInput:AVCaptureDeviceInput
        do {
            deviceInput = try AVCaptureDeviceInput(device: captureDevice)
        } catch {
            return
        }

        if (captureSession.canAddInput(deviceInput)){
            // Show live feed
            captureSession.addInput(deviceInput)
            // 設定output
            self.addMetaDataCaptureOutToSession()
            // 設定previewLayer
            self.setupPreviewLayer(completion: {
                self.captureSession.startRunning()
            })
        } else {
            self.showMessage(title: nil, message: NSLocalizedString("errorWhileSettingUpInputCaptureSession", comment: ""), action: nil)
        }
    }

    // Metadata capture
    func addMetaDataCaptureOutToSession(){

        metadata = AVCaptureMetadataOutput()
        self.captureSession.addOutput(metadata)

        // 文件規定要提供serial的queue，所以預設使用main thread來做
        metadata?.setMetadataObjectsDelegate(self, queue: DispatchQueue.main)
        // 設定支援的code類型
        metadata?.metadataObjectTypes = [AVMetadataObjectTypeQRCode, AVMetadataObjectTypeCode128Code, AVMetadataObjectTypeCode39Code, AVMetadataObjectTypeCode93Code, AVMetadataObjectTypeUPCECode, AVMetadataObjectTypePDF417Code, AVMetadataObjectTypeEAN13Code, AVMetadataObjectTypeAztecCode,AVMetadataObjectTypeEAN8Code]
    }
    
    // Set preview layer
    func setupPreviewLayer(completion:() -> ()){
        
        self.captureLayer = AVCaptureVideoPreviewLayer(session: captureSession)
        self.captureLayer?.frame = CGRect(x: 0.0, y: 0.0, width: self.screenWidth(), height: self.screenHeight())
        self.captureLayer?.borderColor = UIColor(red:0/255.0, green:0/255.0, blue:0/255.0, alpha: 0.0).cgColor
        self.captureLayer?.videoGravity = AVLayerVideoGravityResize
        self.previewView.layer.addSublayer(self.captureLayer!)
        completion()
    }
```

* 然後實作 delegate `AVCaptureMetadataOutputObjectsDelegate`

```
    func captureOutput(_ captureOutput: AVCaptureOutput!, didOutputMetadataObjects metadataObjects: [Any]!, from connection: AVCaptureConnection!) {
        
        guard metadataObjects != nil && metadataObjects.count > 0 else {
            return
        }
        let decodedData = metadataObjects[0] as! AVMetadataMachineReadableCodeObject
        print("Barcode String \(decodedData.stringValue) Type \(decodedData.type)")
        
        if decodedData.stringValue != nil && decodedData.stringValue.length > 0 {
            self.captureSession.stopRunning()
            callProductAPI(eanStr: decodedData.stringValue)
        }
    }
```

* 想要限制掃描的區域，請在 `viewDidLoad()` 內先宣告 Notification

```
    override func viewDidLoad() {
        super.viewDidLoad()
        
        self.setupCaptureSession()
        NotificationCenter.default.addObserver(self, selector: #selector(self.avCaptureInputPortFormatDescriptionDidChangeNotification(notification:)), name: NSNotification.Name.AVCaptureInputPortFormatDescriptionDidChange, object: nil)
    
```

* 然後實作 

```
    func avCaptureInputPortFormatDescriptionDidChangeNotification(notification: NSNotification) {
    // metadataOutputRectOfInterest(for:) 內的CGRect的值，左下是(0,0)，右上是(1,1)，跟一般座標不一樣
        self.metadata?.rectOfInterest = (self.captureLayer?.metadataOutputRectOfInterest(for: CGRect(x:  self.screenWidth() * 0.075, y: self.screenHeight() * 0.25, width: self.screenWidth() * 0.85, height: self.screenHeight() * 0.25)))!
    }
```



