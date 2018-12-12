---
title: 入門 SourceTree
date: 2018-12-8
author: Yang
img: https://firebasestorage.googleapis.com/v0/b/yangyangxun-4937f.appspot.com/o/%E9%83%A8%E8%90%BD%E6%A0%BC%E6%96%87%E7%AB%A0%E9%A6%96%E5%9C%96%2F2018-12-4-GitFlow-SourceTree.png?alt=media&token=96cfb2d7-1a39-40fe-9002-1e00a1af2a67
category: Development Tools
tag: 
 - Git
 - SourceTree 
---


## 前言

最近剛到職上班，公司用 SourceTree 當作 Git 圖形化工具，這邊記錄一些入門技巧。

## 實作步驟 


1. 初始環境為 Clone 下 Github 的遠端 Repo 。我的專案內只有 index.html 檔，並且有一次提交紀錄，此時 History 畫面如下。
   可以看到目前的 Graph 有三個 Mark ，解釋如下方。 
*    `master` : 主分支
*    `origin/master` : 我們用 (遠端倉庫名)/(分支名) 這樣的形式表示遠端分支。Git 會自動為你將 Clone 位址的遠端倉庫命名為 origin，
      並下載其中所有的資料，建立一個指向它的 master 分支的指標。
*    `origin/HEAD` : 用來指向目前分支的最新版本，也就是指向origin/master。
*    origin 其實就是遠端儲存庫的別名，你可以輸入 `git remote -v` 就可以看到遠端儲存庫的路徑。

   ![](https://firebasestorage.googleapis.com/v0/b/yangyangxun-4937f.appspot.com/o/Git%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6%2F2018-12-3-Git-With-SourceTree%2Fstep1.png?alt=media&token=6f13c184-6c0f-4ffa-b1b4-5ab2c27ed145)


2. 接著就來建立我們 GitFlow 大地圖的第一步，創建一個 develop 分支。上方欄 Branch 按下去，填入 Branch 名稱即可。
   **細部觀察**可以發現創建分支後 SourceTree 會自動幫我們跳到分支上。
   此動作相當於**指令方式** `git branch develop` 建立分支。如果有勾選 `Checkout new branch` 就會在建立分支後立即跳到分之。
   
   ![](https://firebasestorage.googleapis.com/v0/b/yangyangxun-4937f.appspot.com/o/Git%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6%2F2018-12-3-Git-With-SourceTree%2Fstep2.png?alt=media&token=70a4083e-f0b1-4f06-b998-59b2514e092a)
   
3. 再加入兩支 feature 分支。分別是 feature/EditHomePage 以及 feature/AddAboutMe。
   一樣可以發現圓點標記都停留在最後加入的分支上。
   
   ![](https://firebasestorage.googleapis.com/v0/b/yangyangxun-4937f.appspot.com/o/Git%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6%2F2018-12-3-Git-With-SourceTree%2Fstep3.png?alt=media&token=0af6ed08-a6e8-4a72-b8b1-9fb04cd8fd1c)
   
4. 回到 feature/EditHomePage 編輯 index.html 並且做一次提交。結果如下。

   ![](https://firebasestorage.googleapis.com/v0/b/yangyangxun-4937f.appspot.com/o/Git%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6%2F2018-12-3-Git-With-SourceTree%2Fstep4.png?alt=media&token=0f2c8c4a-fc9a-4881-9232-f9ef145f173f)

5. 如果成功完成 feature 分支任務了。我們就可以做 merge 到 develop 的動作，**首先要先跳到 develop
   分支**，鼠標移動到要 merge 得分支上，右鍵選 merge 。

   ![](https://firebasestorage.googleapis.com/v0/b/yangyangxun-4937f.appspot.com/o/Git%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6%2F2018-12-3-Git-With-SourceTree%2Fstep5.png?alt=media&token=cdb37280-189e-4860-8ad8-1a355a0958f3)
   
   完成後如下圖。
   
   ![](https://firebasestorage.googleapis.com/v0/b/yangyangxun-4937f.appspot.com/o/Git%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6%2F2018-12-3-Git-With-SourceTree%2Fstep5-2.png?alt=media&token=27a90c63-8535-44c2-9e7b-89e6388a19cb)

6. 都沒問題後可以刪除 feature 分支，因為它已經完成階段性的任務了。同時跳到 feature/AddAboutMe 新增一支 about.html 並提交。結果如          圖。**指令方式**刪除分支 `git branch -d feature/EditHomePage`
   
   ![](https://firebasestorage.googleapis.com/v0/b/yangyangxun-4937f.appspot.com/o/Git%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6%2F2018-12-3-Git-With-SourceTree%2Fstep6.png?alt=media&token=f90560d1-a902-4dd7-91e3-38e9814a83e0)
   
7. 一樣完成 feature 後 merge 到 develop。完成如圖。(完成就可以刪除 feature 分支)
   **注意**盡量不要有太多或是剩餘未 merge 的 feature 分支。

   ![](https://firebasestorage.googleapis.com/v0/b/yangyangxun-4937f.appspot.com/o/Git%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6%2F2018-12-3-Git-With-SourceTree%2Fstep7.png?alt=media&token=096825f5-a773-4a16-90bf-8b55481032d0)
   
   
8. 接下來我們要來搞一點破壞了，模擬一下開發中如果 commit 上錯誤的版本要如何撤回。
   這邊示範如果提交兩次錯誤 commit 在未 push 到遠端 server 之前都能夠撤回。
   直接把游標移動到想撤回的地方，右鍵 Reset develop to commit。
   
   ![](https://firebasestorage.googleapis.com/v0/b/yangyangxun-4937f.appspot.com/o/Git%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6%2F2018-12-3-Git-With-SourceTree%2Fstep8-1.png?alt=media&token=79da2cc8-dec1-4e3e-ac4b-3a433647feb1)
   
   點擊之後會有三個選項可以選擇。這裡選 Hard
   
   ![](https://firebasestorage.googleapis.com/v0/b/yangyangxun-4937f.appspot.com/o/Git%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6%2F2018-12-3-Git-With-SourceTree%2Fstep8-2.png?alt=media&token=edc47583-8408-4204-9c81-3f4c43354118)
   
*    `Soft` : 這個模式下的 reset，工作目錄跟暫存區的檔案都不會被丟掉，所以看起來就只有 HEAD 的移動而已。也因此，Commit 拆出來的檔案會直接放在暫存區 (Stage)。
*    `Mixed` : 為預設模式。這個模式會把暫存區的檔案丟掉，但不會動到工作目錄的檔案，也就是說 Commit 拆出來的檔案會留在工作目錄，但不會留在暫存區 (Unstaged)。
*    `Hard` : 在這個模式下，不管是工作目錄以及暫存區的檔案都會丟掉 (砍掉重練)。
   
   撤回後圖型就回到 step7 囉！

## 結語

除了使用方便的圖形化介面，也期許自己能利用指令來做好版本控制，而不只是依賴圖形工具。

