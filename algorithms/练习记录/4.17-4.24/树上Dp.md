### 总结

[树形 dp](https://www.luogu.com.cn/blog/xky-666/solution-p1352) 

### 典型-[没有上司的舞会](https://blog.csdn.net/Jacob0824/article/details/123535953)   

​         

题意：

有N名职员，编号为1~N。他们的关系就像一棵以校长为根的树，父节点就是子节点的直接上司。

每个职员有一个快乐指数，用整数happy给出，其中 1≤i≤N。

现在要召开一场周年庆宴会，不过，没有职员愿意和他的直接上司一起参会。

在满足这个条件的前提下，选择部分职员参加宴会，使得所有参会职员的快乐指数happy总和最大，

求这个最大值。
 思路：

首先，如果仅仅使用f[i]表示i这个子树最多能选的分值的话，我们发现状态无法进行转移，因为在分析每一棵子树的时候，我们无从得知当前子树的根节点是否选择，所以为了能正确区分，我们需要对状态进行进一步划分（这是一种简单的状态机模型）
状态表示

我们可以划分两种情况：

`f[u][0]  `：所有以 u 为根的子树中选择，并且不选 u 这个点的方案

`f[u][1] `：所有以 u 为根的子树中选择，并且选 u 这个点的方案
属性：Max

 状态计算

（1）当前 u 结点不选，子结点可选可不选

求解树形 dp 时我们是从**根节点开始向下递归求解**，当我们递归到 u 这个点是我们先将它的两个儿子的状态（设为s1、s2）处理好，即算出`f[s1, 0]、f[s1, 1]、f[s2, 0]、f[s2, 1] `之后再来计算`f[u, 0]`（所有以 u 为根的子树中选择，并且不选 u 这个点的最大值）。首先每个儿子都是独立的，若使得`f[u, 0]`最大，就应该使u每棵子树达到最大，它们的加和即为答案。

由于 u 没有选择，所以对于它的每棵子树（注意分析的对象是子树），既可以选择其根节点，也可以不选其根节点，比如对于某一棵子树 s 来说，则有： **f [ u , 0 ] + = m a x ( f [ s , 0 ] , f [ s , 1 ] )** 

推出最终的式子为：**f [ u ] [ 0 ] = ∑ m a x ( f [ si , 0 ] , f [ s i , 1 ] )** ( si 表 示 u 的 各 棵 子 树 )  

（2）当前 u 结点选，子结点一定不能选

​		**f [ u ] [ 1 ] = ∑ ( f [ s i , 0 ] )**  (由于选择了 u ，所以对于它的每棵子树，不选其根节点）


时间复杂度分析：

首先一共有2n个状态，每个状态计算的时候需要计算的是它所有的儿子，又树中所有节点的儿子数量即为树当中边的数量（n-1条），所以计算所有状态时总共枚举的次数应当为：O(n-1)。

最终分析的总时间复杂度为：$O(n)$
注意：

本题输入的是一棵有根树（指定了节点间的上下属关系)，故我们需要先找出没有上司的节点root作为根,

DP的目标为：`max(f[root, 0], f[root, 1])`。

1.用数组模拟邻接表存图

```cpp
#include<bits/stdc++.h>

using namespace std;
const int N = 6010;
int n;
int happy[N];
bool has_father[N];
int h[N], e[N], ne[N], idx;
int dp[N][2];

void add(int a, int b)
{
    e[idx] = b, ne[idx] = h[a], h[a] = idx++;
}

void dfs(int u)
{
    dp[u][0] = 0, dp[u][1] = happy[u];
    for(int i=h[u]; ~i; i=ne[i])
    {
       int j = e[i];
       dfs(j);
       dp[u][0] += max(dp[j][0], dp[j][1]);
       dp[u][1] += dp[j][0];
    }
}

int main()
{
    cin>>n;
    for(int i=1; i<=n; ++i) cin>>happy[i];
    memset(h, -1, sizeof h);
    for(int i=0; i<n-1; ++i)
    {
        int a, b;
        cin>>a>>b;
        add(b, a), has_father[a] = true;
    }
    int root = 1;
    while(has_father[root]) root++;
    dfs(root);
    cout<<max(dp[root][0], dp[root][1])<<endl;
    
    return 0;
}

```

2.用`vector`存图

```cpp
#include<bits/stdc++.h>

using namespace std;

const int N = 6010;
int happy[N];
bool has_father[N];
int n;
int dp[N][2];
vector<int> g[N];

void dfs(int u)
{
    dp[u][0] = 0, dp[u][1] = happy[u];
    for(auto x : g[u])
    {
        dfs(x);
        //回溯的时候更新答案
        dp[u][0] += max(dp[x][0], dp[x][1]);
        dp[u][1] += dp[x][0];
    }
}

int main()
{
    cin>>n;
    for(int i=1; i<=n; ++i) cin>>happy[i];
    for(int i=0; i<n-1; ++i)
    {
        int a, b;
        cin>>a>>b;
        has_father[a] = true, g[b].push_back(a);
    }

    int root = 1;
    while(has_father[root]) root++;
    dfs(root);
    cout<<max(dp[root][0], dp[root][1])<<endl;

    return 0;
}

```

### [最大子树和](https://www.luogu.org/problemnew/show/P1122)

````cpp
#include <bits/stdc++.h>
using namespace std;
#define INF 0x3f3f3f3f
#define int long long
const int maxn=1e5+10;
const int mod = 10007;
const int N=16010;
int beauty[N];

int h[2*N],e[2*N],ne[2*N],idx; //双向建边，开两倍！ 
int f[N],ans=-INF;
void add(int u,int v){ 
	e[idx]=v;ne[idx]=h[u];h[u]=idx++;
}
void dfs(int u,int fa){
	 f[u]=beauty[u];
	for(int i=h[u];~i;i=ne[i]){ // ~i -> (i!=-1)
		int v=e[i]; 
		if(v!=fa){
			dfs(v,u);
			f[u]+=max((int)0,f[v]);
		}
	}
		ans=max(ans,f[u]); 
}
int n;
signed main() {
	cin>>n;
	for(int i=1;i<=n;i++){
		cin>>beauty[i];
	} 
	for(int i=0;i<=n;i++) {
		h[i]=-1;
	}
    //memset(h,-1,sizeof h);
    for(int i=1;i<=n-1;i++){
    	int a,b;
    	cin>>a>>b;
    	add(b,a),add(a,b);
		 
	}
	dfs(1,0);
	cout<<ans<<endl;
 
		return 0;
}
//
````





### [选课](https://www.luogu.org/problemnew/show/P2014)（背包类树形DP

1. **题意简述**

- 一堆树构成的森林，共N 个点。
- 每个点有一个权值$s_i$
- 一个点可以被选择，当且仅当它到根节点的路径上的**所有点**都被选择。

共选择M 个点，求被选择的点的权值和的最大值

2. **一个小技巧**

我们发现，如果0算一个节点的话，整张图就是一棵树了

这样的好处：

1. 一棵树就不用分别考虑各棵树然后合并了
2. 输入方便很多，不用特别处理0 的情况

但是M 就会受影响

因为根节点00是必选的，所以只要让M 增加1 就好了

3. **dp及初步设计状态**

首先，不难看出，父节点的信息可以由子节点合并得到并且不会影响子节点

所以使用 dp/记忆化搜索 就好了 

不难想到，用 `dp[u][i]`表示以节点u 为根的子树 ，选择i 个点可以获得的最大权值和

然后想如何转移->

显然合并子节点的信息一定能得到父节点的信息，但使用简单的算法好像不行了

没事反正数据范围小

可以考虑dp套dp（当然这个题算比较简单的）

4. **背包**

继续观察，发现每个子节点都会占用父节点i*i*的一部分，又有一个贡献，可以选择或不选择

重量。。。价值。。。总重。。。

这不是01背包吗？

不同之处在于，每个子节点的重量都是变量

**重新设计状态**

用`dp[u][i][j] `表示节点u 的前i*i*个子节点，限重为j 能得到的最大权值和（价值和）

像01背包一样压缩空间，得到：`dp[u][j]`表示节点u，限重j的最大权值和（价值和）

```cpp
for(int i=head[u]; i; i=e[i].next)//遍历所有子节点
	for(int j=m, v=e[i].to; j>0; --j)//这里和01背包一样，总重从大到小循环
		for(int k=0; k<j; ++k)//这里是不同之处，子节点的重量需要规定
			chk_max(dp[u][j], dp[u][j-k]+dp[v][k]);
			//此函数是将前一个参数设为二者的最大值
```

```cpp
#include <bits/stdc++.h>
using namespace std;
#define INF 0x3f3f3f3f
#define int long long
const int maxn=1e5+10;
const int mod = 10007;
const int N=310;
int n,m;
int h[2*N],e[2*N],ne[2*N],idx; //双向建边，开两倍！ 
int f[N][N],ans=-INF;
void add(int u,int v){ 
	e[idx]=v;ne[idx]=h[u];h[u]=idx++;
}
void dfs(int u){
	
	for(int i=h[u];~i;i=ne[i]){ // ~i -> (i!=-1)
		int v=e[i]; dfs(v); 	//先处理子节点
	}
	for(int i=h[u];~i;i=ne[i]){	   	//遍历所有子节点
		for(int j=m,v=e[i];j>0;j--){ //倒序循环当前选课的总门数
		 
			for(int k=0;k<j;k++){	 // 循环更深子树上的选课门数	 
				f[u][j]=max(f[u][j],f[u][j-k]+f[v][k]);
				//chk_max(dp[u][j], dp[u][j-k]+dp[v][k]);
				//此函数是将前一个参数设为二者的最大值
			}
		}
	}
	
}

signed main() {
	cin>>n>>m;
    m++; //因为根节点00是必选的，所以只要让MM增加11就好了
	for(int i=0;i<=n;i++) {
		h[i]=-1;
	}

    for(int i=1;i<=n;i++){
    	int k,s; cin>>k>>s;
    	f[i][1]=s;
    	add(k,i); 
		 
	}
	dfs(0);
	cout<<f[0][m]<<endl;
 
		return 0;
}
 
```





### [Strategic game](https://www.luogu.org/problemnew/show/UVA1292)



### [天价橘子](https://ac.nowcoder.com/acm/contest/54484/D)

```cpp
#include<bits/stdc++.h>
#define int long long

using namespace std;

const int N=1e4+8;
int n,a[N],head[N],ans,nxt[N],to[N],cnt,f[N][N],res,g[N];

void add(int u,int v){
	to[++cnt]=v;
	nxt[cnt]=head[u];
	head[u]=cnt;
}

void dfs(int u,int fa){
	f[u][0]=1;
	g[u]=a[u];
	for(int i=head[u];i;i=nxt[i]){
		int v=to[i];
		if(v==fa) continue;
		dfs(v,u);
		g[u]+=g[v];
		for(int j=ans;j>=0;--j)
		    for(int k=j;k>=0;--k)
		        f[u][j]|=(f[u][j-k]&f[v][k]);
	}
	f[u][g[u]]=1;
}

signed main(){
	ios::sync_with_stdio(false);
    cin.tie(0);
    cin>>n;
    for(int i=1;i<=n;++i) cin>>a[i],ans+=a[i];
    for(int i=0;i<n-1;++i){
    	int u,v;
    	cin>>u>>v;
    	add(u,v),add(v,u);
	}
	dfs(1,0);
	for(int i=0;i<=ans;++i){
		if(f[1][i]) res=max(res,i*(ans-i));
	}
	cout<<res<<endl;
}
```



### [1074 二叉苹果树（树形dp）](https://blog.csdn.net/qq_39445165/article/details/120555880)

思路分析：

​	分析题目可以知道选择子节点的时候是一定需要选择父节点的，所以在选择节点的时候是有依赖关系的，因为我们需要求解出最多能够保留苹果的数量，所以属于最优化问题，我们可以看成是有依赖背包问题的简化版本：

​	将保留的边的数目看成是背包的容量（最多可以保留Q条边），边的权重看成是价值，每条边看成是体积为1，我们需要求解出在不超过背包容量Q的情况下能够获得的最大价值，使用有依赖的背包问题的求解思路即可。

​	有依赖的背包问题其实是分组背包问题与树形dp的结合，首先我们需要声明一个二维数组dp，其中`dp[u][j]`表示以u为根节点选j条边能够获得的最大价值；

​	怎么样进行状态计算呢？我们可以在递归调用完当前节点u的子节点`next[0]`时候（回溯）更新当前父节点的信息（更新以当前的父节点所有背包容量的最大价值），

​	可以使用两层循环枚举:

​		- 第一层循环枚举背包容量i，

​		- 第二层循环枚举背包容量为i的情况下对应的子节点next[0]占用的体积j，

​	我们可以将当前节点u的每棵子树看成是一组物品，类似于分组背包问题中每一组的的物品，这里在枚举子树的时候不是枚举当前子树中的所有物品选还是不选，而是枚举子树占用的体积，这样比较容易操作而且时间复杂度不会太高，最终一定是可以枚举到与1联通的保留Q条分支的最大价值的。注意因为最终需要保留与1联通，所以`dp[u][j]`以u为父节点的时候是一定选择了某条与子节点的边，这样才可以保证最终选择的边与1是联通的。
————————————————



思路

闫氏DP
分析法：
状态表示：`f[i,j]`以 i 为根节点的子树，包含i的连通块的边数不超过 j 的所有方案
属性：max

状态计算：
这里k是枚举保留的边数,这里要减1的原因是要包含节点`i`
所以状态转移方程是`f[i,j]=max(f[i][j],f[i][j−1−k]+f[soni][k]+wedge[i]) ;   `

k∈[0,j−1]      



### [2019CSP day1t2 括号树](https://my.oschina.net/u/4264835/blog/3246599)

[P5658 [CSP-S2019] 括号树](https://www.luogu.com.cn/problem/P5658)  

明显的树形 $DP$。

思路有点难讲。花了考场上 $1.5h$ 想出来的。

先考虑暴力。我们需要一个能过 $50pts$ 的暴力，所以对于每一个节点，我们必须在最多 $O (n)$ 的时间处理出答案贡献。

考虑类似单调性优化的方法。容易想到，对于一个点 $u$ 的父亲，当它转移到 $u$ 时，所增加的合法子串数量只有这个括号加上从这个点到之前链上所有括号的匹配情况。

比如说我们加了一个右括号，我只需要往回搜索所有合法的每个链上的左括号即可。由此，我们需要用 $O (1)$ 的时间检查每个左括号是否能对新加入的右括号作出贡献。

我们需要用一个栈记录所有没有匹配过的右括号。每次遇到一个右括号就把它进栈；每次遇到左括号如果栈空直接  $break$，因为再往前搜的字串一定经过这个不可能匹配到的左括号；否则把它出栈，如果出栈之后栈空说明从这个位置到新加入的位置恰好构成一个合法串，答案加一。

这个复杂度是 $O (n)$ 的主要原因是对于每一个点必须扫描所有前面的点，这个过程效率实在太低。考虑优化这个过程。

对于每一个新进入栈的右括号，能对答案做出的贡献只有两种情况：

第一，找到了**从当前位置往根节点方向走**第一个没有匹配的左括号，这样从这个左括号到当前位置一定是合法的子串，因为这两个括号之间所有的左括号一定匹配了一个子串上的右括号。

第二，第一个没有匹配的左括号前面**紧挨着它**的合法子串可以和第一种情况的子串共同构成新的合法子串，而紧挨着当前链上第一个没有匹配的左括号的位置一定是**固定的**。

上面两种情况加起来得到了这个有括号的总计答案。

考虑设计 $dp$ 转移状态。从第二部分入手，我们发现因为用来转移的位置是固定的（它紧挨着当前链上第一个没有匹配的左括号），当前加入点的位置也是固定的，考虑将前者作为后者的子问题。所以我们得到，用 $dp [i]$ 表示从根节点走到点 $i$ 的链上**严格以 $i$ 结尾的合法子串**数目。

同时我们需要维护  “第一个没有匹配的左括号的位置”，所以可以借助暴力的思路使用一个栈。用栈顶表示当前链上第一个没有匹配的左括号的位置，每次遇到一个左括号进栈并标记 $dp [i]=0$，遇到一个右括号时如果栈为空则标记 $dp [i]=0$ 因为没有可以和它匹配的左括号；否则弹出栈顶，标记 $dp  [i]=dp [fa [s [top]]]+1$。那个加上的 $1$  表示这个加入的右括号和第一个没有匹配的左括号匹配上的子串，这个没有匹配的左括号是 $s [top]$；所以 $fa [s [top]]$  表示紧挨着它的第一个括号，即 $dp [fa [s [top]]]$  表示这个位置对应上述第二种情况。因为从这个点走到根节点且以这个点结尾的合法子串数目恰好每个合法子串都可以和上面那个加上的 $1$  组成一个新的子串。

比如说，从 ()(变成 ()()，新加入的右括号在对应那个没有匹配的左括号同时，这个括号对又能和前面匹配好的 () 组成新的合法串 ()()。

注意一个问题。因为我们全局只使用一个栈，所以我们当搜完一棵子树并回溯的时候必须恢复栈的状态到刚搜到这个点时的状态。所以我们考虑递归地恢复状态。对于每次搜索我们只有进栈 / 出栈两种可能，所以如果 $dp$ 这个点进过栈，我们就将其弹出；如果出过栈我们就重新进

```cpp
```



### 【洛谷P2899】[USACO08JAN]手机网络Cell Phone Network

题意

n个点，n−1条边（这就告诉我们这是一棵树），一个点染色可以传递给相邻的结点（也就是说相邻结点相当于被染色了）并将这些相邻结点覆盖，问最少染多少个结点可以完全覆盖这n个结点

```cpp
#include<cstdio>
const int N=200000;
const int MAX=100000;
int n,i,a,b,h[N],t[N],name[N],f[N][3];
int min(int x,int y){return x<y?x:y;}
int dfs(int i,int j,int fa){//当前计算f[i][j],fa是i的父亲
    if(f[i][j]>=0)
        return f[i][j];
    f[i][j]=0;
    if(j==2){
        for(int k=h[i];k;k=t[k])
            if(name[k]!=fa)
                f[i][2]+=dfs(name[k],0,i);
        return f[i][2];
    }
    if(j==1){
        for(int k=h[i];k;k=t[k])
            if(name[k]!=fa)
                f[i][1]+=min(min(dfs(name[k],0,i),dfs(name[k],1,i)),dfs(name[k],2,i));
        return ++f[i][1];
    }
    if(j==0){
        f[i][0]=MAX;int s=0;
        for(int k=h[i];k;k=t[k])
            if(name[k]!=fa)
                s+=min(dfs(name[k],0,i),dfs(name[k],1,i));
        for(int k=h[i];k;k=t[k])
            if(name[k]!=fa)
                f[i][0]=min(f[i][0],dfs(name[k],1,i)+s-min(dfs(name[k],0,i),dfs(name[k],1,i)));
        return f[i][0];
    }
}    
int main(){
    scanf("%d",&n);
    for(i=1;i<n;i++){
        scanf("%d%d",&a,&b);
        t[i]=h[a];
        h[a]=i;
        name[i]=b;
        t[i+n]=h[b];
        h[b]=i+n;
        name[i+n]=a;
        f[i][0]=f[i][1]=f[i][2]=-1;
    }
    f[i][0]=f[i][1]=f[i][2]=-1;
    printf("%d",min(min(dfs(1,0,0),dfs(1,1,0)),dfs(1,2,0)+1));//记忆化搜索
    return 0;
}
```









### P3478 [POI2008]STA-Station ——树形DP    

https://www.luogu.com.cn/problem/P3478

https://www.cnblogs.com/wuyueyu/p/13836853.html

给定一个 n 个点的树，请求出一个结点，使得以这个结点为根时，所有结点的深度之和最大。

一个结点的深度之定义为该节点到根的简单路径上边的数量。



题解：

首先我们可以假设1为根结点，然后进行dfs，可以求出每个节点的的深度，以及对应的子树的大小

我们假设当前根节点为u，对应的所有节点的深度和为f[u],然后u的一个子节点为j，如果以j为根结点的话，那么j的所有子树的深度会-1，所以深度和 - Size[j]，所有不在子树上的点的深度全部都要+1，所以所以深度和 + (n -  Size[j]），所以状态转移方程为 `f[j] =  f[u] - (Size[j] << 1) + n `

`f[j] = f[u] - szie[j] + n -size[j]`

```cpp
#include <iostream>
#include <cstring>
#include <cstdio>

using namespace std;

const int N = 1e6 + 10,M = 2 * N;
typedef long long ll;
ll f[N],Size[N],d[N];
int h[N],ne[M],e[M],idx;
int n;

void add(int x,int y){
    ne[idx] = h[x],e[idx] = y,h[x] = idx++;
}

void dfs(int u,int fa){
    Size[u] = 1;
    d[u] = d[fa] + 1;
    for(int i = h[u];~i;i = ne[i]){
        int j = e[i];
        if(j == fa) continue;
        dfs(j,u);
        Size[u] += Size[j];
    }
}

void DFS(int u,int fa){
    for(int i = h[u];~i;i = ne[i]){
        int j = e[i];
        if(j == fa) continue;
        f[j] = f[u] - (Size[j] << 1) + n;
        DFS(j,u);
    }
}

int main(){
    scanf("%d",&n);
    memset(h,-1,sizeof h);
    for(int i = 1;i < n;i++){
        int x,y;
        scanf("%d%d",&x,&y);
        add(x,y),add(y,x);
    }
    dfs(1,0);
    for(int i = 1;i <= n;i++) f[1] += d[i];
    DFS(1,0);
    ll ans = 1,res = f[1];
    for(int i = 2;i <= n;i++) if(f[i] > res) ans = i,res = f[i];
    printf("%lld\n",ans);
    return 0;
}

```





### [树上染色](https://www.luogu.com.cn/problem/P3177)

https://www.luogu.com.cn/problem/solution/P3177

https://blog.csdn.net/weixin_62887323/article/details/126021411

https://www.cnblogs.com/gzh-red/p/14207802.html //有tle的点

https://www.cnblogs.com/Juve/p/11195688.html

​	题目要求将k个点染成黑色，求黑点两两距离及白点两两距离，使他们之和最大。

​	我们可以将距离转化为路径，然后再将路径路径拆分成边，就可以记录每条边被经过的次数，直接计算即可。

​	我们可以这样想，我们任意取两个同色的点，对于每一条边，若不在这两个点的路径上，我们自然不考虑，若是在两个点的路径上，那么这条边的计数加一。我们可以转换一下，若是两个点在边的一侧，则不影响计数，若在边的两侧，则边的计数加一。那么我们推广一下，便可以得出，一条边的两侧每有一对同色点，这条边就要被经过一次。也就是说，一条边被经过的次数等于边的两侧同色点个数的乘积。那么我们便可以求出每条边被经过的次数



```cpp
#include<iostream>
#include<cstdio>
#include<cstring>
#define ll long long
#define MAXN 2005
using namespace std;
ll n,k;
ll fr[MAXN<<1],to[MAXN<<1],nxt[MAXN<<1],pre[MAXN],cnt=0,dis[MAXN<<1];
void add(ll u,ll v,ll w){
    cnt++,fr[cnt]=u,to[cnt]=v,nxt[cnt]=pre[u],pre[u]=cnt,dis[cnt]=w;
}
ll f[MAXN][MAXN],temp[MAXN],size[MAXN];
void dfs(ll x,ll fa){
    size[x]=1;
    for(ll i=pre[x];i;i=nxt[i]){
        ll y=to[i];
        if(y==fa) continue;
        dfs(y,x);
        ll num_b1=min(k,size[x]),num_b2=min(k,size[y]),l;
        memset(temp,0,sizeof(temp));
        for(ll j=0;j<=num_b1;j++){
            for(ll p=0;p<=num_b2&&p+j<=k;p++){
                l=dis[i]*((k-p)*p+(size[y]-p)*(n-k-size[y]+p));
                temp[j+p]=max(temp[j+p],f[x][j]+f[y][p]+l);
            }
        }
        ll m=min(num_b1+num_b2,k);
        for(ll j=0;j<=m;j++)
            f[x][j]=temp[j];
        size[x]+=size[y];
    }
}
int main(){
    scanf("%lld%lld",&n,&k);
    for(ll i=1,u,v,d;i<n;i++){
        scanf("%lld%lld%lld",&u,&v,&d);
        add(u,v,d),add(v,u,d);
    }
    dfs(1,0);
    printf("%lld\n",f[1][k]);
    return 0;
}

 
```

