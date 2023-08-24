# 有向图

将任意有向图转化为强连通，需要$\max(p,q)$条有向边，其中$p$和$q$表示零入度点和零出度点的个数

注意重边

```c++
//有向图tanjan
namespace tanjan
{
	vector<int>G[N];
	int st[N], ins[N], c[N];	//ins表示已经找到的点中不在环上的点，标记为1 
	int dfn[N], low[N];
	vector<int>scc[N];
	int ind = 0, top = 0, cnt = 0;
	void add(int x, int y){G[x].push_back(y);}
	void tanjan(int x)
	{
		dfn[x] = low[x] = ++ind;
		st[++top] = x, ins[x] = 1;
		for(auto y:G[x])
		{
			if(!dfn[y])
			{
				tanjan(y);
				low[x] = min(low[x], low[y]);
			}
			else if(ins[y])
			{
				low[x] = min(low[x], dfn[y]);
			}
		}
		if(low[x] == dfn[x])
		{
			cnt++;
			int y;
			do{
				y = st[top--]; ins[y] = 0;
				c[y] = cnt; scc[cnt].push_back(y);
			}while(x != y);
		}
	}
	
	void solve(int n)
	{
		for(int i = 1; i <= n; ++i)
		{
			if(!dfn[i]) tanjan(i);
		}
	} 
	
	vector<int>G_c[N];
	void add_c(int x, int y){ G_c[x].push_back(y);}
	
	void get(int n)	//缩点
	{
		for(int x = 1; x <= n; ++x)
		{
			for(auto y:G[x])
			{
				if(c[x] == c[y])continue;
				add_c(c[x],c[y]);
			}
		}
	 } 
} 
using tanjan::add;
void solve()
{
	int n,m;cin>>n>>m;
	for(int i=1;i<=m;++i)
	{
		int x,y;cin>>x>>y;
		add(x,y); 
	}
	tanjan::solve(n);
}
```

