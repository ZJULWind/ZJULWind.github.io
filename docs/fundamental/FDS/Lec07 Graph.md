# 一、图的概念
有向图
无向图
简单图：不存在重复边，不存在顶点到自身的边
多重图：某两个结点之间的边数多于一条，允许与自己连
完全图：简单图的特例，每两个结点均相连
子图
连通、连通图、连通分量
**强连通：v到w与w到v均有路径**
强连通图、强连通分量
**生成树与生成森林**
![[Attachments/Lec07 Graph_image_1.png]]
度
权
网：带权图
稠密图、稀疏图
路径、路径长度、回路
简单路径、简单回路：顶点不重复出现
距离：u到v的最短路径若存在，则为u到v的距离，否则距离为无穷
有向树：一个顶点的入度为0，其余顶点出度均为1

# 二、图的存储结构
## 1.邻接矩阵
利用一个二维数组来存储，查询行列即可。
## 2.邻接表
每一个结点u指向的结点vi，依附于一个开头为u的单链表
```c
#来自pta的一个邻接表模型
typedef struct AdjVNode *PtrToAdjVNode; 
struct AdjVNode{
    Vertex AdjV;
    PtrToAdjVNode Next;
};

typedef struct Vnode{
    PtrToAdjVNode FirstEdge;
} AdjList[MaxVertexNum];

typedef struct GNode *PtrToGNode;
struct GNode{  
    int Nv;
    int Ne;
    AdjList G;
};
typedef PtrToGNode LGraph;
```
## 3.邻接多重表
多用于无向图
每一个顶点用一个结点表示
$$data| firstedge$$
每一个边也用一个结点表示
$$
ivex|ilink|jvex|jlink
$$
解释：**其中ivex和jvex是与某条边依附的两个顶点在顶点表中下标。ilink 指向依附顶点ivex的下一条边，jlink 指向依附顶点jvex的下一条边。**

![[Attachments/Lec07 Graph_image_2.png]]


# 三、拓扑排序
有向无环图一定是拓扑序列
拓扑排序就是只有从前指向后的边，没有从后指向前的边，如果是一个有向无环图，那么一定有一个点的入度为0。
## 1.排序思路
如果有入度为0的点，那么入队，将队列里的点依次出列，找到所有与这个点相邻的点，删除这条边（入度-1），如果所有都入队，那么是一个拓扑排序。
## 2.代码实现

# 四、最短路问题

基本的思路： 
1. 在未访问的顶点中，寻找一个和目标距离最短的顶点V
2. 如果没有找到，就停止，如果找到了，将V标记位已访问
3. 对所有和V相邻的节点W，更新最多路径距离的值
# 五、Network Flow Problems最大流问题
最大流问题，决定最大能入多少管道
![[Attachments/Lec07 Graph_image_3.png]]
## A Simple Algorithm
1. 三幅图 原图-流图-残差图
![[Attachments/Lec07 Graph_image_4.png]]
2. augmenting path 增长通路
![[Attachments/Lec07 Graph_image_5.png]]
选定一条路径，取最大的流量，在流图上添加流量，在残差图上进行做差，如果残差图中为0那么删除
## To Be Greedy 如果先选最大路径
我们需要做的操作：支持撤回并需要画反向边
这个算法在G中有环依旧可行
## Analysis
T = $O( f |E|)$ where  f  is the maximum flow.
$$ T = T_{augmentation} * T_{find a path}$$
$$ = O( |E| log_{capmax} ) * O( |E| log |V| )$$
$$
= O( |E|^2 log |V| )
$$
# 六、Minimum Spanning Tree最小生成树
## 概念
### 生成树
【Definition】 A spanning tree of a graph G is a tree which consists of V( G ) and a subset of E( G ) 
这说明顶点和边都为原图中存在的
#### note一些性质
1. 如果存在spanning tree 那原图一定是联通的
2. spanning tree不唯一
3. 仅有n-1条边，这是树的性质。
4. 无环

### 最小生成树MST
生成树中权重和最小的一个，也有可能是不唯一的
## 算法
### Prim’s Algorithm
类似于
### Kruskal’s Algorithm
1. 使用堆，把每个权重丢进去
2. 每次取最小；
3. 判断是否形成cycle，如果不是就加进去，如果是就丢掉这条边
#### note
判断是否是cycle的时候必须要使用并查集
```
void Kruskal ( Graph G )
{   
	T = { } ;
    while  ( T contains less than |V| -1 edges && E is not empty ) 
    {
        choose a least cost edge (v, w) from E ;
        delete (v, w) from E ;
        if  ( (v, w) does not create a cycle in T )    
		  add (v, w) to T ;// Union / Find
        else    
		  discard (v, w) ;
    }
    if  ( T contains fewer than |V| -1 edges )
        Error ( “No spanning tree” ) ;
}
```

# 七、DFS深度优先遍历
深度优先遍历算法
![[Attachments/Lec07 Graph_image_6.png]]
## 无向图找联通单元
```
void ListComponents ( Graph G )
{   for ( each V in G )
        if ( !visited[ V ] ) {
			DFS( V );
            printf(“\n“);
        }
}
```
## 双联通性
Articulation point关节点
### 定义
1. v is an **articulation point** if G’ = DeleteVertex(G, v) has at least 2 connected components.
2. G is a **biconnected graph** if G is connected and has no articulation points.
3. A **biconnected component** is a maximal biconnected subgraph.
### 找关节点
1. 用深度优先生成一个深度优先树，标出深度优先访问顺序
2. 虚线画出回边（back edges）
3. 对根节点：查看有几个孩子，超过一个就行；对叶结点， 直接不考虑；对其他，需要它不能在向下走的时候碰到回边。
![[Attachments/Lec07 Graph_image_7.png]]
#### 性质
深度优先树中祖先的深度顺序一定小于孩子的深度顺序，后文我们用这个性质来进行程序的实现
### 程序实现
Low(u)![[Attachments/Lec07 Graph_image_8.png]]对非根非叶结点：要求Low(child)>=Num(u)，就是一个关节点（这说明它的下方没有路径通向它上方）

## Euler Circuits欧拉环
欧拉路径与欧拉环
![[Attachments/Lec07 Graph_image_9.png]]
要求条件
欧拉回路定理与欧拉路径定理
![[Attachments/Lec07 Graph_image_10.png]]
用深度优先搜索找到路径

# 题目
1.For a graph, if each vertex has an even degree or only two vertexes have odd degree, we can find a cycle that visits every edge exactly once 错误
