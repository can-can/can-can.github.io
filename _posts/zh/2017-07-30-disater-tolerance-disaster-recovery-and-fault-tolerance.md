---
layout: post
title: 对容灾、容错的理解
categories: zh
category: zh
tag: 容灾 容错 灾难恢复 高可用

---

## 背景
最近在考虑提高可用性的事情。团队使用的名次是”容灾“这个词。但是还有一些类似的概念比较混淆，如容错，高可用，灾难恢复。我决定先确定这些名词的概念，再去讨论可用性的问题。

## 概念解析
一下内容作为个人的理解，作为之后其他人讨论问题时术语的定义。
### 高可用（High Availability)
[高可用](https://en.wikipedia.org/wiki/High_availability)是指：
>一个系统的可用性高于通常水准。

一般会用[SLA](https://en.wikipedia.org/wiki/Service-level_agreement)来衡量。

### 容错(Fault Tolerance)
#### 概念
[容错](https://en.wikipedia.org/wiki/Fault_tolerance)是指:
>即使出现错误，系统也能在不影响用户或者影响用户较小的情况下，提供操作的能力。

需要指出的是，容错是在系统的内部进行的。所以要做容错，需要划分好系统的边界。
另外，在容错的概念中系统的所有组件都在提供服务。
#### 例子
最简单的一个例子集群。首先集群中的服务器都在提供服务，当集群中的某一台服务器挂掉时，并不会影响集群对外提供服务。

### 容灾(Disaster Tolerance)和灾难恢复(Disaster Recovery)
#### 概念
[容灾](https://baike.baidu.com/item/%E5%AE%B9%E7%81%BE)是指:
> 容灾系统是指在相隔较远的异地，建立两套或多套功能相同的IT系统，互相之间可以进行健康状态监视和功能切换，当一处系统因意外（如火灾、地震等）停止工作时，整个应用系统可以切换到另一处，使得该系统功能可以继续正常工作。

在英文文章中，Disaster Tolerance 没有找到统一的描述。有一些文章在说自己系统是“Disaster Tolerant Architecture”[1] [2]。大概意思是两个集群，primary提供服务，second做备份，不提供服务。当primary挂了，就自动跳到second集群。

[灾难恢复](https://en.wikipedia.org/wiki/Disaster_recovery)是指:
>一系列的原则、过程和工具，能使关键设施和系统在遭遇灾害后恢复。

这两个概念的共同点都是“整个系统”挂了以后，可以恢复。这也是它们和容错的一个区别。

#### 它们是一个概念吗？
从概念上看，灾难恢复更宏观一些，而容灾更具体一些。
根据灾难恢复的[等级划分](https://en.wikipedia.org/wiki/Seven_tiers_of_disaster_recovery)可以看出，容灾概念的表现正好符合最高等级的描述。
那么我理解为，容灾是灾难恢复的一个具体的高级别的实践。

[1] http://docs.oracle.com/cd/E19528-01/819-0420/introduction-7/index.html

[2] https://docstore.mik.ua/manuals/hp-ux/en/T1906-90022/ch01s02.html

