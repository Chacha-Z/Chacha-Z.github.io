---
title: D3 brush 设置默认选中
date: 2020-07-05 14:45:23
categories:  
    - D3
tags: 
    - D3 Brush
comments: true
---

D3 brush 设置默认选中

<!--more-->

自动触发刷选事件，传入参数

```javascript
  //刷选工具

  var brushNode = $timeline.append('g').attr('class', 'brush')

​      .call(brush);

  //默认刷选

  const extent = [x2(new Date('2020-01-01')), x2(new Date('2020-01-25'))]

  d3.selectAll(".brush").call(brush.move, extent);
```





 

扩展：自动触发事件 despatch方法

> https://blog.csdn.net/yiifaa/article/details/52133516

```javascript
  var e = d3.selectAll('#mark0')

  e.dispatch('click')

\\ 元素上的数据会自动传入
```



