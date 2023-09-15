ST表的功能很简单

它是解决[RMQ问题](https://baike.baidu.com/item/rmq/1797559?fr=aladdin)(区间最值问题)的一种强有力的工具

它可以做到O(nlogn) 预处理，O(1) 查询最值

>RMQ (Range Minimum/Maximum Query)问题是指**：对于长度为n的数列A，回答若干询问RMQ(A,i,j)(i,j<=n)，返回数列A中下标在i,j里的最小(大）值，也就是说，RMQ问题是指求区间最值的问题。**
>
>主要方法及复杂度如下：
>
>1、朴素（即搜索），O(n)-O(qn) online。
>
>2、[线段树](https://baike.baidu.com/item/线段树?fromModule=lemma_inlink)，O(n)-O(qlogn) online。
>
>3、ST（实质是[动态规划](https://baike.baidu.com/item/动态规划?fromModule=lemma_inlink)），O(nlogn)-O(q) online。
>
>ST算法（Sparse Table），以求最大值为例，设d[i,j]表示[i,i+2^j-1]这个区间内的最大值，那么在询问到[a,b]区间的最大值时答案就是max(d[a,k], d[b-2^k+1,k])，其中k是满足2 ^ k<=b-a+1(即长度)的最大的k,即k=[ln(b-a+1)/ln(2)]。
>
>d的求法可以用[动态规划](https://baike.baidu.com/item/动态规划/529408?fromModule=lemma_inlink)，d[i, j]=max(d[i, j-1],d[i+2^(j-1), j-1])。
>
>4、RMQ标准算法：先规约成LCA（Lowest Common Ancestor），再规约成约,束RMQ，O(n)-O(q) online。
>
>首先根据原[数列](https://baike.baidu.com/item/数列?fromModule=lemma_inlink)，建立[笛卡尔树](https://baike.baidu.com/item/笛卡尔树?fromModule=lemma_inlink)，从而将问题在[线性时间](https://baike.baidu.com/item/线性时间/6738492?fromModule=lemma_inlink)内规约为LCA问题。LCA问题可以在线性时间内规约为约束RMQ，也就是数列中任意两个相邻的数的差都是+1或-1的RMQ问题。约束RMQ有O(n)-O(1)的在线解法，故整个算法的[时间复杂度](https://baike.baidu.com/item/时间复杂度/1894057?fromModule=lemma_inlink)为O(n)-O(1)。

[st表 CSDN](https://blog.csdn.net/Lucas_FC_/article/details/125837983?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522167758887216782425650951%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=167758887216782425650951&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_click~default-4-125837983-null-null.142^v73^insert_down2,201^v4^add_ask,239^v2^insert_chatgpt&utm_term=st%E8%A1%A8&spm=1018.2226.3001.4187)

- ## 预处理阶段。

1. 首先你应该知道的是，ST表是利用**倍增**思想来缩短时间的。而倍增就体现在他数组的定义中：对于$f [i] [j]$，指的是在序列的**第 $i$ 项**，**向后$2^j$个元素所包含序列间的最大值**。

```cpp
inline void prework(){
    for(int i=1;i<=n;i++){
        f[i][0]=a[i];
    }
    int t=log(n)/log(2)+1;
    for(int j=1;j<t;j++){
        for(int i=1;i+(1<<j)-1<=n;i++){
         f[i][j]=max(f[i][j-1],f[i+(i<<j-1)][j-1]);
 	   }
    }
     
}
```



```cpp
inline int query(int l,int r){
    int k=log(r-l+1)/log(2);
    return max(f[l][k],f[r-(1<<k)+1][k]);
}
```



[模板](https://www.luogu.com.cn/problem/P3865)

```cpp
 #include<bits/stdc++.h>
using  namespace std;

int n,m,x,y,a[100010],lg[100010],f[100010][20];

int main(){
    lg[1]=0;
    cin>>n>>m;
    for(int i=2;i<=n;i++){
        lg[i]=lg[i>>1]+1;
    }
    for (int i=1;i<=n;i++) cin>>f[i][0];
    for(int j=1;j<=lg[n];j++){
        for(int i=1;i<=n;i++){
       	 f[i][j]=max(f[i][j-1],f[i+(1<<(j-1))][j-1]);
		}
	}
    for(int i=1;i<=m;i++){
        cin>>x>>y;
        int l=lg[y-x+1];
        cout<<max(f[x][l],f[y-(1<<l)+1][l])<<endl;
	}
    return 0;
}
```

快读优化版

```cpp
//Sparse Table 稀疏表
#include<bits/stdc++.h>
using  namespace std;

int n,m,x,y,a[100010],lg[100010],f[100010][20];
inline int read()
{
    int x=0,f=1;char ch=getchar();
    while (ch<'0'||ch>'9'){if (ch=='-') f=-1;ch=getchar();}
    while (ch>='0'&&ch<='9'){x=x*10+ch-48;ch=getchar();}
    return x*f;
}
//注意输入和输出！！用快读和printf 不然狠狠滴TLE呜呜呜
int main(){
    lg[1]=0;
    n=read();m=read();
    for(int i=2;i<=n;i++){
        lg[i]=lg[i>>1]+1;
    }
    for (int i=1;i<=n;i++){
        f[i][0]=read();
    }  
    for(int j=1;j<=lg[n];j++){
        for(int i=1;i<=n-(1<<j)+1;i++){
       	 f[i][j]=max(f[i][j-1],f[i+(1<<(j-1))][j-1]);
		}
	}
    //求区间[的最大值
    for(int i=1;i<=m;i++){
        x=read(),y=read();
        int l=lg[y-x+1];
        printf("%d\n",max(f[x][l],f[y-(1<<l)+1][l]));
	}
    return 0;
}
```

