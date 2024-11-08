# [USACO20Jan] Berry Picking
原题link: https://usaco.org/index.php?page=viewproblem2&cpid=990

洛谷链接:https://www.luogu.com.cn/problem/P6002


## 题目描述

Bessie 和她的妹妹 Elsie 正在 Farmer John 的浆果园里采浆果。Farmer John 的浆果园里有 NN 棵浆果树（1≤N≤10001≤N≤1000）；树 ii 上有 BiBi 个浆果（1≤Bi≤10001≤Bi≤1000）。Bessie 有 KK 个篮子（1≤K≤10001≤K≤1000，KK 为偶数）。每个篮子里可以装同一棵树上采下的任意多个浆果，但是不能装来自于不同的树上的浆果，因为它们的口味可能不同。篮子里也可以不装浆果。

Bessie 想要使得她得到的浆果数量最大。但是，Farmer John 希望 Bessie 与她的妹妹一同分享，所以 Bessie 必须将浆果数量较多的 K/2K/2 个篮子给 Elsie。这表示 Elsie 很有可能最后比 Bessie 得到更多的浆果，这十分不公平，然而姐妹之间往往就是这样。

帮助 Bessie 求出她最多可以得到的浆果数量。

#### 测试点性质：

- 测试点 1-4 满足 K≤10K≤10。
- 测试点 5-11 没有额外限制。



#### 输入格式（文件名：berries.in）：

输入的第一行包含空格分隔的整数 NN 和 KK。

第二行包含 NN 个空格分隔的整数 B1,B2,…,BNB1,B2,…,BN。



#### 输出格式（文件名：berries.out）：

输出一行，包含所求的答案。



#### 输入样例：

```
5 4
3 6 8 4 2
```

#### 输出样例:

```
8
```

如果 Bessie 在



- 一个篮子里装树 2 的 6 个浆果
- 两个篮子里每个装树 3 的 4 个浆果
- 一个篮子里装树 4 的 4 个浆果

那么她能够得到两个各装有 4 个浆果的篮子，总共 8 个浆果。




By AP G2-1 文奉璋 (超级快)
```
#include<bits/stdc++.h>
using namespace std;
int b[2000],ans,l,r,mid,t,n,k;
bool cmp (int a,int b) {
	return a>b;
}
int main(){
	ios::sync_with_stdio(0);cin.tie(0),cout.tie(0);
	cin>>n>>k;
	for (int i=1;i<=n;i++)cin>>b[i];
	sort(b+1,b+1+n,cmp);
	for (int x=1;;x++){
		priority_queue<int> q;
		int cnt=0;
		for (int j=1;j<=n;j++) {
			cnt+=b[j]/x;
			q.push(b[j]%x);
		}
		if (cnt<k/2) break;
		if (cnt>k) continue;
		t = (cnt-k/2)*x;
		for (int j=cnt+1;j<=k;j++)
			t+=q.top(),q.pop();
		ans=max(t,ans);
	}
	cout<<ans;
	return 0;
}
```
