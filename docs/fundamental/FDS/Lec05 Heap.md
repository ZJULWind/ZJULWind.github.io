## 一、堆的概念  
首先，堆是一个完全二叉树，一般采取层序的顺序把他转化为一维数组。
1. 大根堆：每个结点的值都大于或等于其左右孩子结点的值
2. 小根堆：每个结点的值都小于或等于其左右孩子结点的值
牢记二叉树性质：编号i的父节点为[i/2],左孩2*i,右孩2*i+1。
## 二、堆的创建  
涉及到下溯和上溯。
1. 下溯：用于构造堆。维护堆的性质。
2. 上溯：用于插入元素。
```c
void PercolateUp( int p, PriorityQueue H )
{
    int t=H->Elements[p];
    while(t<H->Elements[p/2])
    {
        H->Elements[p]=H->Elements[p/2];
        p/=2;
    }
    H->Elements[p]=t;
}
void PercolateDown( int p, PriorityQueue H )
{
    int child,i,t=H->Elements[p];
    i=p;
    for(i=p;i*2<=H->Size;i=child)
    {
        child=2*i;
        if(child!=H->Size)
        {
            if(H->Elements[child]>H->Elements[child+1])child++;
        }
        if(t>H->Elements[child])
        {
            H->Elements[i]=H->Elements[child];
        }else break;
    }
    H->Elements[i]=t;
}
```

## 三、堆的删除
堆的删除一定是堆顶元素。
1. 判断堆是否为空，空堆不能删除
2. 堆顶去除，堆底到堆顶
3. size--
4. 新的堆顶下溯