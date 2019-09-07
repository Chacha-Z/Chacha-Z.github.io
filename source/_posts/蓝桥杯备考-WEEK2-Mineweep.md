---
title: 蓝桥杯备考-WEEK2_Mineweep
date: 2019-03-10 11:06:13
tags:
categories:  
    - 蓝桥杯
description: 边界判断
---

### [问题描述]

<!-- more -->
    Have you ever played Minesweeper? It’s a cute little game which comes within a certain Operating

    System which name we can’t really remember. Well, the goal of the game is to find where are all the mines within a M × N field. To help you, the game shows a number in a square which tells you how many mines there are adjacent to that square. For instance, supose the following 4 × 4 field with 2 mines (which are represented by an ‘*’ character):

    *...

    ....

    .*..

    ....

    If we would represent the same field placing the hint numbers described above, we would end up

    with:

    *100

    2210

    1*10

    1110

    As you may have already noticed, each square may have at most 8 adjacent squares.



#### [输入]

    The input will consist of an arbitrary number of fields. The first line of each field contains two integers

    n and m (0 < n, m ≤ 100) which stands for the number of lines and columns of the field respectively.

    The next n lines contains exactly m characters and represent the field.

    Each safe square is represented by an ‘.’ character (without the quotes) and each mine square

    is represented by an ‘*’ character (also without the quotes). The first field line where n = m = 0

    represents the end of input and should not be processed.



#### [输出]

    对于每对整数 i 和 j，按原来的顺序输出 i 和 j，然后输出二者之间的整数中的最大循环节长度。这三个整数应该用单个空格隔开，且在同一行输出。对于读入的每一组数据，在输出中应位于单独的一行。



#### [样例输入]

    4 4

    *...

    ....

    .*..

    ....

    3 5

    **...

    .....

    .*...

    0 0



#### [样例输出]

    Field #1:

    *100

    2210

    1*10

    1110



    Field #2:

    **100

    33200

    1*100

    */

### 问题解决

1. 我的思路  
    为了不考虑边界问题,并且可以只判断"*"（真的是懒的，反而给自己增添了很多麻烦，绕得不行），使用了一个比目标数组大两行两列的整型数组，目的是为了可以刚好框下目标数组；这样可以只对*周围的空间进行处理（+1），存储对应计数。  
    BUT！比较绕的地方在于，目标数组[i, j], 对应的是计数数组的[i+1, j+1]

    ``` java
    int[][] decode = new int[n+2][m+2];
    for(int i = 0; i < n; ++i){
        for(int j = 0; j < m; ++j){
            
            if(field[i][j] == '*'){
                
                for(int k = 0; k <= 2; ++k){
                    for(int l = 0; l <= 2; ++l){
                        decode[i+k][j+l] += 1;
                    }
                }
            }
        }
    }
    
    for(int i = 0; i < n; ++i){
        for(int j = 0; j < m; ++j){
            if(field[i][j] == '*'){
                System.out.print('*');
            }else{
                System.out.print(decode[i+1][j+1]);
            }
        }
        System.out.println();
    }
    ```

2. 遍历数组，逐个处理
    对每一个元素，遍历其周围元素，计数有几个"*", 直接输出  
    关键：！！IF语句对边界进行判断就OK了！超过了边界不计数就完事儿了！不知道自己在想什么

    ``` java
    for(int i = 0; i < n; ++i){
        for(int j = 0; j < m; ++j){
            
            if(field[i][j] == '*'){
                System.out.print('*');
                continue;
            }
            
            int count = 0;
            for(int k = i-1; k <= i+1; ++k){
                for(int l = j-1; l <= j+i; ++l){
                    if(k >= 0 && k < n && l >= 0 && l < m && field[k][l] == '*'){
                        count++;
                    }
                }
            }
            System.out.print(count);
        }
        System.out.println();
    }
    ```