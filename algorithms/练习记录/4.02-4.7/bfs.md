[方格迷宫](https://www.luogu.com.cn/problem/CF877D)

# Olya and Energy Drinks

## 题面翻译

##### 题目描述
有一NxM的迷宫，'#'是墙，‘.’是路，一秒钟可以向四个方向中的一个移动1~k步，求从起点到终点的最短时间。
##### 输入格式：
第一行n、m、k，下面是NxM的迷宫，最后是起点到终点的坐标。
##### 输出格式：
输出最短时间。如果不能离开迷宫，输出-1。

 

## 样例 #1

### 样例输入 #1

```
3 4 4
....
###.
....
1 1 3 1
```

### 样例输出 #1

```
3
```

## 样例 #2

### 样例输入 #2

```
3 4 1
....
###.
....
1 1 3 1
```

### 样例输出 #2

```
8
```

## 样例 #3

### 样例输入 #3

```
2 2 1
.#
#.
1 1 2 2
```

### 样例输出 #3

```
-1
```

## 提示

In the first sample Olya should run $ 3 $ meters to the right in the first second, $ 2 $ meters down in the second second and $ 3 $ meters to the left in the third second.

In second sample Olya should run to the right for $ 3 $ seconds, then down for $ 2 $ seconds and then to the left for $ 3 $ seconds.

Olya does not recommend drinking energy drinks and generally believes that this is bad.

### 题解

不过有一些容易使代码不 AC 的点：

1. 如果往一个方向遍历从 1步到 k 步究竟走多少步合法时，如果遇到一个出格，那么直接 `break`，因为再往后遍历也一定出格；同理，只要有一个是 `#`，那么直接停止遍历，因为就算一次走多个格也是不能穿墙的。
2. 本题疑问一次可以走 k 步 以内，所以需要放进队列的比较多，所以可以==在加入新结点时就判断一下是不是到达了终点==，如果到了就直接输出，这样可以防止再多循环遍历一次而造成的 TLE

```cpp
#include<bits/stdc++.h>
using namespace std;
//#define int long long
#define endl "\n"
#define fast std::ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define inf 0x3f3f3f3f
const int mod=1e9+7;
const int maxn=1010;
vector<int>vec;
int n,m,k;
queue<pair<int,int> >q;
int a[maxn][maxn],stp[maxn][maxn];
char s[maxn][maxn];
int ans=0;
void solve(){
	cin>>n>>m>>k;
	int next[4][2]={{0,1},{1,0},{0,-1},{-1,0}};
	for(int i=1;i<=n;i++){
		cin>> s[i]+1;
		for(int j=1;j<=m;j++){
			if(s[i][j]=='.'){
				a[i][j]=0; // 0 可走
			}else{ 
				a[i][j]=1; // 1 障碍
			}
		}
	}
		
	
	int x1,x2,y1,y2;
	cin>>x1>>y1>>x2>>y2;
	stp[x1][y1]=1;
	q.push(make_pair(x1,y1));
	while(!q.empty()){
		int x=q.front().first,y=q.front().second;
		if(x==x2&&y==y2){ //到终点
			cout<<stp[x2][y2]-1<<endl;
			return ;
		}
		q.pop();
		for(int i=0;i<4;i++){
			for(int j=1;j<=k;j++){
				int vx=x+next[i][0]*j;
				int vy=y+next[i][1]*j;
                //出格
				if(vx<1||vx>n||vy<1||vy>m||a[vx][vy]/*是墙*/){
					break;
				}
				if(stp[vx][vy]&&stp[vx][vy] <= stp[x][y]){
					break;
				}
				if(stp[vx][vy]){
					continue;
				}
				stp[vx][vy]=stp[x][y]+1;
				q.push(make_pair(vx,vy));//加到队列里
			}
		}
	}
	if(stp[x2][y2]==0){
		cout<<-1;
	}else{
		cout<<stp[x2][y2]-1<<endl;
	}
	
	   
}
 												
signed main(){
    fast
	int t = 1 ;
    //cin >> t ;
	while( t -- ){
		solve();
	} 
    return 0;
}
```

