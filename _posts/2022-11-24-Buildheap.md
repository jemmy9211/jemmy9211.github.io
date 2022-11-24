---
layout: single
title: "以buttom-up方式建立Heap 在O(n)時間內完成"
date:  2022-11-24 00:00:00 +0800
permalink: /buildheap/
categories: 
  - Heap
tags:
  - data structure
  - c++
---
以兩個function構成  
Heapify調整以該node為root為子樹的subtree成heap  
Build Heap依序從最後一個parent回調到root   

``` c++
#include<iostream>
#include<stdio.h>
#include <algorithm>    // std::swap
using namespace std;
int arr[11]={1,3,5,4,6,13,10,9,8,15,17};
//complete tree
//            1
//         /     \
//        3       5
//      /  \     / \
//     4    6   13  10
//    / \  / \  
//   9  8 15 17
void heapify(int* arr,int n,int i){
    int root=i;
    int l=i*2+1;
    int r=i*2+2;
    if(l<n && arr[l]>arr[root]){
        root=l;
    }

    if(r<n && arr[r]>arr[root]){
        root=r;
    }

    if(root!=i){
        swap(arr[i],arr[root]);
        heapify(arr,n,root);
    }
}

void buildheap(int *arr,int n){
    int lastparent=(n/2)-1;
    for(int i=lastparent;i>=0;i--){
        heapify(arr,n,i);
    }
}
void printheap(int *arr,int n){
    int next=1;
    for(int i=0;i<n;i++){
        cout<<arr[i]<<"\t";
        if(i+1==next){
            cout<< endl;
            next=next*2+1;
        }
    }
    cout<<endl;
}
int main(){
    int n=11;
    buildheap(arr,n);
    printheap(arr,n);

}

```
