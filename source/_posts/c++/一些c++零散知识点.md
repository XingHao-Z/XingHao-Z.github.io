---
title: 一些c++零散知识点
date: 2023-07-30 22:02:23
tags:
 - c++
categories:
 - c++
---

一些c++零散的，常忘的语法知识。后续可能会被整理到其他文章。

<!--more-->

# 优先级队列

priority_queue

第三个谓词设置排序规则，默认是std::less，实际是从大到小，和map和set是相反的，这是因为使用的不同底层数据结构。

```cpp
std::priority_queue <int, vector<int>, std::greater<int>> q;
q.push(1);
q.push(3);
q.push(2);
//q此时：队头1,2,3队尾
```



# 函数对象

在标准算法中使用时，必须带括号

在创建容器时使用，不能带括号

```cpp
class bigger {
public:
    bool operator() (const int a, const int b) {
        return a > b;
    }
};
void f() {
    std::vector<int> v{ 5,3,8,6,1,3,2 };
    sort(v.begin(), v.end(), bigger());
    sort(v.begin(), v.end(), std::less<int>());
    //sort(v.begin(), v.end(), std::less<int>);   //报错，必须带括号
    //std::map<int, int, bigger()> m1;  //报错，不能带括号
    std::map<int, int, bigger> m2;
    std::priority_queue<int, std::vector<int>, bigger> q1;
    //std::priority_queue<int, std::vector<int>, bigger()> q2;  //报错，不能带括号
    //std::priority_queue<int, std::vector<int>, std::less<int>()> q3;  //报错，不能带括号
}
```

在标准算法（如 `std::sort`）中将 `bigger` 作为函数对象（比较函数）使用时，需要使用 `bigger()` 创建 `bigger` 的临时实例。`bigger` 后面的 `()` 表示我们正在使用 `bigger` 的默认构造函数创建一个临时对象。

将 `bigger` 作为容器（如 `std::map` 或 `std::priority_queue`）的自定义比较类型时，不需要括号，直接使用 `bigger` 即可。因为容器需要一个比较函数的类型，而不是一个对象。
