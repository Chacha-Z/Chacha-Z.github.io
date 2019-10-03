---
title: '[V]AirVis-Visual Analytics of Air Pollution Propagation'
date: 2019-09-24 11:05:03
categories:  
    - 论文研读
tags: 
    - pattern mining
    - air pollution propagation
    - graph visualization
comments: true
---

**title**: AirVis: Visual Analytics of Air Pollution Propagation
**source**:  IEEE 2019: Geovisualization
**authors**:  Zikun Deng, Di Weng, Jiahui Chen, Ren Liu, Zhibin Wang, Jie Bao, Yu Zheng, Yingcai Wu
**summarize in 50 words**:  层次化的空气污染传播模式可视化
<!-- more -->

### 读论文的目的： 
现阶段阅读论文的目的还主要在于扩大自己的知识面、积累素材、学习论文写作

### WHAT
> 一个基于图形可视化的可视分析系统，用以帮助领域专家有效地捕捉和解释不确定的空气污染传播模式。

### WHY
- 空气污染已经成为一个全球性的问题；减轻空气污染的一个很重要的前提就是要清楚空气污染在大空间范围内的传播，以使专家能够确定污染的来源和发展模式
- 由于风的不确定因素，捕捉不确定污染传播过程极具挑战性；
- 目前最先进的HYSPLIT方法旨在自动推测污染物在大气中的扩散和对一个区域的影响，但HYSPLIT没有考虑动态传播模式内在的不确定性以及多个城市之前复杂的区域级相互作用，且缺乏在大空间区域内以overview到detail的形式呈现传播过程的交互工具；
- 模型驱动和数据驱动的空气污染分析，前者不能捕捉复杂的区域级相互作用、后者没有考虑多区域间传播的连续性，且二者都忽略了传播过程的不确定性，此外，只有很少的研究结合了交互式可视化。

### HOW
> 第一遍阅读有比较多的地方没看懂，之后阅读明白，认为理解的关键在于：明白系统意图，是为了分析传播模式，以便专家做出决策，而不是实时的观看传播情况。如此就能明白作者在做什么：

- 数据是非实时的、区域性的、长时间跨度的所有数据；
- 数据从下到上的计算过程：
   - 从数据中计算得到**传输实例（transportation instance）**；
   - 从传输实例根据连续性合成**传播实例（propagation instance）**
   - 在众多的传播实例中采用FSM方法找到频繁发生（可以这样说？）的即为**传播模式（propagation pattern）**
   - 使用MDL原则从众多的模式中抽取上下文无关的频繁拓扑结构**motif**(不是聚类，是对模式进行抽取，形成拓扑结构的motifs，1:n)
   - 对模式使用word2vec模型基于拓扑相似性聚类并使用t-SNE进行二维投影；
- 从用户使用角度理解即为反方向层次化（聚类框选-motif-pattern-inspect-instance）
![数据抽象过程](/数据抽象过程.png)


### 可视化设计
- **Motif**: 
    边使用梭形图元，梭形图元编码了概率分布的均值（透明度）和方差（宽度）（一个motif由多个patterns抽取而来），Motif的展示可根据这两者进行排序；
    （可选编码：使用热力图来编码边所对应的所有传播模式的该边传播概率）
- **Pattern gylphs**: 
    点代表区域，根据其地理空间的相对位置放置；
    传播模式上的区域和路径被高亮为橙色，其余为灰色；圆域边上的红色箭头指向传播的大致方向；
    鼠标悬停在上面会呈现鱼眼镜头效果；
    传播模式对应的多条传播实例的时间分布被描述为模式图外围的热力图，每一个热力小块代表一周，该周内该模式的传播实例越多颜色饱和度越高；
    为了避免误以为时间分布是一个圈，最上方热力图不连续。
- **Pattern praph**: 
    在地图上可视化一个传播模式的不确定传播过程；
    所有传输实例的每条路径有两个变量contribution和impact（百分数），在模式中两个变量的中位数被编码为红色和绿色的饼图；
    每一个地区以画在白色背景上的黄色实心圆表示，圆越大，对应区域污染物的浓度越高。
- **Projection view**: 
    模式的二维投影散点图，模式相似性越高投影后的距离越近，投影点的透明度代表对应模式所有区域污染物浓度的均值；
- **Instance visualization**: 
    选择一个传播模式，可查看其细节的传播实例；
    对应区域对应的所有传输实例以一对弦图的形式展现；
    每个区域以一段弧表示，随时间变化的污染物浓度以顺时针方向的柱形图高度和亮度编码，弦的宽度编码实例的impact；
    下方表格展示传输实例的原始数据；

![系统视图](/系统视图.png)


### 阅读过程中的困惑（通过反复阅读解开）：
- **为什么说是graph visualization?** 
    visualizing a large number of graphs（针对pattern而言）
- **什么是uncertainty-aware visualization?** 
    针对传输实例对应的传输概率，也即传输浓度。将传播概率可视化出来？详见motifs的可视化设计。
- **compact设计?** 
    对应the scalability of pattern visualization，在一张图中不止展示传播路径，使用恰当的编码同时展示传播时间、概率等。
- **层次化视觉设计体现在?** 
    'associating the abstract patterns with physical instances'
- **topology analysis?**
    对应motif设计
    
    

### 方法总结：
- **FSM**： is particularly effective in extracting frequent subgraphs that represent typical propagation patterns；从多个传播实例到一个传播模式。·
- **MDL**：通过为相似数据元素创建总结展示来压缩数据（minimum description length (MDL) principle：compresses data by creating summary representations for similar data items）；为多个模式抽取拓扑抽象。
- **word2vec**：词袋模型
- **t-SNE**：二维投影方式
- **motif**: 拓扑图元

### 启发：
- 在related work一节中体会到：
    参考文献的意义在这一节体现尤其明显，调查的方向和方法（关于其是什么、为什么、做了什么等）都要有相关的参考文献来佐证，比如在讲图像可视化的时候，提到了两个方向，并分别都有对应的文献引用（大于一篇）；又比如在讲动态图像可视化时，尽管是概括性的提到一句“使用多种方法来组织图形”，都会在括号里列出各种方法及其参考文献；又或者是类似于“PM2.5对人体和环境都有很大的伤害”这样的论述，都能找到相关的文献引用。（可见论文的编写需要有足够的阅读量和清晰的逻辑思维，所以一定要形成自己的总结和概括，一方面是方便回顾，而一方面是在于能够总结出来才是真正读懂了）

- 作者一直强调“模式”：
    其中一句很重要的解释的话为“ Compared with the individual propagation instance that maybe arandom and unrepresentative event,these patterns strongly indicate the latent pathways of pollution propagation. ”，即，模式可以用于不确定性数据的可视化，以概括和抽象的方法揭示事务潜在的规律。

- 从overview到detail的层次化数据可视化方式。

- 设计备选可视化方案。


### 遗留问题： 
对相关工作里提到的模型驱动和数据驱动的理解还是很模糊，不知道他们具体是怎么个表现形式，能够怎么被使用，模型是什么模型、数据是什么数据，为什么为称作模型和数据驱动。



