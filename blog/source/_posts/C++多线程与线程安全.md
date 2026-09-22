---
title: C++ 多线程与线程安全
date: 2025-02-23
categories:
  - C++
tags:
  - C++
  - 多线程
---

## 线程

线程是程序执行的基本单位，一个进程可以有至少一个线程。

## 并发与并行

### 并发

多个任务在时间片段内交替执行，表现出同时进行的效果。

### 并行

多个任务在多个处理器或处理器核上同时执行。

## 线程同步

线程同步是多个线程同时访问共享资源时，为防止数据的不一致而通过某种机制协调线程之间的执行顺序，确保每次只有一个线程可以访问共享资源，保证程序运行的正确性。

## C++11 支持多线程操作

thread 线程库，头文件 `<thread>`。

```cpp
#include <iostream>
#include <thread>

void printMessage(int count) {
    for (int i = 0; i < count; ++i) {
        std::cout << "Hello from thread (function pointer)!\n";
    }
}

int main() {
    std::thread t1(printMessage, 5); // 创建线程，传递函数指针和参数
    t1.join(); // join() 用于等待线程完成执行。如果不调用 join() 或 detach() 而直接销毁线程对象，会导致程序崩溃。
    return 0;
}
```

## 线程同步与互斥

### 互斥量（Mutex）

`std::mutex` 用于防止多个线程同时访问共享资源，一个线程访问的时候先锁定 lock，结束的时候释放 unlock。

```cpp
std::mutex mtx;
mtx.lock();   // 锁定互斥锁
// 访问共享资源
mtx.unlock(); // 释放互斥锁
```

`std::lock_guard` 和 `std::unique_lock`：自动管理锁的获取和释放。

```cpp
std::lock_guard<std::mutex> lock(mtx); // 自动锁定和解锁
// 访问共享资源
```

### 锁（Locks）

- `std::lock_guard`：作用域锁，当构造时自动锁定互斥量，当析构时自动解锁。
- `std::unique_lock`：与 `std::lock_guard` 类似，但提供了更多的灵活性，例如可以转移所有权和手动解锁。

```cpp
#include <mutex>

std::mutex mtx;

void safeFunctionWithLockGuard() {
    std::lock_guard<std::mutex> lk(mtx);
    // 访问或修改共享资源
}

void safeFunctionWithUniqueLock() {
    std::unique_lock<std::mutex> ul(mtx);
    // 访问或修改共享资源
    // ul.unlock(); // 可选：手动解锁
}
```

### 条件变量（Condition Variable）

条件变量用于线程间的协调，允许一个或多个线程等待某个条件的发生。它通常与互斥量一起使用，以实现线程间的同步。`std::condition_variable` 用于实现线程间的等待和通知机制。

```cpp
std::condition_variable cv;
std::mutex mtx;
bool ready = false;

std::unique_lock<std::mutex> lock(mtx);
cv.wait(lock, []{ return ready; }); // 等待条件满足
// 条件满足后执行
```

### 原子操作（Atomic Operations）

原子操作确保对共享数据的访问是不可分割的，即在多线程环境下，原子操作要么完全执行，要么完全不执行，不会出现中间状态。

```cpp
#include <atomic>
#include <thread>

std::atomic<int> count(0);

void increment() {
    count.fetch_add(1, std::memory_order_relaxed); // fetch_add 自增操作
}

int main() {
    std::thread t1(increment);
    std::thread t2(increment);
    t1.join();
    t2.join();
    return count; // 应返回 2
}
```

### 线程局部存储（Thread Local Storage, TLS）

线程局部存储允许每个线程拥有自己的数据副本。这可以通过 `thread_local` 关键字实现，避免了对共享资源的争用。

```cpp
#include <iostream>
#include <thread>

thread_local int threadData = 0;

void threadFunction() {
    threadData = 42; // 每个线程都有自己的 threadData 副本
    std::cout << "Thread data: " << threadData << std::endl;
}

int main() {
    std::thread t1(threadFunction);
    std::thread t2(threadFunction);
    t1.join();
    t2.join();
    return 0;
}
```

## 死锁（Deadlock）和避免策略

死锁发生在多个线程互相等待对方释放资源，但没有一个线程能够继续执行。避免死锁的策略包括：

- 总是以相同的顺序请求资源。
- 使用超时来尝试获取资源。
