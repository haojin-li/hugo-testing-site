---
title: 三角形牧场
toc: true
categories:
  - Learn
  - Competitive Programming
abbrlink: 90cd
tags: []
date: 2019-01-05 00:45:59
thumbnail:
cover:
---

# [P1284三角形牧场](https://www.luogu.org/problemnew/show/P1284)

------

## 题意

> 现在有n段木棍，全部使用组成三角形的三条边，使三角形的面积最大

## 分析

- 首先看**数据范围**，边长最大为`40*40/3`，并且因为要使用所有的木棍，所以只要两条边确定就可以知道第三条边的确定长度。因此我们可以设状态`f[i][j]`表示三角形的两条边分别是i，j的情况是否成立

- f[i][j]=f[i−a[k]][j] || f[i][j−a[k]] || f[i][j]f[i][j]=f[i−a[k]][j] || f[i][j−a[k]] || f[i][j]，相当于01背包，就不解释了……

- 定义初始状态f[0][0]=1f[0][0]=1

- 三条边都知道了，如何求面积呢？这里我们需要用到海伦公式

  S=√p(p−a)(p−b)(p−c)S=p(p−a)(p−b)(p−c)，p=12(a+b+c)p=12(a+b+c)

## 遇到的坑

~~好像没有什么~~



# [P1929 迷之阶梯](https://www.luogu.org/problemnew/show/P1929)

*~~真的好坑，做了一下午……~~*

## 题意

> 登上阶梯必须要按照它要求的方法， 否则就无法登上阶梯。它要求的方法有以下三个限制：
>
> 1. 如果下一步阶梯的高度只比当前阶梯高 1，则可以直接登上。
> 2. 除了第一步阶梯外，都可以从当前阶梯退到前一步阶梯。
> 3. 当你连续退下 k 后，你可以一次跳上不超过当前阶梯高度 2^{k}2k的阶梯。比如说你现 在位于第 j 步阶梯，并且是从第 j+k 步阶梯退下来的，那么你可以跳到高度不超过当前阶 梯高度+2^{k}2k的任何一步阶梯。跳跃这一次只算一次移动。
>
> 开始时我们在第一步阶梯，由于时间紧迫，我们需要用最少的移动次数登上迷之阶梯。 请你计算出最少的移动步数。

## 分析

- 定义状态为f[i]表示到第i个阶梯的最小步数
- 由2可以直接得出`if(h[i]==h[i-1]+1) f[i]=f[i-1]+1`

## 遇到的坑

- `if(f[n]>=0x3f3f3f3f) f[n]=-1;`在状态转移的过程中有可能比初始值更大，所以是**大于等于**