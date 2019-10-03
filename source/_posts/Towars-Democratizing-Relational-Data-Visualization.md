---
title: Towards Democratizing Relational Data Visualization
date: 2019-09-14 17:01:26
categories:  
    - 论文研读
tags: 
    - relational data
    - smart data visualization
    - data visualization
    - toturial
comments: true
---

**title**: Towars Democratizing Relational Data Visualization  
**source**:  SIGMOD 2019: Accepted Tutorials
**authors**:  Nan Tang (Qatar Computing Rsearch Insitute); Eugene Wu (Columbia University); Guoliang Li (Tsinghua University)
**summarize in 50 words**:  详解了关系型数据可视化的结构栈（定义、分类以及所涉及实现），是一篇指导性文章，建议结合引文理解
<!-- more -->

# 摘要之三大主题  
+ visualization languages(可视化语言)  
> *how users can interact with various visualization*  

+ efficient data visualization(高效的数据可视化)  
> *processes the data and produces visualizations base on well-specified user queries*  

+ smart data visualization(智慧的数据可视化)  
> *recommends data visualizations based on underspecified user queries*  

<i class="icon-weibo"></i>

# 关键词  
+ relational data(关系型数据)  
+ data visualization(数据可视化)  

# 介绍
> ## POINT  
* Compelling -> Nowadays -> Consequently -> However(行文思路)  
* the purpose of this tutorial is to provide an overview of where we are from the DB perspective(本文的目的)  
* formalism  
* architectural tack for relational data visualization(关系型数据可视化的结构栈)  

> ## architectural tack 详解 (自底向上)  
+ ### Data Storage  
    *describes the data storage layer containing the relational data D*  
    + DBMS\Cloud stroage\Flat files  
    + large (maybe) -> tables\wide\volumes  
    + multiple source (Most commercial visualization systems)  
    + mainly DBMSs (Most research prototypes)  
    + won't discuss storage technical details, but three visualization-specific components  
+ ### Efficient Data Visualization    
    *to quickly generate visualizations V when the specifications S is well-specified*  
    + no ambiguity  
    + responsiveness and scalability (if F can be evaluated in real time)  
    + relax the semantics to return approximatie and progressive results (when cannot)  
+ ### Smart Data Visualization  
    *when the user underspecifies S, the system must first 'smartly' complete the specification in a way that anticipates the user's intentions, before it can render a visualization*  
    + analogous to keyword search  
    + automatic\reference visualization based\user behavior based\personalized...  
+ ### Visualization Language   
    *the mechanism that users express their visualization goals*   
    + precise enough  
    + textually\interactively  

> ## Open Problems  
+ big data challenges  
+ dirt data  
+ deep data visualization  
+ benchmark  
...  

# 受众和篇幅  
+ researchers/practitioners/students  
+ non-specialists (broad introduction/motivating examples)  
+ data mining and machine learning communities  

+ 3h

# 指南大纲  
+ ## Data Visualization Languages  
    + well-specified languages  
        + Procedural language  
            *Graphics Libraries, such as OpenGL/DirectX/Qt/Java2D/HTML Canvas...*  
            **
        + Declarative language  
            + low-level  
                *abstract graphical elements, such as D3/Vega/Reactive Vega*  
            + high-level  
                *further abstract the details of low-level visualization construction (with defaults), such as ggplot2/Vega-Lite*  
        + Visual language   
            *visual interface. such as Excel/Tableau/Apple Numbers/Amazon Redash...*  
    + Underspecified Languages  
        *hints*
        + reference-based  
            *such as zenvisage/Draco/Voyager/...*
        + keyword-based  
            *such as VizDeck/Deep-Eye*  

+ ## Efficient Data Visualization  
    *four important classes od techniques*
    + Exact data visualization  
        *based on ---*
        + Apply existing systems and technique
            *issue SQL queries/use hardware/parallel processing/data structures to accelerate vis*
        + Modify DMBS designs  
        + Predictive data visualization  
    + Approximate data visualization  
        *trade-off responsiveness and accuracy* 
    + Progressive data visualization  
        *provide an overview*


+ ## Smart Data Visualization  
    + difficulties of specifing S -> nowdays -> its pratical need
    + hardest part: guess what uers want
    + similarity-based -> behavior-based ->deviation-based -> personalized -> prediction-based

# 总结和开放性问题  
+ Interactivity under massive data volumes
+ Dirty data
    *后果（mislead） -> 例子(duplicates) -> 并且（清洗的代价） -> 因此 -> 方法*
+ Deep learning 
    *smart data vis -> domains -> recommend data vis*
+ Data Visualization Benchmarks
    *for performance and recommendation*

