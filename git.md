# 用Dropbox來建置git server （Mac）

* ### 很重要！

  ```
  想要用此git server的mac電腦，都要安裝dropbox的App，並且登入相同帳號
  ```
* ### 先在Dropbox的資料節內建立Git的repository

  ```
  cd ~/Dropbox/
  mkdir git (隨便你取，名字不重要，用來當作git專案的根目錄)
  cd git
  git init --bare myProject.git （這樣就會在git目錄下，建立名叫myProject.git的資料夾，並且是這個專案的git根目錄）
  ```
* ### 將現有專案Clone到Dropbox並且設為master branch

  ```
  cd ~/Desktop/myProject (請切換到專案的根目錄下)
  git init (初始化git）
  git remote add origin ~/Dropbox/git/myProject.git （將遠端的Dropbox專案目錄"myProject.git"，命名為origin的遠端repository）
  git push -u origin master（將目前專案上傳到遠端origin，並且建立一個叫做"master"的branch）
  ```
* ### 另外一台電腦將遠端檔案clone到本地

  ```
  cd ~/ (切換到想要建立專案的資料夾)
  git clone ~/Dropbox/git/myProject.git myNewProject（將git server上的myProject專案，複製到本機端的myNewProject資料夾下）
  ```

  ### 現在就可以開始協同合作寫Code囉！

### Rename branch

* `git branch -m <origin name> <new name>  //rename any branch`
* `git branch -m <new name> //rename current branch`





