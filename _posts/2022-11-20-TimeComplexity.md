---
layout: single
title: "常見的時間複雜度"
date:  2022-11-20 00:00:00 +0800
permalink: /time/
categories: 
  - algorithm
tags:
  - markdown
  - algorithm
  - data structure
---
####資料結構的操作
|Data Structure|Insert|Delete|Search|
|:----         |:----:|:----:|:----:|
|Array         |O(n)  |O(n)  |O(n)  |
|Link list     |O(1)  |O(1)  |O(n)  |
|Heap(min、max)|O(1)  |O(1)  |O(n)  |


   

####排序
|Sort Type     |Avg     |Best    |Worst |
|:----         |:----:  |:----:  |:----:|
|Bubble        |O(n^2)  |O(n)    |O(n^2)|
|Insert        |O(n^2)  |O(n)    |O(n^2)|
|Selection     |O(n^2)  |O(n^2)  |O(n^2)|
|Merge         |O(nlogn)|O(nlogn)|O(nlogn)|
|Quick         |O(nlogn)|O(nlogn)|O(n^2)|
|Heap          |O(nlogn)|O(nlogn)|O(nlogn)|
|Radix         |O(d*(n+r)) |
|Counting      |O(n+k)     | 
**注**:k是值域、d是位數、r是進位制

####高等樹操作關鍵字複習
|Advanced Tree |簡述  |Insert |delete |
|:----         |:----:|:----:|:----:|
|MinMaxHeap    |一層min一層max...|  |  |
|Deap          |分邊 一邊min一邊max  |  |  |
|SMMH          | 點的值界在祖父的左右兒子之間|||
|Btree         |2<=root degree<=m ceiling(m/2)<=中間node<=m|||
|Red Black tree|Root到leaf有相同的黑node|||
|Leftist Heap  |Liftist tree and min heap|||
|Binomial Heap ||||
|Fibonacci Heap||||
