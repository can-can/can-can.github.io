---
layout: post
title: 什么是高可用、容错、容灾和灾难恢复？
categories: zh
category: zh
tag: 高可用 容错 容灾 灾难恢复

---

# 前言	
在讨论系统可用性时，常会涉及到“高可用”、“容灾”和“容错”几个概念。还有一个“灾难恢复”较少用到。

之前对这几个概念也知之甚少，为了交流方便，我在网上调研了这几个概念，并做了总结和理解。也发现了一些有意思的事情。


# 高可用（High Availability)
[高可用](https://en.wikipedia.org/wiki/High_availability)是指：
>一个系统的可用性高于通常水准。

一般会用[SLA](https://en.wikipedia.org/wiki/Service-level_agreement)来衡量。

高可用是一个宏观的概念，只要你的系统 uptime 够长，那么你的系统就可以称之为高可用系统。

容灾和容错都是为了达到高可用这个目标而做的方案。

在调研时，发现错误的使用方法有以下两种：
1. 将容灾和高可用做对比，但内容却是容灾和容错的对比。
2. 将高可用做为容灾的措施。
# 容错(Fault Tolerance)
[容错](https://en.wikipedia.org/wiki/Fault_tolerance)是指:
>即使出现错误，系统也能在不影响用户或者影响用户较小的情况下，提供操作的能力。

需要指出的是，容错是在系统的内部进行的。所以要做容错，需要划分好系统的边界。

# 容灾(Disaster Tolerance)和灾难恢复(Disaster Recovery)
这两个概念为什么放到一起呢？因为通过调研，我发现这两个概念是**等价**的。

我们先来看一下这两个概念。

[灾难恢复](https://en.wikipedia.org/wiki/Disaster_recovery)是指:
>一系列的原则、过程和工具，能使关键设施和系统在遭遇灾害后恢复。

灾难恢复有[等级划分](https://en.wikipedia.org/wiki/Seven_tiers_of_disaster_recovery)。

百度百科给出了容灾的定义，但英文没有的定义。

[容灾](https://baike.baidu.com/item/%E5%AE%B9%E7%81%BE)是指:
> 容灾系统是指在相隔较远的异地，建立两套或多套功能相同的IT系统，互相之间可以进行健康状态监视和功能切换，当一处系统因意外（如火灾、地震等）停止工作时，整个应用系统可以切换到另一处，使得该系统功能可以继续正常工作。

调研中，我发现使用“容灾”有以下情况：
1. 名词用“容灾”，内容讲的是“灾难恢复”。有的更是中文容“容灾”，英文用DR。
2. 就是上述百度百科中的描述。这种情况，相当于灾难恢复级别的[最高级别](https://en.wikipedia.org/wiki/Seven_tiers_of_disaster_recovery#Tier_7:_Highly_automated.2C_business_integrated_solution)的一个方案。

所以给出了它们是等价的结论。

我更倾向于使用“灾难恢复”，即使“容灾”更顺口。原因见下面的发现。
## 有意思的发现
Google “容灾”，有100万条结果。
Google “灾难恢复”， 有600万条结果。
Google “Disater Tolerance"，有66万条结果。
Google “Disater Recovery"，有3800万条结果。

## 容错和灾难恢复的区别
容错中的错误是发生在*系统内*。

灾难恢复中的灾难是发生在*系统外*。

# 结束
文章中没有给出调研材料的链接做为证据，以免产生误会。大家可以自行搜索。

