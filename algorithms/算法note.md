[TOC]



 



# -典型算法例题

### 字符/数组

##### 1.字符替换

~~~c++
 #include<bits/stdc++.h>
using namespace std;
string s;
char a,b;
int main(){
	cin>>s>>a>>b;
	int  len=s.size(); 
    for( int i=0;i<len;i++){
        //-----key------
        if(s[i]==a){
            cout<<b;
        }else{
            cout<<s[i];
        }
        //--------------
    }
    return 0;
}
~~~

### 斐波那契数列

##### 1.递归（经典）

~~~c++
int f1(int n) {
    if(n < 1) {
        return 0;
    }else if(n == 1 || n == 2) {
        return 1;
    }
 
    return f1(n-1) + f1(n-2);
}
~~~

//递归n次，时间复杂度O(2^n)，跑到后面会很慢很慢的！一般不用

##### 2.顺序求法

~~~c++
int f2(int n) {
    if(n < 1) {
        return 0;
    }else if(n == 1 || n == 2) {
        return 1;
    }
    int res = 1;
    int pre = 1;
    int temp = 0;
    for(int i = 3; i < n; i++) {
        temp = res;
        res = pre + res;
        pre  = temp;
    }
    return res;
~~~

//时间复杂度为O(n)

##### 3.递推，用数组存储

~~~c++
long double fib3(int n){
    long double temp;
    if(n<1){
        return -1;
    }
    long double *a=new long double[n+1];//?
    a[i]=a[2]=1;
    for(int i=3;i<=n;i++){
        a[i]=a[i-1]+a[i-2];
        cout<<a[i]<<enndl;
    }
    temp=a[n];
    delete []a;
    return temp;
}
~~~



## 二分

#### Def:

>相对于枚举算法，二分查找具有比较次数少，查找速度快。平均性能好的优点。缺点是要求待查的数据已被整理为有序列表。
>
>二分查找的目标是对于有序列表，在其中寻找指定的目标元素的位置。其基本操作方式:将列表中间位置的元素与目标元素比较，如果两者相等，则查找成功;否则将列表从中间位置分开，分成前后两个子列表，如果中间位置的元素大于目标元素，则进一步查找前一个子列表，否则进一步查找后一子列表。重复以上过程，直到找到满足条件的元素，使查找成功;或子表为空，此时指定元素不在列表内部。为了直观地理解二分查找的过程，下面给出具体的例子。

#### 1.最大值最小化

**在单调递增序列S中查找大于等于t的数中的最小值(最大值最小化)**

code

~~~c++
//最大值最小化
while(l<r)
{
    int mid=( l+r)>>1; //相当于（l+r）/2
    if(s[mid]>=t) r=mid; //一般是 check(mid),
    //根据题目写check（
    else l=mid+1;
}
~~~



#### 2.最小值最大化

第二种情况:在单调递增序列S中查找小于等于t的数中的最大值(最小值最大化)

~~~c++
while(l<r){//最小值最大化
    int mid=(l+r+1)>>1;
	if(s[mid]<=t) l=mid;
	else r=mid-1;
}

~~~





#### 例题

> 1.原题链接:http://bailian.openjudge.cn/practice/4140/ 最短的连续子序列的长度
>
> 2.原题链接: https://www.jisuanke.com/problem/T1883Problem  切绳子
>
> 3.原题链接: http://poj.org/problem?id=2739  Sum of Consecutive Prime 

##### 1.Problem 

>给定一个序列a，使得其和大于等于S，求最短的连续子序列的长度。
>
>lnput
>输入有T组数据;
>每组数据第一行为n和S;
>接下来一行输入n个正整数，中间用空格分开。
>
>output
>针对每组数据输出答案，如果不存在输出0。
>
>

~~~c++
#include <iostream>
using namespace std;
const int maxn=1e5+20;
int t,n,s , a[maxn];
int main ()
{
	scanf ("%d",&t);
	while ( t--){
		scanf ("%d%d" , &n , &s) ;
		for (int i=1;i<=n;i++)  scanf("%d" , a+i);
               int l=1,r=1,ans=1000000 ,tmp=a[1];
		while (r<=n)
		{
			if (tmp<s)r++,tmp+=a[r];
			else
			{
				while ( tmp>=s)
				{
					ans=min(ans ,r-l+1) ;
					tmp-=a [l];
					l++;
				}
			}		
		}
		if(ans==1000000)printf ("0\n" ,ans );
	    else printf ("%d \n" , ans) ;
	}
	return 0;
}

~~~



##### 2.Problem 

>一本书有P，每一页都一个知识点，求去最少的连续页数覆盖所有的知识点。
>
>Input
>第一行输入一个正整数P(1<=P<=10);
>第二行输入P个非负整数，表示每页的知识点编号。
>
>output
>输出答案。



![img](%E7%AE%97%E6%B3%95note.assets/A__@%60R$A%5D9440XL%7BK1%5B7%7DA.png)

~~~c++

#include <iostream>
#include <map>
using namespace std;const int maxn=1e6+20;
int n,p[maxn] ;
map<int,int> mp , cnt;
int main ( )
{
	scanf ("%d", &n) ;
	int k=0;
	for (int i-1; i<=n; i++)
	{
		scanf ("%d" , p+i);
		if ( ! mp [p[i]]) mp[p[i]]=1,k+t;
	}	
	int ans=n,l=1,r=1 ,len=1;
	cnt[p[1]]++;
	while (r<=n)
	{
		if( len<k){
		r++;
		if ( !cnt [p[r]]) len++;
		cnt [p[r]]++;
		}
		else
		{
			whi1e ( len==k)
			{
				ans=min(ans, r-l+1);
				cnt[p[l]]--;
				if (cnt[p [ l] ]==0)len--;
				l++;
			}
		}
	printf("%d" , ans ) ;
	return 0;
}

~~~

##### 3.Problem 

>给定一个正整数n(2<=n<=10000)， n可以有多个连续或者单个质数相加得到，问这样的累加组合方案数是多少。例如: 41=2+3+5+7+11+13=11+13+17=41，因此答案=3。
>
>Input
>多组测试数据，输入0结束。每行输入一个正整数n。
>
>Output
>针对每组测试数据输出相应答案，换行输出。





## 搜索

### DFS

==基本模型==

~~~c++
void dfs(int step){
    //判断边界
    //尝试每一种可能 for(i=1;i<=n;i++)
    {
        //继续下一步 dfs(step+1);
    }
    //返回
}
~~~



## 线段树

[博客园线段树](https://www.cnblogs.com/xenny/p/9801703.html)

[csdn线段树](https://blog.csdn.net/weixin_45697774/article/details/104274713?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166972247316800184179987%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166972247316800184179987&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-104274713-null-null.142^v67^wechat_v2,201^v3^control,213^v2^t3_control2&utm_term=%E7%BA%BF%E6%AE%B5%E6%A0%91&spm=1018.2226.3001.4187)

[oiwiki-线段树](https://oi-wiki.org/ds/seg/)



### 树

#### 堆排

~~~cpp
#include<bits/stdc++.h>
using namespace std;
#define MAXN 55
#define ll long long int
/**
 * 堆，特殊的二叉树
 * 《啊哈算法》P194 建堆以及堆排序
*/
int h[101];//用来存放堆的元素  
int n; //用来存储堆中元素的个数，也就是堆的大小

void swap(int x,int y){
    int t;
    t=h[x];
    h[x]=h[y];
    h[y]=t;
    return;
}

//传入一个需要向下调整的结点,1即是堆顶
void siftdown(int i){  
    int t,flag=0;//用flag来标记是否需要向下调整
    //当i结点有儿子，并且需要继续调整的时候，循环就执行
    while(i*2<=n&&flag==0){
        //首先判断和左二子的关系，用t记录比值较小的结点编号
        if(h[i]>h[i*2]){
            t=i*2;
        }else{
            t=i;
        }
        //如果它有右儿子，再和右儿子进行讨论
        if(i*2+1<=n){
            //如果右儿子的值更小，更新较小的结点编号
            if(h[t]>h[i*2+1]){
                t=2*i+1;
            }
        }
        //如果发现最小结点的编号不是自己，
        //说明子节点中有比父节点更小的
        if(t!=i){
            swap(t,i);
            i=t;//更新i为刚才与它交换的儿子结点的编号
        }else{
            flag=1;
        }
    }
    return;
}

void creat(){//建立堆的函数
    int i;
    //从最后一个非叶结点（内部结点）到第一个结点依次向下调整
    for(i=n/2;i>=1;i--){
        siftdown(i);
    }
    return;
}

int deletmax(){//删除最大元素
    int t;
    t=h[1];//用一个临时变量记录堆顶点的值
    h[1]=h[n];//将堆的最后一个点赋值到堆顶
    n--;//堆的元素-1
    siftdown(1);//向下调整
    return t;//返回之前记录的堆的顶点的最小值
}

int main(){
    int i,num;
    //读入要排序的数字的个数
    cin>>num;

    for(i=1;i<=num;i++){
        cin>>h[i];
    }
    n=num;
    creat();//建堆
    //删除顶部元素，连续删除n次，其实也就是从小到大把数输出来
    for(int i=1;i<=num;i++){
        cout<<deletmax()<<" ";
    }
    getchar();
    getchar();
    
    return 0;
} 
~~~





# -板子

## 1.判断素数

1.开根号法

~~~c++
int isPrime(int n)
{
    int i;
    for ( i=2; i<=sqrt(n); i++ )    
    {
        if(n%i==0)    // 如果不为素数返回0 
    　　{
           return 0;
        }
    }
    return 1;    // 反之则返回1 
}
~~~

2.==素数筛选法==：就是当i是素数的时候，i的所有的倍数必然是合数。如果i已经被判断不是质数了，那么再找到i后面的质数来把这个质数的倍数筛掉。

>一个简单的筛素数的过程：n=30。
>  1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30
>
>  第 1 步过后2 4 ... 28 30这15个单元被标成false,其余为true。
>  第 2 步开始：
>   i=3; 由于prime[3]=true, 把prime[6], [9], [12], [15], [18], [21], [24], [27], [30]标为false.
>   i=4; 由于prime[4]=false,不在继续筛法步骤。
>   i=5; 由于prime[5]=true, 把prime[10],[15],[20],[25],[30]标为false.
>   i=6>sqrt(30)算法结束。
>  第 3 步把prime[]值为true的下标输出来：
>   for(i=2; i<=30; i++)
>   if(prime) printf("%d ",i);
>  结果是 2 3 5 7 11 13 17 19 23 29

 

~~~c++
void compute_prime_table() //筛选法求出500000以内的所有素数
{	int i,j;
	p[0] = p[1] = 0;
	for(i=2;i<=500000;i++)
		p[i]=1; //初始化
	for(i=2;i<=1000;)//对所有小于1000的素数，删除他们的倍数
	{	for(j=i+i;j<=500000;j+=i)
			p[j]=0;//删除i的所有倍数
		for(i++;!p[i];i++);//找下一个素数}
	for(i=0,k=0;i<=500000;i++)
	{	if(p[i])
		{	primes[k]=i;
			k++;}
	}
}
~~~

3.**基于筛选法的素数求取方式**

- 用数组的方式存取筛选候选集，根据质数的倍数不是质数，偶数不是质数的原则进行一次次筛选。

~~~c++
#include <stdio.h>
#include <math.h>
#define N 10000001
int prime[N];
int main()
{
   int i, j;
   for(i=2; i<N; i++){
       if(i%2) prime[i]=1;
       else prime[i]=0;
   }
 
   for(i=3; i<=sqrt(N); i++)
   {   if(prime[i]==1)
       for(j=i+i; j<N; j+=i) prime[j]=0;
   }
 
   for(i=2; i<100; i++)//只输出2-100内的素数
    if( prime[i]==1 )printf("%d ",i);
   printf("\n");
 
   return 0;
}
~~~





## 2.二分



[七种二分板子](https://blog.csdn.net/weixin_41568030/article/details/104590055)



>1. 最朴素的二分查找，查找数num.
>2. 第一个与数num相等的值得位置。`=`
>3. 第一个大于等于num的数 `>=`  ,即：`lower_bound( begin,end,num)`
>4. 第一个大于num的数        `>`,  即：`upper_bound( begin,end,num)`
>5. 第一个小于等于num的数 `<=` ,即：`lower_bound( begin,end,num,greater<type>() )`
>6. 第一个小于num的数        ` <`,即：`upper_bound( begin,end,num,greater<type>() )`
>7. 最后一个与数num相等的数。`=`
>8. 最后一个小于等于num的数。 `<=`
>9. 最后一个小于num的数 `<`
>

1.最朴素的二分查找，查找数num.

```cpp
#include<bits/stdc++.h>
using namespace std;
 
int x,n,a[105];
bool flag=false;
 
void f(int l,int r){
	int mid=(l+r)/2;
	if(l>r)return ;
	if(a[mid]==x){
		flag=true;
		return ;
	}
	if(a[mid]<x)f(l,mid-1);
	if(a[mid]>x)f(mid+1,r);
	return ;
} 
 
int main(){
	cin>>n>>x;
	for(int i=1;i<=n;i++){
		cin>>a[i]; 
	} 
	sort(a+1,a+n+1,greater<int>());//防止缺德、毒瘤数据 
	f(1,n);
	if(flag)cout<<"YES"<<endl;
	else cout<<"NO"<<endl;
	return 0; 
}
```

2.第一个与数num相等的值的位置。`=`

```cpp
void f(int l,int r){
    int left = l;
	int right = r;
    while (left <= right) { // 这里是 <=
        int mid = (left + right) >>1;
        if (a[mid] >= key) {
            right = mid - 1;
        }else {
            left = mid + 1;
        }
    }
    if (left < n && a[left] == key) {
        return left;
    } 
    return -1;//不一定有相等的
}

```

7.最后一个与数num相等的数。

```cpp
void f(int l,int r){
    int left = l;
	int right = r;
    
    while (left <= right) {  
        int mid = (left + right) >>1;
        if (a[mid] <= key) { // 差别  这里是 <=
            left = mid + 1;
        }
        else {
            right = mid - 1;
        } 
    }
    if (right >= 0 && a[right] == key) {
        return right; 
    }
    return -1;
}

```



8.最后一个小于等于num的数。 `<=`

```cpp
void f(int l,int r){
    int left = l;
	int right = r;
    
    while (left <= right) {
        int mid = (left + right) >>1;
        if (a[mid] > key) { // 这里是 >
            right = mid - 1;
        }
        else {
            left = mid + 1; } 
    }
    return right;
}

```

9.最后一个小于num的数

同上，除了第七排--- > ` if (a[mid] >= key)`





iowiki 

~~~cpp
int binary_search(int start, int end, int key) {
	int ret = -1;  // 未搜索到数据返回-1下标
	int mid;
	while (start <= end) {
		mid = start + ((end - start) >> 1);  // 直接平均可能会溢出，所以用这个算法
		if (arr[mid] < key)
			start = mid + 1;
		else if (arr[mid] > key)
			end = mid - 1;
		else {  // 最后检测相等是因为多数搜索情况不是大于就是小于
			ret = mid;
			break;
			}
  	  }
	return ret;  // 单一出口
}
~~~



>（换一个板子吧，上面那个不会用QAQ



~~~cpp
int n,m,p;
int a[MAXN];
int bs(int s,int e,int k){

int ret =-1;

	ret = lower_bound(a , a + n , k) - a;
// if(a[ret] == k)return ret;
// return -1;

return a[ret] == k ? ret : -2 ;

}
~~~

 

## 3.高精度

acwing板子



~~~c++
//oiwiki，高精乘法
void mul_short(int a[], int b, int c[]) {
  clear(c);

  for (int i = 0; i < LEN - 1; ++i) {
    // 直接把 a 的第 i 位数码乘以乘数，加入结果
    c[i] += a[i] * b;

    if (c[i] >= 10) {
      // 处理进位
      // c[i] / 10 即除法的商数成为进位的增量值
      c[i + 1] += c[i] / 10;
      // 而 c[i] % 10 即除法的余数成为在当前位留下的值
      c[i] %= 10;
    }
  }
}
~~~



> 
