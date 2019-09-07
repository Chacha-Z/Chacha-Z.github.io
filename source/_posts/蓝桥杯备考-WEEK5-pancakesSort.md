---
title: 蓝桥杯备考-WEEK5_pancakesSort
date: 2019-03-10 12:58:28
tags:
categories:  
    - 蓝桥杯
description: 这么简单为什么想不到呢！思路理清代码很简单；主要思路就是：找最大的，把最大的翻到最前面，再整个倒转将最大的翻到最后
---

### 关键：
    思路：找最大的，把最大的翻到最前面，再整个倒转将最大的翻到最后
    技巧：如果最大的已经在对应的最后面则不用翻转；如果最大的在第一个也可以省去第一步翻转

``` java
public static void pancakesSort(int[] p){
    
    for(int i = 0; i < p.length; ++i){
        int max_i = 0;
        
        for(int j = 0; j < p.length-i; ++j){
            
            if(p[j] > p[max_i]){
                max_i = j;
            }
        }
        if(max_i != p.length-i-1){
            if(max_i != 0){
                convertArr(p, 0, max_i);
                System.out.println(Arrays.toString(p));
            }
            convertArr(p, 0, p.length-1-i);
            System.out.println(Arrays.toString(p));
            System.out.println();
        }
    }
}

public static void convertArr(int[] p, int n, int m){
    
    if(n < 0 || m < 0 || n > p.length || m > p.length || m <= n){
        return ;
    }
    
    while(n < m){
        int temp = p[n];
        p[n] = p[m];
        p[m] = temp;
        n++;
        m--;
    }
    
}
```