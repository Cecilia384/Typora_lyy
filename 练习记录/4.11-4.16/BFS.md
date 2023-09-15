bfs是一层一层搜的 框架如下

```cpp
//bfs模板
struct ed
{
	.....
}
deque<ed>q;
void bfs()
{
	标记起点 
	起点入队列 
	while(!q.empty())//队列不为空 
	{
		ed nw=q.front();//返回队首
		for(拓展出接下来可能的状态)
		{
			ed nxt;
			记录这一状态
			判断状态是否合法 
			标记状态 
			q.push_back(nxt);//状态入队列 
		}
		q.pop_front();//弹出队首 
	}
}
```