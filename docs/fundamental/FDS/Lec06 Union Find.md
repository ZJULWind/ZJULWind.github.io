# Lec06 Union Find

## 一、概念  

并查集主要由一个整型数组pre[ ]和两个函数find( )、join( )构成。  

数组 pre[ ] 记录了每个点的前驱节点是谁，函数 find(x) 用于查找指定节点 x 属于哪个集合，函数 join(x,y) 用于合并两个节点 x 和 y 。

## 二、实现  
### (1)pre数组 
根节点的上级是自己  
### (2)find函数:  
```c
int find(int x)                
{
    while(pre[x] != x)          
        x = pre[x];            
    return x;              
}
```
### (3)join函数：

```c
void join(int x,int y)                    
{
    int fx=find(x), fy=find(y);            
    if(fx != fy)                          
        pre[fx]=fy;                        
}
```

## 三、优化  
### (1)路径优化find函数  
思路：将x到根节点路径上的所有点的pre（上级）都设为根节点。
```c
int find(int x)                    
{
    if(pre[x] == x) return x;      
    return pre[x] = find(pre[x]);  
}
```
### (2)加权标记优化join函数
思路：所有节点都增设一个权值，用以表示该节点所在树中的高度。这样一来，在合并操作的时候就能通过这个权值的大小来决定谁当谁的上级
```c
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