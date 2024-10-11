---
layout: single
title: "git版本控制簡易教學-使用範例練習"
date:  2020-2-21 23:34:00 +0800
permalink: /gitexample/
categories: 
  - git
tags:
  - git
  - 版本控制
  - 例子
---

我自從想要在github pages上面放網頁之後，使用**git(版本控制)**就變成更新和維護這個網頁的必要工具，因此學習git的路就此開始，以下記錄我學習的重點，可能寫得有點精簡，往後會慢慢補齊。  
  
**1. 安裝git 註冊github 選擇一個喜歡的shell**  
  
+ 此步驟因為過於簡單我就不詳細講解了，基本比較有麻煩的部分應該只有安裝git的部分。  
  
**2. 初始設定git**   
  
```
    git config --list //查看設定值
    git config --global user.name "username" //設定使用者名稱
    git config --global user.email "username@email.com"  
    // 使用者Email  
```  
     
**3. 基礎git概念**  
  
+ 不管如何，要使用git之前都要先使專案(資料夾)變成git倉儲  
```
    git init //方法一，進入專案資料夾並初始化
    git clone //方法二，clone現有專案的網址
```
   
**4. 使用commit!**  
  
+ 擁有一個git repo(git倉儲)就能使用基礎的git功能
```
    git add . //將檔案加入追蹤
    git commit -m '...' //commit並註解
```
  
**5. 創建分支branch**  
  
+ 理論上一開始的初始化的git repo會建立在master這條分支上，如果想在不影響現有專案的狀態上(也就是master的分支狀態)，就要開另一條分支繼續開發專案，這時候就需要使用到git branch的功能  
```
    git branch "BRANCHNAME" //建立新的branch
    git checkout "BRANCHNAME" //將狀態轉移到另一條branch
```
  
**6. 合併分支到master並且push上github**

+ 當在分支修改的專案你認位已經完成，那就可以merge到master，更新整體專案進
度
```
    git status //確認目前狀態
    git checkout "master" // 切回master分支
    git merge "BRANCHNAME" // 合併分支
    git push //push上github!!
```
  
**7. 回復到之前版本(實用)**

+ 當你會目前版本不滿意，想回到之前的版本
```
    git log --oneline -10 //顯示前幾次的版本編號
    git reset --hard HEAD~n //回到上n個版本(n=1/2/3...)
    git reset --hard "commitid"
```


