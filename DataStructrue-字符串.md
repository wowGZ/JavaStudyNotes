---
title: DataStructure-字符串
---
# 字符串、数组和特殊矩阵

## 字符串基本数据结构和算法

字符串也是一种特殊的线性表，由于线性表有顺序存储和链式存储两种基本存储结构，因此字符串
也有两种基本存储结构：顺序串和链式串。

### 串的顺序存储结构

```c
#define MAXSIZE 100
typedef struct{
  char str[MAXSIZE];
  int length;
}seqstring;
```

### 顺序串的插入算法

```c
void strInsert(seqstring *s, int i, seqstring T){
  int k;
  if(i < 1 || i > s->length - 1 || s->length + T.length > MAXSIZE - 1){
    printf("cannot insert!");
  }
  else {
    for(k = s->length - 1; k >= i - 1; k--){
      s->str[T.length + k] = s-> str[k];
    }
    for(k = 0; k < t.length; k++){
      s->str[i + k - 1] = t.str[k];
    }
    s->length = s->length + t.length;
    s->str[s->length] = '\0';
  }
}
```

### 顺序串的删除算法

```c
void strdelete(seqstring *s, int i, int len){
    int k;
    if(i < 1 || i > s->length || i + len - 1 > s->length){
      printf("cannot delete! ");
    }
    else {
      for(k = i + len - 1;k < s->length ){
        s->str[k - len] = s->str[k];
      }
      s->length = s->length - len;
      s->str[s->length] = '\0';
    }
}
```

### 顺序串的连接运算算法

```c
seqstring * strconcat(seqstring s1, seqstring s2){
  int i;
  seqstring *r;
  if(s1.length + s2.length > MAXSIZE - 1){
    printf("cannot concat!");
    return (NULL);
  }
  else {
    r = (seqstring*)malloc(sizeof(seqstring));
    for(i = 0; i < s1.length; i++){
      r->str[i] = s1.str[i];
    }
    for(i = 0; i < s2.length; i++){
      r->str[s1.length] = s2.str[i];
    }
    r->length = s1.length + s2.length;
    r->str[r->length] = '\0';
  }
  return r;
}
```

### 求顺序串子串的算法

```c
seqstring *substring(seqstring s, int i, int len){
  int k;
  seqstring *r;
  if(i < 1 || i > s.length || i + len - 1 > s.length){
    printf("error!\n");
    return NULL;
  }
  else {
    r = (seqstring*)malloc(sizeof(seqstring));
    for(k = 0; k < len; k++){
      r->str[k] = s.str[i + k -1];
    }
    r->length = len;
    r->str[r->length] = '\0';
  }
  return r;
}
```

### 串的链式存储

```c
typedef struct node{
  char data;
  struct node *next;
}linkstrnode;
typedef linkstrnode *linkstring;
```

### 链式串的建立运算

```c
void strcreat(linkstring *s){
  char ch;
  linkstrnode *p, *r;
  *s = NULL;
  r = NULL;
  while ((ch = getchar()) != '\0'){
    p = (linkstrnode*)malloc(sizeof(linkstrnode));
    p->data = ch;
    if (*s == NULL){
      *s = p;
    }
    else {
      r->next = p;
      r = p;
    }
    if(r != NULL){
      r->next = NULL;
    }
  }
}
```

### 链式串的插入算法

```c
void strinsert(linkstring *s, int i, linkstring T){
  int k;
  linkstring p,q;
  p = *s;
  k = 1;
  while(p && k < i - 1){
    p = p->next;
    k++;
  }
  if(!p){
    printf("error!\n");
  }
  else {
    q = T;
    while(q && q->nexe){
      q = q->next;
    }
    q->next = p->next;
    p->next = T;
  }
}
```

### 链式串的删除算法

```c
void strdelete(linkstring *s, int i, int len){
  int k;
  linkstring p, q, r;
  p = *s;
  q = NULL;
  k = 1;
  while(p && k < i){
    q = p;
    p = p->next;
    k++;
  }
  if(!p){
    printf("error!\n");
  }
  else {
    k = 1;
    while(k < len && p){
      p = p->next;
      k++;
    }
    if(!p){
      printf("error!\n");
    }
    else {
      if(!p){
        r = *s;
        *s = p->next;
      }
      else {
        r = q->next;
        q->next = p->next;
      }
      p->next = NULL;
      while(r != NULL){
        p = r;
        r = r->next;
        free(p);
      }
    }
  }
}
```

### 链式串的连接算法

```c
void strconcat(linkstring *s1, linkstring s2){
  linkstring p;
  if(!(*s)){
    *s1 = s2;
    return;
  }
  else {
    p = *s;
    while(p->next){
      p = p->next;
    }
    p->next = s2;
  }
}
```

### 求链式串子串的算法

```c
linkstring substring (linkstring s, int i, len){
  int k;
  linkstring p, q, r, t;
  p = s;
  k = 1;
  while(p && k < i){
    p = p->next;
    k++;
  }
  if(!p){
    printf("error!\n");
    return NULL:
  }
  else {
    r = (linkstring)malloc(sizeof(linkstring));
    r->data = p->data;
    r->next = NULL;
    k = 1;
    q = t;
    while(p->next && k < len){
      p = p->next;
      k++;
      t = (linkstring)malloc(sizeof(linkstring));
      t->data = p->data;
      q->next = t;
      q = t;
    }
    if(k < len){
      pritnf("error!\n");
      return NULL;
    }
    else {
      q->next = NULL;
      return r;
    }
  }
}
```

## 字符串的模式匹配

### 朴素的模式匹配

朴素的模式匹配的基本思想是：用模式中的每一个字符去与正文中的自负一一比较。

```c
int index(seqstring p, seqstring t){
  int i, j, succ;
  i = 0;
  succ = 1;
  while((i <= t.length - p.length ) && (!succ)){
    j = 0;
    succ = 1;
    while((j < p.length -1) && succ){
      if(p.str[j] == t.str[i + j]){
        j++
      }
      else {
        succ = 0;
      }
      ++i;
    }
    if(succ){
      return i - 1;
    }
    else {
      return -1;
    }
  }
}
```
