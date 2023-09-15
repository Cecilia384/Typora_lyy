`lower_bound`应用

```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define fast std::ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
const int mod=1e9+7;
const int maxn=1e5+100;
int n,k,a[maxn],b[maxn],sum;
 
void solve(){
   cin>>n;
   memset(a,0,sizeof(a));
   memset(b,0,sizeof(b));
   for(int i=1;i<=n;i++){
    	cin>>a[i];
    	b[i]=a[i];
    }
    sort(a+1,a+n+1);
     for(int i=2;i<=n;i++){
    	a[i]=a[i-1]*(a[i]/a[i-1])+a[i-1];
    }
    cout<<n<<endl;
    for(int i=1;i<=n;i++){
    	int pos=lower_bound(a+1,a+n+1,b[i])-a;
    	//cout<<"a[pos]  "<<a[pos]<<endl;
    	cout<<i<<" "<<a[pos]-b[i]<<endl;
    }
}
signed main(){
    fast
    int t=1;
    cin>>t;
    for(int i=1;i<=t;i++){
//      printf("Case #%d: ",i);
        solve();
    }
    return 0;
}
```

