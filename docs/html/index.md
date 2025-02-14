# Original



## 简介

Original是一个C++基础工具库,也是本人的第一个正式项目，用于学习C++相关基础以及STL、Boost等库。项目的目标是实现STL的主要内容以及Boost的某些相关功能，具体已经实现和未来计划实现的模块内容在下文列出，计划实现的部分会根据情况进行调整，不一定都实现，以最终项目为准。如有问题可以在[Issues](https://github.com/FrozenLemonTee/original/issues)中提出，也欢迎一起参与到本项目的实现中来，如Fork等。

## 文档
[文档-Original](https://documents-original.vercel.app/)

## 安装

这里以项目`hello_original`为例：
```text
├─CMakeLists.txt
└─main.cpp
```

方法一 使用Cmake远程拉取（推荐）：

配置`CMakeLists.txt`：
```cmake
cmake_minimum_required(VERSION 3.30)
project(hello_original)

set(CMAKE_CXX_STANDARD 20)

set(BUILD_TESTING OFF CACHE BOOL "Disable tests in the fetched project")

include(FetchContent)

FetchContent_Declare(
        original
        GIT_REPOSITORY git@github.com:FrozenLemonTee/original.git
        GIT_TAG master
)

FetchContent_MakeAvailable(original)

add_executable(hello_original main.cpp)


target_link_libraries(hello_original PRIVATE original)
```
方法二 使用Cmake本地构建、安装：

在该项目文件夹下新建文件夹`build`并进入：
```shell
mkdir build
cd build
```
利用cmake构建库：
```shell
cmake .. -DCMAKE_BUILD_TYPE=Debug -DBUILD_TESTING=OFF
cmake --build . --config Debug
cmake --install . --config Debug
```
将生成的`build`和`install`文件夹复制到项目`hello_original`中。

复制后项目的结构如下：
```text
├─build
├─install
├─CMakeLists.txt
└─main.cpp
```

配置`CMakeLists.txt`：
```cmake
cmake_minimum_required(VERSION 3.30)
project(hello_original)

set(CMAKE_CXX_STANDARD 20)

set(CMAKE_PREFIX_PATH "${CMAKE_SOURCE_DIR}/install/cmake")
list(APPEND CMAKE_PREFIX_PATH "${CMAKE_SOURCE_DIR}/install/cmake/original")

find_package(original REQUIRED)

add_executable(hello_original main.cpp)

target_link_libraries(hello_original PRIVATE "${ORIGINAL_LIBRARIES}")
```

接下来展示测试Demo：

`main.cpp`：
```c++
#include <iostream>
#include "original.h"


int main() {
    std::cout << "Hello, Original!" << std::endl;
    auto a1 = original::array({"Hello, Original!"});
    std::cout << a1 << std::endl;
    printf("%s\n", static_cast<const char*>(a1));
    return 0;
}
```
输出：
```text
Hello, original!
array("Hello, original!")
array("Hello, original!")
```

## 模块进度

### 已实现&正在实现：

#### Core

正在实现中。包含了常用容器与结构、算法、内存管理等部分，是项目的核心功能模块。

常用容器与结构：已经实现array（定长数组）、chain（双向链表）、forwardChain（单向链表）、vector（变长数组）、bitSet（位集合）、blocksList（双端队列的底层容器）、stack&queue&deque&prique（栈、队列、双端队列、优先队列四种容器适配器），尚未实现部分有哈希表和树表（红黑树实现）等。

算法：已经实现iterator（迭代器）、filter&filterStream（谓词工具类）、transform&transformStream（单一操作类）、comparator（比较器）、部分算法（非修改类、修改类算法），排序算法（堆算法）等。

内存管理：待实现内存池、分配器、智能指针等。



### 计划实现：

#### 多线程&并发模块

#### 网络模块

#### 文件读取和结构化数据解析模块

##### ...


