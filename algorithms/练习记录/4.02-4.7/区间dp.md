# 区间dp入门

### **一.什么是区间dp?**

> ​    顾名思义：区间dp就是在区间上进行[动态规划](https://so.csdn.net/so/search?q=动态规划&spm=1001.2101.3001.7020)，求解一段区间上的最优解。主要是通过合并小区间的 最优解进而得出整个大区间上最优解的dp算法。

### **二.核心思路**

​        既然让我求解在一个区间上的最优解，那么我把这个区间分割成一个个小区间，求解每个小区间的最优解，再合并小区间得到大区间即可。所以在代码实现上，我可以枚举区间长度len为每次分割成的小区间长度（由短到长不断合并），内层枚举该长度下可以的起点，自然终点也就明了了。然后在这个起点终点之间枚举分割点，求解这段小区间在某个分割点下的最优解。板子如下：

 

#### 典例

 [环形石子合并](https://www.luogu.com.cn/problem/P1880)

[加强版石子合并](https://www.luogu.com.cn/problem/P5569)（GarsiaWachs算法）

[解法：](https://blog.csdn.net/wjh2622075127/article/details/82534271?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522168068056316800211562951%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=168068056316800211562951&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-82534271-null-null.142^v81^wechat_v2,201^v4^add_ask,239^v2^insert_chatgpt&utm_term=%E7%8E%AF%E5%BD%A2%E7%9F%B3%E5%AD%90%E5%90%88%E5%B9%B6&spm=1018.2226.3001.4187)

其一：使用一个取模运算，实现环形dp。

​	**`dp[n][m]`数组的含义是：从石头n到石头m这个闭区间的dp结果。**

```cpp
#include <iostream>
using namespace std;

int n, num[105], sum[105] = {};
int dp[105][105], ans = 0x3f3f3f3f;;

int main()
{
    cin >> n;
    for (int i = 1; i <= n; ++i) {
        cin >> num[i];
        num[i + n] = num[i];
        dp[i][i] = 0;
    }
    for (int i = 1; i <= n + n; ++i) {
        sum[i] = sum[i - 1] + num[i];
    }
    for (int k = 2; k <= n; ++k) {
        for (int i = 1; i <= 2*n - k + 1; ++i) {
            int j = i + k - 1;
            dp[i][j] = 0x3f3f3f3f;
            for (int t = i; t < j; ++t) {
                dp[i][j] = min(dp[i][j], dp[i][t] + dp[t + 1][j] + sum[j] - sum[i - 1]);
            }
        }
    }
    for (int i = 1; i <= n; ++i) {
        ans = min(ans, dp[i][i + n - 1]);
    }
    cout << ans;
}

```



其二：将环形拓展成2倍链状，开二倍的数组即可实现，这个比较好理解好实现 

​	**`dp[n][m]`：从石头n开始的长度m的区间的dp结果**

```cpp
#include <iostream>
using namespace std;

int sum[100] = {0}, ans = 0x3f3f3f3f;
int n, num[100], dp[100][100];

int getsum(int u, int s)
{
    s--;
    if (u + s > n) return sum[n] - sum[u - 1] + sum[(u + s)%n];
    else return sum[u + s] - sum[u - 1];
}

int main()
{
    cin >> n;
    for (int i = 1; i <= n; ++i) {
        cin >> num[i];
        sum[i] = sum[i - 1] + num[i];
        dp[i][1] = 0;
    }
    for (int k = 2; k <= n; ++k) {
        for (int i = 1; i <= n; ++i) {
            dp[i][k] = 0x3f3f3f3f;
            for (int t = 1; t < k; ++t) {
                dp[i][k] = min(dp[i][k], dp[i][t] + dp[(i + t - 1) % n + 1][k - t] + getsum(i, k));
            }
        }
    }
    for (int i = 1; i <= n; ++i) {
        ans = min(ans, dp[i][n]);
    }
    cout << ans;

```



>可以把链延长两倍，变成 2n 个堆，其中 i和 i+n 是相同的两个堆，然后直接套 区间DP 模板，但对于 阶段 len 只枚举到 n，根据 状态的定义，最终可以得到所求的方案，时间复杂度为 O(n3)



```cpp
#include <iostream>
#include <cstring>

using namespace std;

const int N = 410, M = N << 1, INF = 0x3f3f3f3f;

int n;
int w[M], s[M];
int f[M][M], g[M][M];

int main()
{
    //读入
    scanf("%d", &n);
    for (int i = 1; i <= n; ++ i) cin >> w[i], w[i + n] = w[i];

    //预处理前缀和（DP状态转移中会频繁的用到区间和）
    for (int i = 1; i <= n << 1; ++ i) s[i] = s[i - 1] + w[i];

    memset(f, -0x3f, sizeof f);//求最大值预处理成最小值（可以省掉，这题不会有负数状态所以0就是最小）
    memset(g, +0x3f, sizeof g);//求最小值预处理成最大值（不可省掉）

    for (int len = 1; len <= n; ++ len)//阶段
    {
        for (int l = 1, r; r = l + len - 1, r < n << 1; ++ l)//左右区间参数
        {
            if (len == 1) f[l][l] = g[l][l] = 0;//预处理初始状态
            else
            {
                for (int k = l; k + 1 <= r; ++ k)//枚举分开点
                {
                    f[l][r] = max(f[l][r], f[l][k] + f[k + 1][r] + s[r] - s[l - 1]),
                    g[l][r] = min(g[l][r], g[l][k] + g[k + 1][r] + s[r] - s[l - 1]);
                }
            }
        }
    }
    //目标状态中找出方案
    int minv = INF, maxv = -INF;
    for (int l = 1; l <= n; ++ l)
    {
        minv = min(minv, g[l][l + n - 1]);
        maxv = max(maxv, f[l][l + n - 1]);
    }

    //输出
    printf("%d\n%d\n", minv, maxv);

    return 0;
}

```



#### [能量项链](https://www.luogu.com.cn/problem/P1063)



```cpp
#include <bits/stdc++.h>
using namespace std;
int f[405][405];
int n,a[205]; 
int main()
{
    cin >> n;
    for(int i=1;i<=n;i++)   
    {
        cin >> a[i];
        a[n+i]=a[i];
    } 
    for(int i=2;i<=n+1;i++)
    {
        for(int l=1;l+i-1<=2*n;l++)   
        {
            int r=l+i-1;
            for(int k=l+1;k<=l+i-2;k++)
                f[l][r]=max(f[l][r],f[l][k]+f[k][r]+a[l]*a[k]*a[r]); 
        }
    }
    int res=0;
    for (int i=1;i<=n;i++) res=max(res,f[i][n+i]);
    cout << res;
    return 0;
}
```



[HDU:4632-Palindrome subsequence](https://www.cnblogs.com/GoldenFingers/p/9107228.html) 

题意：找到一个字符串里又多少个回文串子序列，要注意子序列的定义哦！


```cpp
#include <stdio.h>
#include <string.h>
#include <algorithm>
using namespace std;
 
const int mod = 10007;
char str[1005];
int dp[1005][1005];
 
int main()
{
    int t,i,j,k,len,cas = 1;
    scanf("%d",&t);
    while(t--)
    {
        scanf("%s",str);
        len = strlen(str);
        for(i = 0; i<len; i++)
            dp[i][i] = 1;//单个字符肯定是一个回文子串
        for(i = 1; i<len; i++)
        {
            for(j = i-1; j>=0; j--)
            {
                dp[j][i] = (dp[j+1][i]+dp[j][i-1]-dp[j+1][i-1]+mod)%mod;
                //之前没有加mod，wa了，
                j~i的区间的回文数是j+1~i与j~i-1区间回文数的和
                //但是要注意这里会有重复的
                if(str[i] == str[j])
                    dp[j][i] = (dp[j][i]+dp[j+1][i-1]+1+mod)%mod;
                //如果区间两头是相等的，则要加上dp[j+1][i-1]+1，
                //因为首尾是可以组成一个回文子串的，
                //而且首尾可以与中间任何一个回文子串组成新的回文子串
            }
        }
        printf("Case %d: %d\n",cas++,dp[0][len-1]);
    }
 
    return 0;
}
```



#### [**括号序列 DP**](https://blog.csdn.net/yjt9299/article/details/78152065) 

状态定义：

`dp[i][j]:表示从s[i~j]至少需要添加几个括号`   //`dp[i][j] `表示从i到j  所需要配对的最小字符个数。

状态转移方程式：

`if(match(s[i],s[j]))`
    `  dp[i][j]=min(dp[i][j],dp[i+1][j-1]);`
`for(int k=i;k<j;k++)//以k做断点（必须枚举判最优，不管是否匹配）`
   `  dp[i][j]=min(dp[i][j],dp[i][k]+dp[k+1][j]);`

```cpp
#include<cstdio>
#include<algorithm>
#include<cstring>
using namespace std;
#define INF 0x3f
int t,n;
char s[102];
int dp[102][102];
bool match(char a,char b)
{
	return (a=='('&&b==')')||(a=='['&&b==']');
}
void print(int i,int j)
{
	if(i>j)return;
	if(i==j)
	{
		if(s[i]=='('||s[j]==')')printf("()");
		else printf("[]");
		return;
	}
	int a=dp[i][j];
	if(match(s[i],s[j])&&a==dp[i+1][j-1])
	{
		printf("%c",s[i]);
		print(i+1,j-1);
		printf("%c",s[j]);
		return;
	}
	for(int k=i;k<j;k++)
		if(a==dp[i][k]+dp[k+1][j])
		{
			print(i,k);print(k+1,j);
			return;
		}
}
int main()
{
	scanf("%d",&t);
	while(t--)
	{
		fgets(s,102,stdin);
		fgets(s,102,stdin);
		n=strlen(s)-1;
		memset(dp,0,sizeof(dp));
		for(int i=0;i<n;i++)
			dp[i+1][i]=0,dp[i][i]=1;
		for(int i=n-2;i>=0;i--)
			for(int j=i+1;j<n;j++)
			{
				dp[i][j]=n;
				if(match(s[i],s[j]))
					dp[i][j]=min(dp[i][j],dp[i+1][j-1]);
				for(int k=i;k<j;k++)
					dp[i][j]=min(dp[i][j],dp[i][k]+dp[k+1][j]);
			}
		print(0,n-1);
		printf("\n");
		if(t)printf("\n");
	}
}
```



思路2：

根据“黑书”的思路，定义：

`d[i][j]`为输入序列从下标i到下标j最少需要加多少括号才能成为合法序列。`0<=i<=j<len `(len为输入序列的长度)。`c[i][j]`为输入序列从下标i到下标j的断开位置，如果没有断开则为-1。

- 当`i==j`时，`d[i][j]`为1 。

- 当`s[i]=='(' && s[j]==')'` 或者 `s[i]=='[' && s[j]==']'`时，`d[i][j]=d[i+1][j-1] ` 。

- 否则`d[i][j]=min{d[i][k]+d[k+1][j]}`,	` i<=k<j `，  `c[i][j]`记录断开的位置k

采用递推方式计算`d[i][j]`




输出结果时采用递归方式输出`print(0, len-1)`

输出函数定义为`print(int i, int j)`，表示输出从下标i到下标j的合法序列。

- 当`i>j`时，直接返回，不需要输出。

- 当`i==j`时，`d[i][j]`为1，至少要加一个括号，如果`s[i]`为`'(' `或者`')'`，输出`"()"`，否则输出`"[]"`。

- 当`i<j`时，如果`c[i][j]>=0`，说明从i到j断开了，则递归调用`print(i, c[i][j]);`和`print(c[i][j]+1, j);`  。如果`c[i][j]<0`，说明没有断开，如果`s[i]=='(' `则输出`'('、 print(i+1, j-1); 和")"`否则输出`"[" print(i+1, j-1);`和`"]"`

黑书上的半括号的那种情况是多余的，包含在`d[i][j]=min{d[i][k]+d[k+1][j]}`这种情况里。

```cpp
#include<stdio.h>
#include<string.h>
#include<iostream>
#include<algorithm>
#define N 305
#define inf 0x3f3f3f
using namespace std;
int dp[N][N],pos[N][N];
char s[N];
void solve()
{
	int i,j,k,d;
	memset(dp,0,sizeof(dp));
	memset(pos,-1,sizeof(pos));
	int len=strlen(s);
	for(i = 1; i < len; i++)
        dp[i][i-1] = 0;
	for(i=1;i<len;i++) dp[i][i]=1;
	
	for(d=1;d<len;d++)
	{
		for(i=0;i<len-d;i++)
		{
			j=d+i;
			dp[i][j]=inf;
			if((s[i] == '(' && s[j] == ')') || (s[i] == '[' && s[j] == ']')){
                dp[i][j]=min(dp[i][j],dp[i+1][j-1]);//i  ，j 字符匹配
            } 
			for(k=i;k<j;k++)
			{
                dp[i][j]=min(dp[i][j],dp[i][k]+dp[k+1][j]);
				pos[i][j]=k;
				//找到使得从i到j中需要配对的括号的个数为最小的k，
                    //也就是在位置k处进行括号配对。 
			}
		}
	}
	
	return ;
}
 
void print(int l,int r)
{
	if(l>r) return ;
	if(l==r){
		if(s[l]=='('||s[l]==')') printf("()");
		else if(s[l]=='['||s[l]==']') printf("[]");
		return ;
	}
	else{
		if(pos[l][r]!=-1)
		{
			print(l,pos[l][r]);
			print(pos[l][r]+1,r);
		}
		else{
			if(s[l]=='('){
				printf("(");
				print(++l,--r);
				printf(")");
			}
			else if(s[l]=='['){
				printf("[");
				print(++l,--r);
				printf("]");
			}
		}
	}
	return ;
}
 
int main()
{
	scanf("%s",s);
	int len=strlen(s);
	solve();
	
	for(int i=0;i<len;i++)
	{
		for(int j=0;j<len;j++)
		{
			printf("%d ",pos[i][j]);
		}
		printf("\n");
	}
	
	print(0,len-1);
	printf("\n");
	return 0;
}
```





#### [**P1086**  施工](http://202.120.222.93:8888/p/P1086)

区间dpdp

`f[i][j]`表示$i$到$j$区间内将高于$a[i] $的楼摧毁所需的代价



```cpp
#include<bits/stdc++.h>
using namespace std;
const int N=505;
int a[N],n,x,y;
long long dp[N][N];
int main() {
	int t;
	scanf("%d",&t);
	while(t--) {
		scanf("%d%d%d",&n,&x,&y);
		for(int i=0; i<=n; i++)
			for(int j=0; j<=n; j++)
				dp[i][j]=0;
		for(int i=1; i<=n; i++)
			scanf("%d",&a[i]);
		for(int i=2; i<=n+1; i++)
			for(int l=0; l+i-1<=n; l++) {
				int r=l+i-1;
				if(a[r]<a[l])dp[l][r]=dp[l][r-1];
				else {
					dp[l][r]=1e18;
					for(int j=l+1; j<r; j++) // 以j为断点
						if(a[j]<=a[r])
							dp[l][r]=min(dp[l][r],dp[l][j-1]+dp[j][r-1]+y);
                    
					dp[l][r]=min(dp[l][r],dp[l][r-1]+x);
				}
			}
		printf("%lld\n",dp[0][n]);
	}
}
```

