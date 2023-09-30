端点！！

#### [A线段染色](http://202.120.222.93:8888/p/P1170)

```cpp
#include<bits/stdc++.h>
using namespace std;
#define fast ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define int long long
priority_queue<int,vector<int>,greater<int> > pqu;
const int maxn = 2e5+10;
int n,k,l[maxn],r[maxn],ans=1;
int nl,nr;
typedef struct st{
	int l,r;
}st;
st s[maxn];
bool cmp(st s1,st s2){ 
    //切记，采取从这种策略的时候不能先对左端排序
	if(s1.r!=s2.r){
		return s1.r<s2.r;
	}else{
		return s1.l<s2.l;
	}
}
signed main(){
	fast
	cin>>n>>k;
	 for(int i=0;i<n;i++){
		cin>>s[i].l>>s[i].r;
	} 
	sort(s,s+n,cmp);
	nr=s[0].r+k-1;
	for(int i=1;i<n;i++){
		//cout<<i<<" "<<nr<<endl;
		if(nr<s[i].l){
			ans++;
			nr=s[i].r+k-1;
		}
	}
	cout<<ans;
	return 0;
}
```

#### [B第k小子串](http://202.120.222.93:8888/p/176?tid=6413e1f0e987a0ffb495bf43)

有一个字符串序列*S*，已知它有多个**不同**的子串$S_1,S_2,S_3,...,S_n $，比如字符串`abc`包含的不同子串有`a`,`b`,`c`,`ab`,`bc`,`abc`。

现在请你找出 S 中字典序第k 小的子串t ，并将其输出。

**注意：字符串S 只包含小写字母！**

因为k 很小，所以只需要对k 长度以内的子串进行截取和排序即可，排序这里用的是c++\ stl 里面的set  

---

KEY-> `set` （自动排序，去重

```cpp
#include<bits/stdc++.h>
using namespace std;
#define fast ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define int long long
priority_queue<int,vector<int>,greater<int> > pqu;
const int maxn = 2e5+10;
int k;
string s;
set<string> t;
signed main(){
	fast
	cin>>s>>k;
 	for(int i=0;i<s.size();i++){
 		for(int j=1;j<=10;j++){
 			if((i+j)>s.size()){
 				continue;
			 }else{
			 	t.insert(s.substr(i,j));	
			 }
		 }
	 }
	 set<string>::iterator it=t.begin();
	 int cnt=0;
	 for(;it!=t.end();it++){
	 	cnt++;
	 	if(cnt==k) cout<<*it;
	 }
	 
}
```

