---
title: 班机航路
description: 有关神秘班机航路的介绍及使用
slug: Airline Flight Route 
date: 2026-06-27 17:46:00+0800
image: cover.png
categories:
    - 游戏
tags:
    - 航路
    - 飞行
weight: 1

---

# 班机航路

班级航路是指由当地空中交通管理机构，向国内外航司发布的，可用于改地区飞行的航路。

## 国内段

由A机场到B机场，经由A机场的初始点（不一定是离场点），到达B机场的结束点（不一定是进场点）。

## 出入境段

由出入境点到A机场。

## 国际段

由入境点进入，再由出境点离开。

## rtecheck

[https://github.com/supermastergui/rtecheck](https://github.com/supermastergui/rtecheck)

公版航线数据 → MTEP Route Check 格式转换工具。

我写这个转换器的目的是为了便于虚拟航空航路一键导入，以下是算法解析：

`FLIGHT_AIRLINE.csv`中有全部的上述国内段、出入境段、国际段的航路。但是，这并不是一步到位的，需要首先将这个航路的识别码，放入`FLIGHT_AIRLINE_POINT.csv`找到。

然后，再按升序找到一个个点。然而，这些点通常是所有点，不是我们正常飞的航路。例如：`A W1 B W1 C`而不是`A W1 C`。因此，需要“去重”工作，这一步还是比较寻常的。

除此之外，如果飞一班有限制的航路，需要查询这段是不是有限制，进入`ROUTE_RESTRICT.csv`，看这个限制话语的影响识别码，然后再放入`ROUTE_RESTRICT_RTE.csv`，看有多少，再添加到`FLIGHT_AIRLINE.csv`识别码中的那些班机航路。高度限制是中`FLIGHT_AIRLINE.csv`进行添加。总而言之是非常的复杂。

你以为这一步就结束了吗？

**没有**

接下来还需要脱敏处理，将所有涉及NAIP的航路替换以及计算单双数高度层。

详情算法可见：[https://github.com/supermastergui/rtecheck#%E7%AE%97%E6%B3%95](https://github.com/supermastergui/rtecheck#%E7%AE%97%E6%B3%95)