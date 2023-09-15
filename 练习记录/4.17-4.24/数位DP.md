# [数位DP学习整理](https://blog.csdn.net/hzf0701/article/details/116717851?ops_request_misc=&request_id=&biz_id=102&utm_term=%E6%95%B0%E4%BD%8DDP&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-1-116717851.nonecase&spm=1018.2226.3001.4187)

数位DP介绍

（dfs 记忆化搜索

数位DP往往都是这样的题型，给定一个闭区间 [ l , r ] ，让你求这个区间中满足某种条件的数的总数。而这个区间可能很大，简单的暴力代码如下：

```cpp
int ans=0;
for(int i=l;i<=r;i++){
    if(check(i))ans++;
}
```

我们发现，若区间长度超过 1e8，我们暴力枚举就会超时了，而数位DP则可以解决这样的题型。数位DP实际上就是在数位上进行 DP。


数位DP解法

​		==数位 DP就是换一种暴力枚举的方式，使得新的枚举方式符合DP的性质，然后预处理好即可==

​		 我们来看：我们可以用 $f(n)$表示$ [ 0 , n ]$的所有满足条件的个数，那么对于 $[ l , r ]$我们就可以用 $[ l , r ]    ⟺    f ( r ) − f ( l − 1 ) $，相当于前缀和思想。

​		那么也就是说我们只要求出$ f ( n )$即可。那么数位DP==关键==的思想就是==从树的角度来考虑。将数拆分成位，从高位到低位开始枚举==。我们可以视 N为 n位数，那么我们拆分$N:a_{n}、a_{n-1}...a_1$ 。那么我们就可以开始分解建树，如下。之后我们就可以预处理再求解 $f(n)$了，个人认为求解$f(n)$是最难的一步。


![img](%E6%95%B0%E4%BD%8DDP.assets/cfc37954b97e29aa1d848925105fec1b.png)

## -数位DP资料

1.[数位DP模板详解_AC__dream的博客-CSDN博客](https://blog.csdn.net/AC__dream/article/details/123168715?ops_request_misc=%7B%22request%5Fid%22%3A%22164759937016780271527937%22%2C%22scm%22%3A%2220140713.130102334.pc%5Fblog.%22%7D&request_id=164759937016780271527937&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_ecpm_v1~rank_v31_ecpm-1-123168715.nonecase&utm_term=数位DP&spm=1018.2226.3001.4450) 

2.[浅谈数位DP](https://www.cnblogs.com/zbtrs/p/6106783.html)

[3.oiwiki](https://oi-wiki.org/dp/number/)

## -经典例题

### [例题1：度的数量](https://www.acwing.com/activity/content/11/)

题面

求给定区间$ [X,Y]$ 中满足下列条件的整数个数：这个数恰好等于 K  个互不相等的 B  的整数次幂之和。例如，设 X = 15 , Y = 20 , K = 2 , B = 2 ，则有且仅有下列三个数满足题意：
$17=2^4+2^0 $ 
$18=2^4+2^1 $ 
$20=2^4+2^2 $ 
输入格式
第一行包含两个整数 X 和 Y，接下来两行包含整数 K K K 和 B B B。
输出格式
只包含一个整数，表示满足条件的数的个数。

>数据范围
>1 ≤ X ≤ Y ≤ 2 31 − 1 , 1≤X≤Y≤2^{31}−1, 1≤X≤Y≤231−1,
>1 ≤ K ≤ 20 , 1≤K≤20, 1≤K≤20,
>2 ≤ B ≤ 10 2≤B≤10 2≤B≤10
>输入样例：
>15 20
>2
>2
>输出样例：
>3



![image-20230418134027222](%E6%95%B0%E4%BD%8DDP.assets/image-20230418134027222.png)

 

`f[i][j]` : 表示还剩下 i  位没有填，且需要填写 j  个 1 的方案数。

```cpp
/**
  *@filename:度的数量
  *@author: pursuit
  *@csdn:unique_pursuit
  *@email: 2825841950@qq.com
  *@created: 2021-05-12 11:23
**/
#include <bits/stdc++.h>

using namespace std;

typedef long long ll;
const int maxn = 100000 + 5;
const int mod = 1e9+7;

int l,r,k,b;
int f[35][35];
//首先我们先预处理f数组。其中f[i][j]表示剩下还有i个没填，需要填写j个1的方案数。
void init(){
    for(int i=0;i<35;i++){
        for(int j=0;j<=i;j++){
            if(!j)f[i][j]=1;
            else{
                f[i][j]=f[i-1][j]+f[i-1][j-1];
            }
        }
    }
}
int dp(int n){
    //求解f(n)。我们需要避免n为0的情况，这里需要特判。
    if(!n)return 0;
    vector<int> nums;//将n分割，存储位数。
    while(n){
        nums.push_back(n%b);
        n/=b;
    }
    int ans=0;//答案。
    int last=0;//前面的信息，这里代表的是前面分支选取了多少个1.
    for(int i=nums.size()-1;i>=0;i--){
        int x=nums[i];
        if(x){
            //说明x>0，我们可以选择左边分支填0.
            ans+=f[i][k-last];
            if(x>1){
                //当x>1我们才可以枚举左边分支填1.
                if(k-last-1>=0){
                    //如果还可以填1的话。
                    ans+=f[i][k-last-1];
                }
                break;//因为右边分支只能为0或1，所以不符合条件。break。
            }
            else{
                //当x=1就可以进入右边的分支继续讨论。
                last++;
                if(last>k)break;
            }
        }
        //考虑到最后一位，如果符合条件那么末位填0也算一种方案。
        if(!i&&last==k)ans++;
    }
    return ans;
}
void solve(){
}
int main(){
    cin>>l>>r>>k>>b;
    init();
    cout<<dp(r)-dp(l-1)<<endl;
    solve();
    return 0;
}

```



### [例题2：计数问题](https://www.acwing.com/problem/content/340/)



![QQ浏览器截图20210315122504.png](%E6%95%B0%E4%BD%8DDP.assets/d9cff4c573361692ac8f6cef1b47a916.png)



<img src="%E6%95%B0%E4%BD%8DDP.assets/image-20230418141834640.png" alt="image-20230418141834640" style="zoom: 200%;" />

`f[i,j,u]` : 表示 i 位，最高位为 j 的数拥有 u 的个数



//好像有点问题 wa30(初始化的位数放少了qaq)

```cpp
/**
  *@filename:计数问题
  *@author: pursuit
  *@csdn:unique_pursuit
  *@email: 2825841950@qq.com
  *@created: 2021-05-12 13:12
**/
#include <bits/stdc++.h>

using namespace std;

typedef long long ll;
const int maxn = 100000 + 5;
const int mod = 1e9+7;

int l,r;
int f[11][10][10];//预处理f数组。其中f[i][j][u]表示i位最高位为j的数拥有u的个数。
void init(){
    for(int i=0;i<10;i++)f[1][i][i]=1;
    for(int i=2;i<13;i++){ //i<11 -> i<13
        for(int j=0;j<10;j++){
            for(int u=0;u<10;u++){
                //判断j是否等于u。
                if(j==u)f[i][j][u]+=pow(10,i-1);
                for(int k=0;k<10;k++){
                    f[i][j][u]+=f[i-1][k][u];
                }
            }
        }
    }
}
ll dp(int n,int u){
    //1~n,求x的出现次数。
    if(!n)return u?0:1;//特判n是否为0.根据u的值确定返回值。
    vector<int> nums;//存储分割后的位数。
    while(n)nums.push_back(n%10),n/=10;
    int last=0;//last记录前面u出现的次数。
    ll ans=0;//答案。
    for(int i=nums.size()-1;i>=0;i--){
        int x=nums[i];
        //左边分支，0~x。
        for(int j=(i==nums.size()-1);j<x;j++){
            //由于此题不能有前导0.
            ans+=f[i+1][j][u];//注意这里i需要+1，因为我们i下标从0开始。而位数从1开始。
        }
        //走左边分支，那么我们需要加上前面的个数。注意这里需要乘上x，因为左边分支有x中选择。
        ans+=x*last*pow(10,i);
        if(x==u)last++;//记录last。
        if(!i)ans+=last;//加上这个数本身含有的。
    }
    //由于我们前面都是枚举n位数的，我们还需要统计所有0~n-1位数的方案数量。
    //例如000011是不合法的，但11是合法的。
    //这一步确实很容易忽略，没办法，数位DP就是这么难。
    for(int i=1;i<nums.size();i++){
        for(int j=(i!=1);j<=9;j++){
            ans+=f[i][j][u];
        }
    }
    return ans;
}
void solve(){
}
int main(){
    init();
    while(cin>>l>>r&&(l||r)){
        if(l>r)swap(l,r);
        for(int i=0;i<=9;i++){
            cout<<dp(r,i)-dp(l-1,i);
            i==9?cout<<endl:cout<<" ";
        }
    }
    solve();
    return 0;
}

```

wa30(初始化的位数放少了qaq)

```cpp
# include <iostream>
# include <cmath>
using namespace std;

int dgt(int n) // 计算整数n有多少位
{
    int res = 0;
    while (n) ++ res, n /= 10;
    return res;
}

int cnt(int n, int i) // 计算从1到n的整数中数字i出现多少次 
{
    int res = 0, d = dgt(n);
    for (int j = 1; j <= d; j ++) // 从右到左第j位上数字i出现多少次，所有位上的次数加起来就是i出现的总次数
    {
        // l和r是第j位左边和右边的整数 (视频中的abc和efg); dj是第j位的数字
        int p = pow(10, j - 1), l = n / p / 10, r = n % p, dj = n / p % 10;
        // 计算第j位左边的整数小于l (视频中xxx = 000 ~ abc - 1)的情况
        if (i) res += l * p; 
        if (!i && l) res += (l - 1) * p; // 如果i = 0, 左边高位不能全为0(视频中xxx = 001 ~ abc - 1)，并且&&l表示这时i也不能在最高位出现。
        // 计算第j位左边的整数等于l (视频中xxx = abc)的情况
        if ( (dj > i) && (i || l) ) res += p;  //(i || l)表示i=0时，i不能出现在最高位（即l不能为0），因为这种数是不存在的
        if ( (dj == i) && (i || l) ) res += r + 1;  //(i || l)表示i=0时，i不能出现在最高位（即l不能为0），因为这种数是不存在的
    }
    return res;
}

int main()
{
    int a, b;
    while (cin >> a >> b , a)
    {
        if (a > b) swap(a, b);
        for (int i = 0; i <= 9; ++ i) cout << cnt(b, i) - cnt(a - 1, i) << ' ';
        cout << endl;
    }
    return 0;
}

 
```



dfs

```cpp
#include <bits/stdc++.h>
using namespace std;

int dp[10][10][2][2];
int calc(int num, int x)
{
    memset(dp, -1, sizeof dp);
    auto digit = to_string(num);
    // 当前位数u, 统计次数cntx, 是否被限制, 前面是否选择
    function<int(int, int, bool, bool)> f = [&](int u, int cntx, bool is_limit, bool is_num) {
        if (u == digit.size())
            return cntx;
        
        if (dp[u][cntx][is_limit][is_num] >= 0) 
            return dp[u][cntx][is_limit][is_num];
            
        int res = 0;
        if (!is_num)
            res += f(u + 1, cntx, false, false);
            
        int up = is_limit ? digit[u] - '0' : 9;
        for (int d = is_num ? 0 : 1; d <= up; ++d)
            res += f(u + 1, cntx + (d == x), is_limit && (d == up), true);
            
        return dp[u][cntx][is_limit][is_num] = res;
    };
    return f(0, 0, true, false);
}

int main()
{
    int a, b;
    while (cin >> a >> b, a || b)
    {
        if (a > b) swap(a, b);
        for (int i = 0; i < 10; ++i)
            cout << calc(b, i) - calc(a - 1, i) << " \n"[i == 9];
    }
    return 0;
}

```







### [二进制问题](https://blog.csdn.net/qq_54468377/article/details/124519501?spm=1001.2101.3001.6650.2&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-124519501-blog-125278665.235%5Ev29%5Epc_relevant_default_base3&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-124519501-blog-125278665.235%5Ev29%5Epc_relevant_default_base3&utm_relevant_index=5)



#### 典型：limit pos

```cpp
#include<iostream>
#include<cstdio>
#include<cstring>
#include<cmath>
#include<algorithm>
#include<queue>
#include<vector>
using namespace std;
const int N=63;
long long f[N][N];
int a[N];
int k;
long long dfs(int pos,int cnt,int limit)
{
	if(!pos) return cnt==k;
	if(!limit&&f[pos][cnt]!=-1) return f[pos][cnt];
	int up=limit?a[pos]:1;
	long long ans=0;
	for(int i=0;i<=up;i++)
		ans+=dfs(pos-1,cnt+(i==1),limit&&(i==up));
	if(!limit) f[pos][cnt]=ans;
	return ans;
}
long long solve(long long x)
{
	int pos=0;
	memset(f,-1,sizeof f);
	while(x)
	{
		a[++pos]=x%2;
		x/=2;
	}
	return dfs(pos,0,1);
}
int main()
{
	long long n;
	cin>>n>>k;
	cout<<solve(n);
	return 0;
}
```





### [例题4：windy数](https://www.luogu.com.cn/problem/P2657)

同样，我们先进行预处理 f 数组，其中`f[i][j] `表示 i 位，其中最高位为j的方案数。那么根据题意，状态转移方程即为 $f[i][j]=\sum_{}f[i-1][k] $，其中$ 0 \leq k \leq 9 \space and \space abs(k-j)>=2 $ 。 而初始状态即为 `f[1][i] = 1  `预处理完之后就好处理了，这里不再提供思路，请大家自己画出树结构并完成此题。


==0,1,2,3,4...9都属于windy数==

```cpp
#include <bits/stdc++.h>
#define int long long 
using namespace std;

typedef long long ll;
const int maxn = 100000 + 5;
const int mod = 1e9+7;

int l,r;
int f[11][10] ; //[i][j]表示i位，其中最高位为j的方案数。
void init(){
	for(int i=0;i<10;i++) f[1][i]=1;
	for(int i=2;i<=10;i++){
		for(int j=0;j<=9;j++){
		//从第二位开始 每次枚举最高位j 并找到k 使得j-k>=2 
			for(int k=0;k<=9;k++){
				if(abs(j-k)>=2){
					f[i][j]+=f[i-1][k];
				}
			}
		}
	}
}
int dp(int n){
     if(n==0) return 0;
     vector<int> nums;
     int last=-2; // 存储上一位的值
     //这里初值为-2,是因为我们需要确定1可以。
	 int ans=0;
	 while(n) nums.push_back(n%10) ,n/=10;
	 for(int i=nums.size()-1;i>=0;i--){
	 	int x=nums[i]; //左分支
		 for(int j=(i==nums.size()-1);j<x;j++){
		 	//因为首位不能为0，所在枚举最高位时，j从1开始
			 if(abs(j-last)>=2){
			 	ans+=f[i+1][j];
			 }
		 } 
		 if(abs(x-last)<2) break;
	 	 last=x;
	 	 if(i==0) ans++;//枚举到最后一位，自身也形成了一种方案。
	 } 
	 //???   特殊枚举有前导0的数。
	 for(int i=1;i<nums.size();i++){
	 	for(int j=1;j<=9;j++){
	 		ans+=f[i][j];
		 }
		 
	 } 
	 return ans;
	 
}
 
signed main(){
    init();
    cin>>l>>r;
    cout<<dp(r)-dp(l-1)<<endl;
     
    return 0;
}

```



## [记忆化搜索法](https://zhuanlan.zhihu.com/p/348851463)

### (**[HDU2089 不要62](https://link.zhihu.com/?target=http%3A//acm.hdu.edu.cn/showproblem.php%3Fpid%3D2089)**)

>**Problem Description**
>杭州人称那些傻乎乎粘嗒嗒的人为62（音：laoer）。
>杭州交通管理局经常会扩充一些的士车牌照，新近出来一个好消息，以后上牌照，不再含有不吉利的数字了，这样一来，就可以消除个别的士司机和乘客的心理障碍，更安全地服务大众。
>不吉利的数字为所有含有4或62的号码。例如：
>62315 73418 88914
>都属于不吉利号码。但是，61152虽然含有6和2，但不是62连号，所以不属于不吉利数字之列。
>你的任务是，对于每次给出的一个牌照区间号，推断出交管局今次又要实际上给多少辆新的士车上牌照了。
>**Input**
>输入的都是整数对n、m（0<n≤m<1000000），如果遇到都是0的整数对，则输入结束。
>**Output**
>对于每个整数对，输出一个不含有不吉利数字的统计个数，该数值占一行位置。

为了简化问题，我们只需要求出  内符合条件的值，以及  内符合条件的值，再把两者相减即可。首先，我们要把数字拆成数位的数组，一般我喜欢从高位到低位存储，这样需要`reverse`一下：

```cpp
cnt = 0;
while (x)
    A[cnt++] = x % 10, x /= 10;
reverse(A, A + cnt);
```

我们一般使用**记忆化搜索**的方法来实现数位DP。例如，如果我们要求 231756 以内符合条件的数，我们只需要知道形如 $0????? $、$1?????$  或 $2?????$ ，且小于等于原数的符合条件的数的数量即可。

这样直接递归地搜索下去，会遍历所有范围内的值，所以我们要记忆化。数位DP和其他很多DP一样，减少复杂度的核心就是合并相同状态。例如在本题中，$ 106???$ 和 $206???$ 的答案是一样的，所以他们可以当作同样的状态。当我们搜到$ 206???$时，发现这种状态的答案已经被记录过了，于是可以直接返回。

不过你肯定发现，上面的 $2?????$ 和另两种不同，因为它的第一个  ? 只能取 0,1,2,3 。所以我们引入一个常用的状态$limit$  。它表示，当前位是最多只能取到原数这一位的值，还是可以任意取 $0~9$ 。显然，某位 $limit$ 为 1   当且仅当上一位  $limit$为 1 且上一位已取到最大值。

对于本题而言，除了 $limit$ 和代表正在处理的位数的 $pos$ 外，只需要确定上一位的数字（$last$  ），就可以确定一个状态，所以代码如下：

```cpp
#include <algorithm>
#include <cstring>
#include <iostream>
using namespace std;
int A[8], cnt, dp[8][12][2];
int dfs(int pos, int last, bool limit)
{
    int ans = 0;
    if (pos == cnt)
        return 1; // 搜索终点
    if (dp[pos][last][limit] != -1)
        return dp[pos][last][limit];
    for (int v = 0; v <= (limit ? A[pos] : 9); ++v) // 根据是否limit决定循环上界
    {
        if (last == 6 && v == 2 || v == 4) // 舍弃不合法解
            continue;
        ans += dfs(pos + 1, v, limit && v == A[pos]);
    }
    dp[pos][last][limit] = ans;
    return ans;
}
int f(int x)
{
    cnt = 0;
    memset(A, 0, sizeof(A));
    memset(dp, -1, sizeof(dp)); // 初始化dp数组为-1
    while (x)
        A[cnt++] = x % 10, x /= 10;
    reverse(A, A + cnt);
    return dfs(0, 11, true);    // 用last为11表示不存在上一位
}
int main()
{
    ios::sync_with_stdio(false);
    int x, y;
    while (cin >> x >> y, x || y)
    {
        int l = f(x - 1), r = f(y);
        cout << r - l << endl;
    }
    return 0;
}
```



### **[洛谷P2602 [ZJOI2010\]数字计数](https://link.zhihu.com/?target=https%3A//www.luogu.com.cn/problem/P2602)**





### [M. XOR Sum(数位dp 数位背包)](https://blog.csdn.net/Code92007/article/details/127840174)





[知乎](https://zhuanlan.zhihu.com/p/583717989)



[CCPC](https://www.cnblogs.com/lunasama/p/16890445.html)

```cpp
int a[105];
int n, m, k;
map<int, int>dp[105][105];
int dfs(int cur, int s, int lv) {
    if (lv < 0)return 0;
    if (cur < 0)return lv == 0;
    int s1 = k / 2, s0 = k - s1;
    if (((1ll << cur + 1) - 1) * s0 * s1 < lv)return 0;
    if (dp[cur][s].count(lv))return dp[cur][s][lv];
    int res = 0;
    if (a[cur] == 1) {
        for (int i = 0; i <= s; i++) {
            for (int j = 0; j <= k - s; j++) {
                int val = 1ll * (k - i - j) * (i + j) * (1ll << cur);
                int t = c[s][i] * c[k - s][j] % mod;
                res += t * dfs(cur - 1, i, lv - val) % mod;
                res %= mod;
            }
        }
    }
    else {
        for (int i = 0; i <= 0; i++) {
            for (int j = 0; j <= k - s; j++) {
                int val = 1ll * (k - i - j) * (i + j) * (1ll << cur);
                int t = c[s][i] * c[k - s][j] % mod;
                res += t * dfs(cur - 1, s, lv - val) % mod;
                res %= mod;
            }
        }
    }
    return dp[cur][s][lv] = res;
}
void slove() {
    c[0][0] = 1;
    c[1][0] = c[1][1] = 1;
    for (int i = 2; i <= 100; i++) {
        c[i][0] = 1;
        for (int j = 1; j <= 100; j++) {
            c[i][j] = c[i - 1][j] + c[i - 1][j - 1];
        }
    }
    cin >> n >> m >> k;
    int t = m, id = 0;
    while (t)a[id++] = t % 2, t /= 2;
    id--;
    cout << dfs(id, k, n) << endl;
}
```



```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=42,M=256,K=19,mod=1e9+7;
ll n,m,dp[N][M][K],c[K][K];
int k,a[N];
ll dfs(int x,int r,int cur){
	if(r>=M)return 0;
	if(x==-1)return r==0;
	if(~dp[x][r][cur])return dp[x][r][cur];
	ll &ans=dp[x][r][cur];ans=0;
	int nb=(x==0?0:(n>>(x-1)&1));
	//printf("x:%d ax:%d\n",x,a[x]);
	if(a[x]==0){
		for(int i=0;i<=k-cur;++i){
			int nr=r-i*(k-i);
			if(nr<0)continue;
			ans=(ans+1ll*c[k-cur][i]*dfs(x-1,(nr<<1)|nb,cur)%mod)%mod;
		}
	}
	else{
		for(int i=0;i<=cur;++i){
			for(int j=0;j<=k-cur;++j){
				int nr=r-(i+j)*(k-(i+j));
				//printf("x:%d r:%d cur:%d i:%d j:%d nr:%d\n",x,r,cur,i,j,nr);
				if(nr<0)continue;
				ans=(ans+1ll*c[cur][i]*c[k-cur][j]%mod*dfs(x-1,(nr<<1)|nb,i)%mod)%mod;
			}
		}
	}
	//printf("x:%d r:%d cur:%d ans:%lld\n",x,r,cur,ans);
	return ans;
}
ll cal(){
	if(k==1)return !n;
	if(!m)return !n;
	memset(dp,-1,sizeof dp);
	int c=0;
	for(ll x=m;x;x>>=1){
		a[c++]=x%2;
	}
	ll rn=0;
	for(int i=c;i<=50;++i){
		if(n>>i&1){
			rn+=1ll<<(i-c);
			if(rn>=M)return 0;
		}
	}
	return dfs(c,(int)rn,k);
}
int main(){
	c[0][0]=1;
	for(int i=1;i<K;++i){
		c[i][0]=c[i][i]=1;
		for(int j=1;j<i;++j){
			c[i][j]=(c[i-1][j]+c[i-1][j-1])%mod;
		}
	}
	cin>>n>>m>>k;
	cout<<cal()<<endl;
	return 0;
}
```





[Fun with Stones](https://blog.csdn.net/yanweiqi1754989931/article/details/127340465)

```cpp
#include <bits/stdc++.h>
#pragma gcc optimize("O2")
#pragma g++ optimize("O2")
#define int long long
#define endl '\n'
using namespace std;

const int N = 2e5 + 10, mod = 1e9 + 7;
int l1,r1,l2,r2,l3,r3;
int dp[40][10];
int way[]={0,3,5,6};
int qpow(int x,int y,int res=1){
    for(;y;y>>=1,(x*=x)%=mod) if(y&1) (res*=x)%=mod;
    return res;
}
int ck(int x,int y,int z){
    int res=0;
    for(int i=0;i<3;i++){
        int fg1=((x>>i)&1),fg2=((y>>i)&1),fg3=((z>>i)&1);
        if(fg1!=fg2){
            res+=(fg1<<i);
        }
        else{
            res+=(fg3<<i);
        }
    }
    return res;
}
int dfs(int x,int y,int z){
    memset(dp,0,sizeof dp);
    dp[0][0]=1;
    for(int i=0;i<32;i++){
        int fg1=((x>>i)&1),fg2=((y>>i)&1),fg3=((z>>i)&1);
        int now=fg1*4+fg2*2+fg3;
        for(auto t:way){
            for(int j=0;j<8;j++){
                (dp[i+1][ck(t,now,j)]+=dp[i][j])%=mod;
            }
        }
    }
    return dp[32][0];
}
inline void solve(){
    cin>>l1>>r1>>l2>>r2>>l3>>r3;
    int ans1=dfs(r1,r2,r3),
        ans2=dfs(r1,r2,l3-1),
        ans3=dfs(r1,l2-1,r3),
        ans4=dfs(r1,l2-1,l3-1),
        ans5=dfs(l1-1,r2,r3),
        ans6=dfs(l1-1,r2,l3-1),
        ans7=dfs(l1-1,l2-1,r3),
        ans8=dfs(l1-1,l2-1,l3-1);
    int fenzi=((ans1-ans2-ans3+ans4-ans5+ans6+ans7-ans8)%mod+mod)%mod;
    int fenmu=(r1-l1+1)*(r2-l2+1)%mod*(r3-l3+1)%mod;
    cout<<(mod+1-fenzi*qpow(fenmu,mod-2)%mod)%mod;
}

signed main(){
    ios_base::sync_with_stdio(false), cin.tie(0);
    cout << fixed << setprecision(12);
    int t = 1; // cin >> t;
    while(t--) solve();
    return 0;
}

```

