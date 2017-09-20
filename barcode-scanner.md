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

    //MARK: Metadata capture
    func addMetaDataCaptureOutToSession(){

        metadata = AVCaptureMetadataOutput()
        self.captureSession.addOutput(metadata)

        // 文件規定要提供serial的queue，所以預設使用main thread來做
        metadata?.setMetadataObjectsDelegate(self, queue: DispatchQueue.main)
        // 設定支援的code類型
        metadata?.metadataObjectTypes = [AVMetadataObjectTypeQRCode, AVMetadataObjectTypeCode128Code, AVMetadataObjectTypeCode39Code, AVMetadataObjectTypeCode93Code, AVMetadataObjectTypeUPCECode, AVMetadataObjectTypePDF417Code, AVMetadataObjectTypeEAN13Code, AVMetadataObjectTypeAztecCode,AVMetadataObjectTypeEAN8Code]
    }
```

* 然後實作 delegate `AVCaptureMetadataOutputObjectsDelegate`

```

```

* 


