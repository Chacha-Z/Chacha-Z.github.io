---
title: LIS问题
date: 2019-03-10 15:27:35
tags:
    - DynamicProblem
    - GreedyAlgorithm
categories:  
    - 算法
description: 动态规划；O(n^2)和O(nlogn)
---

### LIS问题

    有一个长为n的数列a0, a1, ......, a(n-1)。请求出这个序列中最长的上升子序列的长度。上升子序列指的是对于任意的i< j都满足ai < aj的子序列

#### 例
    序列为（1，5 ，2，6，9，10，3，15），那么它的最长上升子序列为：（1，2，6，9，10，15）

### O(N^2)
    
#### 思路：DP
    dp[i] = max(1, dp[j]+1) 其中：i > j && ai > aj

``` java
public static int lis(int[] a){
    int max = Integer.MIN_VALUE;
    int[] maxSub = new int[a.length];
    
    for(int i = 0;  i< a.length; ++i){
        int curMaxSub = 1;
        for(int j = 0; j < i; ++j){
            if(a[i] > a[j] && curMaxSub < maxSub[j]+1){
                curMaxSub = maxSub[j]+1;
            }
        }
        maxSub[i] = curMaxSub;
        if(maxSub[i] > max){
            max = maxSub[i];
        }
    }
    
    return max;
}
```

### O(nlogn) 
#### 思路：  

+ 标记路径；
+ 贪心算法：使序列整体尽可能的小，以便加入更多的元素;  
    实现方式：维护一个标志路径数组，遍历原数组。如果当前元素大于标志数组中的最后一个，则加入标志数组后面；否则使用当前元素替换标志数组中，第一个大于当前元素的元素;  
    例如：{5, 3, 1, 2, 4, 7, 8, 6}的标志路径为{1, 2， 4， 6， 8}；但这**并不一定等于最长上升子序列**，实际的最长上升子序列应该是{1, 2, 4, 7, 8}, 该贪心算法仅仅是所求的的长度相同（为什么长度就一定相同？）
+ BUT：得到的序列是一个伪序列，里面的元素，并不是真正的最长上升子序列，而仅仅和最长上升子序列的个数一样。
+ 时间复杂度：因为查找的时候用的二分查找，所以时间复杂度为o（nlogn）

``` java
public static int getLis(int[] a){
    int[] dp = new int[a.length];
    int len = 0;
    
    dp[len++] = a[0];
    for(int i = 1; i < a.length; ++i){
        if(a[i] > dp[len-1]){
            dp[len++] = a[i];
        }else{
            int replaceIndex = getIndex(dp, len, a[i]);
            dp[replaceIndex] = a[i];
        }
    }
    System.out.println(Arrays.toString(dp));
    return len;
}

public static int getIndex(int[] arr, int n, int x){
    int low = 0;
    int high = n-1;
    int mid = (low + high)/2;
    while(low < high){
        if(arr[mid] > x){
            high = mid-1;
        }else if(arr[mid] < x){
            low = mid+1;
        }
        mid = (low + high)/2;
    }
    
    return low;
}
```
