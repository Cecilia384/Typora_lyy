5



```cpp
#include<bits/stdc++.h>
using namespace std;
#define MAXN 100100
#define ll long long int
/**
 * <啊哈算法>p92
 * BFS 走迷宫找人
*/
struct note{
    int x;//横坐标
    int y;//纵坐标
    int f;//父亲在队列中的编号（本题不要求输出路径，可以不需要f
    int s;//步数
};
struct note que[MAXN];//maxn=地图 长x宽
int a[100][100];
int book[100][100];
int tail,head;
int i,j,k,n,m,startx,starty,p,q,tx,ty,flag;

int main(){
	 int next[4][2]={{0,1},{1,0},//顺序：右下左上
            {0,-1},{-1,0}};
     cin>>n>>m;
     for(int i=1;i<=n;i++){
        for(int j=1;j<=m;j++){
            cin>>a[i][j];//输入地图
        }
     }
     cin>>startx>>starty>>p>>q;
     //队列初始化
     head=1;
     tail=1;
     //往队列插入迷宫入口坐标
     
     que[tail].x=startx;
     que[tail].y=starty;
     que[tail].f=0;
     que[tail].s=0;
     tail++;
     //并标记入口坐标处已经走过
     book[startx][starty]=1;
     flag=0;//用来标记是否到达目标点，0表示暂未到达，1表示到达
     //当队列不为空时循环
     while(head<tail){
        //枚举四个方向
        for(k=0;k<=3;k++){
            //计算下一个点的坐标
            tx=que[head].x+next[k][0];
            ty=que[head].y+next[k][1];
            //判是否越界
            if(tx<1||tx>n||ty<1||ty>m){
               continue;
             }
            //判断该点是否为障碍物或者已经在路径中
            if(a[tx][ty]==0&&book[tx][ty]==0){
                book[tx][ty]=1;//标记这个点已经走过
                // 注意，宽搜每个点只入队一次，
                //所以不需要将book数组还原
                book[tx][ty]=1;//插入新的点到队列中
                que[tail].x=tx;
                que[tail].y=ty;
                que[tail].f=head;
                que[tail].s=que[head].s+1;//步数是父亲步数+1
                tail++;
            }
            //如果到目标点，停止扩展，任务结束，退出循环
            if( tx==p && ty == q){
                flag=1;
                break;
            }
        }
         if(flag==1){
             break;
         }
         head++;//当一个点扩展结束以后，head++才能对后面的点再进行扩展
     }
    //打印队列中最后一个点的（目标点）的步数
    //注意tail是指向队列队尾的下一个位置，所以需要-1
    cout<<que[tail-1].s;
     getchar();
	return 0;
} 
```

