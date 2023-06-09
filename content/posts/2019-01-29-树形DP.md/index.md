---
title: 树形DP
toc: true
categories:
  - Learn
  - Competitive Programming
abbrlink: 8dc9
tags: []
date: 2019-01-29 00:48:22
thumbnail:
cover:
---

## 二叉苹果树

------

### 思路

- $dp[u][j表示节点u留下j条边的最大价值，每一次决策只有三种情况：剪左子树，剪右子树，两个都不剪
- 剪左边：dp[u][j]=dp[rson][j−1]+v[rson]dp[u][j]=dp[rson][j−1]+v[rson]，同理，剪右边：dp[u][j]=dp[lson][j−1]+v[lson]dp[u][j]=dp[lson][j−1]+v[lson]
- 两边都不剪：dp[u][j]=dp[lson][j]+dp[rson][k−j−2]dp[u][j]=dp[lson][j]+dp[rson][k−j−2]

## 代码：记忆化搜索

```C++
int f[N][N];
bool t[N][N];
int dp(int u,int k)
{
    if(t[u][k]) return f[u][k];
	t[u][k]=1;
    if(!k) return f[u][k]=0;
    int tmp1=dp(lson[u],k-1)+v[sonl[u]];
    int tmp2=dp(rson[u],k-1)+v[sonr[u]];
    int tmp3=0;
    for(int l=0;l<k-2;l++)
        tmp3=max(tmp3,dp(lson[u],l)+dp(rson[u],k-l-2));
   	return f[u][k]=max(tmp1,max(tmp2,tmp3+lson[u]+rson[u]));
}
```



## 先修课

------

### 题目

> 课的先修关系形成一棵树的结构，每门课有一门或者没有先修课。选M门课，能获得的最大学分是多少？

### 思路

- dp[u][j]dp[u][j]以u为根的子树选j门课
- 把j-1门课分配给子树，就是一个背包？
- 然后我们用f[i][j]f[i][j]表示当前树中，前i棵子树选择j门课的最大学分。这样就能够通过f算出dp[i][j]dp[i][j],相当于树上DP套背包。**对于每一个状态dp[i][j]dp[i][j]都需要用f算出学分分配的最佳方案**

## K-set

------

### 题目

> 在一棵树中选出最多的点，使得这些点中每个点最多与其他点连了k条边

### 思路

- dp[u][0/1][0/1]dp[u][0/1][0/1]表示以u为父亲，取/不取父亲,取/不取自己的最大值

- dp[u][0][0]dp[u][0][0]：自己和父亲都不取，u的儿子随便取。$f[u][0][0]=size∑i=1max( dp(vi,0,0) , dp(vi,0,1) )f[u][0][0]=∑i=1sizemax( dp(vi,0,0) , dp(vi,0,1) )$

- dp[u][1][0]dp[u][1][0]：父亲要取，u自己不取，u的儿子同样随便取。f[u][1][0]=f[u][0][0]f[u][1][0]=f[u][0][0]

- 

  dp[u][1][1]dp[u][1][1]

  ：父亲要取，自己也要取，儿子取k-1条边。

  - 这时我们就要考虑取哪几条边，也就是哪几个点。
  - 对于任意一个u的儿子vivi,如果取这个点，那么它的贡献就是dp(vi,1,1)dp(vi,1,1)，如果不取这个点，那么它的贡献就是dp(vi,1,0)dp(vi,1,0)
  - 因此这个点取或者不取，带来的贡献就是两种情况的差，所以我们只要按两种情况的差从大到小排序就好了。最后选取差值最大的k-1个点就OK了（前提是这k-1个点带来的贡献都是正的，如果有负贡献那么就取不满k-1个点）

- dp[u][0][1]dp[u][0][1]：父亲不取，自己要取，儿子取k条边