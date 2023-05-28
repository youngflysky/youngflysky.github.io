---
title: "09-List Leaves"
subtitle: "PTA 陈越数据结构第 9 题"
layout: post
author: "youngflysky"
date: 2022-04-25 23:48:12
header-style: text
catalog: true
tags:
- C++
- OJ笔记
- 算法
---

> - **[PTA OJ 网页](https://pintia.cn/problem-sets?tab=0)**
> - **[源代码 GitHub 地址](https://github.com/youngflysky/DateStruct/blob/main/ChengYueDataStruct/PTA/09-List%20Leaves.cpp)**
> - **[数据结构_中国大学MOOC(慕课)](https://www.icourse163.org/learn/ZJU-93001?tid=1466830443#/learn/announce)**
> - **[YFS Blog 原创](https://youngflysky.fun/)**

---

<br/>

# **09-List Leaves** 

> 1. **使用静态链表存储二叉树；**
> 2. **使用层次遍历方式以由上至下、由左至右的顺序打印叶子节点；**
> 3. **<strong style="color:#c00000;">层次遍历只能通过队列以非递归方式实现</strong>**

## <strong style="color:#0070c0;"> (1)	题目:</strong>

- **Given a tree, you are supposed to list all the leaves in the order of top down, and left to right.**

- **Input Specification:**

  Each input file contains one test case. For each case, the first line gives a positive integer *N* (≤10) which is the total number of nodes in the tree -- and hence the nodes are numbered from 0 to *N*−1. Then *N* lines follow, each corresponds to a node, and gives the indices of the left and right children of the node. If the child does not exist, a "-" will be put at the position. Any pair of children are separated by a space.

- **Output Specification:**
  
  For each test case, print in one line all the leaves' indices in the order of top down, and left to right. There must be exactly one space between any adjacent numbers, and no extra space at the end of the line.
  
- **Sample Input:**
  
   ```cpp
    8
     1 -
     - -
     0 -
     2 7
     - -
     - -
     5 -
     4 6
   ```
  
   
  
- **Sample Output:**
 ```cpp
  4 1 5
 ```

---

## <strong style="color:#0070c0;">(2)	解:</strong>
- <strong style="color:#00b0f0;">  分析 : </strong>
  1. 选用顺序存储的<strong style="color:#00b050;">静态链表结构</strong>存储二叉树结点 ;
  
     ```cpp
     #define Null -1
     struct TNode		//本题只要求输出指定位置节点,故没有节点关键字的存储
     {
         //elementType data;
         int left;
         int right;
     } T[10];
     ```
  
  2. 建树：
  
     1. 依次将节点信息存入静态链表数组 T[10] 中；
  
     2. <strong style="color:#00b050;">找到并返回根节点所在位置的下标。</strong>
  
        每个结点的位置信息都被存储在了各自的父结点中。由于根节点没有父节点，位置信息没有存入二叉树中的节点即为根节点。
  
        **可以定义 int root=0 ;每次读入节点位置时 root - = index ,再将 0~N-1 累加到  root 中，此时 root 即为根节点下标。**
  
        ```cpp
        int buildTree() // Build a static linked list to store the binary tree and return the subscript of the root node;
        {
            int N;
            cin >> N;
            if (!N)
            {
                return Null;
            }
            int root = 0;
            char l, r;
            for (int i = 0; i < N; ++i)
            {
        
                cin >> l >> r;
                if (l != '-')
                {
                    T[i].left = l - '0';
                    root -= T[i].left;
                }
                if (r != '-')
                {
                    T[i].right = r - '0';
                    root -= T[i].right;
                }
                root += i;
            }
            return root;
        }
        ```
        <br/>3. Level Traversal
        Level Traversal <strong style="color:#ff0000;">只能建立队列实现</strong>
        
        ```cpp
        // NOTE:Level traversal has no recursive algorithm and relies on queues to achieve;
        #define maxSize 5
            int queue[maxSize];
            int front = 0, rear = 0;
            int p;
        
            rear = (rear + 1) % maxSize;
            queue[rear] = R;
            while (front != rear)
            {
                front = (front + 1) % maxSize;
                p = queue[front];
                if (T[p].left == Null && T[p].right == Null)
                {
                    leaves[++top] = p;
                }
                if (T[p].left != Null)
                {
                    rear = (rear + 1) % maxSize;
                    queue[rear] = T[p].left;
                }
                if (T[p].right != Null)
                {
                    rear = (rear + 1) % maxSize;
                    queue[rear] = T[p].right;
                }
            }
        }
        ```
---

## <strong style="color:#00b0f0;">(3)完整代码</strong>

```cpp

// README: 09 树 List Leaves

#include <iostream>
using namespace std;
#define Null -1

struct TNode // define array;
{
    int left = Null;
    int right = Null;
} T[10];

int leaves[10];
int top = -1;

int buildTree() // Build a static linked list to store the binary tree and return the subscript of the root node;
{
    int N;
    cin >> N;
    if (!N)
    {
        return Null;
    }
    int root = 0;
    char l, r;
    for (int i = 0; i < N; ++i)
    {

        cin >> l >> r;
        if (l != '-')
        {
            T[i].left = l - '0';
            root -= T[i].left;
        }
        if (r != '-')
        {
            T[i].right = r - '0';
            root -= T[i].right;
        }
        root += i;
    }
    return root;
}

void printLeaves(int R)
{
    if (R == Null)
    {
        return;
    }

// NOTE:Level traversal has no recursive algorithm and relies on queues to achieve;
#define maxSize 5
    int queue[maxSize];
    int front = 0, rear = 0;
    int p;

    rear = (rear + 1) % maxSize;
    queue[rear] = R;
    while (front != rear)
    {
        front = (front + 1) % maxSize;
        p = queue[front];
        if (T[p].left == Null && T[p].right == Null)
        {
            leaves[++top] = p;
        }
        if (T[p].left != Null)
        {
            rear = (rear + 1) % maxSize;
            queue[rear] = T[p].left;
        }
        if (T[p].right != Null)
        {
            rear = (rear + 1) % maxSize;
            queue[rear] = T[p].right;
        }
    }
}

int main()
{
    int R;
    R = buildTree();
    printLeaves(R);

    for (int i = 0; i < top; ++i)
    {
        cout << leaves[i] << ' ';
    }
    cout << leaves[top];
    return 0;
}
```

