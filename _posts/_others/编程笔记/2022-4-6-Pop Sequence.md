---
title: "7.Pop Sequence"
subtitle: "PTA 陈越数据结构第 7 题"
layout: post
author: "youngflysky"
date: 2022-04-06 11:32:10
header-style: text
catalog: true
tags:
- C++
- 算法
- OJ笔记
---

><strong style="color:#c00000;">通过模拟法对问题求解</strong><br/>
---
<br/>

# **Pop Sequence** 

## <strong style="color:#0070c0;"> (1)	题目:</strong>

- Given a stack which can keep M numbers at most. Push N numbers in the order of 1, 2, 3, ..., N and pop randomly. You are supposed to tell if a given sequence of numbers is a possible pop sequence of the stack. For example, if M is 5 and N is 7, we can obtain 1, 2, 3, 4, 5, 6, 7 from the stack, but not 3, 2, 1, 7, 5, 6, 4.

- **Input Specification:**<br/>Each input file contains one test case. For each case, the first line contains 3 numbers (all no more than 1000): M (the maximum capacity of the stack), N (the length of push sequence), and K (the number of pop sequences to be checked). Then K lines follow, each contains a pop sequence of N numbers. All the numbers in a line are separated by a space.
- **Output Specification:**<br/>
  For each pop sequence, print in one line "YES" if it is indeed a possible pop sequence of the stack, or "NO" if not.
- **Sample Input:**

```cpp
5 7 5
1 2 3 4 5 6 7
3 2 1 7 5 6 4
7 6 5 4 3 2 1
5 6 4 3 7 2 1
1 7 6 5 4 3 2
```
- **Sample Output:**
```cpp
YES
NO
NO
YES
NO
```
## <strong style="color:#0070c0;">(2)	解:</strong>
- <strong style="color:#00b0f0;">  分析 : </strong>
1. 题干要点 : <br/>输入数据是给定的 Pop Sequence , 输出结果是 判断所给 Pop Sequence 能否 由指定顺序 Push 的序列和 指定最大容量的 栈 Pop 得到.
2. 题目分析:<br/>给定的输入输出数据是对 原本 <strong style="color:#7030a0;">入栈出栈</strong> 过程的逆推, 可以通过 **模拟入栈出栈** 来判断结果
- <strong style="color:#0070c0;">解析 :</strong><br/>

- 列表分析 :  

- <strong style="color:#c00000;">P : P 用来标识当前已扫描到的数字中最大的数字</strong><br/> **通过对 P 状态的更新从而更新栈的状态,达到模拟出栈的效果**

- top :  <strong style="color:#00b0f0;">top >= Capacity</strong>  ,则 return　false

- 出栈　stack[top--]：<strong style="color:#00b0f0;">stack[top--] != *当前数字*  || top = -1 </strong> , 则 return false

- **[例一]** 5 6 4 3 7 2 1 [由左向右逐个扫描每个数字]

  | <span style="display:inline-block;width: 70px"><strong style="color:#00b050;">当前数字<br/><strong style="color:#c00000;">S</strong></strong></span> | <span style="display:inline-block;width: 30px"><strong style="color:#c00000;">p</strong></span> | <span style="display:inline-block;width: 30px"><strong style="color:#00b050;">top</strong></span> | <span style="display:inline-block;width: 60px"><strong style="color:#00b050;">栈状态</strong></span> | <span style="display:inline-block;width: 70px"><strong style="color:#00b050;">出栈数字<br/><strong style="color:#c00000;">T</strong></strong></span> | <span style="display:inline-block;width: 60px"><strong style="color:#00b050;">判断</strong></span> |
  | :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------- | :----------------------------------------------------------: | :----------------------------------------------------------- |
  |                              5                               |           <strong style="color:purple;">5</strong>           |                              4                               | 1,2,3,4,5                                                    |                              5                               | S == T ; top < capacity ; true                               |
  |                              6                               |           <strong style="color:purple;">6</strong>           |                              4                               | 1,2,3,4,6                                                    |                              6                               | S == T ; top < capacity ; true                               |
  |                              4                               |          <strong style="color:#c00000;">6</strong>           |                              3                               | 1,2,3,4                                                      |                              4                               | S == T ; top < capacity ; true                               |
  |                              3                               |          <strong style="color:#c00000;">6</strong>           |                              2                               | 1,2,3                                                        |                              3                               | S == T ; top < capacity ; true                               |
  |                              7                               |           <strong style="color:purple;">7</strong>           |                              3                               | 1,2,3,7                                                      |                              7                               | S == T ; top < capacity ; true                               |
  |                              2                               |          <strong style="color:#c00000;">7</strong>           |                              1                               | 1,2                                                          |                              2                               | S == T ; top < capacity ; true                               |
  |                              1                               |          <strong style="color:#c00000;">7</strong>           |                              0                               | 1                                                            |                              1                               | S == T ; top < capacity ; true                               |

- **[例二]** 3 2 1 7 5 6 4

	| <span style="display:inline-block;width: 70px"><strong style="color:#00b050;">当前数字<br/><strong style="color:#c00000;">S</strong></strong></span> | <span style="display:inline-block;width: 30px"><strong style="color:#c00000;">p</strong></span> | <span style="display:inline-block;width: 30px"><strong style="color:#00b050;">top</strong></span> | <span style="display:inline-block;width: 60px"><strong style="color:#00b050;">栈状态</strong></span> | <span style="display:inline-block;width: 70px"><strong style="color:#00b050;">出栈数字<br/><strong style="color:#c00000;">T</strong></strong></span> | <span style="display:inline-block;width: 60px"><strong style="color:#00b050;">判断</strong></span> |
  | :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------- | :----------------------------------------------------------: | :----------------------------------------------------------- |
  |                              3                               |           <strong style="color:purple;">3</strong>           |                              2                               | 1,2,3                                                        |                              3                               | S == T ; top < capacity ; true                               |
  |                              2                               |                              3                               |                              1                               | 1,2                                                          |                              2                               | S == T ; top < capacity ; true                               |
  |                              1                               |                              3                               |                              0                               | 1                                                            |                              1                               | S == T ; top < capacity ; true                               |
  |                              7                               |          <strong style="color:#c00000;">7</strong>           |                              3                               | 4,5,6,7                                                      |                              7                               | S == T ; top < capacity ; true                               |
  |                              5                               |                              7                               |                              2                               | 4,5,6                                                        |          <strong style="color:#c00000;">6</strong>           | <strong style="color:#c00000;">S != T</strong> ; top < capacity ; <strong style="color:#c00000;">false</strong> |
  |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |
  |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |

## <strong style="color:#0070c0;">(3) 代码注释</strong>

1. 初始化
```cpp
int stack[maxSize];	
int top =-1;
int p=0;	// p 是更新当前栈状态的依据
```
2. <strong style="color:#00b0f0;">p 更新</strong>，执行　<strong style="color:#00b0f0;">入栈　出栈</strong>　操作：
```cpp
for (int j = p + 1; j <= GivenARR[i]; ++j)
//若当前数字大于 P, 将 P 和 当前数字间的所有数入栈
{
	stack[++top] = j;
}
if (top >= capacity)//若 栈溢出, return false
{
	return false;
}
else
{
	top--;					//否则执行出栈操作
	p = GivenARR[i]; //并更新 P 为当前数字
}
```
3. <strong style="color:#00b0f0;">P 不更新</strong>时　出栈　操作
```cpp
if (GivenARR[i] <= p) //若当前数字小于P,执行出栈操作
{
	if (top == -1 || stack[top--] != GivenARR[i]) 
	//若栈空无法出栈,或出栈数字与当前数字不等, return false
	{
		return false;
	}
}
```











<br/><br/><br/>

# <strong style="color:#7030a0;">完整代码:</strong>

```cpp
#include <iostream>
using namespace std;
#define maxSize 1005
bool isPopSequence(int length, int capacity)	//模拟数组法
{
	int GivenARR[maxSize] = { 0 };
	for (int i = 0; i < length; ++i)
	{
		cin >> GivenARR[i];
	}
	int stack[maxSize] = { 0 }; int top = -1;
	int p = 0;		//P 用来标记已经入栈的数字以及是否进行入栈操作,初始化为 0
	for (int i = 0; i < length; ++i)//从第1个数字依次开始进行处理
	{
		if (GivenARR[i] <= p) //若当前数字小于P,执行出栈操作
		{
			if (top == -1 || stack[top--] != GivenARR[i]) //若栈空无法出栈,或出栈数字与当前数字不等, return false
			{
				return false;
			}
		}
		else
		{
			for (int j = p + 1; j <= GivenARR[i]; ++j)//若当前数字大于 P, 将 P 和 当前数字间的所有数入栈
			{
				stack[++top] = j;
			}
			if (top >= capacity)//若 栈溢出, return false
			{
				return false;
			}
			else
			{
				top--;					//否则执行出栈操作
				p = GivenARR[i]; //并更新 P 为当前数字
			}
		}
	}
	return true;
}
int main()
{
	int capacity, length, number;
	cin >> capacity >> length >> number;

	int result[maxSize] = { 0 };	//通过结果数组暂存判断结果,方便连续输出

	for (int i = 0; i < number; ++i)
	{
		if (isPopSequence(length, capacity))
		{
			result[i] = 1;
		}
	}
	for (int i = 0; i < number; ++i)
	{
		if (result[i])
		{
			cout << "YES\n";
		}
		else
		{
			cout << "NO\n";
		}
	}

	return 0;
}
```

