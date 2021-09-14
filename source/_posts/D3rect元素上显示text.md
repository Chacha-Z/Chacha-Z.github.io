---
title: D3在rect元素上显示text
date: 2020-06-14 15:12:23
categories:  
    - D3
tags: 
    - D3
comments: true
---



不能直接使用rect包围text，否则设置无效

<!--more-->

  ```html
// 比较优雅的作法是，把rect标签和text标签用一个g标签包裹，并列在一起，并调节text标签的dy属性，使其居中
<g>
    <rect></rect>
	<text dy='1em'>text</text>
</g>
  ```



```javascript
const legendtext = [{label:'分数', color: colour(0)}, {label:'平均分', color: colour(1)}, {label:'最高/低分', color: 'grey'}];
//添加颜色标签
const legend = $plot.append('g')
       .attr('class', 'line-legend')
       .attr("font-family", "sans-serif")
       .attr("font-size", 10)
       .attr('text-anchor', 'end')
       .selectAll("g")
       .data(legendtext)
       .enter().append("g")
       .attr("transform", (d, i) => `translate(${w+15}, ${i*20 +h/2})`);
legend.append('rect')
       .attr('width', 10)
       .attr('height', 10)
       .attr('opacity', .7)
       .attr('fill', (d, i) => d.color)
       .attr('rx', 2);
legend.append('text')
      .attr('x', 10)
      .attr('dx', '0.325em')
      .attr('y', 10)
      .attr('dy', '-0.2em')
      .attr('text-anchor', 'start')
      .text(d => d.label)
```

