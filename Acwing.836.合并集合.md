# Acwing.836.合并集合

原题链接: [Acwing.836.合并集合](https://www.acwing.com/problem/content/838/)

## 并查集操作

1. 将两个集合合并
2. 询问两个元素是否在一个集合中

**原理:**

每个集合用一个棵树表示.树的编号就是整个集合的编号,每个节点存储它的父节点,q[x]表示x的父节点.

**问题**

1. 如何判断树根: if(q[x] == x)
2. 如何求x的集合编号 : while(q[x] != x) x = q[x];
3. 如何合并两个集合:找到两个集合的祖先节点,a,b,给祖先节点认个爹.

贴个代码吧!感觉举个栗子就懂了

~~~c++
#include <iostream>
using namespace std;

const int N = 100010;
int q[N];
int n,m;
int find(int x){
	if(q[x] != x)
	q[x] = find(q[x]);
	return q[x];
}
int main(){
	scanf("%d%d",&n,&m);
	for(int i = 1;i <= n;i++) q[i] = i;
	while(m--){
		char op[2];
		int a,b;
		scanf("%s%d%d",op,&a,&b);
		if(*op == 'M') q[find(a)] = find(b);
		else
		if(find(a) == find(b))
		printf("Yes\n");
		else
		printf("No\n");
	}
	return 0;
}
~~~

