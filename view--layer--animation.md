* ####View
* ####Layer
 * 一個layer可以有很多sublayer，一個sublayer只有一個父layer
 * sublayer被加入的順序會是被畫出來的順序
 * layer所屬的View的subview的layer，會跟layer的sublayer在同一個z平面
 * 低zPosition（CGFloat）的layer會比高的更早被畫出來，利用zPosition取代layer的加入順序會更方便解決呈現順序（預設layer的zPosition都是0.0）
 
 