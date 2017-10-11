* #### 將String轉成Date

  * 先實作出遵循 TransformType 這個protocol的class

  ```
  open class StringTransform:TransformType {

      public typealias Object = Date
      public typealias JSON = String

      public init() {}

      open func transformFromJSON(_ value: Any?) -> Date? {

          let formatter = DateFormatter()
          formatter.dateFormat = "yyyy-MM-dd'T'HH:mm:ssZ"

          if let dateString = value as? String {
              return formatter.date(from: dateString)
          }
          return nil
      }

      open func transformToJSON(_ value: Date?) -> String? {

          let formatter = DateFormatter()
          formatter.dateFormat = "yyyy-MM-dd'T'HH:mm:ssZ"

          if let date = value {
              return formatter.string(from: date)
          }
          return nil
      }
  }
  ```

  * 然後在Mapping的時候調用

  ```
      mutating func mapping(map: Map) {
          date <- (map["date"], StringTransform())
      }
  ```



