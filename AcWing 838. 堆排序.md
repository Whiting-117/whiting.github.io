# AcWing 838. 堆排序

原题链接: [AcWing 838. 堆排序](https://www.acwing.com/problem/content/840/)

## 什么是堆

堆,就是一个**完全二叉树**

## 堆的操作:

1. 插入一个数
2. 求集合中的最小值
3. 删除最小值
4. 删除任意一个元素
5. 修改任意一个元素

## 具体代码实现

~~~c++
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 100010;

int h[N],mySize;//h数组是个堆,mySize是堆的长度
int n,m;

void down(int u){
	int t = u;//让t成为那个三角形的中最小值的下标
	if(u * 2 <= mySize && h[t] > h[u * 2])
		t = u * 2;
	if(u * 2 + 1 <= mySize && h[t] > h[u * 2 + 1])
		t = u * 2 + 1;
	if(u != t){//如果u == t就意味着这个三角形的顶点是最小值,不需要交换
		swap(h[u],h[t]);
		down(t);
	}
}
int main(){
	cin >> n >> m;
	mySize = n;//初始化堆的大小为n
	for(int i = 1;i <= n;i++) scanf("%d",&h[i]);
	for(int i = n/2;i;i--)
		down(i);//为什么是n/2呢?因为下标为n/2的结点没有叶节点,就不需要down了
	while(m--){
		cout << h[1] << " ";
		h[1] = h[mySize];//
		mySize --;
		down(1);
	}
	return 0;
}
~~~

