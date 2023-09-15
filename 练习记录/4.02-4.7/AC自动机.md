### [普通版](https://www.luogu.com.cn/blog/juruohyfhaha/ac-zi-dong-ji)

```cpp
#include<bits/stdc++.h>
#define maxn 1000001
using namespace std;
struct kkk{
    int son[26],flag,fail;
}trie[maxn];
int n,cnt;
char s[1000001];
queue<int >q;
void insert(char* s){
    int u=1,len=strlen(s);
    for(int i=0;i<len;i++){
        int v=s[i]-'a';
        if(!trie[u].son[v])trie[u].son[v]=++cnt;
        u=trie[u].son[v];
    }
    trie[u].flag++;
}
void getFail(){
    for(int i=0;i<26;i++)trie[0].son[i]=1;          //初始化0的所有儿子都是1
    q.push(1);trie[1].fail=0;               //将根压入队列
    while(!q.empty()){
        int u=q.front();q.pop();
        for(int i=0;i<26;i++){              //遍历所有儿子
            int v=trie[u].son[i];           //处理u的i儿子的fail，这样就可以不用记父亲了
            int Fail=trie[u].fail;          //就是fafail，trie[Fail].son[i]就是和v值相同的点
            if(!v){trie[u].son[i]=trie[Fail].son[i];continue;}  //不存在该节点，第二种情况
            trie[v].fail=trie[Fail].son[i]; //第三种情况，直接指就可以了
            q.push(v);                      //存在实节点才压入队列
        }
    }
}
int query(char* s){
    int u=1,ans=0,len=strlen(s);
    for(int i=0;i<len;i++){
        int v=s[i]-'a';
        int k=trie[u].son[v];       //跳Fail
        while(k>1&&trie[k].flag!=-1){   //经过就不统计了
            ans+=trie[k].flag,trie[k].flag=-1;  //累加上这个位置的模式串个数，标记已经过
            k=trie[k].fail;         //继续跳Fail
        }
        u=trie[u].son[v];           //到下一个儿子
    }
    return ans;
}
int main(){
    cnt=1;            //代码实现细节，编号从1开始
        scanf("%d",&n);
    for(int i=1;i<=n;i++){
        scanf("%s",s);
        insert(s);
    }
    getFail();
    scanf("%s",s);
    printf("%d\n",query(s));
    return 0;
}
```





### 加强版

首先题目统计的是出现次数最多的字符串，所以有重复的字符串是没有关系的。（因为后面的会覆盖前面的，统计的答案也是一样的）

那么我们就将标记模式串的flag设为当前是第几个模式串。就是下面插入时的变化：

```cpp
trie[u].flag++;
变为
trie[u].flag=num; //num表示该字符串是第num个输入的
```

求Fail指针没有变化，原先怎么求就怎么求。

**查询**：我们开一个数组vis，表示第i个字符串出现的次数。

因为是重复计算，所以不能标记为-1了。

我们每经过一个点，如果有模式串标记，就将vis[模式串标记]++。然后继续跳fail。

这样我们就可以将每个模式串的出现次数统计出来。剩下的大家应该都会QwQ！

```cpp
//AC自动机加强版
#include<bits/stdc++.h>
#define maxn 1000001
using namespace std;
char s[151][maxn],T[maxn];
int n,cnt,vis[maxn],ans;
struct kkk{
	int son[26],fail,flag;
	void clear(){memset(son,0,sizeof(son));fail=flag=0;}
}trie[maxn];
queue<int>q;
void insert(char* s,int num){
	int u=1,len=strlen(s);
	for(int i=0;i<len;i++){
		int v=s[i]-'a';
		if(!trie[u].son[v])trie[u].son[v]=++cnt;
		u=trie[u].son[v];
	}
	trie[u].flag=num;			//变化1：标记为第num个出现的字符串
}
void getFail(){
	for(int i=0;i<26;i++)trie[0].son[i]=1;
	q.push(1);trie[1].fail=0;
	while(!q.empty()){
		int u=q.front();q.pop();
		int Fail=trie[u].fail;
		for(int i=0;i<26;i++){
			int v=trie[u].son[i];
			if(!v){trie[u].son[i]=trie[Fail].son[i];continue;}
			trie[v].fail=trie[Fail].son[i];
			q.push(v);
		}
	}
}
void query(char* s){
	int u=1,len=strlen(s);
	for(int i=0;i<len;i++){
		int v=s[i]-'a';
		int k=trie[u].son[v];
		while(k>1){
			if(trie[k].flag)vis[trie[k].flag]++;	//如果有模式串标记，更新出现次数
			k=trie[k].fail;
		}
		u=trie[u].son[v];
	}
}
void clear(){
	for(int i=0;i<=cnt;i++)trie[i].clear();
	for(int i=1;i<=n;i++)vis[i]=0;
	cnt=1;ans=0;
}
int main(){
	while(1){
		scanf("%d",&n);if(!n)break;
		clear();
		for(int i=1;i<=n;i++){
			scanf("%s",s[i]);
			insert(s[i],i);
		}
		scanf("%s",T);
		getFail();
		query(T);
		for(int i=1;i<=n;i++)ans=max(vis[i],ans);	//最后统计答案
		printf("%d\n",ans);
		for(int i=1;i<=n;i++)
		if(vis[i]==ans)
		printf("%s\n",s[i]);
	}
}
```

O(模式串长度 · 文本串长度)



### 二次加强（拓扑

## 拓扑建图优化

让我们来分析一下刚才那个程序的时间复杂度，算了不分析了，直接告诉你吧，这样暴力去跳fail的最坏时间复杂度是O(模式串长度 ·  文本串长度)。为什么？因为对于每一次跳fail我们都只使深度减1，那样深度(深度最深是模式串长度)是多少，每一次跳的时间复杂度就是多少。那么还要乘上文本串长度，就几乎是 O(模式串长度 · 文本串长度)的了。

那么模板1的时间复杂度为什么就只有O(模式串总长)。因为每一个Trie上的点都只会经过一次（打了标记），但刚才那个程序每一个点就不止经过一次了，所以时间复杂度就爆炸了。

那么我们可不可以让刚才那个程序的Trie上每个点只经过一次呢？让时间复杂度降至O(模式串总长)呢？

##### 做法：拓扑排序

让我们把Trie上的fail都想象成一条条有向边，那么我们如果在一个点使那个点进行一些操作，那么沿着这个点连出去的点也会进行操作（就是跳fail），所以我们才要暴力跳fail去更新之后的点。

#### 代码实现：

首先是getfail这里，记得将fail的入度更新。

```cpp
trie[v].fail=trie[Fail].son[i]; in[trie[v].fail]++;  	//记得加上入度
```

然后是query，不用暴力跳fail了，直接打上标记就行了，很简单吧

```cpp
void query(char* s){
	int u=1,len=strlen(s);
	for(int i=0;i<len;++i)
	u=trie[u].son[s[i]-'a'],trie[u].ans++;							//直接打上标记
}
```

最后是拓扑，解释都在注释里了OwO!

```cpp
void topu(){
	for(int i=1;i<=cnt;++i)
	if(in[i]==0)q.push(i);				//将入度为0的点全部压入队列里
	while(!q.empty()){
		int u=q.front();q.pop();vis[trie[u].flag]=trie[u].ans;	//如果有flag标记就更新vis数组
		int v=trie[u].fail;in[v]--;		//将唯一连出去的出边fail的入度减去（拓扑排序的操作）
		trie[v].ans+=trie[u].ans;		//更新fail的ans值
		if(in[v]==0)q.push(v);			//拓扑排序常规操作
	}
}
```

code

```cpp
#include<bits/stdc++.h>
#define maxn 2000001
using namespace std;
char s[maxn],T[maxn];
int n,cnt,vis[200051],ans,in[maxn],Map[maxn];
struct kkk{
    int son[26],fail,flag,ans;
    void clear(){memset(son,0,sizeof(son)),fail=flag=ans=0;}
}trie[maxn];
queue<int>q;
void insert(char* s,int num){
    int u=1,len=strlen(s);
    for(int i=0;i<len;i++){
        int v=s[i]-'a';
        if(!trie[u].son[v])trie[u].son[v]=++cnt;
        u=trie[u].son[v];
    }
    if(!trie[u].flag)trie[u].flag=num;
    Map[num]=trie[u].flag;
}
void getFail(){
    for(int i=0;i<26;i++)trie[0].son[i]=1;
    q.push(1);
    while(!q.empty()){
        int u=q.front();q.pop();
        int Fail=trie[u].fail;
        for(int i=0;i<26;i++){
            int v=trie[u].son[i];
            if(!v){trie[u].son[i]=trie[Fail].son[i];continue;}
            trie[v].fail=trie[Fail].son[i]; in[trie[v].fail]++;
            q.push(v);
        }
    }
}
void topu(){
    for(int i=1;i<=cnt;i++)
    if(in[i]==0)q.push(i);
    while(!q.empty()){
        int u=q.front();q.pop();vis[trie[u].flag]=trie[u].ans;
        int v=trie[u].fail;in[v]--;
        trie[v].ans+=trie[u].ans;
        if(in[v]==0)q.push(v);
    }
}
void query(char* s){
    int u=1,len=strlen(s);
    for(int i=0;i<len;i++)
    u=trie[u].son[s[i]-'a'],trie[u].ans++;
}
int main(){
    scanf("%d",&n); cnt=1;
    for(int i=1;i<=n;i++){
        scanf("%s",s);
        insert(s,i);
    }getFail();scanf("%s",T);
    query(T);topu();
    for(int i=1;i<=n;i++)printf("%d\n",vis[Map[i]]);
}
```

