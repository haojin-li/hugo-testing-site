---
title: 随机数基本使用方法
toc: true
tags: []
categories:
  - Learn
  - Competitive Programming
abbrlink: 64fb
date: 2019-01-15 00:46:25
thumbnail:
cover:
---

## 基本公式：

要取得[a,b)的随机整数，使用(rand() % (b-a))+ a;
要取得[a,b]的随机整数，使用(rand() % (b-a+1))+ a;
要取得(a,b]的随机整数，使用(rand() % (b-a))+ a + 1;
通用公式:a + rand() % n；其中的a是起始值，n是整数的范围。
要取得a到b之间的随机整数，另一种表示：a + (int)b * rand() / (RAND_MAX + 1)。
要取得0～1之间的浮点数，可以使用rand() / double(RAND_MAX)。