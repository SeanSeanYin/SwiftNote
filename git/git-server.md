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
* 把使用者加入群組，方便做權限控管

```
// 查詢Group
cat /etc/group
// 新增到group
groupadd [groupname]
// -a -G 將某位user加入到新群組，但不將使用者從原本群組移除
usermod -a -G [groupname] [username]
// 更改將Group綁定到某個路徑上
chgrp -R [groupname] [path] //ex chgrp -R git /var/git
// 更改path底下所有檔案的rwx權限for group
chown g+rwx -R [path]
```



