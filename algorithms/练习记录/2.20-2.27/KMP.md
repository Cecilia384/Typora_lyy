KMP板子acwing

```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define fast std::ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
const int N=1e5+10;
const int M=1000010;
int n,m;
int ne[M];// next[]数组
char s[N],p[M];
// KMP 字符符匹配算法
void solve(){
    cin>>m>>p+1>>n>>s+1;//字符串下标从1开始

	//求next[]数组
    //字符串下标从1开始
	for(int i=2,j=0;i<=m;i++){
		while(j && p[i]!=p[j+1]) j=ne[j];
		if(p[i]==p[j+1]) j++;
		ne[i]=j;
	}
	//匹配操作
	for(int i=1,j=0;i<=n;i++){
		while(j && s[i]!=p[j+1]) j=ne[j];
		if(s[i]==p[j+1]) j++;
		if(j==m){ //满足匹配条件，打印开头下标, 从0开始
			//匹配完成后的具体操作
             //如：输出以0开始的匹配子串的首字母下标
			printf("%d ", i - m);// (若从1开始，加1)
			j=ne[j];
		} 
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



```cpp
#include<bits/stdc++.h>
using namespace std;
//#define int long long
#define ll long long
const int maxn=1e6+10;
const int N=2e9+10;

int ne[maxn]; 
char s[maxn],t[maxn];
 
signed main()
{
    cin>>s+1>>t+1;
    int ls=strlen(s+1);
	int lt=strlen(t+1);
	int j=0;
	//求next数组 
	for(int i=2;i<=lt;i++){
		while(j&&t[i]!=t[j+1]){
			j=ne[j];
		}
		if(t[i]==t[j+1]){
			j++;
		}
		ne[i]=j;
	} 
    for(int i=1,j=0;i<=ls;i++){
    	while(j&&s[i]!=t[j+1]) j=ne[j];
    	//当前字符匹配失败（即S[i] != P[j]），则令 i 不变，j = next[j]。
		 
    	if(s[i]==t[j+1]) j++;//匹配成功 
    	
    	if(j==lt){
    		cout<<i-lt+1<<endl; // 输出成功匹配的时候t在s中的位置 
		}
	}
	for(int i=1;i<=lt;i++){
		cout<<ne[i]<<" ";
	}
	
 
	return 0;
}
```





`std::ios::sync_with_stdio(false);`

`cin.tie(0);`

`cout.tie(0);`



```cpp
std::ios::sync_with_stdio(false);
cin.tie(0);

```

