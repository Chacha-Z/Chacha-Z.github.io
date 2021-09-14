---
title: react修改state没有立即改变问题
date: 2020-07-02 08:12:23
categories:  
    - React
tags: 
    - React
    - BUG
comments: true
---

react 的 setState 是异步执行的

<!--more-->

> react 的 setState 是异步执行的，所以你后面立即 console 是还没改变状态， setState 函数接受两个参数，一个是一个对象，就是设置的状态，还有一个是一个回调函数，就是设置状态成功之后执行的
>
> 
>
> From <https://blog.csdn.net/z69183787/article/details/52277173>

 

 

善用官方文档，使用回调函数进行后续操作

 ```javascript
void setState( function|object nextState, [function callback] ... )
 ```

