# Acwing.845.八数码

原题链接:[Acwing.945.八数码](https://www.acwing.com/problem/content/847/)

**描述**

在一个3x3矩阵里面,通过交换x使得矩阵按顺序排列,输出交换的最少次数



**算法思路**

1. 使用队列记录当前获取的序列
2. 使用一张哈希表记录保存的所有序列,和与每个序列对应的交换次数
3. 从队头取出序列,进行交换(枚举),如果这个新序列没有出现过(在哈希表中查找),那么就让交换的次数加一,并将这个新序列加入队列中.
4. 再恢复现场,往下一个方向交换

**新学的知识**

- Unordered_map<string,int>

  这是无序映射容器,又称哈希表或字典

  在此题中,第一个string存储所有的序列,int存储这个序列是经过多少次交换得到的

- 一维和二维之间的坐标转换

  已知在一维数组中某点的下标是k,那么在二维数组中对应的坐标是(k/n,k%n) *n代表矩阵的长度*

  已知在二维数组中的某点的坐标是(a,b),那么转换成一维数组对应的下标是(a*3+b)

## AC代码

```cpp
// Problem: 八数码
// Contest: AcWing
// URL: https://www.acwing.com/problem/content/847/
// Memory Limit: 64 MB
// Time Limit: 1000 ms
// 
// Powered by CP Editor (https://cpeditor.org)

#include <iostream>
#include <algorithm>
#include <cstring>
#include <queue>
#include <unordered_map>

using namespace std;
int bfs(string s){
	string e = "12345678x";
	//定义队列和状态
	queue<string> q;
	unordered_map<string,int> d;
	//初始化
	q.push(s);
	d[s] = 0;
	//定义方向
	int dx[4] = {-1,0,1,0},dy[4] = {0,1,0,-1};
	while(q.size()){
		string t = q.front();
		q.pop();
		int distence = d[t];//记录当前状态交换的次数
		if(t == e) return distence;
		
		int k =  t.find('x');
		int x = k / 3,y = k % 3;//常用寄巧,将一维坐标转换成二维坐标
		
		for(int i = 0;i < 4;i++){
			int a = x + dx[i],b = y + dy[i];
			
			if(a >= 0 && a < 3 && b >= 0 && b < 3){
				swap(t[k],t[a * 3 + b]);
				
				if(!d.count(t)){
					d[t] = distence + 1;
					q.push(t);
				}
				swap(t[k],t[a * 3 + b]);
			}
		}
		
	}
	return -1;
}
int main(){
	string s;
	for(int i = 0;i < 9;i++){
		char c;
		cin >> c;
		s += c;
	}
	cout << bfs(s) << endl;
	return 0;
}
```



