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
chmod g+rwx -R [path]
// 讓其他使用者無法存取此repository
chmod o-rwx -R [path]
```

* 架設gitolite的流程

  * 先安裝好git server

  * 選擇一台client端電腦作為晚點要設定gitolite的主帳號

    * 利用ssh-keygen產生一對公鑰私鑰

    * 透過scp將公鑰上傳到gitolite的server上（在此假設公鑰名稱叫做id\_rsa.pub）

  * 在ubuntu內開啟一個名叫git的userid（這會是以後所有人要來存取此台gitolite的唯一帳號），再使用su - git的方式切換到git

  * 然後在git的家目錄底下抓取gitiolite的source code

  ```
  git clone git://github.com/sitaramc/gitolite
  ```

  * 安裝gitolite

  ```
  cd $HOME
  mkdir -p bin
  gitolite/install -to $HOME/bin
  ```

  * 設定gitolite，並選擇gitolite帳號的公鑰

  ```
  cd $HOME
  $HOME/bin/gitolite setup - /tmp/id_rsa.pub
  ```

  * 用client端（要有id\_rsa.pub這私鑰的別台電腦）測試gitolite是否安裝成功

  ```
  git ls-remote git@server:gitolite-admin

  //如果有回覆類似下面的東西，代表安裝成功
  9dd8aab60bac5e54ccf887a87b4f3d35c96b05e4    HEAD
  9dd8aab60bac5e54ccf887a87b4f3d35c96b05e4    refs/heads/master
  ```

* 加入使用者的方式

  * 把使用者的公鑰放入client端的gitolite-admin/keydir底下

  * 假設公鑰名稱叫做user1.pub，這個user在repo裡面的名稱就會叫做user1

  * 之後add & commit & push

* 替使用者開新專案的流程

  * 先編輯gitolite-admin/conf/gitolite.conf來開啟專案，並同時給予使用者權限

  ```
  repo   projectName
      RW     =    user1
      -R     =    user2
  ```

  * 然後commit & push
  * 然後用對此專案有寫權限的user先clone

  ```
  git clone git@server ip or domain name:projectName.git
  ```

  * 之後先把所有專案檔案拉入此專案資料夾底下，再add & commit & push即可

* 使用者的權限設定
  * 想要多瞭解可以看這兩篇

    * [Tsung's blog](https://blog.longwin.com.tw/2011/03/linux-gitolite-git-server-2011/)

    * [CrBoy's blog](http://blog.crboy.net/2012/06/gitolite-settings-and-managements.html)

  * C, R, RW, RW+, RWC, RW+C, RWD, RW+D, RWCD, RW+CD, -

    * R 讀取
    * W 寫入或建立新的 refs \(branches, tags\)
    * + 刪除或改變 refs `（允許push -f）`
    * - 拒絕存取 \(可用以明確拒絕使用者存取此 repo，須寫在 R 權限之前\)
    * C 和 D是比較特別的權限
    * C（獨立）僅用於使用正規表示法的repo，表示可建立符合該正規表示法的repo名稱
    * C（組合）僅用於使用正規表示法的refs，表示可建立符合該正規表示法的refs名稱
    * D僅用於使用正規表示法的refs，表示可刪除符合該正規表示法的refs名稱



