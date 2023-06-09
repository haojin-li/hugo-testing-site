---
title: Markdown 入门指南
toc: true
tags: []
categories:
  - Learn
  - Hacks
thumbnail: http://ww1.sinaimg.cn/large/bea775ably1g44dxxt7qvj21ky11yk1i.jpg
cover: http://ww1.sinaimg.cn/large/bea775ably1g44dxxt7qvj21ky11yk1i.jpg
abbrlink: deb1
date: 2019-06-18 00:52:45
---

# 什么是Markdown？

`Markdown` 是一种轻量级标记语言，通过一些简单的符号来表示多级标题、引用等不同属性的文本。对于一般的写作者，我们可以把`Markdown`理解为word的简约替代方案。

# Markdown的优点

- 专注于文本本身，不需要考虑文本的样式
- 逻辑条理清晰，自动生成文本大纲,本文左侧的大纲就是自动生成的，点击题目可以自动跳转
- 通用性
- 个性化外观和样式

# 基本语法介绍

## 多级标题

------

在`Markdown`中，‘#’代表标题，只需要在标题前加‘#’就可以了。几个‘#’就代表是第几级标题

***注意‘#’和文字之间要有一个空格\***

### Example

```
# 一级标题
## 二级标题
### 三级标题
……
```

### 效果

> # 一级标题
>
> ## 二级标题
>
> ### 三级标题

## 引用

------

有时候会需要引用一些内容，这个时候我们可以使用`>`表示引用

### Example

```
> 此处为引用
```

### 效果

> 此处为引用

## 代码块

------

有时候会有大量的代码，这个时候使用代码块表示非常方便

### Example

```
`单行代码`
​```C++(此处为代码的语言，可以辅助高亮)
#include <iostream>
using namespace std;
int main()
{
	cout<<"Hello World!"<<endl;
	return 0;
}
```

### 效果

‘单行代码’

```
#include <iostream>
using namespace std;
int main()
{
	cout<<"Hello World!"<<endl;
	return 0;
}
```

## 加粗 & 斜体

------

### Example

```
*斜体*
**加粗**
***加粗斜体***
```

### 效果

> *斜体*
> **加粗**
> ***加粗斜体\***

## 列项

------

### Example

```
1. 一
2. 二
3. 三

- 一
- 二
- 三
```

### 效果

> 1. 一
> 2. 二
> 3. 三
>
> - 一
> - 二
> - 三

## 分割线

------

### Example

```
上

---

下
```

### 效果

上

------

下

# 软件支持

‘Markdown’相当是一种语言，当然有很多不同的软件都支持该格式。我个人推荐[Typora](https://typora.io/),非常美观的一款‘Markdown’软件

***欢迎进入Markdown的奇妙世界……\***

***持续更新中……\***