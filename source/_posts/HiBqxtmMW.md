---
title: '关于C语言数组排序的一点想法'
date: 2019-11-16 09:59:16
tags: [C语言]
published: true
hideInList: false
feature: 
isTop: false
---
普遍的方法是先用for语句输入数组的值，再用for与for的嵌套语句实现历遍并排序，这一整套下来使用了三次for语句，特别是最后的两个让人头大。
```c
    for(i=0; i<10-1; i++){ 
        for(j=0; j<10-1-i; j++){
            if(nums[j] > nums[j+1]){
                temp = nums[j];
                nums[j] = nums[j+1];
                nums[j+1] = temp;}}}
```
我的想法是，不如在输入后立刻排序，减少了语句使用，而且更加直观。
```c
int a[20],i,j,temp;
    for(i=0;i<=19;i++){
        printf("请输入第%d个数:",i+1);
        scanf("%d",&a[i]);
        for(j=i;j>0;j--)
            if(a[j]<a[j-1]){temp=a[j];a[j]=a[j-1];a[j-1]=temp;}}
```
其实两者差别不大，结合第后一个方法很容易就把前一个看懂了。