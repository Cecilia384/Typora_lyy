1.

~~~c++
#include<bits/stdc++.h>
using namespace std;
#define MAXN 10010
#define ll long long int
/**
 * <啊哈算法>p86
 * DFS 走迷宫找人
*/
int n,m,p,q,minx=99999999;//先给min一个极大值
int a[MAXN][MAXN],book[MAXN][MAXN];
void dfs(int x,int y,int step){
    int next[4][2]={{0,1},{1,0},//顺序：右下左上
            {0,-1},{-1,0}};
    int tx,ty,k;
    if(x==p&&y==q){
        //更新最小值
        if(step<minx){
            minx=step;
        }
        return;
    }
    //枚举四种走法
    for(k=0;k<=3;k++){
        //计算下一个点的坐标
        tx=x+next[k][0];
        ty=y+next[k][1];
        //判是否越界
        if(tx<1||tx>n||ty<1||ty>m){
            continue;
        }
        //判断该点是否为障碍物或者已经在路径中
        if(a[tx][ty]==0&&book[tx][ty]==0){
            book[tx][ty]=1;//标记这个点已经走过
            dfs(tx,ty,step+1);//开始尝试下一个点，递
            //book[tx][ty]=0;//尝试结束，取消这个点的标记

        }
    }
    return;
}
int main(){
	 int i,j,startx,starty;
     cin>>n>>m;
     for(int i=1;i<=n;i++){
        for(int j=1;j<=m;j++){
            cin>>a[i][j];
        }
     }
     cin>>startx>>starty>>p>>q;
     book[startx][starty]=1;
     dfs(startx,starty,0);//初始步数为0
     cout<<minx;
     getchar();
	return 0;
} 
~~~



#### 12.28 dfs板子题

![image-20221228161453635](dfs%E6%9D%BF%E5%AD%90.assets/image-20221228161453635.png)

（演佬

<img src="dfs%E6%9D%BF%E5%AD%90.assets/image-20221228161715210.png" alt="image-20221228161715210" style="zoom:80%;" />



~~~cpp
#include <bits/stdc++.h>
using namespace std;
typedef unsigned long long ll;
const int N = 1e5;
int a[N],vis[N],n;
void dfs(int x)
{
    if(x>n)
    {
        for(int i=1;i<=n;i++)
            cout<<a[i]<<' ';
        cout<<endl;
    }
    for(int i=1;i<=n;i++)
    {
        if(!vis[i]&&x!=i)//-
        {
            a[x]=i;
            vis[i]=1;
            dfs(x+1);
            vis[i]=0;
        }
    }
   
}
int main()
{
    ios::sync_with_stdio(0);
    cin.tie(0);
    cin>>n;
    dfs(1);
}
~~~





>**if( ! vis[i] && x ! = i )**

  my code

~~~cpp
#include<bits/stdc++.h>
#include<iomanip>
using namespace std;

int a[15],book[15],n,r;
int f=1;
void dfs(int step)
{
    int i;
    if(step==n+1){ 
    f=1;//在这里加了一个f来判断
        //实际上还是没有实现剪枝
        
        for(int i=1;i<=n;i++){ 
           if(a[i]==i){
           	f=0;
           }
        }
        if(f){
        	for(int i=1;i<=n;i++){ 
            cout <<" "<< a[i];
        } cout<<"\n";
        }
         
        return;   //回到前一层
    }
    for(int i=1;i<=n;i++){  
        //这里其实改一下就好
        //if(!book[i] && step!=i )
        if(book[i]==0){  
            a[step]=i;  
            book[i]=1; 
            dfs(step+1);//直接进行下一次调用
            book[i]=0; 
        }
    }
    return;
}
int main(){
    cin>>n;
    a[0]=1;
    dfs(1);
    getchar();getchar();
    return 0;

}
~~~



