# Acwing.154 滑动窗口

原题链接:[Acwing.154滑动窗口](https://www.acwing.com/problem/content/156/)

一个单调队列的经典例题



以求最小值为例:

**使用暴力做法**:扫描整个数组,每次遍历一遍队列,输出最值,这样的时间复杂度比较高.

**优化**

![截屏2023-04-05 09.54.39](/Users/acedsteve/Library/Application Support/typora-user-images/截屏2023-04-05 09.54.39.png)



如图,在-3入队后,找窗口中的最小值,那么只要-3在队列中,-1将永无出头之日.

每次插入新的值都将和队尾元素坐对比,最小值的情况,如果将成入队的值比队尾元素小的话,就将队尾元素删除,然后循环,直到循环终止,将这个值入队,这样就**维护了一个单调队列**

AC代码

~~~c++
#include <iostream>
using namespace std;

const int N = 1000010;

int n,k;
int a[N],q[N];

int main(){
	scanf("%d%d",&n,&k);
	for(int i = 0; i < n;i++)
		scanf("%d",&a[i]);
	int hh = 0,tt = -1;

	for(int i = 0;i < n;i++){
		if(hh <= tt && i - k + 1 > q[hh]) ++ hh;//队头滑出队列
		while(hh <= tt && a[i] <= a[q[tt]]) -- tt;//维护单调队列
		q[++tt] = i;

		if(i + 1 >= k) printf("%d ",a[q[hh]]);
	}
	cout << endl;

	hh = 0,tt = -1;

	for(int i = 0;i < n;i++){
		if(hh <= tt && i - k + 1 > q[hh]) ++ hh;
		while(hh <= tt && a[i] >= a[q[tt]]) -- tt;
		q[++tt] = i;

		if (i + 1 >= k) printf("%d ",a[q[hh]]);
	}
	cout << endl;
	return 0;
}
~~~

