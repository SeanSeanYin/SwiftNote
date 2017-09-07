* #### View
* #### Layer

  * 一個`layer`可以有很多`sublayer`，一個`sublayer`只有一個父`layer`
  * `sublayer`被加入的順序會是被畫出來的順序\(Queue\)，因此越先加入在越下面
  * `layer`所屬的`View的subview的layer`，會跟`layer的sublayer`在同一個z平面
  * `低zPosition（CGFloat）`的`layer`會比高的更早被畫出來，利用`zPosition`取代`layer`的加入順序會更方便解決呈現順序`（預設layer的zPosition都是0.0）`
  * `Layer`創建時，預設的`frame是(0,0,0,0)`，所以要給定`Width＆Height`再`addSublayer`，才會看得到
  * Layer有兩個座標系統，Postion和AnchorPoint
    * Postion：Layer的AnchorPoint在SuperLayer的點
    * AnchorPoint：Layer內部的點，\(0.0\)代表這Layer的左上角，\(1,1\)代表右下角。預設值為\(0.5,0.5\)
    * Postion和AnchorPoint的關係
      ```
      position.x = frame.origin.x + anchorPoint.x * bounds.size.width  
      position.y = frame.origin.y + anchorPoint.y * bounds.size.height
      ```
    * 變換Position或AnchorPoint的值，不相互影響，只影響Frame的x和y值，上面公式可換為
      ```
      frame.origin.x = position.x - anchorPoint.x * bounds.size.width
      frame.origin.y = position.y - anchorPoint.y * bounds.size.height
      ```
  * ScrollerLayer適合用來呈現需要滑動點or視窗的效果

#### 





