---
title: 高精度模板
toc: true
categories:
  - Learn
  - Competitive Programming
abbrlink: f136
tags: []
date: 2019-01-29 00:48:40
thumbnail:
cover:
---

```C++
define N 1e5
struct bign
{
    int len;
    int v[N];
    
 	// 赋值 bign=bign
    bign operator = (char* s)
    {
        len=strlen(s);
        memset(v,0,sizeof(v));
        for(int i=0;i<len;i++)
        	v[i]=s[len-i-1]-'0';
        return *this;
    }
    //赋值 bign=int
    bign operator = (int x)
    {
        char s[N];
        sprintf(s,"%d",x);
        return *this=s;
	}
    
    // 高精加
  	bign operator + (const bign &b) const
    {
        bign c;
        memset(c.v,0,sizeof(c.v));
        c.len=max(len,b.len);
    	for(int i=0;i<c.len;i++)
            c.v[i]=v[i]+b.v[i];
        for(int i=0;i<c.len;i++)
        {
            c.v[i+1]+=c.v[i]/10;
            c.v[i]%=10;
		}
        if(c.v[c.len]) c.len++;
        return c;
	}
    // 高精乘
    bign operator * (const bign &b) const
    {
        bign c;
        memset(c.v,0,sizeof(c.v));
        c.len=len+b.len;
        for(int i=0;i<len;i++)
        	for(int j=0;j<b.len;j++)
                c.v[i+j]+=v[i]*b.v[j];
        for(int i=0;i<len;i++)
        {
            c.v[i+1]=c.v[i]/10;
            c.v[i]%=10;
		}
        while(c.len>1 && c.v[c.len-1]) c.len--;
      	return c;
	}
    // 高精加等于
    bign operator += (const bign &b)
    {
        return *this+b;
    }
    
    // 比大小
    bool operator < (const bign &b) const
    {
        if(len<b.len) return 1;
        if(len>b.len) return 0;
        for(int i=len-1;i>=0;i--)
        {
            if(v[i]<b.v[i]) return 1;
        	if(v[i]>b.v[i]) return 0;
        }
        return 0;//两个数相等返回flase
    }
    
    bool operator > (const bign &b) const
    {
        return b<*this;
	}
    
    bool operator <= (const bign &b) const
    {
        return !(b>*this);
	}
    
    bool operator >= (const bign &b) const
    {
        return !(b<*this);
	}
    
    bool operator == (const bign &b) const
    {
        return (b>*this)^(b<*this)
	}
};
```