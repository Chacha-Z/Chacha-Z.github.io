---
title: 机器学习实战-KNN
date: 2019-10-15 10:25:03
categories:  
    - 机器学习
tags: 
    - KNN
    - 《机器学习实战》
comments: true
---

# 函数总结
<!--more-->

**shape：numpy函数**

- shape(eye(3)) -> (3, 3)
- shape([1,2,3,4])  -> (4,) 
- shape(7) -> ()
OR
- a.shape -> a.shape[0] / a.shape[1]

**np.tile(A, reps)**
- 将原矩阵横向、纵向地复制。tile 是瓷砖的意思，顾名思义，这个函数就是把数组像瓷砖一样铺展开来。
- reps: d or (d1, d2)
**np.zeros(shape, dtype=float, order='C')**
- 返回来一个给定形状和类型的用0填充的数组

**dict.get(key[,default=None])**
- 返回指定的键值，如果指定的键值不存在时则返回defaul指定的默认值

**numpy中axis = 0/1**
- axis=1 按行
- axis=0 按列

