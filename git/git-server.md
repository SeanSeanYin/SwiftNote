* 以ubuntu 16.10版的Azure server為例
* 先透過ssh登入ubuntu server
* 然後`sudo -s` 切換到超級使用者模式
* 安裝需要的套件
  ```
  apt-get install libcurl4-gnutls-dev libexpat1-dev gettext libz-dev libssl-dev 
  ```
* 安裝git server
  ```
  apt-get install git-core
  ```
* 新增要存取git server的使用者
  ```
  // 建立user
  adduser [username]
  // 把user加入到root群組
  usermod -g admin [username]
  ```
* 


