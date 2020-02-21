---
layout: single
title: "git版本控制簡易教學，使用範例練習"
date:  2020-2-21 23:34:00 +0800
permalink: /gitexample/
categories: 
  - git
tags:
  - git
  - 版本控制
  - 例子
  - 做自己
---

我自從想要在github pages上面放網頁之後，使用git-版本控制-就變成更新和維護這個網頁的必要工具，學習git的路就此開始，以下記錄我學習的一些重點，我喜歡直接使用例子學習，因此以下的筆記會用一個例子講解。  
  
**1. 安裝git 註冊github 選擇一個喜歡的shell**  
  
此步驟因為過於簡單我就不詳細講解了，基本比較有麻煩的部分應該只有安裝git的部分。  
  
**2. 初始設定git**   
  
```
    git config --list //查看設定值
    git config --global user.name "username" //設定使用者名稱
    git config --global user.email "username@email.com"  
    // 使用者Email  
```  
     
**3. 基礎git概念**  
  
+ 不管如何，要使用git之前都要先使你的專案(資料夾)變成git倉儲  
```
    git init //方法一，進入你的專案資料夾初始化
    git clone //方法二，clone現有專案的網址
```
   
**4. 使用commit!**  
  
+ 擁有一個git repo就能使用基礎的git功能
```
    git add .
    git commit -m '...'
```
  
**5. 創建分支branch**  
  
+ 理論上一開始的初始化的git repo會建立在master這條分支上，如果想要不影響現有專案的狀態，也就是master的狀態，並且開另一條分支繼續開發專案，就需要使用到git branch的功能  
```
    git branch "BRANCHNAME"
    git checkout "BRANCHNAME"
```
  
**6. 合併分支到master&push上github**

+ 當在分支修改的專案你認位已經沒問題，那就可以merge到master，更新專案進
度
```
    git status
    git checkout "BRANCHNAME"
    git merge "BRANCHNAME"
    git push
```
  
**7. 回復到之前版本(實用)**

+ 當你會目前版本不滿意，想回到之前的版本
```
    git log --oneline -10 //顯示前幾次的版本編號
    git reset --hard HEAD~n //回到上n個版本(n=1/2/3...)
    git reset --hard "commitid"
```


