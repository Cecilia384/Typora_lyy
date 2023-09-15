[acwing898. 数字三角形](https://www.acwing.com/solution/content/139219/)            

## 典例：数字三角形

```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define endl '\n'
#define fast std::ios::sync_with_stdio(false);cin.tie.(0);cout.tie(0);
const int maxn=1e5+100;
const int N=550,INF=0x3f3f3f3f;
int a,b,n,t;int x,y;
int g[1010][1010];
int f[1010][1010];
signed main(){
	  t=1;
	  while(t--){
	  	
	  	cin>>x;
	  	for(int i=1;i<=x;i++){
	  		for(int j=1;j<=i;j++){
	  			cin>>g[i][j];
	  			 
	  		}
	  	}
	  	memset(f,-0x3f3f3f3f,sizeof f);
	  	f[1][1]=g[1][1];
	  	for(int i=2;i<=x;i++){
	  		for(int j=1;j<=i;j++){
	  			f[i][j]=max(f[i-1][j-1],f[i-1][j])+g[i][j];
	  		}
	  	}
	  	 //cout<<f[x][x]<<endl;
	   
	  }
	  int res=-INF;
      for(int i=1;i<=x;i++) res=max(res,f[x][i]);
      cout<<res<<endl;
	 
	return 0;
}
```



法2.

```cpp
#include <iostream>
using namespace std;
const int N = 510;
int n;
int a[N][N];
int f[N][N];
int main () {
    cin >> n;
    for (int i = 1;i <= n;i++) {
        for (int j = 1;j <= i;j++) cin >> a[i][j];
    }
    for (int i = 1;i <= n;i++) f[n][i] = a[n][i];
    for (int i = n - 1;i >= 1;i--) {
        for (int j = 1;j <= i;j++) {
            f[i][j] = max (f[i + 1][j],f[i + 1][j + 1]) + a[i][j];
        }
    }
    cout << f[1][1] << endl;
    return 0;
}
```



## [LIS最长上升子序列](https://blog.csdn.net/lxt_Lucia/article/details/81206439?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522168122019216782427441898%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=168122019216782427441898&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-81206439-null-null.142^v82^control,201^v4^add_ask,239^v2^insert_chatgpt&utm_term=%E6%9C%80%E9%95%BF%E4%B8%8A%E5%8D%87%E5%AD%90%E5%BA%8F%E5%88%97&spm=1018.2226.3001.4187)



### 1.$O(N^2)$

```cpp
#include <iostream>
using namespace std;
const int N = 1010;
int n;
int a[N];
int f[N];
int main () {
    cin >> n;
    for(int i=1;i<=n;i++){
        cin>>a[i];
    }
    int ans=0;
    for(int i=1;i<=n;i++){
        f[i]=1;
        for(int j=1;j<i;j++){
            if(a[i]>a[j]){
              f[i]=max(f[i],f[j]+1);  
            }
        }
        ans=max(ans,f[i]);
    }
    cout<<ans;
    return 0;
}
```



〇〇〇	〇〇〇	〇〇〇	〇〇〇



### 2.贪心+二分$O(logn)$

新建一个 low 数组，`low [ i ]`表示长度为i的LIS结尾元素的最小值。对于一个上升子序列，显然其结尾元素越小，越有利于在后面接其他的元素，也就越可能变得更长。

因此，我们只需要维护 low 数组，对于每一个`a[ i ]`，如果a[ i ] > low [当前最长的LIS长度]，就把 a [ i ]接到当前最长的LIS后面，即`low [++当前最长的LIS长度] = a [ i ]`  。 

那么，怎么维护 low 数组呢？

对于每一个a [ i ]，如果a [ i ]能接到 LIS 后面，就接上去；否则，就用 a [ i ] 取更新 low 数组。具体方法是，在low数组中找到第一个大于等于a [ i ]的元素low [ j ]，用a [ i ]去更新 low [ j ]。如果从头到尾扫一遍 low 数组的话，时间复杂度仍是O(n^2)。我们注意到 low 数组内部一定是单调不降的，所有我们可以二分 low 数组，找出第一个大于等于a[ i ]的元素。二分一次 low 数组的时间复杂度的O(lgn)，所以总的时间复杂度是O(nlogn)。
**但是，但是！！！B[ ] 中的序列并不一定是正确的最长上升子序列。**

　因为在B中插入的数据是有序的，不需要移动，只需要替换，所以可以用二分查找插入的位置，那么插入n个数的时间复杂度为〇(logn)，这样我们会把这个求LIS长度的算法复杂度降为了〇(nlogn)。话不多说了

1.手写     `lower_bound(g, g+l, num[i]) - g;  `

```cpp
#include <cmath>
#include <cstdio>
#include <cstdlib>
#include <cstring>
#include <iostream>
#include <algorithm>
using namespace std;
 
const int maxn =300003, INF = 0x7f7f7f7f;
int low[maxn], a[maxn];
int n, ans;
 
int binary_search(int *a, int R, int x)
//二分查找，返回a数组中第一个>=x的位置 
{
    int L = 1, mid;
    while(L <= R)
    {
        mid = (L+R) >> 1;
        if(a[mid] <= x)
            L = mid + 1;
        else 
            R = mid - 1;
    }
    return L;
}
 
int main()
{
    scanf("%d", &n);
    for(int i=1; i<=n; i++) 
    {
        scanf("%d", &a[i]); 
        low[i] = INF;   //由于low中存的是最小值，所以low初始化为INF 
    }
    low[1] = a[1]; 
    ans = 1;   //初始时LIS长度为1 
    for(int i=2; i<=n; i++)
    {
        if(a[i] > low[ans])    //若a[i]>=low[ans]，直接把a[i]接到后面 
            low[++ans] = a[i];
        else       //否则，找到low中第一个>=a[i]的位置low[j]，用a[i]更新low[j] 
            low[binary_search(low, ans, a[i])] = a[i];
    }
    printf("%d\n", ans);   //输出答案 
    return 0;
}

```

`lower_bound(g, g+l, num[i]) - g;  `

```cpp
#include<stdio.h>  
#include<string.h>  
#include<algorithm>  
  
using namespace std;  
  
int num[10]={3,6,3,2,4,6,7,5,4,3};  
  
const int INF=0x3f3f3f3f;  
int l=10, g[100], d[100];  
 
int main()  
{  
    fill(g, g+l, INF);  
    int max_=-1;  
    for(int i=0; i<l; i++)  
    {  
        int j = lower_bound(g, g+l, num[i]) - g;  
        d[i] = j+1;  
        if(max_<d[i])  
            max_=d[i];  
        g[j] = num[i];  
    }  
    printf("%d\n", max_);  
    return 0;  
}  
  /*
这个算法其实已经不是DP了，有点像贪心。至于复杂度降低其实是因为这个算法里面用到了二分搜索。
本来有N个数要处理是O(n)，每次计算要查找N次还是O(n)，一共就是O(n^2)；
现在搜索换成了O(logn)的二分搜索，总的复杂度就变为O(nlogn)了。
这里主要注意一下lower_bound函数的应用，注意减去的g是地址。
地址 - 地址 = 下标。
*/
 
```



me

```cpp
#include <iostream>
using namespace std;
const int N = 101000;
const int INF=0x3f3f3f3f;
int n;
int a[N];
int f[N],low[N];
int main () {
	//system("COLOR fd");
	 cin>>n;
	 for(int i=1;i<=n;i++){
	 	cin>>a[i];
	 	low[i]=INF;
	 }
	 int ans=1;
	 low[0]=-INF;
	 low[1]=a[1];
	 for(int i=2;i<=n;i++){
	 	if(a[i]>low[ans]){
	 		low[++ans]=a[i];
		 }else{
		 	int pos=lower_bound(low+1,low+n+1,a[i])-low;
		 	low[pos]=a[i];
		 }
	
	 }
     	cout<<ans<<endl;
    
    return 0;
}
```

**解法3：树状数组维护**：

我们再来回顾O(n^2)DP的状态转移方程：F [ i ] = max { F [ j ] + 1 ，F [ i ] }  (1 <= j <  i，A[ j ] < A[ i ])
我们在递推F数组的时候，每次都要把F数组扫一遍求F[ j ]的最大值，时间开销比较大。我们可以借助数据结构来优化这个过程。用树状数组来维护F数组（据说分块也是可以的，但是分块是O(n*sqrt(n)）的时间复杂度，不如树状数组跑得快），首先把A数组从小到大排序，同时把A[ i ]在排序之前的序号记录下来。然后从小到大枚举A[ i ]，每次用编号小于等于A[ i ]编号的元素的LIS长度+1来更新答案，同时把编号大于等于A[ i ]编号元素的LIS长度+1。因为A数组已经是有序的，所以可以直接更新。有点绕，具体看代码。

还有一点需要注意：树状数组求LIS不去重的话就变成了最长不下降子序列了。



```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <cstdlib>
#include <cstring>
#include <cmath>
using namespace std;
const int maxn =103, INF=0x7f7f7f7f;
struct Node{
    int val,num;
}z[maxn]; 
int T[maxn];
int n;
bool cmp(Node a,Node b)
{
    return a.val==b.val?a.num<b.num:a.val<b.val;
}
void modify(int x, int y)//把val[x]替换为val[x]和y中较大的数 
{
    for(; x<=n; x+=x&(-x))
        T[x] = max(T[x],y);
}
int query(int x)//返回val[1]~val[x]中的最大值 
{
    int res=-INF;
    for(; x; x-=x&(-x))
        res=max(res,T[x]);
    return res;
}
int main()
{
    int ans=0;
    scanf("%d",&n);
    for(int i=1; i<=n; i++)
    {
        scanf("%d", &z[i].val);
        z[i].num = i;//记住val[i]的编号，有点类似于离散化的处理，但没有去重 
    }
    sort(z+1, z+n+1, cmp);//以权值为第一关键字从小到大排序 
    for(int i=1; i<=n; i++)//按权值从小到大枚举 
    {
        int maxx = query(z[i].num);//查询编号小于等于num[i]的LIS最大长度
        modify(z[i].num, ++maxx);//把长度+1，再去更新前面的LIS长度
        ans=max(ans, maxx);//更新答案
    }
    printf("%d\n", ans);
    return 0;
}
```







## LCS最长公共子序列

s1={1,**3**,4,**5**,6,**7,7,8**},

s2={**3**,**5**,**7**,4,8,6,**7**,**8**,2}

构建`c[i][j]`表需要$Θ(mn)$​，输出1个LCS的序列需要$Θ(m+n)$

![img](%E7%BA%BF%E6%80%A7DP.assets/Center.jpeg)。



```cpp
#include <iostream>
using namespace std;
const int maxn=1e5+10;
const int N=1010;
int n,m;
char a[N],b[N];
int f[N][N]; 
int main()
{
    cin>>n>>m>>a+1>>b+1;
    for(int i=1;i<=n;i++){
    	for(int j=1;j<=m;j++){
    		if(a[i]==b[j]){
    			f[i][j]=f[i-1][j-1]+1;
			}else{
				f[i][j]=max(f[i-1][j],f[i][j-1]);
			}
		}
	}
	cout<<f[n][m]<<endl;
	
	return 0;
}

```



 

例题 AcWing 902. 最短编辑距离 



```cpp
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 1010;

int m, n;
char a[N],b[N];
int dp[N][N];

int main()
{
    scanf("%d%s", &m, a + 1);   // a + 1 这里的小技巧
    scanf("%d%s", &n, b + 1);

    //cout << a[1] <<  endl;

    for(int i = 0; i <= m; i++) dp[i][0] = i;  //全删除
    for(int i = 0; i <= n; i++) dp[0][i] = i;  //全插入

    for(int i = 1; i <=m; i++)
        for(int j = 1; j <=n; j++)
        {
            dp[i][j] = min(dp[i][j-1], dp[i-1][j]) + 1;
            dp[i][j] = min(dp[i][j], dp[i-1][j-1] + (a[i] != b[j]));  // 注意这里 i的原因 是 scanf("%d%s", &m, a + 1);
        }

    printf("%d\n",dp[m][n]);

    return 0;
}
```



AcWing 899. 编辑距离

```cpp
#include<bits/stdc++.h>

using namespace std;

const int N = 1010, M = 15;

int n,m;
char str[N][M];
int f[M][M];

// a 变成 b 的最少操作数
int edit_distance(char a[],char b[])
{
    int n=strlen(a+1),m=strlen(b+1); 

    for(int i=1;i<=n;i++) f[i][0]=i; //删除

    for(int i=1;i<=m;i++) f[0][i]=i; //插入

    for(int i=1;i<=n;i++)
        for(int j=1;j<=m;j++)
            f[i][j]=min(min(f[i-1][j],f[i][j-1])+1,f[i-1][j-1]+(a[i]!=b[j]));

    return f[n][m];
}

int main()
{
    cin>>n>>m;

    for(int i=0;i<n;i++) cin>>str[i]+1;

    while(m--)
    {
        char s[M];
        int k;
        cin>>s+1>>k;

        int res=0;
        for(int i=0;i<n;i++)
            if(edit_distance(str[i],s)<=k)
                res++;

        cout<<res<<endl;
    }

    return 0;
}

 
```

##  最长公共上升子序列   LCIS

