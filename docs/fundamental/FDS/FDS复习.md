[fds复习](FDS-Review.pdf)
## 一、记录一些性质
·对树来说，如果有N个结点，那么有N-1条边。

·对二叉树来说 n0=n2+1

·对完全二叉树（或者堆）来说，如果根节点的序号为1，那么左孩为2i,右孩为2i+1,所以对于任意孩子，他们的parent都是\[i/2]

·对于图来说度的和为2|E|

·欧拉环--连通图且每个度为偶数；欧拉路-两个度为奇且从奇数开始

## 二、猜测考的代码段
### 1.树-遍历
递归
```c
void preorder(Tree T)
{
	if (T=NULL)return;
	printf(T.data);
	preorder(T.left);
	preorder(T.right);
}

void inorder(Tree T)
{
	if (T=NULL)return;
	inorder(T.left);
	printf(T.data);
	inorder(T.right);
}

void postorder(Tree T)
{
	if (T=NULL)return;
	postorder(T.left);
	postorder(T.right);
	printf(T.data);
}

void levelorder(Tree T)
{
	int queue[maxn];
	int front.rear;
	
	enqueue(T.data,s);
	while (!isempty(q))
	{
		printf(q.front);
		dequeue(q);
		for(each child)
		{
			enqueue(child,s);
		}
			
	}
}
```

非递归中序
```c
void iter_inorder(Tree T)
{
	stack s;
	while(1)
	{
		for(;T;T=T.left){
			push(T,s);
		}
		T=top(s);
		pop(s);;
		
		if(T=NULL) break;
		print(T.data);
		T=T.right;
	}	
}
```
### 2.堆-上溯下溯
```c
void percolateup (int p,pq H)
{
	int t=H.element[p];
	for(t<H.element[p/2])
	{
		H.element[p]=H.element[p/2];
		p=p/2;
	}
	H.element[p]=t;
}

void percolatedown(int p,pq H)
{
	int child ,i ,t=H.element[p];
	for(i=p;i*2<=H.size;i=child)
	{
		child=2*i;
		if(child!=H.size)
		{
			if(H.element[child+1]<H.element[child])child=child+1;
		}
		if(t>H.element[child])
		{
			H.element[i]=H.elemnt[child];
		}
		else break;
		H.element[i]=t;
	}
}


#对一个数组建堆
void percolatedown(int a[],int start,int end)
{
	int t=a[start];
	for(int i=2*start+1;i<=end;i=i*2+1)
	{
		if(i<end)
		{
			if(a[i]<a[i+1])i++;
			if(a[i]>t)
			{
				a[start]=a[i];
				start=i;
			}
		}
		else break;
	}
	a[start]=t;
}
for(int i=n/2-1;i>=0;i--)
{
	percolatedown(c,i,n-1)
}
```

### 3.并查集
```c
int find(int x)                
{
    while(pre[x] != x)          
        x = pre[x];            
    return x;              
}

void join(int x,int y)                    
{
    int fx=find(x), fy=find(y);            
    if(fx != fy)                          
        pre[fx]=fy;                        
}
```
优化
```c
int find(int x)                    
{
    if(pre[x] == x) return x;      
    return pre[x] = find(pre[x]);  
}

void union(int x,int y)
{
    x=find(x);                          //寻找 x的代表元
    y=find(y);                          //寻找 y的代表元
    if(x==y) return ;                   //如果 x和 y的代表元一致，说明他们共属同一集合，则不需要合并，直接返回；否则，执行下面的逻辑
    if(rank[x]>rank[y]) pre[y]=x;       //如果 x的高度大于 y，则令 y的上级为 x
    else                                
    {
        if(rank[x]==rank[y]) rank[y]++; //如果 x的高度和 y的高度相同，则令 y的高度加1
        pre[x]=y;                       //让 x的上级为 y
    }
}
```


## 三、时间复杂度汇总
[老师我学不会时间复杂度](https://blog.csdn.net/csyifanZhang/article/details/107009215)
