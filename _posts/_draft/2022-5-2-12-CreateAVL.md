---
title: "Root Of AVL"
subtitle: "PTA 陈越数据结构第 11 题"
layout: post
author: "youngflysky"
date: 2022-05-02 17:15:46
header-style: text
catalog: true
tags:
- C++
- binary tree
- AVL
- 陈越数据结构 
---

>- **[YFS Blog 原创](https://youngflysky.fun/)**

---

<br/>

# Root Of AVL

>1. 给定一串数据建立 AVL；
>2. AVL 相比于 BST，其节点中多出一个<strong style="color:#ff0000;"> int height</strong>，记录子树高度信息以维护平衡因子；
>3. AVL 在节点插入过程中要 <strong style="color:#ff0000;">实时更新</strong> 每个受影响节点的 height 值
>4. AVL 在节点插入过程中要 <strong style="color:#ff0000;">实时监测</strong> 平衡因子 ，并依据四种不同的 【平衡被破坏状态”】 作出相应调整。



## <strong style="color:#0070c0;"> (1)	[题目:](https://github.com/youngflysky/Typora/blob/main/img/2022-5-2-12-CreateAVL.png?raw=true)</strong>

























