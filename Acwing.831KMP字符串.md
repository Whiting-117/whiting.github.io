# Acwing.831KMP字符串

题目链接:[Acwing.831KMP字符串](https://www.acwing.com/problem/content/description/833/)

## 什么是KMP算法

KMP是一个字符串匹配算法,优化了传统的暴力匹配.将时间复杂度从$O(nm)$降到了$O(n+m)$

**一些基本概念**

1. s[ ]是模版串
2. p[ ]是模式串
3. 前缀:**除最后一个字符以外**一个字符串的全部头部组合
4. 后缀:和前缀差不多,去除第一个字符
5. 部分匹配值:前缀后缀的最长共有元素的长度
6. next[ ]:部分匹配值表,它存储的是每一个下标对应的“部分匹配值”是KMP算法的核心.

## next数组的含义及求法

对于next[j],是p[1,j]串中前缀和后缀相同的最大长度,即:部分匹配值

$p[1,next[j]] = p[j - next[j] + 1,j]$

***举个栗子***

|  下标   | 1    | 2    | 3    | 4    | 5    |
| :-----: | ---- | ---- | ---- | ---- | ---- |
|   p串   | a    | b    | c    | a    | b    |
| next[ ] | 0    | 0    | 0    | 1    | 2    |

| next[ ] | 前缀              | 后缀              | 值   |
| ------- | ----------------- | ----------------- | ---- |
| 1       | $\varnothing$     | $\varnothing$     | 0    |
| 2       | a                 | b                 | 0    |
| 3       | a , ab            | c , bc            | 0    |
| 4       | ==a== , ab , abc  | ==a==, ca, bca    | 1    |
| 5       | a,==ab==,abc,abca | b,==ab==,cab,bcab | 2    |

求next数组只用到p[ ]数组,

代码如下:

```cpp
for(int i = 2,j = 0;i <= m;i++){
  while(j && p[i] != p[j + 1]) j = next[j];
  if(p[i] == p[j + 1]) j++;
  next[i] = j;
}
```





完整代码:

```cpp
#include <iostream>
using namespace std;

const int N = 100010,M = 1000010;

int n,m;
char s[N],p[M];
int ne[N];

int main(){
	cin >> n >> p + 1 >> m >> s + 1;
	//next
	for(int i = 2,j = 0;i <= n;i++){
		while(j && p[i] != p[j + 1]) j = ne[j];
		if(p[i] == p[j + 1]) j++;
		ne[i] = j;
	}
	for(int i = 1,j = 0;i <= m;i++){
		while(j && s[i] != p[j + 1]) j = ne[j];
		if(s[i] == p[j + 1]) j++;
		if(j == n){
			printf("%d ",i - n);
			j = ne[j];
			
		}
	}
	return 0;
}
```

*好像也不太懂.......背模版算了*



> 一个人能走的多远不在于他在顺境时能走的多快，而在于他在逆境时多久能找到曾经的自己。         																	-----KMP