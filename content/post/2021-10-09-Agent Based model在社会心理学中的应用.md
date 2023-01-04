---
title: Agent Based model在社会心理学中的应用
author: yuanbo
date: 2021-08-29
slug: mouse-tracking-learning-record
category:   
tags: 
draft: no


---

# Agent Based model在社会心理学中的应用



> 基于个体建模（Agent based modeling, ABM）是一种基于个体行为特征，考察由这种个体组成的群体（例如，社会），经过长时间的大量个体之间的相互作用而涌现出来的群体行为模式的计算方法。目前已经在计算社会科学中取得了广泛的应用。本讲座拟介绍ABM的基本原理，并通过ABM在社会现象研究中的例子，探讨ABM在法学理论与实际研究（包括立法前评估）中的可能应用。

https://www.machinegurning.com/rstats/gamelife/

> The goal of ABM is to search for explanatory insight into the collective behavior of agents obeying simple rules, typically in natural systems. There are many ways to get hooked on ABM, for me I found the Game of Life intriguing (there are many examples from [biological](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3640333/), [ecological](https://www.openabm.org/book/3138/12-interesting-example-bali) and [socioeconomical systems](http://www.sciencedirect.com/science/article/pii/S2095263512000167)).
>
> This blog post is interested in how from simple rules complexity can [emerge](https://en.wikipedia.org/wiki/Emergence).
>
> ABM 的目标是寻找对遵守简单规则的agents代理的集体行为（通常是在自然系统中）的解释性见解。有许多方法可以迷上ABM，对我来说，我发现生命游戏很有趣（有很多来自生物、生态和社会经济系统的例子）。
>
>  这篇博文对如何从简单的规则复杂性中产生感兴趣。

### Conway’s Game of Life

[Life](https://en.wikipedia.org/wiki/Conway's_Game_of_Life) (or the Game of Life) was introduced by the mathematician John Horton Conway in 1970. Though originally introduced to demonstrate interesting mathematical behaviour, we can consider it as a simple model for how cells interact. In this model time is discrete and represents generations. The cells lie on a rectangular grid. At each time step there are a set of rules that determine whether a cell lives or dies depending on the number of surrounding cells present. There is also the possibility that cells are `born’.生命（或生命游戏）是由数学家约翰·霍顿·康威在1970年介绍的。虽然最初是为了展示有趣的数学行为而引入的，但我们可以把它看作是细胞如何相互作用的简单模型。在这个模型时间是离散的，代表几代人。细胞位于矩形网格上。每次步骤都有一套规则，根据周围细胞的数量确定细胞是活还是死。细胞也有"出生"的可能性。

Before we proceed to give the rules of Life and a R implementation you should investigate it for yourself. The rules all depend on the eight nearest-neighbours of a cell.