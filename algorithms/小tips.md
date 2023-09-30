[TOC]



~~~c++
/*
When you are coding,remember to:
    - clear the arrays if a problem has many tasks.
    - pay attention to some =special cases(n=0,1).
    - Don't code before think completely.
    - ...
*/
~~~



# 一 基础知识

---

#### 1.万能头

 ~~~c++
#include<bits/stdc++.h>
using namespace std;
 ~~~

#### 2.求最大公约数



~~~c++
int gcd(int a int b){
	int r;
	while(b>0){
		r=a%b;a=b;b=r;
	}
	return a;
}
~~~

#### 2.1求最小公倍数

~~~c++
int lcm(int x,int y){
    int g;
    g=gcd(x,y);
    return (x*y/g);
}
int gcd(int a int b){
	int r;
	while(b>0){
		r=a%b;a=b;b=r;
	}
	return a;
}       
~~~





#### 3.求字符串长度(c++)

 ~~~c++
string s;
int len=sizeof(s);//1
len=s.size();	  //2
 ~~~

---

#### 4.c++控制输出小数点

~~~c++
#include<iomanip>
...
	cout<<fixed<<setprecision()<<a;
~~~

#### 5.c++中的sort（）

~~~c++
#include<algorithm>
...
	int arr[MAX];
	...//下面这句为将arr全部排列
	sort(a,a+MAX,cmp); //cmp可以省略，默认升序排列
	//sort(start,end,排序方法)
~~~

#### 6.数组去重--unique()

~~~c++
...
    sort(a,a+n);
	int len=unique(a,a+n)-a;//得到去重后数组的长度
	//将数组中相邻重复的元素去除
~~~

#### 7.数组初始化--memset（）

详细用法参见

->  https://www.cnblogs.com/handsomecui/p/4723949.html

~~~c++
//void memset(void *S,int ch,size_t)
bool a[105][105];
memset(a,0,sizeof(a));//将二维数组a中所有值初始化为0
~~~

==key==：memset 是==以字节为单位==来初始化数组的，若为`memset(a,1,sizeof(a))`---

>在a中每个元素占 4字节
>比如int型的0为 0x00000000
>==int 型的最大值为 0x7FFFFFFF==
>0xF = 0b1111 占四位
>1字节为8bit ，所以两位为1字节
>--使用memset进行初始化后会变为 0x01010101 也就是16843009
>所以一下两种初始化效果是一样的
>
>~~~c++
>memset(a,-1,sizeof(a));
>memset(a,255,sizeof(a));
>~~~

2.赋极大值

~~~c++
int a[100];
memset(a,0x3f,sizeof(a) );
~~~

关于==0x3f==

- 0x3f=0011 1111=63
  C++中int型变量所占的位数为4个字节，即32位
  0x3f显然不是int型变量中单个字节的最大值，应该是0x7f=0111 1111 B

- 那为什么要赋值0x3f：

  1.作为无穷大使用
  		因为4个字节均为0x3f时，0x3f3f3f3f的十进制是1061109567，也就是10^ 9级别的（和0x7fffffff一个数量级），而一般场合下的数据都是小于10^9的，所以它可以作为无穷大使用而不致出现数据大于无穷大的情形。

  2.可以保证无穷大加无穷大仍然不会超限。
  		另一方面，由于一般的数据都不会大于10^9，所以当我们把无穷大加上一个数据时，它并不会溢出（这就满足了“无穷大加一个有穷的数依然是无穷大”），事实上0x3f3f3f3f+0x3f3f3f3f=2122219134，这非常大但却没有超过32-bit int的表示范围，所以0x3f3f3f3f还满足了我们“无穷大加无穷大还是无穷大”的需求。
  首先要知道memset函数是对字节为单位进行赋值的；
  void *memset(void *s, int ch, size_t n);
  函数解释：将s中前n个字节 （typedef unsigned int size_t ）用 ch 替换并返回 s 。
  其实这里面的ch就是ascii为ch的字符；
  将s所指向的某一块内存中的前n个 字节的内容全部设置为ch指定的ASCII值
  ————————————————
  原文链接：https://blog.csdn.net/qq_42386788/article/details/116427457



#### 8.字符串与数字的转换

> 使用系统提供的库函数
>
> ###### 1.字符串传数字
>
>  (1)、使用**stoi()**
>
> ~~~c++
> string s("12345");
> long long a = stoi(s);
> cout << a << endl;
> ~~~
>
>  
>  
>   （2）、使用**atoi()**
>
> ~~~c++
>char str3[10] = "3245345";
> //数字简单，所以转数字一个参数 
> long long a = atoi(str3);  
> cout << a << endl;
> ~~~
> 
> 
>
>   (3)、使用 **sscanf() 映射**
>  
>  ~~~c++
>  long long c = 0;
>char str5[10] = "661234544";
> sscanf(str5, "%d", &c); //从左至右，字符串转数字 
>cout << c << endl;
> ~~~
> 
> 
> 
>  (4)、自己写一个简单的
> 
>~~~c++
>  //字符串转为整数,通过减'0'字符,底层用ASCII码相减 
>  void myAtoi(char str[],long long& m){  
>  	int i(0);
>  	int temp = 0;
>	while(str[i] != '\0'){
> 		temp = temp*10 + (str[i] -'0');
>		++i;
> 	}
> 	m = temp; //转换后赋值给m
> } 
> ~~~
> 
> 
> 
> **2.数字转字符串**
> 
>  (1)、使用c++里的to_string()
> 
> ~~~c++
>long long m = 1234566700;
>  string str = to_string(m);   //系统提供数字转字符 
>  cout << str << endl;
>  ~~~
>  
>  
>  
>  
>  
>   (2)、使用itoa()
>  
>~~~c++
> int n = 100;
>char str2[10];
> //字符串比较麻烦，所以转字符串三个参数，我是这么记得(手动滑稽） 
>itoa(n,str2,10); //第一个参数为整数，第二个为字符串(char*)，第三个为进制 
> cout << str2 << endl;
> ~~~
> 
> 
> 
>
>  
>  (3)、使用sprintf() 映射
>  
>~~~c++
> long long b = 1234560;
>char str4[10] = {0};
> sprintf(str4, "%d", b); //从右至左，把数转换为字符串 
>cout << str4 << endl;
> ~~~
> 
> 
> 
>  (4)、自己写一个简单的
> 
> ~~~c++
>//整数转为字符串：通过加 '0'字符 
>  void myItoa(long long n, char str[]){
>  	char temp[MAX]{0};
>  	int i(0);
>  	int j = 0;
>  	while(n){
>		temp[i++] = n%10 + '0';
> 		n /= 10; 
>	}
> 	//此时为逆序，需要调整为正序 
>	//cout <<  temp << endl;
> 	while(i>0)
> 		str[j++] = temp[--i];
> 	//cout << str << endl;
> } 
> //————————————
> 
>
>  //原文链接：https://blog.csdn.net/weixin_43971252/article/details/104063490
>  ~~~



#### 9.读入带空格的字符串

~~~c++
string s;
getline(cin,s);
~~~



#### 10.**输入总数未知数据**

~~~c++
while((scanf("%d",&n)!)=EOF) 
    //EOF就是-1，当scanf返回值为-1时停止输入
while((cin>>n)!=0)
     //当cin返回值为0时停止输入
while(~(scanf("%d",&n))) 
~~~



# --tips--

### 10.16回文素数

+ 偶数长度的回文数只有11是素数

  #### 回文素数

  >求一亿以内的回文素（质）数
  >
  >> 先求质数再判断回文，效率低下；所以先构造[回文数](https://so.csdn.net/so/search?q=回文数&spm=1001.2101.3001.7020)，再判断质数。
  >> 偶数位的回文数都能被11整除。所以，**偶数位的回文数除了11都是合数**.
  >
  >> 观察偶数位的回文数，提取所有奇数位的数字，与提取所有偶数位的数字，正好是相反的顺序。 因此，偶数位数和等于奇数位数和，从而差等于0，而0能被11整除，因此这个回文数，可以被11整除
  >> 例：1331 13 31
  >
  >> 一个k位数，可以构造出一个奇数位的回文数。比如13，可以构造131；189可以构造18981.所以100000000内的只要从1构造到9999即可。

~~~java
import java.util.ArrayList;
public class  Huiwenzhishu {   //一亿以内的回文质数
	public static ArrayList<Integer> list = new ArrayList<Integer>(); 
	public static void main(String[] args) {
		list.add(11);
		for (int i = 2; i < 100; i++) {
			int tmp = i / 10, sum;

			for (sum = i; tmp != 0; tmp /= 10) {
				sum = sum * 10 + tmp % 10;
			}
			bool(sum);
		}
		System.out.println(list);
	}
	public static void bool(int n){
		int sqrt =   (int) Math.sqrt(n+0.5);
		for(int i:list){
			if(n%i==0){
				return  ;
			}
			else if(i>sqrt){
				return  ;
			}
		}
		list.add(n);
		return  ;
	}

}


~~~

### 10.21 阶乘

~~~c++
int jiecheng(int x){
	long logng ret=1;
	for(int i=x;i>0;i--){
		ret*=i;
	}
	return ret;
}
~~~

排列：

组合：



### 10.23前缀和

~~~c++
#include<iostream>
using namespace std;
long long sum[1000001];//因为有10^12的a，所以用long long
int main()
{
	long long n,k,a,maxx=0;
	cin>>n>>k;
	sum[1]=0;
   //---------------------------
	for(int i=2;i<=n;i++)
	{
		cin>>a;
		sum[i]=sum[i-1]+a;//算前缀和
	}
    //-----------------------------
	return 0;
}
~~~

### vector应用（模拟栈）

~~~c++
#include<bits/stdc++.h>
using namespace std;
# define ll long long
#define MAX 100100 
/**
*P1427 小鱼的数字游戏 
* 	   题目见下方
*/
vector<ll>b;
 
int main(){
	 //memset(a,0,sizeof(a));
	 ll a;
	 int n=0;
	 while(cin>>a){
	 	if(a!=0){
	 		b.push_back(a);
		 }else{
		 	break;
		 }
	     
	 }
	vector<ll>::iterator v =b.end()-1;
    while(v!=b.begin()-1){
        cout<<*v<<" ";
        v--;
    }
	return 0;
}
~~~





># 小鱼的数字游戏
>
>#### 题目描述
>
>小鱼最近被要求参加一个数字游戏，要求它把看到的一串数字 $a_i$（长度不一定，以 $0$ 结束），记住了然后反着念出来（表示结束的数字 $0$ 就不要念出来了）。这对小鱼的那点记忆力来说实在是太难了，你也不想想小鱼的整个脑袋才多大，其中一部分还是好吃的肉！所以请你帮小鱼编程解决这个问题。
>
>## 输入格式
>
>一行内输入一串整数，以 $0$ 结束，以空格间隔。
>
>## 输出格式
>
>一行内倒着输出这一串整数，以空格间隔。
>
>## 样例 #1
>
>### 样例输入 #1
>
>```
>3 65 23 5 34 1 30 0
>```
>
>### 样例输出 #1
>
>```
>30 1 34 5 23 65 3
>```
>
>## 提示
>
>#### 数据规模与约定
>
>对于 $100\%$ 的数据，保证 $0 \leq a_i \leq 2^{31} - 1$，数字个数不超过 $100$。

### 11.29

#### 杨辉三角

构造

~~~c++
int c[MAx][MAX];
c[1][1]=1;
for(int i=2;i<=n;i++)
		for(int j=1;j<=i;j++)
			c[i][j]=c[i-1][j]+c[i-1][j-1];//生成杨辉三角
~~~

#### assert()

>[原文链接](https://blog.csdn.net/u014082714/article/details/45190505)
>
>- assert宏的原型定义在==<assert.h>==中，其作用是如果它的条件返回错误，则终止程序执行，原型定义：
>
>~~~c++
>#include <assert.h>
>void assert( int expression );
>~~~
>
>
>
>- assert的作用是现计算表达式 expression ，如果其值为假（即为0），那么它先向stderr打印一条出错信息，然后通过调用 abort 来终止程序运行
>  ————————————————
>
>- 使用assert()的缺点是，频繁的调用会极大的影响程序的性能，增加额外的开销。在调试结束后，可以通过在包含#include <assert.h>的语句之前插入 # eedefine NDEBUG 来禁用assert调用，示例代码如下：
>
># include <stdio.h>
># define NDEBUG
># include <assert.h>
>————————————————

### 12.4

#### 大小写转换

~~~c++
if(ch[j]>='A'&&ch[j]<='Z'){
    ch[j]=ch[j]+('a'-'A');
   }
~~~

#### freopen用法

[freopen](https://blog.csdn.net/qq_37870050/article/details/81293598?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522167015045116782390596818%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=167015045116782390596818&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-2-81293598-null-null.142^v67^wechat_v2,201^v3^control,213^v2^t3_control2&utm_term=%20freopen%281.in%2Cr%2Cstdin%29%3B&spm=1018.2226.3001.4187)

[freopen2](https://blog.csdn.net/XavierDarkness/article/details/80638641?spm=1001.2101.3001.6650.3&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-3-80638641-blog-81293598.pc_relevant_aa2&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-3-80638641-blog-81293598.pc_relevant_aa2&utm_relevant_index=6)

`freopen("文件名.拓展名","操作种类(r/w)","标准输入输出");`



按f6直接运行

### 12.5

>+的优先级比右移>>的优先级高
>
>位运算比乘除快

### 12.8异或运算

异或运算

1.按位异或的几个常见用途：

- （1） 使某些特定的位翻转

  例如对数10100001的第2位和第3位翻转，则可以将该数与00000110进行按位异或运算。

  10100001^00000110 = 10100111

  （2） 实现两个值的交换，而不必使用临时变量。

  　　例如交换两个整数a=10100001，b=00000110的值，可通过下列语句实现：

  　　a = a^b； 　　//a=10100111

  　　b = b^a； 　　//b=10100001

  　　a = a^b； 　　//a=00000110



##### nim

 [nim博弈](http://202.120.222.93:8888/p/P1068)

[博弈论之Nim游戏](https://zhuanlan.zhihu.com/p/347392691)



### 2023.3.1 inline

[inline 简介](https://blog.csdn.net/K346K346/article/details/52065524)

>1. inline 函数由 inline 关键字定义，引入 inline 函数的主要原因是用它替代 C 中复杂易错不易维护的宏函数。
>
>​    2.编译器在编译阶段完成对 inline 函数的处理，即对 inline 函数的调用替换为函数的本体。但 inline 关键字对编译器只是一种建议，编译器可以这样去做，也可以不去做。从逻辑上来说，编译器对 inline 函数的处理步骤一般如下：
>（1）将 inline 函数体复制到inline函数调用处；
>（2）为所用 inline 函数中的局部变量分配内存空间；
>（3）将 inline 函数的的输入参数和返回值映射到调用方法的局部变量空间中；
>（4）如果 inline 函数有多个返回点，将其转变为 inline 函数代码块末尾的分支（使用GOTO）。
>————————————————

### 3.4 min_element()

[min_element()和max_element()函数的使用](https://blog.csdn.net/weixin_38505045/article/details/88656453?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522167791247116800184149348%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=167791247116800184149348&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-88656453-null-null.142^v73^insert_down2,201^v4^add_ask,239^v2^insert_chatgpt&utm_term=min_element&spm=1018.2226.3001.4187)

>min_element()和max_element
>头文件：#include
>作用：返回容器中最小值和最大值。
>max_element(first,end,cmp);其中cmp为可选择参数!
>max函数|C++返回数组中的最大值——max_element函数
>
>在头文件 #include 中，返回的是迭代器，所以输出值的话要在前面加 *
>
>第三个参数cmp可写可不写， max_element() 和 min_element() 默认是从小到大排列，然后 max_element() 输出最后一个值， min_element() 输出第一个值，但是如果自定义的 cmp 函数写的是从大到小排列，那么会导致 max_element() 和min_element() 的两个结果是对调的
>
>可以用于 vector 或者 vector 等，也可以用于 int arr[4] 或者string arr[4] ，也可以用于结构体vector或者结构体数组～
>———————————————

```cpp
#include<bits/stdc++.h>
using namespace std; 
struct node {
   int x, y;
};
bool cmp1(node a, node b) {
    return a.x > b.x;
}
int main() {
    vector<int> v(3);
    int arr[4];
    vector<node> v1(3);
    cout << *max_element(v.begin(), v.end());
    cout << *min_element(arr, arr + 4);
    cout << (*max_element(v1.begin(), v1.end(), cmp1)).y;
    return 0;
}

```

```cpp
#include<iostream>  
#include<algorithm>  
using namespace std;  
bool cmp(int a,int b){  
      return a < b;  
}  
int main(){  
      int num[]={2,3,1,6,4,5};  
      cout << "最小值是 " << *min_element(num,num+6) << endl;  
      cout << "最大值是 " << *max_element(num,num+6) << endl;  
      cout << "最小值是 " << *min_element(num,num+6,cmp) << endl;  
      cout << "最大值是 " << *max_element(num,num+6,cmp) << endl;  
      return 0;   
}

```

### 3.7unordered_map<int,int>

[csdn](https://blog.csdn.net/zou_albert/article/details/106983268)

- `unordered_map`是一个将key和value关联起来的容器，它可以高效的根据单个key值查找对应的value。
- key值应该是唯一的，key和value的数据类型可以不相同。
- unordered_map存储元素时是没有顺序的，只是根据key的哈希值，将元素存在指定位置，所以根据key查找单个value时非常高效，平均可以在常数时间内完成。
  **unordered_map查询单个key的时候效率比map高，但是要查询某一范围内的key值时比map效率低**。
- 可以使用[]操作符来访问key值对应的value值。
  ————————————————

### 3.10 next_permutation()



[csdn](https://blog.csdn.net/qq_43488547/article/details/100032724?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522167845772916800226514958%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=167845772916800226514958&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-100032724-null-null.142^v73^insert_down2,201^v4^add_ask,239^v2^insert_chatgpt&utm_term=next_permutation%28%29&spm=1018.2226.3001.4187)

>**next_permutation()** 是 C++ STL 中的一个函数，**用于求一个序列的下一个全排列**。该函数会改变原序列，并返回一个布尔值，表示是否存在下一个全排列。如果存在，则返回 true，并将原序列更新为下一个全排列；如果不存在，则返回 false，并将原序列更新为最初的序列。
>
>

eg

```cpp
#include <iostream>  
#include <algorithm>  
using namespace std;  
int main()  
{  
    int num[3]={1,2,3};  
    do  
    {  
        cout<<num[0]<<" "<<num[1]<<" "<<num[2]<<endl;  
    }while(next_permutation(num,num+3));  
    return 0;  
}  

```

输出结果

```
1 2 3
1 3 2
2 1 3 
2 3 1
3 1 2

```

### 3.11 memcpy(a1,a2);

`memcpy`函数是C/C++语言中的一个用于内存复制的函数，声明在 string.h 中（C++是 cstring）。其原型是：

```cpp
void *memcpy(void *destin, void *source, unsigned n);
```

作用是：以source指向的地址为起点，将连续的n个字节数据，复制到以destin指向的地址为起点的内存中。
函数有三个参数，第一个是目标地址，第二个是源地址，第三个是数据长度。

使用memcpy函数时，需要注意：

- 数据长度（第三个参数）的单位是字节（1byte = 8bit）。
- 注意该函数有一个返回值，类型是void*，是一个指向destin的指针。





### 4.23 assign函数

 [c++ string的详细用法（1）assign()](https://blog.csdn.net/qq_40630246/article/details/103643728)

```cpp
//字符串变量
string a="123";
string b="456";

1.字符串直接赋值
a.assign(b); //等于a=b赋值，结果为 a="456"
a.assign("789");//结果为 a="789"

2.一个字符串的子串赋值给另一个字符串
a.assign(b,begin,len);
//从字符串b的第(begin)个字符开始向后数(len)个字符(包括begin)的字符串赋值给字符串a

例：
a.assign(b,0,1); //结果为 a="4"
a.assign(b,1,1); //结果为 a="5"
a.assign(b,0,2); //结果为 a="45";
a.assign(b,1,2); //结果为 a="56";
a.assign("123456",1,3); //结果为 a="234";
/*说明
 *如果第三个参数大于字符串本身的长度，则赋值到该字符串末尾
 *如：a.assign(b,1,4); 结果为 a="56";
 *如果第二个参数大于字符串本身长度则赋值为空
 *如：a.assign(b,3,4); 结果为 a="";
 *第二个参数最大不能超过字符串长度加一，否则程序会运行错误。因为string字符串后面会有一个"\n"符号，这个符号虽然不算在字符串长度里面，但是会占一个字符的空间。所以超过字符串长度加一后会出现std::out_of_range的错误。
 */
 
3.从字符串的某一个字符串开始到结束赋值给另一个字符串
a.assign(b,begin);
//从字符串b的第begin字符串开始到字符串结束赋值给字符串a

a.assign(b,0); //结果为 a="456";
a.assign(b,1); //结果为 a="56";
a.assign(b,4); //error 这样会运行错误（同2） vs2019

4.从字符串开始到字符串的某一个字符赋值给另一个字符串
a.assign("123456",2);//结果为 a="12"
string c="123456";
a.assign(c,2);       //结果为 a="3456"
//根据vs2019运行情况来看，如过第一个参数是字符串常量则按从头到第n个字符赋值，如果第一个参数是字符串变量的话，则从第n个字符开始到字符串结尾赋值（不知道其他编译会是怎么样的,vs2019是调用不同的重载函数）

5.用相同的n个字符给字符串赋值
a.assign(10,'b'); //结果为 a="bbbbbbbbbb";
a.assign(5,'c');  //结果为 a="ccccc";

6.template<class inputIterator> string& assign(inputIterator first,inputIterator last);
//使用这个函数需要引入#include<iterator>头文件 
a.assign(istream_iterator<char>(cin), istream_iterator<char>());
//键盘输入123abcd
//结果为 a="123abcd";
/*注意
 *该函数不接收空格换行等符号，最后（windows系统）按ctrl+z结束输入
 *如输入以下符号（既有空格也有换行）
 123abc    ABC  哈哈 !@#$



 defg)(-=<>-+/*


 123654
 最后结果为 a="123abcABC哈哈!@#$defg)(-=<>-+/*123654";
 */

7.使用迭代器赋值
a.assign(b.begin()+1,b.end()); //结果为 a="67";
a.assign(a.begin(),a.end());   //结果为 a="123";
```





### 4.24 [bitset](https://blog.csdn.net/Mr_dimple/article/details/123478474?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522168232264416800226541246%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=168232264416800226541246&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-123478474-null-null.142^v86^control,239^v2^insert_chatgpt&utm_term=bitset%20%E8%BE%93%E5%87%BA&spm=1018.2226.3001.4187)

```cpp
bitset用来存储二进制数位。像一个bool类型的数组一样，bitset每个元素只有0或1两个数值。
但是有空间优化——bitset中的一个元素一般只占1 bit。
bitset中的每个元素都能单独被访问,例如下面的代码：

输出格式
printf("%d\n",x.to_ulong());
cout<<x<<endl;

bitset<15>a,b(string("101")); //定义bitset，15是指有15位
a[10]=1;  //将第10位定义为1
输出a;
输出b;
a=101; //赋值a
输出a;

输出：
1024
000010000000000
5
000000000000101
101
000000001100101

可以看出，a[10]=1相当于+2^10。
而下面直接输出bitset就很玄妙。
另外，字符串可以直接转到bitset中。
有意思的是，bitset可以直接赋值！
当然也可以bitset<15>c(101)来赋值!

then

bitset<4> a ( string("1001"));
bitset<4> b ( string("0011"));

cout << (a^=b) << endl;       // 1010 
cout << (a&=b) << endl;       // 0010
cout << (a|=b) << endl;       // 0011 

cout << endl << a << endl;    // 0011
cout << b << endl << endl;    // 0011

cout << (a<<=2) << endl;      // 1100 
cout << (a>>=1) << endl;      // 0110

cout << endl << a << endl;    // 0110
cout << b << endl << endl;    // 0011

cout << (~b) << endl;         // 1100 
cout << (b<<1) << endl;       // 0110 
cout << (b>>1) << endl;       // 0001

cout << (a==b) << endl;       // false (0110==0011)
cout << (a!=b) << endl;       // true  (0110!=0011)

cout << (a&b) << endl;        // 0010
cout << (a|b) << endl;        // 0111
cout << (a^b) << endl;        // 0101

看完这些，估计您已经对bitset有个深刻的了解，它资瓷位运算！

then

对于一个叫做a的bitset：
a.size()      返回大小（位数）
a.count()     返回1的个数
a.any()       返回是否有1
a.none()      返回是否没有1
a.set()       全都变成1
a.set(p)      将第p+1位变成1
a.set(p, x)   将第p+1位变成x
a.reset()     全都变成0
a.reset(p)    将第p+1位变成0
a.flip()      全都取反
a.flip(p)     将第p+1位取反
a.to_ulong()  返回它转换为unsigned long的结果，如果超出范围则报错
a.to_ullong() 返回它转换为unsigned long long的结果，如果超出范围则报错
a.to_string() 返回它转换为string的结果
```



