---
layout: single
title: "C/C++中main函數的參數argc、argv"
date:  2022-5-14 00:00:00 +0800
permalink: /argcargv/
categories: 
  - "c++"
tags:
  - "c/c++"
---
>Background:
>  
>因為FILE I/O這門課的HW2需要寫一個類似linux裡的find指令， 
>這個指令會需要有參數輸入(在命令列)，所以我著手搞懂這兩個常常
>看到的參數argv、argc 

先看一個基本的C++ program  

``` c++
#include<iostream>
using namespace std;
int main(int argc,char **argv){
    for(int i=0;i<argc;i++){
        cout << argc[i] << endl;
    }
    return 0;
}
```

+ argc就是輸入參數的數量，注意當你的程式沒有輸入的參數時，這個數為一，因為他預設會包含檔名
+ argv就是存參數的array會依序存放你參數的值
