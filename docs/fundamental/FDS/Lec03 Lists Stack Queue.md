## 一、表(Lists)
几种链表

1. 单向表
2. 单向循环链表
3. 双向链表
4. 带有头节点的双向链表
5. 顺序表

题目  
1. For a sequentially stored linear list of length N, the time complexities for deleting the first element and inserting the last element are O(1) and O(N), respectively.错误
## 二、栈(Stack)
### (1)定义
操作表

1. int Isempty(Stack S);
2. Stack CreateStack(void);
3. void Push(Stack S);
4. void Top(Stack S);
5. void Pop(Stack S);  
### (2)实现

```c
#define MAXSIZE 50  //定义栈中元素的最大个数
//1.定义
typedef int ElemType;   //ElemType的类型根据实际情况而定，这里假定为int
typedef struct{
    ElemType data[MAXSIZE];
    int top;    //用于栈顶指针
}SqStack;

//2，初始化
void InitStack(SqStack *S){
    S->top = -1;    //初始化栈顶指针
}

//3.判断是否为空
bool StackEmpty(SqStack *S){
    if(S->top == -1){    
        return true;    //栈空
    }else{  
        return false;   //不空
    }
}

//4.出栈
void pop(SqStack *S)
{
    if(StackEmpty(S)==true)printf("ERROR");
    else printf("%d",S->data[s->top]);
    S->top--;
}

//5.入栈
void Push(SqStack *S, ElemType e){
    //满栈
    if(S->top == MAXSIZE-1){
        return ERROR;
    }
    S->top++;   //栈顶指针增加一
    S->data[S->top] = e;    //将新插入元素赋值给栈顶空间
    return 1;
}

//6.读栈顶元素 top 省略一下
```
###  (3)应用  
1. **计算一个后缀表达式**：遇到一个操作符将栈顶两个元素弹出进行运算然后压入栈
2. **中缀表达式转后缀表达式**：操作数立刻输出，操作符号压栈

## 三、队列(Queus)

### (1)定义
定义了队头front，队尾rear，队头出，队尾进  

操作表  

1. InitQueue(&Q)
2. QueueEmpty(Q)
3. **EnQueue(&Q, x)**
4. **DeQueue(&Q, &x)**
5. GetHead(Q, &x)
### (2)实现
代码实现中，一般用front=rear来判断队列是否为空，用$(rear+1)\% MAX\_SIZE==front$来判断是否为满。  
```c
#define MAXSIZE 50  //定义队列中元素的最大个数

typedef struct{
    ElemType data[MAXSIZE]; //存放队列元素
    int front,rear;
}SqQueue;

// 初始状态（队空条件）：Q->front == Q->rear == 0。
// 进队操作：队不满时，先送值到队尾元素，再将队尾指针加1。
// 出队操作：队不空时，先取队头元素值，再将队头指针加1。

// 循环队列
// 初始时：Q->front = Q->rear=0。
// 队首指针进1：Q->front = (Q->front + 1) % MAXSIZE。
// 队尾指针进1：Q->rear = (Q->rear + 1) % MAXSIZE。
// 队列长度：(Q->rear - Q->front + MAXSIZE) % MAXSIZE。
```
### (3)应用  
1. 顺序队列
2. 循环队列：rear要超过数组大小的时候，把他转到0
3. 双端队列：可以在rear出列