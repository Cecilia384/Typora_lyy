[csdn](https://blog.csdn.net/qq_39670434/article/details/78425125?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522167724702316800182778988%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=167724702316800182778988&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-78425125-null-null.142^v73^insert_down2,201^v4^add_ask,239^v2^insert_chatgpt&utm_term=dfs%E5%BA%8F&spm=1018.2226.3001.4187)

- **所谓DFS序, 就是DFS整棵树依次访问到的结点组成的序列**
- dfs 序可以将树上的数据线性存储，后续的修改，查询可以用树状数组、线段树来维护
- **DFS序有一个很强的性质: 一颗子树的所有节点在DFS序内是连续的一段, 利用这个性质我们可以解决很多问题**

[Apple Tree题解](https://blog.csdn.net/weixin_43667611/article/details/97411661)

[2](https://blog.csdn.net/qq_45492531/article/details/105485310?spm=1001.2101.3001.6650.4&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-4-105485310-blog-97411661.pc_relevant_aa&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-4-105485310-blog-97411661.pc_relevant_aa&utm_relevant_index=9)

key-> DFS序+树状数组查询

>**dfs序两个数组为l数组和r数组，分别记录某点进入的时间和出来的时间**，**中间的差值就是他的子树的个数**。
>修改的时候是修改 update（l [x],num）,其实是修改s数组的值，l [x]只是定位他是多少时间进入的。s数组可以理解为时间从1-n的数组。
>查询就是 **getsum ( r[k] ) -getsum( l[k]-1 )** ,  r 数组是出的时间，l 数组是入的时间，子树的所有子节点进入和出去的时间都存在 在 l ， r 数组之间，利用前缀和就能求出权值和。
>第x个值的子树权值和就是 l 数组到 r 数组在s数组之前的权值和。
>————————————————

```cpp
#include <cstdio>
#include <algorithm>
#include <cstring>

using namespace std;

typedef long long ll;
const int maxn = 2e5 + 7;

int c[maxn],b[maxn];
int head[maxn],nex[maxn],to[maxn],tot;
int cnt,sta[maxn],ed[maxn],num[maxn];

void add(int x,int y) {
    to[++tot] = y;
    nex[tot] = head[x];
    head[x] = tot;
}

void Add(int x,int v) {
    while(x < maxn) {
        c[x] += v;
        x += x & -x;
    }
}

int Sum(int x) {
    int res = 0;
    while(x) {
        res += c[x];
        x -= x & -x;
    }
    return res;
}

void dfs(int x,int fa) {
    sta[x] = ++cnt;
    num[cnt] = 1;
    Add(cnt,1);
    for(int i = head[x];i;i = nex[i]) {
        int v = to[i];
        if(v == fa) continue;
        dfs(v,x);
    }
    ed[x] = cnt;
}

int main() {
    int n;scanf("%d",&n);
    for(int i = 1;i < n;i++) {
        int x,y;scanf("%d%d",&x,&y);
        add(x,y);add(y,x);
    }
    dfs(1,-1);
    
    int m;scanf("%d",&m);
    for(int i = 1;i <= m;i++) {
        char op[10];scanf("%s",op);
        if(op[0] == 'Q') {
            int x;scanf("%d",&x);
            int l = sta[x],r = ed[x];
            printf("%d\n",Sum(r) - Sum(l - 1));
        }
        else {
            int x;scanf("%d",&x);
            int pos = sta[x];
            if(num[pos] == 0) {
                num[pos] = 1;
                Add(pos,1);
            }
            else {
                num[pos] = 0;
                Add(pos,-1);
            }
        }
    }
    return 0;
}

```



zhy de

```cpp
#include<iostream>

using namespace std;
typedef long long ll;
typedef unsigned long long ull;
#define rep(i,a,n) for(int i=a;i<n;i++)
#define per(i,a,n) for(int i=n-1;i>=a;i--)
#define fastio ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define multi int _;cin>>_;while(_--)
ll gcd(ll a,ll b){ return b?gcd(b,a%b):a;}
const ll MOD = 998244353;
//const ll MOD = 1e9+7;
const ll N = 200005;
//head

int pre[N], idx = 0, hx[N];
int a[N];
int head[N], nxt[N], to[N], id = 0;
int sz[N];

void add(int x, int y)
{
    nxt[++id] = head[x];
    head[x] = id;
    to[id] = y;
}


void dfs(int x, int fx)
{
    pre[++idx] = x;
    for(int i = head[x] ; i ; i = nxt[i])
    {
        int y = to[i];
        if(y == fx) continue;
        dfs(y, x);
        sz[x] += sz[y];
    }
}
int c[N];

int lowbit(int x)
{
    return x & (-x);
}

void change(int x, int y)
{
    for(; x < N ; x += lowbit(x))
    {
        c[x] += y;
    }
}

int query(int x)
{
    int ans = 0;
    for(; x; x -= lowbit(x))
    {
        ans += c[x];
    }
    return ans;
}


int main()
{  
    fastio
    //freopen("1.in","r",stdin);
    int n;
    cin >> n;
    fill(sz + 1, sz + n + 1, 1);
    fill(a + 1, a + n + 1, 1);

    for(int i = 1 ; i < n ; i++ )
    {
        int x, y;
        cin >> x >> y;
        add(x, y);
        add(y, x);
    }
    dfs(1, 0);
    for(int i = 1 ; i <= n ; i++ )
    {
        hx[pre[i]] = i + 1; 
    }
    int m;
    cin >> m;
    /*for(int i = 1 ; i <= n ; i++ )
    {
        cout << pre[i] << " \n"[i == n];
    }*/
    for(int i = 1 ; i <= n ; i++ )
    {
        change(i+1, 1);
    }
    for(int i = 1 ; i <= m ; i++ )
    {
        char op;
        int x;
        cin >> op >> x;
        if(op == 'C')
        {
            if(a[x] == 1)
            {
                change(hx[x], -1);
                a[x] = 0;
            }else{
                change(hx[x], 1);
                a[x] = 1;
            }
        }else{
            cout << query(hx[x] + sz[x] - 1) - query(hx[x] - 1) << "\n";
        }
    }
    return 0;
}
```



```cpp
#include<iostream>
#include<cstring>
#include<vector>
#include<algorithm>
#include<cstdio> 
using namespace std;
const int maxn=1e5+10;
typedef long long ll;
ll s[maxn],sum[maxn],l[maxn],r[maxn];
ll t,tot;
vector<vector<ll> > p(maxn);
int lowbit(int x)
{
	return x&(-x);
}
void update(ll x,ll num)
{ 
	while(x<=t)
	{
		sum[x]+=num;
		x+=lowbit(x);
	}
}
ll getsum(ll x)
{
	ll ans=0;
	while(x>0)
	{
		ans+=sum[x];
		x-=lowbit(x);
	}
	return ans;
}
void dfs(ll x)
{
	l[x]=tot;
	for(ll i=0;i<p[x].size();i++)
	{
		tot++;
		dfs(p[x][i]);
	}
	r[x]=tot;
}
int main()
{
	scanf("%lld",&t);
	for(ll i=1;i<t;i++)
	{
		ll u,v;
		scanf("%lld%lld",&u,&v);
		p[u].push_back(v);
	}
	tot=1;
	dfs(1);
	for(ll i=1;i<=t;i++)
	{
		s[i]=1;
		update(i,1);
	}
	ll m;
	scanf("%lld",&m);
	for(int i=1;i<=m;i++)
	{
		char str;
		ll k;
		scanf("%s%lld",&str,&k);	
		if(str=='Q')
		{

			printf("%lld\n",getsum(r[k])-getsum(l[k]-1));
		}
		else
		{
			if(s[k]==1)
			{
				s[k]=0;
				update(l[k],-1);
			}
			else
			{
				s[k]=1;
				update(l[k],1);
			}
		}
	}
	return 0;
}

```



`  a[u] = ++cnt;
	a[cnt++] = u;`

```cpp
#include<bits/stdc++.h>
using namespace std;
#define ll long long int
const int N=1e5+10,M=N*2;
// M-- 以有向图的格式存储无向图，所以每个节点至多对应2n-2条边
 
int h[N]; //邻接表存储树，有n个节点，所以需要n个队列头节点
int e[M]; //存储元素
int ne[M]; //存储列表的next值
int idx; //单链表指针
int n; //题目所给的输入，n个节点
int ans = N; //表示重心的所有的子树中，最大的子树的结点数目
bool st[N]; //记录节点是否被访问过，访问过则标记为true

int a[N],c[N],cnt;

//a所对应的单链表中插入b , a作为根 
void add(int a,int b){
	e[idx]=b;
	ne[idx]=h[a];
	h[a]=idx++;
}
// 以u为根的子树中点的数量 
int dfs(int u){

    a[u] = ++cnt;
	//a[cnt++] = u;
	
	int res=0;//存储 ，删掉某个结点之后，最大连通子图节点数
	st[u]=true;// 标记访问过的u结点
	int sum=1;//存储以u为根的树的节点数，包括u
	//访问u的每个节点
	for(int i=h[u];i!=-1;i=ne[i]){
		int j=e[j];
		if(!st[j]){
			int s=dfs(j); // u 节点的单棵子树节点数
			res=max(res,s);// 记录最大连通子图的节点数
			sum+=s;//以j为根的树的节点数 
		}
	} 
	res=max(res,n-sum);//选择u节点为重心，最大的连通子图的节点数
	ans=min(res,ans); 
	return sum;
	 
}
int main(){
	memset(h,-1,sizeof(h));
	//初始化h数组 -1表示尾节点
	cin>>n;
	// 树中是不存在环的，对于有n个节点的树，必定是n-1条边
	for(int i=0;i<n;i++){
		int a,b;
		cin>>a>>b;
		add(a,b),add(b,a);
	}
	dfs(1);
	cout<<ans<<endl;
	
	return 0;
} 
```

