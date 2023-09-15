[TOC]



### 优化输入

#### 1.快读

~~~c++
#include <iostream>
#include <cstdio>
using namespace std;
#define ull unsigned long long //防止不开long long见祖宗
#define ll unsigned long long
ull n,k,sum[1000005],cnt;

ll qr()//快读，让您的排名更好看
{
    ll ret=0;
    char c=getchar();
    while (c<'0'||c>'9')
        c=getchar();
    while (c>='0'&&c<='9')
    {
        ret=(ret<<1)+(ret<<3)+c-'0';
        c=getchar();
    }
    return ret;
}
~~~

读取十进制整数

~~~c++
inline int read(int &x)
{
	x=0;
	int f=1;
	char c=getchar();
	while(c>'9'||c<'0')
	{
		if(c=='-') f=-1;
		c=getchar();
	}
	while(c>='0'&&c<='9') x*=10,x+=c-'0',c=getchar();
	x*=f;
}//读完后，是数字的下一个字符
//这是一种任意十进制快速读法
//-------------------------------------
//优化方法如下

inline int read()
{
	int x=0;
    char c=getchar();
    while(c<48||c>47)//c<'0'||c>'9'
    	c=getchar();
    while(c>47&&c<58) x*=10,x+=c-48,c=getchar()
    return x;
}//仅能读正整数

~~~

~~~c++
int n,m,sum[M],Ans,Mid,R,L;
inline int read() {
	reg int ret=0;reg bool flag=0;reg char c=getchar();
	while((c<'0')|(c>'9')) flag^=!(c^'-'),c=getchar();
	while((c>='0')&(c<='9')) ret=(ret<<3)+(ret<<1)+(c^'0'),c=getchar();
	return flag?-ret:ret;
}
int main(){
     n = read(),m = read();
}
~~~



~~~c++
inline int read()
{
    int x=0,k=1; char c=getchar();
    while(c<'0'||c>'9'){if(c=='-')k=-1;c=getchar();}
    while(c>='0'&&c<='9')x=(x<<3)+(x<<1)+(c^48),c=getchar();
    return x*k;
}
~~~



#### 2.未知数目的输入

`while(cin>>a>>b)`

`whle(~(scanf("%d",&a)))`

``

#### 3.提高cin速率

~~~c++
ios::sync_with_stdio(false);
	cin.tie(nullptr);

	cin >> n >> m ;
~~~



### 常用的宏

#### my_acummulation

~~~c++
#include<bits/stdc++.h>
using namespace std;
#define MAXN 110
#define int long long
#define inf 0x3f3f3f3f3f3f3f3f
#define inf2 0x7fffffff
#define pii pair<int, int>
#define fr first
#define sc second
#define ；;
#define PI acos(-1) //此法求出的PI精度不是很高 
#define fast std::ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define multi int _;cin>>_;while(_--)
typedef long long ll;
const int mod=1e9+7;
const int N = 1e6+10;
ll gcd(ll a,ll b){ return b?gcd(b,a%b):a;}
ll lcm(ll a,ll b){ return (a*b)==0?0:a*b/gcd(a,b);}
priority_queue<pair<int,int>pr;
vector<pair<int,int>>vp;
greater<pair<int,int>>>hp;
 

signed main() {
	fast
    //freopen("1.in","r",stdin);
        
	return 0;
}
/** 头文件大全
#include <iostream>
#include <algorithm>
#include <cstring>
#include <string>
#include <vector>
#include <map>
#include <set>
#include <list>
#include <deque>
#include <queue>
#include <stack>
#include <cstdlib>
#include <cstdio>
#include <cmath>
#include <iomanip>
*/
~~~







#### lgt的

~~~c++
#include<bits/stdc++.h>
using namespace std;
#define int long long
//#define ll __int128  需要自己另写输入输出函数
#define endl "\n"
#define fi first
#define se second
#define pb push_back 
#define inf 1e16
#define eps 1e-14
#define fast std::ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
const int mod=998244353;
const int maxn=5e5+100;

//void solve(){}

signed main(){ //注意！这里是signed main()
    fast
    int _=1;
//  cin>>_;
    for(int i=1;i<=_;i++){
//      printf("Case #%d: ",i);
        //solve();
    }
    return 0;
}
/*
When you are coding,remember to:
    - clear the arrays if a problem has many tasks.
    - pay attention to some special cases(n=0,1).
    - Don't code before think completely.
    - ...
*/
~~~



#### `__int128`

~~~c++
#include<bits/stdc++.h>
#define ll __int128
using namespace std;
void print(ll x)
{
    if (x < 0)    putchar('-'), x = -x;
    if (x / 10)    print(x / 10);
    putchar(x % 10 + '0');
}
int main(){
    int n,m;
    ll b=1; cin>>n>>m;
    ll y=m;
    for(int i=1;i<m;i++){
        b*=n;
    }
    ll g=__gcd(b,y);
    ll x=b/g; y/=g;
    print(y);
    cout<<"/";
    print(x);
}
~~~



#### zhy-

~~~c++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
#define rep(i,a,n) for(int i=a;i<n;i++)
#define per(i,a,n) for(int i=n-1;i>=a;i--)
ll gcd(ll a,ll b){ return b?gcd(b,a%b):a;}

int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    //freopen("1.in","r",stdin);
    getprime();
    //right = 1230;
    int n;
    while(cin>>n&&n!=0)
    {
        solve(n);
    }
    return 0;
}

~~~



#### xwy的

~~~c++
#define int long long
/*template <typename T>
void read(T& x) {
    char c = getchar();
    char s = 1;
    x = 0;
    while (c < '0' || c > '9') {
        if (c == '-') s = -1;
        c = getchar();
    }
    while (c >= '0' && c <= '9') {
        x = x * 10 + c - '0';
        c = getchar();
    }
    x *= s;
}
template <typename T, typename... Args>
void read(T& first, Args&... rest) {
    read(first);
    read(rest...);
}*/
inline int read(int &x) { return scanf("%lld", &x); }
inline int read(int &x, int &y) { return (~read(x)) ? read(y) : -1; }
inline int read(int &x, int &y, int &z) { return (~read(x, y)) ? read(z) : -1; }
#define pii pair<int, int>
#define fr first
#define sc second
#define rep(i, a, b) for (auto i = a; i <= b; ++i)
#define dep(i, a, b) for (auto i = a; i >= b; --i)
#define ls rt << 1
#define rs rt << 1 | 1
#define all(it, a) for (auto it = a.begin(); it != a.end(); it++)
#define endl "\n"
const int maxn = 2e6 + 7;
const int mod = 1e9 + 7;
const int one = 1;
inline int qpow(int a, int b, int c = 1) {
    for (; b; b >>= 1, a = a * a % mod)
        if (b & 1) c = c * a % mod;
    return c;
}
~~~



12.4

#### wiki-zhou

~~~cpp
#include <bits/stdc++.h>
using namespace std;
char __split_and_end[2] = {' ', 0};
inline int read(int &x) { return scanf("%d", &x); }
inline int read(long long &x) { return scanf("%lld", &x); }
inline int read(unsigned int &x) { return scanf("%d", &x); }
inline int read(unsigned long long &x) { return scanf("%lld", &x); }
inline int read(char *s) { return scanf("%s", s); }
inline int read(char &x) { return scanf("%c", &x); }
inline int read(double &x) { return scanf("%lf", &x); }
inline int read(long double &x) { return scanf("%Lf", &x); }
template <typename U, typename V>
inline int read(const pair<U, V> &t)
{
    if (read(t.first) == -1)
        return -1;
    return read(t.second);
}
template <typename T>
inline T read()
{
    T x;
    read(x);
    return x;
}
template <typename T>
inline int readArray(T *f, T *l)
{
    for (; f != l; f++)
    {
        if (read(*f) == -1)
            return -1;
    }
    return 0;
}
template <typename T, typename... Args>
int read(T &first, Args &...rest)
{
    if (read(first) == -1)
        return -1;
    return read(rest...);
}
template <typename T, typename... Args>
inline void print(const T &first, const Args &...rest);
inline void print(const int &x) { printf("%d", x); }
inline void print(const long long &x) { printf("%lld", x); }
inline void print(const unsigned int &x) { printf("%d", x); }
inline void print(const unsigned long long &x) { printf("%lld", x); }
inline void print(const char *s) { printf("%s", s); }
inline void println(const char *s) { puts(s); }
inline void print(char *s) { printf("%s", s); }
inline void println(char *s) { puts(s); }
inline void print(const string &s) { print(s.c_str()); }
inline void println(const string &s) { puts(s.c_str()); }
inline void print(const char &x) { printf("%c", x); }
inline void print(const double &x) { printf("%lf", x); }
template <typename U, typename V>
inline void print(const pair<U, V> &t)
{
    print(t.first);
    print(' ');
    print(t.second);
}
template <typename T>
inline void print(const vector<T> &t)
{
    for (auto it = t.begin(); it != t.end(); it++)
        print(*it, __split_and_end[next(it) == t.end()]);
}
template <typename T>
inline void print(const set<T> &t)
{
    for (auto it = t.begin(); it != t.end(); it++)
        print(*it, __split_and_end[next(it) == t.end()]);
}
template <typename T>
inline void print(const multiset<T> &t)
{
    for (auto it = t.begin(); it != t.end(); it++)
        print(*it, __split_and_end[next(it) == t.end()]);
}

template <typename T>
inline void printArray(T *first, T *last)
{
    for (T *it = first; it != last; ++it)
        print(*it), putchar(__split_and_end[next(it) == last]);
}
template <typename T, typename... Args>
inline void print(const T &first, const Args &...rest)
{
    print(first);
    print(rest...);
}
template <typename T>
inline void printlnArray(T *first, T *last)
{
    printArray(first, last);
    putchar('\n');
}
template <typename T>
inline void println(const T &t)
{
    print(t, '\n');
}
template <typename T, typename... Args>
inline void println(const T &first, const Args &...rest)
{
    print(first);
    println(rest...);
}
#define in :
#define var auto
#define final const
#define readonly const
#define ref &
#define pii pair<int, int>
#define pbb pair<double, double>
#define fi first
#define se second
#define rep(i, a, b) for (auto i = a; i <= b; i++)
#define dep(i, a, b) for (auto i = a; i >= b; --i)
#define lc now << 1
#define rc now << 1 | 1
#define lson lc, l, mid
#define rson rc, mid + 1, r
#define range(it, a) for (auto it = a.begin(); it != a.end(); it++)
#define endl "\n"
#define N 10004
#define inf 0x3f3f3f3f3f3f3f3f
#define int long long
#define mod 1000000007
int lg[N];
int deep[N], fa[N][20];
int head[N], Next[N << 1], ver[N << 1], tot;

 
signed main()
{

    lg[1] = 0;
    rep(i, 2, N - 1) lg[i] = lg[i / 2] + 1;
    char filename[20], Filename[20];
    // for (int j = 1; j <= 50; ++j)
    // {
    //     freopen("CON", "w", stdout);
    //     cout << j << endl;
    //     sprintf(Filename, "%d.out", j);
    //     freopen(Filename, "w", stdout);
    //     sprintf(filename, "%d.in", j);
    //     freopen(filename, "r", stdin);
    
    // }
}

~~~

