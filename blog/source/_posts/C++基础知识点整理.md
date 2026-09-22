---
title: C++ 基础知识点整理
date: 2025-02-17
categories:
  - C++
tags:
  - C++
  - 基础
---

## new 和 malloc 的区别

- new 是操作符，而 malloc 是函数。
- new 在调用的时候先分配内存，再调用构造函数，释放的时候调用析构函数；而 malloc 没有构造函数和析构函数。
- malloc 需要给定申请内存的大小，返回的指针需要强转；new 会调用构造函数，不用指定内存的大小，返回的指针不用强转。
- new 可以被重载，malloc 不能。
- new 分配内存更直接和安全。
- new 发生错误抛出异常，malloc 返回 null。

![new/malloc 申请失败对比](/img/cpp-basics-new-malloc.png)

> 当申请失败的时候，它们有什么不同的表现？new 抛异常，malloc 返回空指针。

## 断言的使用

ASSERT 是一个宏，用于在运行时检查一个条件是否为真，如果不满足，运行时会将程序终止，并输出一条错误信息。

### 静态断言 static_assert（C++11 新标准）

静态断言（`static_assert`）是 C++11 中引入的编译时检查工具，用于检查编译时条件是否满足。与 assert 不同，静态断言不会导致程序终止，而只是生成一个编译时错误。当条件不满足时，静态断言将输出一个错误消息。

> static_assert 的断言表达式结果必须是在编译期可以计算的表达式，即必须是常量表达式。如果使用变量，则会导致错误。它与 assert 的区别就在于在编译期给出结果，且内部必须是常量，不能是变量。

## 内存对齐

内存对齐应用于三种数据类型：class、struct、union。

在 C 语言中，结构体是一种复合数据类型，其构成元素既可以是基本数据类型的变量，也可以是一些复合数据类型的数据单元。在结构体中，编译器为结构体的每个成员按其自然边界分配空间。各个成员按照它们被声明的顺序在内存中顺序存储，第一个成员的地址和整个结构体的地址相同。

> 如果说内部有一个 long long 类型大小的数据，内存应该怎么分配？
> 正常的时候会使用 4 字节对齐的方式，但如果想要修改，可以使用 `#pragma pack` 修改对齐字节的大小。

```cpp
#pragma pack(1) // 设置对齐字节大小为 1
#pragma pack()  // 恢复默认对齐
```

## C++ 类型转换

C++ 中四种类型转换分别为 const_cast、static_cast、dynamic_cast、reinterpret_cast。

### const_cast

将 const 变量转变为非 const。

### static_cast

最常用，用于各种隐式转换，比如将非 const 变量转变为 const。static_cast 可以进行上行转换，但是下行转换是不安全的。

### dynamic_cast

只能用于含有虚函数的类转换，用于类向上和向下转换。

- **向上转换**：指子类向基类转换，把派生类的指针或者引用转换成基类表示（安全）。
- **向下转换**：指基类向子类转换，基类指针或者引用转换成派生类表示（不安全）。

### reinterpret_cast

reinterpret_cast 可以做任何类型的转换，不过不对转换结果保证，容易出问题。

> 类型转换的时候会进行类型检查吗？会，但是根据不同的类型转换有不同的标准。

![类型转换](/img/cpp-type-cast.png)

## 使用递归方法遍历文件有什么隐患

- 死循环：阻塞，内存溢出
- 无限递归：爆栈

### 手动实现遍历文件夹下的所有子文件（递归）

```cpp
#include <iostream>
#include <filesystem>
#include <string>

namespace fs = std::filesystem;

void TraverseDirectory(const fs::path& dir_path) {
    // 检查路径是否存在
    if (!fs::exists(dir_path)) {
        std::cerr << "Directory does not exist: " << dir_path << std::endl;
        return;
    }

    // 遍历目录
    for (const auto& entry : fs::directory_iterator(dir_path)) {
        if (fs::is_directory(entry)) {
            TraverseDirectory(entry.path());
        }
        else if (fs::is_regular_file(entry)) {
            std::cout << "File: " << entry.path() << std::endl;
        }
    }
}

int main() {
    fs::path start_dir = "E:\\开发学习保留的文件";
    TraverseDirectory(start_dir);
    return 0;
}
```

### 深度优先搜索 DFS

基本是从一个节点一直深入到最底层，然后重新回到开始节点遍历下一个深度。

### 广度优先搜索

大概就是层层遍历然后一直到遍历结束。

## 智能指针

### auto_ptr（已弃用）

采用所有权模式，当一个指针赋值给另一个指针的时候不会报错，但是重新访问第一个指针的时候会报错，所以会有潜在的内存崩溃问题。

### unique_ptr

采用严格拥有的模式，保证同一时间内只能有一个智能指针可以指向该对象，避免资源泄漏。

### shared_ptr

shared_ptr 实现共享拥有概念，多个智能指针可以指向相同的对象，该对象和其相关资源会在"最后一个指针被销毁"的时候释放。

### weak_ptr

weak_ptr 是一种不控制对象生命周期的智能指针，它指向一个 shared_ptr 管理的对象，为了防止强引用的 shared_ptr 在相互引用的时候出现死锁问题。

## 二叉树求高度

求高度就是需要遍历节点，最后返回一个高度值（广度优先）。

```cpp
struct node
{
    int data;
    struct node* left;
    struct node* right;
};

/* 计算二叉树的高度 */
int height(struct node* node)
{
    if (node == NULL)
        return 0;

    // 计算左子树的高度和右子树的高度
    int lHeight = height(node->left);
    int rHeight = height(node->right);

    return 1 + (lHeight > rHeight ? lHeight : rHeight);
}
```

## 多线程问题

### 多线程用什么实现

C++11 实现了线程库，可以使用 thread 创建线程，join 函数等待线程结束。

```cpp
#include <iostream>
#include <thread>

void func()
{
    std::cout << "Hello, C++11 thread!\n";
}

int main()
{
    std::thread t(func);
    t.join();
    return 0;
}
```

### C++ 怎么保证线程安全（锁）

#### 互斥量 mutex

```cpp
#include <iostream>
#include <thread>
#include <mutex>

std::mutex g_mutex;
int g_counter = 0;

void incrementCounter()
{
    std::lock_guard<std::mutex> lock(g_mutex);
    ++g_counter;
}

int main()
{
    std::thread t1(incrementCounter);
    std::thread t2(incrementCounter);
    t1.join();
    t2.join();
    std::cout << "g_counter = " << g_counter << std::endl;
    return 0;
}
```

## 说说内联函数和宏函数的区别

1. 宏定义不是函数，但是使用起来像函数。预处理器用复制宏代码的方式代替函数的调用，省去了函数压栈退栈过程，提高了效率；而内联函数本质上是一个函数，内联函数一般用于函数体代码比较简单的函数，不能包含复杂的控制语句，如 while、switch，并且内联函数本身不能直接调用自身。
2. 宏函数是在预编译的时候把所有的宏名用宏体来替换，简单的说就是字符串替换；而内联函数则是在编译的时候进行代码插入，编译器会在每处调用内联函数的地方直接把内联函数的内容展开，这样可以省去函数调用的开销，提高效率。
3. 宏定义是没有类型检查的，无论对还是错都是直接替换；而内联函数在编译的时候会进行类型检查，内联函数满足函数的性质，比如有返回值、参数列表等。

## 说说 const 和 define 的区别

const 用于定义常量；define 用于定义宏，而宏也可以用于定义常量。都用于常量定义时，它们的区别有：

1. const 生效于编译阶段；define 生效于预处理阶段。
2. const 定义的常量存储在内存中、需要额外的内存空间；define 定义的常量运行时是直接的操作数，并不会存放在内存中。
3. const 定义的常量是带类型的；define 定义的常量不带类型，因此不利于类型检查。

## 说说 C++ 中函数指针和指针函数的区别

1. 定义不同：指针函数本质是一个函数，其返回值为指针；函数指针本质是一个指针，其指向一个函数。
2. 写法不同：

```cpp
// 指针函数：返回值为指针
int *fun(int x, int y);

// 函数指针：指向函数
int (*pfun)(int, int);
```
