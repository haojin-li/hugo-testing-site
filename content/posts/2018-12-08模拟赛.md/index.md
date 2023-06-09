---
title: 2018/12/8模拟赛
toc: true
categories:
  - Learn
  - Competitive Programming
abbrlink: 84eb
tags: []
date: 2018-12-08 00:04:31
thumbnail:
cover:
---

~~终于有一次能在考场上打出正解的模拟赛~~

## 连线游戏

### 题目

> 连线游戏（lines.cpp）
> 文件输入输出
> 时间限制：1s
> 空间限制：256M
>
> 【题目描述】
> Farmer John最近发明了一个游戏，来考验自命不凡的贝茜。游戏开始的时候，FJ会给贝茜一块画着N (2 <= N <= 200)个不重合的点的木板，其中第i个点的横、纵坐标分别为X_i和Y_i (-1,000 <= X_i <=1,000； -1,000 <= Y_i <= 1,000)。
> 贝茜可以选两个点画一条过它们的直线，当且仅当平面上不存在与画出直线平行的直线。游戏结束时贝茜的得分，就是她画出的直线的总条数。为了在游戏中胜出，贝茜找到了你，希望你帮她计算一下最大可能得分。



> 【输入格式】
> 第1行: 输入1个正整数：N
> 第2..N+1行: 第i+1行用2个用空格隔开的整数X_i、Y_i，描述了点i的坐标
>
> 【输入样例】(lines.in):
> 4
> -1 1
> -2 0
> 0 0
> 1 1
>
> 【输出格式】
> 第1行: 输出1个整数，表示贝茜的最大得分，即她能画出的互不平行的直线数
>
> 【输出样例】 (lines.out):
> 4
>
> 【输出说明】
>
> 贝茜能画出以下4种斜率的直线：-1，0，1/3以及1。

### 思路

- 枚举两两构成直线的k值，如果k值不存在，则`ans++`。

### 遇到的坑

- 要**考虑精度问题**，考试的时候写了`1e-5`，结果炸了，改成`1e-7`就对了，甚至不加精度判断都能AC
- 特判**分母为0的情况**，本来以为`Inf`是无限大，所有`Inf`表示的都是一个意思，但实际炸了……
  \###AC代码

```
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <cstring>
using namespace std;

const int N=210;
int x[N],y[N],n;
double ans[N*N];

int main()
{	
	freopen("lines.in","r",stdin);
	freopen("lines.out","w",stdout);
	
	scanf("%d",&n);
	for(int i=1;i<=n;i++)
		scanf("%d%d",&x[i],&y[i]);
	
	int cnt=0;
	for(int i=1;i<=n;i++)
	for(int j=i+1;j<=n;j++)
	{
		double sta;
		if(x[i]-x[j]==0) sta=0x3f3f3f3f;
		else sta=1.0*(y[i]-y[j])/(x[i]-x[j]);
		
		bool flag=1;
		for(int k=1;k<=cnt;k++)
		{
			if(ans[k]-sta<=1e-10 && ans[k]-sta>=-1e-10)
			{
				flag=0;
				break;	
			} 
		}
		if(flag) ans[++cnt]=sta;//printf("%lf\n",sta);
	}
	printf("%d\n",cnt);
	return 0; 
}
```

------

## 独木桥

### 题目

> 【问题描述】
> 战争已经进入到紧要时刻。你是运输小队长，正在率领运输部队向前线运送物资。运输任务像做题一样无聊。你希望找些刺激，于是命令你的士兵们到前方的一座独木桥上欣赏风景，而你留在桥下欣赏士兵们。士兵们十分愤怒，因为这座独木桥十分狭窄，只能容纳一个人通过。假如有两个人相向而行在桥上相遇，那么他们两人将无法绕过对方，只能由一个人回头下桥，让另一个人先通过。但是，可以有多个人同时呆在同一个位置。
> 突然，你收到从指挥部发来的信息，敌军的轰炸机正朝着你所在的独木桥飞来！为了安全，你的部队必须撤下独木桥。独木桥的长度为L，士兵们只能呆在坐标为整数的位置，所有士兵的速度都为1，当一个士兵某一时刻来到了坐标为0或L+1的位置时，他就离开了独木桥。
> 每个士兵都有一个初始面对的方向，他们会以匀速朝着这个方向行走，中途不会自己改变方向。但是，如果两个士兵面对面相遇，他们无法彼此通过对方，于是就分别转身，继续行走。转身不需要任何时间。
> 由于先前的愤怒，你已不能控制你的士兵。甚至，你连每个士兵初始面对的方向都不知道。因此，你想要知道你的部队最少需要多少时间就可能全部撤离独木桥。另外，总部也在安排阻拦敌人的进攻，因此你还需要知道你的部队最多需要多少时间才能全部撤离独木桥。
>
> 【输入文件】
> 第一行：一个整数L，表示独木桥的长度。桥上的坐标为1..L
> 第二行：一个整数N，表示初始时留在桥上士兵的数目。
> 第三行：有N个整数，分别表示每个士兵的初始坐标。初始时，没有两个士兵在同一坐标。
>
> 【输出文件】只有一行，输出两个整数，分别表示部队撤离独木桥的最小时间和最大时间。两个整数用一个空格分开。
>
> 【样例输入】
> 4
> 2
> 1 3
>
> 【样例输出】
> 2 4
>
> 【数据规模及约定】
> N≤L≤1000

### 思路

`两个人遇见并分别掉头`与`两个人继续往前走`是等价的，因为人与人之间不存在差异。

每个士兵只有两种选择，`向左`或`向右`

最大值就是**每个士兵的最长选择的集合中的最大值**

最小值就是**每个士兵的最短选择的集合中的最大值**

### 遇到的坑

- 最外一层都是max，满足木桶原理

### AC代码

```
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <cstring>
using namespace std;

int l,n,ans1,ans2;//max,min

int main()
{
	freopen("bridge.in","r",stdin);
	freopen("bridge.out","w",stdout);
	
	scanf("%d%d",&l,&n);
	while(n--)
	{
		int x;
		scanf("%d",&x);
		ans1=max(ans1,min(x,l-x+1));//min
		ans2=max(ans2,max(x,l-x+1));//max
	}
	printf("%d %d\n",ans1,ans2);
	return 0;
}
```

------

## 俄罗斯方块

最水的一道题，直接模拟，分七种情况，细心一点就好了

### AC代码

```C++
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <cstring>
using namespace std;

const int N=110;
int mp[N],c,p,ans;

int main()
{
	freopen("game.in","r",stdin);
	freopen("game.out","w",stdout);
	
	scanf("%d%d",&c,&p);
	for(int i=1;i<=c;i++)
		scanf("%d",&mp[i]);

	if(p==1)
	{
		for(int i=1;i<=c-3;i++)
			if(mp[i]==mp[i+1] && mp[i+1]==mp[i+2] && mp[i+2]==mp[i+3]) ans++;
		printf("%d\n",c+ans);
		return 0;
	}
	if(p==2)
	{
		for(int i=1;i<=c-1;i++)
			if(mp[i]==mp[i+1]) ans++;
		printf("%d\n",ans);
		return 0;
	}
	if(p==3)
	{
		for(int i=1;i<=c-2;i++)
			if(mp[i]==mp[i+1] && mp[i+1]==mp[i+2]-1) ans++;
		for(int i=1;i<=c-1;i++)
			if(mp[i]==mp[i+1]+1) ans++;
		printf("%d\n",ans);
		return 0;
	}
	if(p==4)
	{
		for(int i=1;i<=c-2;i++)
			if(mp[i]==mp[i+1]+1 && mp[i+1]==mp[i+2]) ans++;
		for(int i=1;i<=c-1;i++)
			if(mp[i]==mp[i+1]-1) ans++;
		printf("%d\n",ans);
		return 0;
	}
	if(p==5)
	{
		for(int i=1;i<=c-2;i++)
			if(mp[i]==mp[i+1] && mp[i+1]==mp[i+2]) ans++;
		for(int i=1;i<=c-1;i++)
			if(mp[i]==mp[i+1]-1) ans++;
		for(int i=1;i<=c-1;i++)
			if(mp[i]==mp[i+1]+1) ans++;
		for(int i=1;i<=c-2;i++)
			if(mp[i]==mp[i+1]+1 && mp[i]==mp[i+2]) ans++;
		printf("%d\n",ans);
		return 0;
	}
	if(p==6)
	{
		for(int i=1;i<=c-2;i++)
			if(mp[i]==mp[i+1] && mp[i+1]==mp[i+2]) ans++;
		for(int i=1;i<=c-1;i++)
			if(mp[i]==mp[i+1]) ans++; 
		for(int i=1;i<=c-2;i++)
			if(mp[i]==mp[i+1]-1 && mp[i+1]==mp[i+2]) ans++;
		for(int i=1;i<=c-1;i++)
			if(mp[i]==mp[i+1]+2) ans++; 
		printf("%d\n",ans);
		return 0;
	}
	if(p==7)
	{
		for(int i=1;i<=c-2;i++)
			if(mp[i]==mp[i+1] && mp[i+1]==mp[i+2]) ans++;
		for(int i=1;i<=c-1;i++)
			if(mp[i]==mp[i+1]) ans++; 
		for(int i=1;i<=c-2;i++)
			if(mp[i]==mp[i+1] && mp[i+1]==mp[i+2]+1) ans++;
		for(int i=1;i<=c-1;i++)
			if(mp[i]==mp[i+1]-2) ans++; 
		printf("%d\n",ans);
		return 0;
	}
	return 0;
}

/*
5 7
2 0 3 1 2
*/
```