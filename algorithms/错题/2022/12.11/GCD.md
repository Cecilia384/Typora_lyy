# B. Bestie 

You are given an array aa consisting of nn integers a1,a2,…,ana1,a2,…,an. Friends asked you to make the [greatest common divisor (GCD)](https://en.wikipedia.org/wiki/Greatest_common_divisor) of all numbers in the array equal to 11. In one operation, you can do the following:

- Select an arbitrary index in the array 1≤i≤n1≤i≤n;
- Make ai=gcd(ai,i)ai=gcd(ai,i), where gcd(x,y)gcd(x,y) denotes the GCD of integers xx and yy. The cost of such an operation is n−i+1n−i+1.

You need to find the minimum total cost of operations we need to perform so that the GCD of the all array numbers becomes equal to 11.

Input

Each test consists of multiple test cases. The first line contains an integer tt (1≤t≤50001≤t≤5000) — the number of test cases. The description of test cases follows.

The first line of each test case contains a single integer nn (1≤n≤201≤n≤20) — the length of the array.

The second line of each test case contains nn integers a1,a2,…,ana1,a2,…,an (1≤ai≤1091≤ai≤109) — the elements of the array.

Output

For each test case, output a single integer — the minimum total cost of operations that will need to be performed so that the GCD of all numbers in the array becomes equal to 11.

We can show that it's always possible to do so.

### KEY

==答案只有3,2,1,0四种情况==

~~~cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
//#define ll __int128
#define fast std::ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
const int mod=1e9+7;
const int maxn=5e5+100;
int n,m,k,a[maxn];
// __gcd()
int gcd(int a,int b){ return b?gcd(b,a%b):a;}
int gg;
void solve(){
     cin>>n;
     memset(a,0,sizeof(a));
     gg=0;
     for(int i=1;i<=n;i++){
     	cin>>a[i];
	 }
	 gg=a[1];
	 for(int i=2;i<=n;i++){
	 	gg=gcd(gg,a[i]);
	 }
	 //下面这种求公约数的方法就会WA 啊啊啊
	 // for(int i=2;i<n;i++){
	 	// gg=gcd(gg,gcd(a[i],a[i+1]));	 	 
	 // }
	 if((n==1&&a[1]==1)||gg==1){
	 	cout<<0<<endl; return;
	 }
	 if(n==1&&a[1]>1){
	 	cout<<1<<endl;return;
	 }
	 if( gcd(gg,gcd(a[n],n))==1){
	 	cout<<1<<endl;return;
	 }else{
	 	if( gcd(gg,gcd(a[n-1],n-1))==1||n-1==1){
	 	cout<<2<<endl;return;
		 }else{
		 	cout<<3<<endl;return;
		 }
	 }
}
signed main(){
    fast
    int _=1;
    cin>>_;
    for(int i=1;i<=_;i++){
     // printf("Case #%d: ",i);
        solve();
    }
    return 0;
}
~~~



