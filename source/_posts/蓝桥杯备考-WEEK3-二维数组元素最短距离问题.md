---
title: 蓝桥杯备考-WEEK3_二维数组元素最短距离问题
date: 2019-03-10 11:27:00
tags:
categories:  
    - 蓝桥杯
description: 找规律；两个数做减法时，考虑大小；Math.abs(a);
---

### [问题描述]

 X星球居民小区的楼房全是一样的，并且按矩阵样式排列。其楼房的编号为1,2,3...

 当排满一行时，从下一行相邻的楼往反方向排号。

 比如：当小区排号宽度为6时，开始情形如下：



 1  2  3  4  5  6

 12 11 10 9  8  7

 13 14 15 .....



 我们的问题是：已知了两个楼号m和n，需要求出它们之间的最短移动距离（不能斜线方向移动）

 输入为3个整数w m n，空格分开，都在1到10000范围内

 要求输出一个整数，表示m n 两楼间最短移动距离。



#### [样例输入]

 6 8 2

##### [样例输出]

 4



#### [样例输入]

 4 7 20

##### [样例输出]

 5

 */


### 问题解决

``` java
public static int[] getIndex(int w, int n){
    int i = 0, j = 0;

    if(n%w == 0){
        i = n/w;
        
        if(i%2 == 0){
            j = 0;
        }else{
            j = w-1;
        }
    }else{
        i = n/w + 1;
        
        if(i%2 == 0){
            j = w - n%w;
        }else{
            j = n%w - 1;
        }
    }

    int[] result = {i-1, j};
    return result;
}

System.out.println(Math.abs(index_m[0] - index_n[0]) + Math.abs(index_m[1] - index_n[1]));
```

