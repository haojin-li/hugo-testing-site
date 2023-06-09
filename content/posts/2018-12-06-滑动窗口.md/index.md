---
title: 滑动窗口
toc: true
categories:
  - Learn
  - Competitive Programming
abbrlink: ecef
tags: []
date: 2018-12-06 00:03:54
thumbnail:
cover:
---

## 思路：单调队列

### 以求最小值为例

- 在读取每一个数 `ai` 的过程中，判断队尾的数是否大于`ai`,如果大于则证明队尾的数已经没有意义了，因为***它已经不可能成为现在及以后所有窗口内的最小值\***，不妨弹出，重复以上操作，直到`ai`小于队尾的数，再把`ai`放到队尾
- 当现在的长度已经达到窗口的长度时，每一次都会输出最小值，因为队列是单调递减的，第一个数一定是现在窗口内最小的数，直接输出
- 在队尾添加的过程中，***要始终保证队列里的数都在窗口内\***，当区间长度大于窗口长度时，要从队首弹出

------

## 自己遇到的坑

- ***队列内存储的是这个数的位置，不是这个数的大小\***，大小通过数组类似映射表示

- ***要考虑好整个过程的先后顺序\***

  > 1. 先确保队列内的数都在范围内
  > 2. 把所有比`ai`小的队尾数依次弹出
  > 3. 将`ai`入队
  > 4. 如果达到滑动窗口范围，输出值

- ***两个数的编号相减加1代表该闭区间的长度\***

- 当算完最小值时队列不一定是空的，要先清空队列

------

## C++ STL 双端队列 deque

`q.push_back`: 从后端加入 `q.pop_back`: 从后端弹出
从前端就是`front`
`q.clear`: 清空队列
`q.size()`: 读取队列的长度，但是好像类型不是`int`，只能用来判断数组是否为空

------

## AC代码

```C++
#include <iostream>
#include <cstdio>
#include <queue>
using namespace std;

const int N=1e6+5;
int a[N];
deque<int> q;

int main()
{
    int n,k;
    scanf("%d%d",&n,&k);
    for(int i=1;i<=n;i++)
        scanf("%d",&a[i]);
    
//	q.push_back(1);
    //minn
    for(int i=1;i<=n;i++)
    {
        if(q.size() && i-k>=q.front()) q.pop_front();
        while(q.size() && a[i]<=a[q.back()]) q.pop_back();
        q.push_back(i);
        if(i>=k) printf("%d ",a[q.front()]);
    }
    
//	return 0;
    printf("\n");
    q.clear();
//	q.push_back(1);
    //maxn
    for(int i=1;i<=n;i++)
    {
        if(q.size() && i-k>=q.front()) q.pop_front();
        while(q.size() && a[i]>=a[q.back()]) q.pop_back();
        q.push_back(i);
        if(i>=k) printf("%d ",a[q.front()]);
    }
    
    return 0;
}
```