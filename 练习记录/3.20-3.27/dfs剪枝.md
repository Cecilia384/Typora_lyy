[数字替换](https://www.acwing.com/problem/content/description/4871/)

```cpp
#include<bits/stdc++.h>
using namespace std;
#define ll long long
#define int long long
const int maxn = 2e5+10;
const int N =1e5+100;
const int INF = 1000;
int ans=INF;
int n,x;
void dfs(int x,int step){
	bool st[10]={0}; //每一位里出现的数 
 	int cnt=0;
 	for(int y=x;y;y/=10){
 		cnt++;
 		st[y%10]=true;
	 }
	 if(step+n-cnt>=ans) return; 
    //剪枝，一个n位数最理想的步数是n
	 if(cnt==n){
	 	ans=step;return;
	 } 
	 for(int i=9;i>=2;i--){ //优化搜索顺序 
	 	if(st[i]){
	 		dfs(x*i,step+1);
		 }
	 }
 
}
signed main(){
	cin>>n>>x;
    dfs(x,0);
    if(ans==INF){
    	ans=-1;
	} 
	cout<<ans<<endl;
	
	return 0;
}
```

