* # Single

  * #### 適合用在只要知道Success和Error的情況。像是network request或本地file存取
  * #### 只會送出元素一次
  * ```Swift
    enum FileReadError:Error {
        case fileNotFound
        case encodingFailed
    }

    urlString = Single.create(subscribe: { single in
            
        let disposable = Disposables.create()
        var string:String = String()
            
        switch type {
            case .aboutUs:
                string = NSLocalizedString("AboutUsHtml", comment: "")
            case .help:
                string = NSLocalizedString("HelpHtml", comment: "")
            case .privatePolicy:
                string = NSLocalizedString("PrivacyPolicyHtml", comment: "")
            case .termsOfUse:
                string = NSLocalizedString("TermsOfUseHtml", comment: "")
            default:
                break
        }
    
        // 如果讀取資源失敗，就送出fileNotFound的Error
        guard let path = Bundle.main.path(forResource: string, ofType: "html") else {
            single(.error(FileReadError.fileNotFound))
            return disposable
        }
    
        // 如果讀取資源失敗，就送出endingFailed的Error            
        guard let htmlString = try? String.init(contentsOfFile: path, encoding: .utf8) else {
            single(.error(FileReadError.encodingFailed))
            return disposable
        }
    
        // 成功的話，就送出htmlString的success       
        single(.success(htmlString))
    
        // 最後是回收這個Single
        return disposable
    })
    ```



