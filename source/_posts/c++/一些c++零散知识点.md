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

# 计算程序的运行时间

```cpp
#include <chrono>
//...
auto start = std::chrono::steady_clock::now();
//todo
auto end = std::chrono::steady_clock::now();
std::chrono::duration<double, std::micro> elapsed = end - start; // std::micro 表示以微秒为时间单位
std::cout<< "time: "  << elapsed.count() << "us" << std::endl;
```

# 深拷贝

类class1包含成员属性class2，class2中有指针和深拷贝构造函数。创建一个vector存放class1，创建一个class1的对象a，a中的class2对象的指针用new创建。用push_back添加a，会执行class2的深拷贝。

```cpp
class class2 {
public:
	class2() {
		i = nullptr;
	}
	class2(const class2& temp) {
		i = new int(*temp.i);
	}
	int* i;
};

class class1 {
public:
	class2 m;
};

int main() {
	std::vector<class1> v;
	class1 a;
	a.m.i = new int(10);
	v.push_back(a);
	cout << "a.m.i指向的地址：" << hex << b1.a1.i << endl;			//输出：00000176C8BC6180
	cout << "v[0].a1.i指向的地址：" << hex << v[0].a1.i << endl;		//输出：00000176C8BC6C80 不同
    return 0;
}
```

# 析构函数

当从一个存储类对象的 `std::vector` 中弹出元素时，元素的析构函数会被调用。

```cpp
#include <iostream>
#include <vector>

class MyClass {
public:
    MyClass() {
        std::cout << "MyClass constructor" << std::endl;
    }

    ~MyClass() {
        std::cout << "MyClass destructor" << std::endl;
    }
};

int main() {
    std::vector<MyClass> myVector;

    myVector.push_back(MyClass()); // 添加一个元素

    myVector.pop_back(); // 移除最后一个元素，会调用其析构函数

    return 0;
}
```

# const成员函数

`const`成员函数不能返回非`const`引用，否则会导致编译错误

```cpp
class MyClass {
public:
    MyClass(int value) : data(value) {}

    // 错误：const函数不能返回非const引用
    int& GetData() const {
        return data;
    }

private:
    int data;
};
```

# 构造函数调用

用 '=' 创建类的对象，使用的是拷贝构造函数，不是重载等号的函数

```cpp
class MyClass
{
public:
    MyClass() = default;
    MyClass(const MyClass& a) {
        std::cout << "拷贝构造函数调用" << std::endl;
    }
    ~MyClass() {
        std::cout << "析构函数调用" << std::endl;
    }
    MyClass& operator=(const MyClass& a) {
        std::cout << "重载=函数调用" << std::endl;
    }
};
int main(){
    MyClass a;
    MyClass b = a;  //打印："拷贝构造函数调用"
}
```

拷贝构造前不要加`explicit`，会导致以下错误

```cpp
//......
explicit MyClass::MyClass(const MyClass& a);
//......
int main(){
    MyClass a;
    MyClass b = a;  //报错：没有适当的复制构造函数
}
```



# 迭代器运算

所有迭代器支持的操作

- *iter
- iter->mem
- iter++
- iter--（forward_list迭代器不支持）
- iter1 == iter2
- iter1 != iter2

只有`string`、`vector`、`deque`和`array`的迭代器支持的操作

- iter + n
- iter - n
- iter += n
- iter -=n
- iter1 - iter2
- \>, <, >=, <=
