---
title: DataStructure-线性表
---
内容摘自：数据结构（C语言版）第三版 李云清编著

# 线性表的顺序存储

## 顺序表

### 顺序表的存储结构

```c
#define MAXSIZE 100
typedef int datatype;
typedef struct{
    datatype a[MAXSIZE];
    int size;
}sequence_list;
```

### 顺序表的初始化——置空表

```c
void init(sequence_list *slt){
    slt -> size = 0;
}
```

### 在顺序表后部进行插入操作

```c
void append(sequence_list *slt, int x){
    if(slt -> size == MAXSIZE){
        printf("顺序表是满的！");
        exit(1);
    }
    slt -> a[alt -> size] = x;
    slt -> size = slt -> size + 1;
}
```

### 打印顺序表各个节点

```c
void display(sequence_list slt){
    int i;
    if(!slt.size)
        printf("\n顺序表是空的！");
    else{
        for(i = 0; i < slt.size; i++)
            printf("%5d",slt.a[i]);
    }
}
```

### 判断顺序表是否为空

```c
int empty(sequence_list slt){
    return(slt.size == 0 ? 1 : 0);
}
```

### 查找顺序表中值为x的节点的位置

```c
int search(sequence_list slt, int x){
    int i = 0;
    while(i < slt.size && slt.a[i] != x){
        i ++;
    }
    return (i < slt.size ? i : -1);
}
```

### 取得顺序表中第i个节点的值

```c
int get(sequence_list slt, int i){
    if(i < 0 || i >= slt.size){
        printf("\n指定位置节点不存在！");
        exit(1);
    }
    else{
    return slt.a[i];
    }
}
```

### 在顺序表的position位置处插入值为x的节点

所插入位置position之后的元素均需要向后移动一位，为避免已有数据被后移时所覆盖，所以从已有元素的最后一位开始后移操作。

```c
void insert(sequence_list *slt, int x, int position){
    int i;
    if(slt->size == MAXSIZE){
        printf("\n顺序表是满的，无法插入！");
        exit(1);
    }
    if(position < 0 || position > slt->size){
        printf("\n指定的插入位置不存在！");
        exit(1);
    }
    for(i = slt->size; i > position; i --){
        slt->a[i] = slt->a[i-1];
    }
    slt->a[position] = x;
    slt->size ++;
}
```

### 删除顺序表中第position位置的节点

同插入操作相似，需要将position位置之后的节点都向前移动一位，同样是为了避免数据因为覆盖而丢失，从position位置后第一位数据开始前移。

```c
void delete(sequence_list *slt, int position){
    int i;
    if(slt->size == 0){
        printf("\n顺序表为空！");
        exit(1);
    }
    if(position < 0 || position >= slt->size){
        printf("\n指定位置不存在！");
        exit(1);
    }
    for(i = position; i < slt->size - 1; i++){
        slt->a[i] = slt->a[i + 1];
    }
    slt->size --;
}
```

## 栈

栈是一种特殊的线性表，对于这种线性表，规定它的插入运算和删除运算均在线性表的同一端进行，进行插入和删除的那一端称为栈顶，另一端称为栈底。
栈具有后进先出，先进后出的性质的线性结构。

### 顺序栈的存储结构

```c
#define MAXSIZE 100
typedef int datatype;
type struct{
    datatype a[MAXSIZE];
    int top;
}sequence_stack;
```

### 栈的初始化

```c
void init(sequence_stack *st){
    st->top = 0;
}
```

### 判断栈是否为空

```c
int empty(sequence_stack st){
    return(st.top ? 0 : 1);
}
```

### 取得栈顶的节点值

```c
int read(sequence_stack st){
    if(empty(st)){
        printf("\n栈是空的！");
        exit(1);
    }
    else{
        return st.a[st.top - 1];
    }
}
```

### 栈的插入操作

```c
void push(sequence_stack *st, datatype x){
    if(st->top == MAXSIZE){
        printf("\nThe sequence stack is full!");
        exit(1);
    }
    st->a[st->top] = x;
    st->top ++;
}
```

### 栈的删除操作

```c
void pop(sequence_stack *st){
    if(st->top == 0){
        printf("\nThe sequence stack is empty!");
        exit(1);
    }
    st->top --;
}
```

## 队列

队列是一种特殊的线性表，它的特殊性在于队列的插入和删除操作分别在表的两端进行。插入的一端称为队尾，删除的一端称为队首。队列的插入和删除操作分别简称为
进队和出队。
队列是具有先进先出的性质的线性结构。

### 队列的存储结构

```c
#define MAXSIZE 100
typedef int datatype;
typedef struct{
    datatype a[MAXSIZE];
    int front;
    int rear;
}sequence_queue;
```

### 队列的初始化

```c
void init(sequence_queue *sq){
    sp->front = sq->rear = 0;
}
```

### 判断队列是否为空

```c
int empty(sequence_queue sq){
    return(sq.front == st.rear ? 1 : 0);
}
```

### 打印队列的各个节点值

```c
void display(sequence_queue sq){
    int i;
    if(empty(sq)){
        printf("\n队列是空的！");
    }
    else{
        for(i = sq.rear; i < sq.front; i++){
            printf("%5d",sq.a[i]);
        }
    }
}
```

### 取得队列的队首的节点值

```c
datatype get(sequence_queue sq){
    if(empty(sq)){
        printf("\n队列是空的！");
        exit(1);
    }
    return sq.a[sq.front];
}
```

### 队列的插入操作

```c
void insert(sequence_queue *sq, datatype x){
    int i;
    if(sq->rear == MAXSIZE){
        printf("\n顺序队列是满的！");
        exit(1);
    }
    sq->a[sq->rear] = x;
    sq->rear = sq->rear + 1;
}
```

### 队列的出队操作

```c
void delete(sequence_queue *sq){
    if(sq->front == sq->rear){
        printf("\n顺序队列是空的！")；
        exit(1);
    }
    sq->front ++;
}
```

## 顺序循环队列及其实现

为了有效的利用空间，将顺序存储的队列想象为一个环状，把数组中的最前和最后两个元素看作是
相邻的，这就是循环队列。
在循环队列中，如果队列中最后一个节点存放在数组的最后一个元素的位置。其他情况下的插入操作
和一般的队列的插入操作一样。
注意：此时出现问题，当数组空间被全部占用，队列已满，存在rear=front。但是，若队列为空，
条件rear=front仍然成立。这个问题如何解决呢？
一种方法是设置一个标志，标识是由rear增1使rear=front，还是由于front增1使rear=front，
前者是队满，后者是队空。
另一种方法是牺牲一个数组空间，即若数组的大小是MAXSIZE,则该数组所表示的循环队列最多
允许MAXSIZE-1个节点。
这样，循环队列满的条件是：（rear + 1）% MAXSIZE = front。
队列空的条件是：rear = front

### 循环队列插入操作

```c
void insert_sequence_queue(sequence_queue *sq, datatype x){
    if((sq->rear+1) % MAXSIZE == sq->front){
        printf("\n顺序循环队列是满的！无法进行插入！");
        exit(1);
    }
    sq->a[sq->rear+1] = x;
    sq->rear = (sq->rear+1) % MAXSIZE;
}
```

### 循环队列删除操作

```c
void delete_sequence_queue(sequence_queue *sq){
    if(sq->rear == sq->front){
        printf("\n循环队列是空的！无法进行删除操作！");
        exit(1);
    }
    sq->front = (sq->front + 1) % MAXSIZE;
}
```

# 线性表的链式存储

## 单链表

单链表是线性表链式存储的一种形式，其中的节点一般含有两个域，一个是存放数据信息的info域，另一个是指向该节点的后继节点存放指针next域。一个单链表必须
有一个首指针指向单链表中的第一个节点。

### 单链表的存储结构

```c
typedef int datatype;
typedef struct link_node{
    datatype info;
    struct link_node *next;
}node;
```

### 建立一个空的单链表

```c
node *init(){
    return NULL;
}
```

### 输出单链表中的各个节点的值

```bash
void display(node *head){
    node *p;
    p = head;
    if(!p){
        printf("\n单链表是空的！");
    }
    else{
        printf("\n单链表各个节点的值为：\n")；
        while(p){
            printf("%5d",p->info);
            p = p->next;
        }
    }
}
```

### 在单链表中查找第i个节点

```c
node *find(node *head, int i){
    int j = 1;
    node *p = head;
    if(i < 1){
        return NULL;
    }
    while(p && i != j){
        p = p->next;
    }
    return p;
}
```

### 在单链表中的第i个节点之后插入一个值为x的新节点

```c
node *insert(node *head, datatype x, int i){
    node *p,*q;
    p = find(head,i);
    if(!q && i != 0){
        printf("\n找不到第%d个节点，不能插入%d!", i, x);
    }
    else{
        p = (node*)malloc(sizeof(node));
        p->info = x;
        if(i == 0){
            p->next = head;
            head = p;
        }
        else{
            p->next = q->next;
            q->next = p;
        }
    }
}
```

### 在单链表中删除一个值为x的节点

```c
node *delete(node *head, datatype x){
    node *pre = NULL, *p;
    if(!head){
        printf("单链表是空的！");
        return head;
    }
    p = head;
    while(p && p->info != x){
        pre = p;
        p = p->next;
    }
    if(p){
        if(!pre){
            head = head->next;
        }
        else{
            pre = pre->next;
        }
        free(p);
    }
    return head;
}
```

## 带头节点的单链表

一般的单链表中，第一个节点由head指示，而在带头节点的单链表中，head指示的是所谓的头结点，它不是数据结构中的实际节点，第一个实际节点是head->next指
示的。在带头节点的单链表的操作实现时要注意这一点。

### 建立一个空的带头节点的单链表

```c
node *init(){
    node *head;
    head = (node*)malloc(sizeof(node));
    head->next = NULL;
    return head;
}
```

### 输出带头节点的单链表中各个节点的值

```c
void display(node *head){
    node *p;
    p = head->next;
    if(!p){
        printf("\n带头节点的单链表是空的！");
    }
    else{
        printf("\n带头节点的单链表各个节点的值为：\n");
        while(p){
            printf("%5d",p->info);
            p = p->next;
        }
    }
}
```

### 在带头节点的单链表中查找第i个节点

```c
node *find(node *head, int i){
    int j = 0;
    node *p = head;
    if(i < 0){
        printf("\n带头节点的单链表中不存在第%d个节点！",i);
        return NULL;
    }
    while(p && i != j){
        p = p->next;
        j ++;
    }
    return p;
}
```

### 在带头节点的单链表中第i个节点后插入一个值为x的新节点

```c
node *insert(node *head, datatype x, int i){
    node *p,*q;
    q = find(head, i);                      //查找带头节点的单链表中的第i个节点
                                            //i = 0，表示新节点插入在头结点之后，此时q指向的是头结点
    if(!q){                                 //没有找到
        printf("\n带头节点的单链表中不存在第%d个节点，不能插入%d", i, x);
        return head;
    }
    p = (node*)malloc(sizeof(node));        //为准备插入的新节点分配空间
    p->info = x;                            //为新节点设置值x
    p->next = q->next;                      //插入（1）
    q->next = p;                            //插入（2），当i = 0时，由于q指向的是头结点，本语句等价于head->next = p
    return head;
}
```

### 在带头结点的单链表中删除一个值为x的节点

```c
node *delete(node *head, datatype x){
    node *pre = head->,*q;                  //首先p指向头结点
    q = head->next;                         //q从带头节点的第一个实际节点开始找值为x的节点
    while(q && q->info != x){               //没有查找完并且还没有找到
        pre = q;                            //继续查找，pre指向q的前驱
        q = q->next;
    }
    if(q){
        pre->next = q->next;                //删除
        free(q);                            //释放空间
    }
    return head;
}
```

## 链式栈

栈的链式存储称为链式栈。链式栈就是一个特殊的单链表，对于这种特殊的单链表，它的插入和删除操作规定在单链表的同一端进行。链式栈的栈顶指针一般用top表示。

链式栈的节点定义同单链表的节点定义。

### 建立一个空的链式栈

```c
node *init(){
    return NULL;
}
```

### 判断链式栈是否为空

```c
int empty(node *top){
    return (top ? 0 : 1);
}
```

### 取得链式栈的栈顶节点值

```c
datatype read(node *top){
    if(!top){
        printf("\n链式栈是空的！");
        exit(1);
    }
    return (top->info);
}                                           //本函数可以调用empty（）函数
```

### 输出链式栈中各个节点的值

```c
void display(node *top){
    ndoe *p;
    p = top;
    printf("\n");
    if(!p){
        printf("\n链式栈是空的！")；
        while(p){
            printf("%5d",p->info);
            p = p->next;
        }
    }
}
```

### 向链式栈中插入一个人值为x的节点

```c
node *push(node *top, datatype x){
    node *p;
    p = (node*)malloc(sizeof(ndoe));
    p->info = x;
    p->next = top;
    top = p;
    return top;
}
```

### 删除链式栈的栈顶节点

```c
node *pop(node *top){
    node *p;
    if(!top){
        printf("\n链式栈是空的！")；
        return NULL;
    }
    q = top;
    top = top->next;
    free(q);
    return top;
}
```

## 链式队列

队列的链式存储成为链式队列，链式队列就是一个特殊的单链表，对于这种特殊的单链表，它的插入和删除操作规定在单链表的不同端进行。链式队列的队首和队尾指针
分别用front和rear表示。

链式队列的节点定义和单链表一样。队列必须有队首和队尾指针，因此增加定义一个结构类型，其中两个域分别为队首和队尾指针。

### 链式队列的存储结构

```c
typedef int datatype;
typedef struct link_node{
    datatype info;
    struct link_node *next;
}node;
typedef struct{
    node *front, *rear;                     //定义队首和队尾
}queue;
```

### 建立一个空的链式队列

```c
queue *init(){
    queue *qu;
    qu = (queue*)malloc(sizeof(queue));
    qu->front = NULL;
    qu->rear = NULL;
    return qu;
}
```

### 判断链式队列是否为空

```c
int empty(queue qu){
    return (qu.front ? 0 : 1);
}
```

### 输出链式队列中的各个节点的值

```c
void display(queue *qu){
    node *p;
    printf("\n");
    p = qu->front;
    if(!p){
        printf("\nThe link queue is empty!");
    }
    while(p){
        printf("%5d",pu->info);
        p = p->next;
    }
}
```

### 取得链式队列的队首节点值

```c
datatype read(queue qu){
    if(!qu.front){
        printf("\n链式队列是空的！");
        exit(1);
    }
    return(qu->info);
}
```

### 向链式队列中插入一个值为x的节点

```c
queue *insert(queue *qu, datatype x){
    node *p;
    p = (node *)malloc(sizeof(node));       //分配空间
    p->info = x;                            //设置新节点的值
    p->next = NULL;
    if(qu->front == NULL){                  //当前队列为空，新插入的节点为队列中唯一一个节点
        que->front = qu->rear = p;
    }
    else{
        qu->rear->next = p;                 //队尾插入
        qu->rear = p;
    }
    return qu;
}
```

### 删除链式队列中的队首节点

```c
queue *delete(queue *p){
    node *p;
    if(qu->front){
        printf("\/队列为空，无法删除！")；
        return qu;
    }
    q = qu->front;
    qu->front = q->next;
    free(q);
    if(qu->front == NULL){
        qu->rear = NULL;
    }
    return qu;
}
```
