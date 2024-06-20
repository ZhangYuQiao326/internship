该文件未修改

# 一 环境配置

## 1 Visual Studio Code相关信息

- Visual Studio Code 下载地址：https://code.visualstudio.com/download
- VS Code建议安装插件列表：
  - 中文菜单：
    - MS-CEINTL.vscode-language-pack-zh-hans
  - SSH远程开发：
    - ms-vscode-remote.remote-ssh
    - ms-vscode-remote.remote-ssh-edit
    - ms-vscode.remote-explorer
  - C++开发
    - ms-vscode.cpptools
  - python开发
    - ms-python.python
  - 代码补全
    - TabNine.tabnine-vscode
    - GitHub.copilot
- VS Code SSH远程连接Ubuntu主机
  - 本地Ubuntu示例
  - autoDL示例：
    - autoDL地址：https://www.autodl.com/home
    - 省钱妙招：无卡启动（不挂载GPU，￥0.1/h左右）

### 远程免密登录

1. 打开本机cmd终端，输入[ssh](https://so.csdn.net/so/search?q=ssh&spm=1001.2101.3001.7020)可以看到我们的计算机已经存在ssh了，然后输入“**ssh-keygen**”命令，一直按回车跳过三个“Enter”，产生公私[密钥](https://so.csdn.net/so/search?q=密钥&spm=1001.2101.3001.7020)

![image-20240617155055659](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202406171550806.png)

2. 此时进入此电脑，在文件搜索框中输入“**C:\Users\【用户名】\.ssh**”，访问“**id_rsa.pub**”文件用记事本打开并复制其中的内容

![image-20240617155156461](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202406171551626.png)	

3. 打开vscode，首先登录远程服务器，并进入服务器文件夹，

   找到远程服务器的 ~/.ssh/authorized_keys 文件中，找到“.ssh”文件下的“authorized_keys”并打开，将刚才生成的公钥pub文件复制的口令粘贴过来保存到这个文件里即可

   ![image-20240617155531336](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202406171555493.png)

## 2 Python 开发环境配置

- 建议`conda`虚拟环境
- 测试代码`demo.py`：

```py
# python 代码测试

# 计算 1+2+3+4+5 的和
sum = 0;
for i in range(5):
    sum += i

# 打印结果
print(sum);

```

- debuger配置`.vscode`下`launch.json`添加

```py
{
    // 使用 IntelliSense 了解相关属性。 
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Python: Current File",
            "type": "python",
            "request": "launch",
            // "program": "${file}", // 当前文件
            "program": "demo.py", // 指定文件
            "console": "integratedTerminal",
            "justMyCode": true // false表示可以进入第三方库（如Pytorch）里进行调试
        }
    ]
}

```

## 3 c++开发环境配置

- 测试代码`main.cpp`：

```cpp
#include <iostream>
using namespace std;

int main(){
  
    // 计算 1+2+3+4+5
    int sum {0};
    for (int i {0}; i < 5; i++){
        sum += i;
    }
    // 输出结果
    cout << sum << endl;
    return 0;
  
}

```

- 先用`g++  main.cpp -o main`生成可执行文件
- Linux中可以使用`which g++`确定`g++`的路径
- 再用VS Code 菜单：`终端-运行生成任务`生成可执行文件，需要在`.vscode`先添加`tasks.json`

```cpp
{
	"version": "2.0.0",
	"tasks": [
		{
			"type": "cppbuild",
			"label": "C/C++: g++ 生成活动文件",
			"command": "/usr/bin/g++", // g++的路径
			"args": [
				"-fdiagnostics-color=always", // 颜色
				"-g",  // 调试信息
				"-Wall", // 开启所有警告
				"-std=c++14", // c++14标准
				"${file}", // 文件本身，仅适用于C++基础知识教学，无法同时编译所有文件
				// "${fileDirname}/*.cpp", // 文件所在的文件夹路径下所有cpp文件
				"-o", // 输出
				"${workspaceFolder}/release/${fileBasenameNoExtension}" // 文件所在的文件夹路径/release/当前文件的文件名，不带后缀
			],
			"options": {
				"cwd": "${fileDirname}" // 文件所在的文件夹路径
			},
			"problemMatcher": [
				"$gcc"
			],
			"group": {
				"kind": "build",
				"isDefault": true
			},
			"detail": "编译器: /usr/bin/g++"
		}
	]
}

```

- 需要debuger，`launch.json`修改为：

```cpp
{
    // 使用 IntelliSense 了解相关属性。 
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(gdb) 启动",
            "type": "cppdbg", // C++调试
            "request": "launch",
            "program": "${workspaceFolder}/release/${fileBasenameNoExtension}",  // 文件所在的文件夹路径/release/当前文件的文件名，不带后缀
            "args": [],
            "stopAtEntry": false,
            "cwd": "${fileDirname}", // 文件所在的文件夹路径
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "setupCommands": [
                {
                    "description": "为 gdb 启用整齐打印",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                },
                {
                    "description":  "将反汇编风格设置为 Intel",
                    "text": "-gdb-set disassembly-flavor intel",
                    "ignoreFailures": true
                }
            ],
            "preLaunchTask": "C/C++: g++ 生成活动文件" // tasks.json的label
        },
        {
            "name": "Python: Current File",
            "type": "python",
            "request": "launch",
            "program": "${file}", // 当前文件
            // "program": "demo.py", // 指定文件
            "console": "integratedTerminal",
            "justMyCode": true // false表示可以进入第三方库（如Pytorch）里进行调试
        }
    ]
}

```

## 4 变量解释

```cpp
以：/home/Coding/Test/.vscode/tasks.json 为例

${workspaceFolder} :表示当前workspace文件夹路径，也即/home/Coding/Test

${workspaceRootFolderName}:表示workspace的文件夹名，也即Test

${file}:文件自身的绝对路径，也即/home/Coding/Test/.vscode/tasks.json

${relativeFile}:文件在workspace中的路径，也即.vscode/tasks.json

${fileBasenameNoExtension}:当前文件的文件名，不带后缀，也即tasks

${fileBasename}:当前文件的文件名，tasks.json

${fileDirname}:文件所在的文件夹路径，也即/home/Coding/Test/.vscode

${fileExtname}:当前文件的后缀，也即.json

${lineNumber}:当前文件光标所在的行号

${env:PATH}:系统中的环境变量

```

# 二 Cmake基础课

## 1.1 c++编译过程

使用`g++`等编译工具，从源码生成最终的可执行文件一般有这几步：预处理（Preprocess）、编译（Compile）、汇编（assemble）、链接（link）。

![image-20231015175134481](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015175134481.png)

> 输入`g++ --help`可以看到对应命令：

```
-E                       Preprocess only; do not compile, assemble or link.
-S                       Compile only; do not assemble or link.
-c                       Compile and assemble, but do not link.
-o <file>                Place the output into <file>.

```

以下面程序为例：

```cpp
#include <iostream>

int main() {
    std::cout << "Hello World!" << std::endl;
    return 0;
}
```

第一步：预处理
C++中预处理指令以 `#` 开头。在预处理阶段，会对`#define`进行宏展开，处理`#if，#else`等条件编译指令，递归处理`#include`。这一步需要我们添加所有头文件的引用路径。

```cpp
# 将xx.cpp源文件预处理成xx.i文件（文本文件）
g++ -E main.cpp -o main.i

```



第二步：编译

检查代码的规范性和语法错误等，检查完毕后把代码翻译成汇编语言文件

```cpp
# 将xx.i文件编译为xx.s的汇编文件（文本文件）
g++ -S main.i -o main.s

```



第三步：汇编
基于汇编语言文件生成二进制格式的目标文件。

```cpp
# 将xx.s文件汇编成xx.o的二进制目标文件
g++ -c main.s -o main.o

```



第四步：链接

将目标代码与所依赖的库文件进行关联或者组装，合成一个可执行文件

```cpp
# 将xx.o二进制文件进行链接，最终生成可执行程序
g++ main.o -o main

```

## 1.2 静态链接库和动态链接库

所谓静态和动态，其区别是链接的阶段不一样。

- 静态链接库名称一般是`lib库名称.a`（`.a`代表`archive library`），其链接发生在编译环节。一个工程如果依赖一个静态链接库，其输出的库或可执行文件会将静态链接库`*.a`打包到该工程的输出文件中（可执行文件或库），因此生成的文件比较大，但在运行时也就不再需要库文件了。
- 而动态链接库的链接发生在程序的执行过程中，其在编译环节仅执行链接检查，而不进行真正的链接，这样可以节省系统的开销。动态库一般后缀名为`*.so`（`.so`代表`shared object`，Linux：`lib库名称.so` ，macOS：`lib库名称.dylib`）。动态链接库加载后，在内存中仅保存一份拷贝，多个程序依赖它时，不会重复加载和拷贝，这样也节省了内存的空间。
- 以下图为例
  - 工程`A`和`B`依赖静态链接库 `static library`，`A`和`B`在运行时，内存中会有多份`static library`；
  - 工程`A`和`B`依赖动态链接库 `shared library`，`A`和`B`在运行时，内存中只有一份 `shared library`（shared：共享）。

![image-20231015175406217](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015175406217.png)

以上只是非常简单的一个解释以区分动态链接库和静态链接库。更多底层的知识需要单独进行深入讲解

### 1.3 为什么需要CMake

#### 1.3.1 g++ 命令行编译

当我们编译附件中`1.hello_world`时，我们可以运行

```cpp
g++ main.cpp -o main
```



当我们需要引入外部库时，如附件中的`2.external_libs`，需要引入`gflags`（Google开源的命令行参数处理库），我们则需要运行：

```cpp
# 安装gflags
sudo apt-get install libgflags-dev libgflags2.2 

// -lgflags表示链接gflags库，-o main表示输出文件名为main
g++ main.cpp -lgflags -o main 

# 或者：

# 安装pkg-config
sudo apt-get install pkg-config

// pkg-config是一个工具，用于查找和管理安装在系统上的库文件，--cflags --libs gflags表示查找gflags库的头文件和库文件的路径，-o main表示输出文件名为main

g++ main.cpp `pkg-config --cflags --libs gflags`  -o main 


# 测试输出
./main --age 31 --name alice

```

有些时候有一些常用库我们也不用手动添加头文件或链接库路径，通常g++能在默认查询路径中找到他们。当我们的项目文件变得多起来，引入的外部库也多起来时，命令行编译这种方式就会变得十分臃肿，也不方便调试和编辑。通常在测试单个文件时会使用命令行进行编译，但不推荐在一个实际项目中使用命令行编译。

#### 1.3.2 CMake简介

在实际工作中推荐使用CMake构建C++项目，CMake是用于**构建、测试**和软件**打包**的开源**跨平台**工具；

特性：

- 自动搜索可能需要的程序、库和头文件的能力；
- 独立的构建目录（如`build`），可以安全清理
- 支持复杂的自定义命令（下载、生成各种文件）
- 自定义配置可选组件
- 从简单的文本文件（`CMakeLists.txt`）自动生成工作区和项目的能力
- 在主流平台上自动生成文件依赖项并支持并行构建
- 几乎支持所有的IDE

## 二、CMake基础知识

### 2.1 安装

ubuntu上请执行

```cpp
sudo apt install cmake -y

```

或者编译安装

```
# 以v3.25.1版本为例
git clone -b v3.25.1 https://github.com/Kitware/CMake.git 
cd CMake
# 你使用`--prefix`来指定安装路径，或者去掉`--prefix`,安装在默认路径。
./bootstrap --prefix=<安装路径> && make && sudo make install

# 验证
cmake --version

```

### 2.2 第一个CMake例子

附件位置：`3.first_cmake`

```cpp
# 第一步：配置，-S 指定源码目录，-B 指定构建目录，在build目录下生成makefile文件及其配置文件
cmake -S . -B build 
```

![image-20231115113628228](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231115113628228.png)

```
# 第二步：生成，--build 指定Makefile文件的位置，也可以直接使用make命令
cmake --build build
```



![image-20231115113736698](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231115113736698.png)

```
# 运行
./build/first_cmake
```



vs code插件：

- 安装`twxs.cmake`做代码提示；
- 安装`ms-vscode.cmake-tools`界面操作。

### 2.3 语法基础

#### 2.3.1 指定版本

以附件：`3.first_cmake/CMakeLists.txt`为例：

```cpp
# CMake 最低版本号要求
cmake_minimum_required(VERSION 3.10)

# first_cmake是项目名称，VERSION是版本号，DESCRIPTION是项目描述，LANGUAGES是项目语言
project(first_cmake 
        VERSION 1.0.0 
        DESCRIPTION "项目描述"
        LANGUAGES CXX) 

# 添加一个可执行程序，first_cmake是可执行程序名称，main.cpp是源文件
add_executable(first_cmake main.cpp)

```

命令[`cmake_minimum_required`](https://cmake.org/cmake/help/latest/command/cmake_minimum_required.html?highlight=cmake_minimum_required)来指定当前工程所使用的CMake版本，不区分大小写的，通常用小写。`VERSION`是这个函数的一个特殊关键字，版本的值在关键字之后。CMake中的命令大多和`cmake_minimum_required`相似，不区分大小写，并有很多关键字来引导命令的参数输入（类似函数传参）。

#### 2.3.2 设置项目

以附件：`3.first_cmake/CMakeLists.txt`为例：

```cpp
project(ProjectName 
        VERSION 1.0.0 
        DESCRIPTION "项目描述"
        LANGUAGES CXX) 

```

在`CMakeLists.txt`的开头，都会使用[`project`](https://cmake.org/cmake/help/latest/command/project.html)来指定本项目的名称、版本、介绍、与使用的语言。在`project`中，第一个`ProjectName`（例子中用的是`first_cmake`）不需要参数，其他关键字都有参数。

#### 2.3.3 添加可执行文件目标

以附件：`3.first_cmake/CMakeLists.txt`为例：

```cmake
add_executable(first_cmake main.cpp)
```

这里我们用到[`add_executable`](https://cmake.org/cmake/help/latest/command/add_executable.html)，其中第一个参数是最终生成的可执行文件名以及在CMake中定义的`Target`名。我们可以在CMake中继续使用`Target`的名字为`Target`的编译设置新的属性和行为。命令中第一个参数后面的参数都是编译目标所使用到的源文件。

#### 2.3.4 生成静态库并链接

附件位置：`4.static_lib_test`

**A.生成静态库**

```cmake
#account_dir/CMakeLists.txt

# 最低版本要求
cmake_minimum_required(VERSION 3.10)

# 项目信息
project(Account)

# 添加静态库，Linux下会生成libAccount.a
add_library(Account STATIC Account.cpp Account.h)
# 编译静态库后，会在build下生成 build/libAccount.a 静态库文件
account_dir/
├── Account.cpp
├── Account.h
├── build
│   └── libAccount.a
└── CMakeLists.txt
```

这里我们用到[`add_library`](https://cmake.org/cmake/help/latest/command/add_library.html), 和`add_executable`一样，`Account`为最终生成的库文件名（`lib库名称.a`），第二个参数是用于指定链接库为动态链接库（`SHARED`）还是静态链接库（`STATIC`），后面的参数是需要用到的源文件。

**B.链接**

```cmake
# test_account/CMakeLists.txt

# 最低版本要求
cmake_minimum_required(VERSION 3.10)

# 项目名称
project(test_account)

# 添加执行文件
add_executable(test_account test_account.cpp)

# 添加头文件目录，如果不添加，找不到头文件
target_include_directories(test_account PUBLIC "../account_dir")
# 添加库文件目录，如果不添加，找不到库文件
target_link_directories(test_account PUBLIC "../account_dir/build")
# 添加目标链接库
target_link_libraries(test_account PRIVATE Account)
# 编译后目录如下
4.static_lib_test/
├── account_dir
│   ├── Account.cpp
│   ├── Account.h
│   ├── build
│   │   └── libAccount.a
│   └── CMakeLists.txt
└── test_account 
    ├── build
    │   └── test_account
    ├── CMakeLists.txt
    └── test_account.cpp
```

我们通过`add_library`和`add_executable`定义了`Target`，我们可以通过`Target`的名称为其添加属性，例如：

```cpp
# 指定目标包含的头文件目录
target_include_directories(test_account PUBLIC "../account_dir")
# 添加库文件目录，如果不添加，找不到库文件
target_link_directories(test_account PUBLIC "../account_dir/build")
# 指定目标链接的库
target_link_libraries(test_account PRIVATE Account)

```

- 通过[`target_include_directories`](https://cmake.org/cmake/help/latest/command/target_include_directories.html)，我们给`test_account`添加了头文件引用路径`"../account_dir"`。上面的关键词`PUBLIC`,`PRIVATE`用于说明目标属性的作用范围，更多介绍参考下节。
- 通过[`target_link_libraries`](https://cmake.org/cmake/help/latest/command/target_link_libraries.html)，将前面生成的静态库`libAccount.a`链接给对象`test_account`，但此时还没指定库文件的目录，CMake无法定位库文件
- 再通过[`target_link_directories`](https://cmake.org/cmake/help/latest/command/target_link_directories.html)，添加库文件的目录即可。

#### 2.3.5 生成动态库并连接

附件位置：`5.dynamic_lib_test `

**A.生成动态库**

```cmake
#account_dir/CMakeLists.txt

# 添加动态库，Linux下会生成libAccount.so
add_library(Account SHARED Account.cpp Account.h)
# 编译动态库后，会在build下生成 build/libAccount.so 动态库文件
account_dir/
├── Account.cpp
├── Account.h
├── build
│   └── libAccount.so
└── CMakeLists.txt
```

**B.链接**

操作不变。

```shell
# ldd查看依赖的动态库
libAccount.so => /home/enpei/Documents/course_cpp_tensorrt/course_5/src/5.dynamic_lib_test/test_account/../account_dir/build/libAccount.so (0x00007fb692cf1000)
```

当然，也可以用一个`CMakeLists.txt`来一次性编译，参考附件`6.build_together`

```cmake
#6.build_together/CMakeLists.txt`

# 最低版本要求
cmake_minimum_required(VERSION 3.10)

# 项目信息
project(test_account)

# 添加动态库
add_library(Account SHARED "./account_dir/Account.cpp" "./account_dir/Account.h")

# 添加可执行文件
add_executable(test_account "./test_account/test_account.cpp")

# 添加头文件
target_include_directories(test_account PUBLIC "./account_dir")
# 添加链接库
target_link_libraries(test_account Account)
```

#### 2.3.6 CMake 中的 PUBLIC、PRIVATE、INTERFACE

CMake中经常使用`target_...()`类似的命令，一般这样的命令支持通过`PUBLIC`、`PRIVATE`、`INTERFACE`关键字来控制传播。

以`target_link_libraries(A B)`为例，从理解的角度来看

- `PRIVATE` ：依赖项`B`仅链接到目标` A`，如果有`C` 链接了`A`，`C`不会链接`B`
- `INTERFACE` ：依赖项`B`并不链接到目标`A`，如果有`C` 链接了`A`，`C`会链接`B`
- `PUBLIC` ：依赖项`B`链接到目标` A`，如果有`C` 链接了`A`，`C`也会链接`B`

其实就是对象属性的传递，打个散烟的比方：

- `PRIVATE`： 就是自己抽，不给别人抽
- `INTERFACE` ：就是自己不抽，给别人抽
- `PUBLIC` ：就是自己抽，也给别人抽

从使用的角度来说，如果有`C`链接了目标`A`

- 如果`B`仅用于`A`的实现，且不在头文件中提供给`C`使用，使用`PRIVATE`
- 如果`B`不用于`A`的实现，仅在头文件中作为借口给`C`使用，使用`INTERFACE`
- 如果`B`既用于`A`的实现，也在头文件中提供给`C`使用，使用`PUBLIC`

举例：

```cmake
# 创建库
add_library(C c.cpp)
add_library(D d.cpp)
add_library(B b.cpp)

# C是B的PUBLIC依赖项
target_link_libraries(B PUBLIC C)
# D是B的PRIVATE依赖项
target_link_libraries(B PRIVATE D)

# 添加可执行文件
add_executable(A a.cpp)

# 将B链接到A
target_link_libraries(A B)
```

- 因为`C`是`B`的`PUBLIC`依赖项，所以`C`会传播到`A`
- 因为`D`是`B`的`PRIVATE`依赖性，所以`D`不会传播到`A`

#### 2.3.7 变量

附件位置：`7.message_var_demo `

像其他编程语言一样，我们应该将CMake理解为一门编程语言。我们也需要设定变量来储存我们的选项，信息。有时候我们通过变量来判断我们在什么平台上，通过变量来判断我们需要编译哪些`Target`，也通过变量来决定添加哪些依赖。

#### 2.3.8 include引入其他代码

附件位置：`8.include_demo `

#### 2.3.9 条件控制

附件位置：`9.if_demo `

正如前面所讲，应该把CMake当成编程语言，除了可以设置变量以外，CMake还可以写条件控制。

```cmake
if(variable)
    # 为true的常量：ON、YES、TRUE、Y、1、非0数字
else()
    # 为false的常量：OFF、NO、FALSE、N、0、空字符串、NOTFOUND
endif()
```

可以和条件一起使用的关键词有

```cmake
NOT, TARGET, EXISTS (file), DEFINED等
STREQUAL, AND, OR, MATCHES (regular expression), VERSION_LESS, VERSION_LESS_EQUAL等
```

#### 2.3.10 CMake分步编译

附件位置：`10.steps_demo `

```bash
# 查看所有目标
$ cmake -S . -B build
$ cd build
$ cmake --build . --target help

The following are some of the valid targets for this Makefile:
... all (the default if no target is provided)
... clean
... depend
... rebuild_cache
... edit_cache
... steps_demo
... main.o
... main.i
... main.s



# 1.预处理
$ cmake --build . --target main.i
# 输出：Preprocessing CXX source to CMakeFiles/steps_demo.dir/main.cpp.i
# 可以打开滑到底部

# 2.编译
$ cmake --build . --target main.s
# 输出汇编代码：Compiling CXX source to assembly CMakeFiles/steps_demo.dir/main.cpp.s

# 3.汇编
$ cmake --build . --target main.o
# 输出二进制文件：Building CXX object CMakeFiles/steps_demo.dir/main.cpp.o

# 链接
$ cmake --build .
Scanning dependencies of target steps_demo
[ 50%] Linking CXX executable steps_demo
[100%] Built target steps_demo

# 运行
./steps_demo
```

#### 2.3.11 生成器表达式

附件位置：`11.generator_expression `

生成器表达式简单来说就是在CMake生成构建系统的时候根据不同配置动态生成特定的内容。有时用它可以让代码更加精简，我们介绍几种常用的。

> 需要注意的是，生成表达式被展开是在生成构建系统的时候，所以不能通过解析配置`CMakeLists.txt`阶段的`message`命令打印，可以用类似`file(GENERATE OUTPUT "./generator_test.txt" CONTENT "$<$<BOOL:TRUE>:TEST>")`生成文件的方式间接测试。

在其最一般的形式中，生成器表达式是`$<...>`，尖括号中间可以是如下几种类型：

- 条件表达式
- 变量查询（Variable-Query）
- 目标查询（Target-Query）
- 输出相关的表达式

```cmake
# 1.条件表达式：$<condition:true_string>，当condition为真时，返回true_string，否则返回空字符串
$<0:TEST>  
$<1:TEST>  
$<$<BOOL:TRUE>:TEST>

# 2.变量查询（Variable-Query）
$<TARGET_EXISTS:target>：判断目标是否存在
$<CONFIG:Debug>：判断当前构建类型是否为Debug

# 3.目标查询（Target-Query）
$<TARGET_FILE:target>：获取编译目标的文件路径
$<TARGET_FILE_NAME:target>：获取编译目标的文件名
```

4.输出相关表达式：用于在不同的环节使用不同参数，比如需要在`install`和`build`环节分别用不同的参数，我们可以这样写：

```cmake
add_library(Foo ...)
target_include_directories(Foo
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
        $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)
```

其中`$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>`仅在`build`环节生效;而`$<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>`仅在`install`环节生效。通过设定不同阶段不同的参数，我们可以避免路径混乱的问题。

#### 2.3.12 函数和宏

附件位置：`12.function_macro `

```cmake
# 定义一个宏，宏名为my_macro，没有参数
macro(my_macro)
    message("宏内部的信息")
    set(macro_var "宏内部变量test")
endmacro(my_macro)

# 定义一个函数，函数名为second_func，有两个参数
function(second_func arg1 arg2)
    message("第一个参数：${arg1}, 第二个参数：${arg2}")
endfunction(second_func)
```

#### 2.3.13 设置安装

附件位置：`13.install_demo `

当需要发布项目时你需要指定项目文件的安装路径。下面的代码片段中，使用`install`安装`demo_test`，并分别将可执行文件安装在`bin`中，动态链接库和静态链接库都安装在`lib`，公共头文件安装在`include`。这里的路径都将添加`${CMAKE_INSTALL_PREFIX}`作为前缀（如果不设置`CMAKE_INSTALL_PREFIX`，则会安装到`/usr/local` 目录下）。实现安装的功能在你需要发布你项目给其他人使用时，非常有用。

```cmake
# 设置安装
install(TARGETS demo_test
        RUNTIME DESTINATION bin # 可执行文件
        LIBRARY DESTINATION lib # 动态库
        ARCHIVE DESTINATION lib # 静态库
        PUBLIC_HEADER DESTINATION include # 公共头文件
)
```

#### 2.3.14 寻找依赖 find_package

对于大部分支持了CMake的项目来说，均可以通过`find_package`找到对应的依赖库，参考附件：`14.find_demo `

```shell
# 使用find_package寻找<LibaryName>库，如果找到，一般都会有以下变量（库作者设置）
<LibaryName>_FOUND：表示是否找到
<LibaryName>_INCLUDE_DIR：表示头文件目录
<LibaryName>_LIBRARIES：表示库文件目录
```

假设我们编写了一个新的函数库，我们希望别的项目可以通过`find_package`对它进行引用，我们有两种办法：

- 编写一个`Find<LibraryName>.cmake`，适用于导入非cmake安装的项目，参考附件：`15.custom_find`
- 使用`install`安装，生成`<LibraryName>Config.cmake`文件，适用于导入自己开发的cmake项目，参考附件：`16.custom_install_demo`

### 2.4 opencv CMake安装

附件位置：`17.demo_opencv/ `

安装OpenCV：`sudo apt install libopencv-dev`

依赖和链接OpenCV与常规的添加依赖并没有太多不同，同时OpenCV提供了`cmake find package`的功能，因此我们可以通过`find_package`方便的定位opencv在系统中的位置和需要添加的依赖。

```cmake
find_package(OpenCV REQUIRED)

message("OPENCV INCLUDE DIRS: ${OpenCV_INCLUDE_DIRS}")
message("OPENCV LINK LIBRARIES: ${OpenCV_LIBS}")
```

如果cmake找到了OpenCV，配置cmake后，命令行会有如下输出：

```shell
OPENCV INCLUDE DIRS: /usr/include/opencv4
OPENCV LINK LIBRARIES: opencv_calib3d;opencv_core;opencv_dnn;opencv_features2d;opencv_flann;opencv_highgui;opencv_imgcodecs;opencv_imgproc;opencv_ml;opencv_objdetect;opencv_photo;opencv_stitching;opencv_video;opencv_videoio;opencv_aruco;opencv_bgsegm;opencv_bioinspired;opencv_ccalib;opencv_datasets;opencv_dnn_objdetect;opencv_dnn_superres;opencv_dpm;opencv_face;opencv_freetype;opencv_fuzzy;opencv_hdf;opencv_hfs;opencv_img_hash;opencv_line_descriptor;opencv_optflow;opencv_phase_unwrapping;opencv_plot;opencv_quality;opencv_reg;opencv_rgbd;opencv_saliency;opencv_shape;opencv_stereo;opencv_structured_light;opencv_superres;opencv_surface_matching;opencv_text;opencv_tracking;opencv_videostab;opencv_viz;opencv_ximgproc;opencv_xobjdetect;opencv_xphoto
```

# 三 opencv

## 一、vs code 结合Cmake debug

### 1.1 配置`tasks.json`

需要注意`"-DCMAKE_BUILD_TYPE=Debug" `要设置为`Debug`模式。

```json
{
	"version": "2.0.0",
	"tasks": [
		// 1. cmake 配置
		{
			"label": "cmake 配置",
			"type": "shell",
			"command": "cmake -B build -S . -DCMAKE_BUILD_TYPE=Debug",
			"problemMatcher": [],
			"group": {
				"kind": "build",
				"isDefault": true
			},
			"options": {
				"cwd": "${workspaceFolder}"
			}
		},
		// 2. cmake 构建
		{
			"label": "cmake 构建",
			"type": "shell",
			"command": "cmake --build build",
			"problemMatcher": [],
			"group": {
				"kind": "build",
				"isDefault": true
			},
			"options": {
				"cwd": "${workspaceFolder}"
			},
			"dependsOn": [
				"cmake 配置"
			]
		},
		// 3. 删除build 目录
		{
			"label": "删除build 目录",
			"type": "shell",
			"command": "rm -rf build",
			"problemMatcher": [],
			"group": {
				"kind": "build",
				"isDefault": true
			},
			"options": {
				"cwd": "${workspaceFolder}"
			}
		},
		// 4. 运行可执行文件=========================================需要修改
		{
			"label": "运行可执行文件",
			"type": "shell",
			//"command": "./build/demo_${fileBasenameNoExtension}",
			"command": "./build/demo_1.img",
			//"command": "./build/demo_1.img",
			"problemMatcher": [],
			"group": {
				"kind": "build",
				"isDefault": true
			},
			"options": {
				"cwd": "${workspaceFolder}"
			},
			"dependsOn": [
				"cmake 构建"
			]
		},
	]
}
```

### 1.2 配置`launch.json`

```json
{
    // 使用 IntelliSense 了解相关属性。 
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "CMake调试",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}/build/cmake_debug", // 编译后的程序，需要结合CMakeLists.txt中的add_executable()函数
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "miDebuggerPath": "/usr/bin/gdb",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ],
            "preLaunchTask": "CMake编译"
        }
    ]
}
```

### 1.3 CMakeLists.txt

```shell
# 最低版本要求
cmake_minimum_required(VERSION 3.10)

# 项目信息
project(opencv_demo)

# 使用find_package命令查找OpenCV库
find_package(OpenCV REQUIRED)
if (OpenCV_FOUND)
    message(STATUS "OpenCV library status:")
    message(STATUS "    version: ${OpenCV_VERSION}")
    message(STATUS "    libraries: ${OpenCV_LIBRARIES}")
    message(STATUS "    include path: ${OpenCV_INCLUDE_DIRS}")
else()
    message(FATAL_ERROR "Could not find OpenCV library")
endif()

find_package(gflags REQUIRED)
if (gflags_FOUND)
    message(STATUS "gflags library status:")
    message(STATUS "    version: ${gflags_VERSION}")
    message(STATUS "    libraries: ${gflags_LIBRARIES}")
    message(STATUS "    include path: ${gflags_INCLUDE_DIR}")
else()
    message(FATAL_ERROR "Could not find gflags library")
endif()
#find_package(GLIB 2.72.4 REQUIRED)


# 添加头文件
include_directories(${OpenCV_INCLUDE_DIRS} ${gflags_INCLUDE_DIR})
# 链接库
link_libraries(glib-2.0 gio-2.0 ${OpenCV_LIBRARIES} ${gflags_LIBRARIES} )


# 添加      ================================需要修改最后生成的可执行文件名
add_executable(demo_1.img src/1.img.cpp)       
add_executable(demo_2.video src/2.video.cpp)
#add_executable(demo_3.camera src/3.camera.cpp)
```



### 1.4 build 视频文件报错

```shell
/usr/bin/ld: /lib/x86_64-linux-gnu/libgio-2.0.so.0: undefined reference to `g_log_set_debug_enabled'
collect2: error: ld returned 1 exit status
gmake[2]: *** [CMakeFiles/demo_2.video.dir/build.make:149：demo_2.video] 错误 1
gmake[1]: *** [CMakeFiles/Makefile2:83：CMakeFiles/demo_2.video.dir/all] 错误 2
gmake: *** [Makefile:91：all] 错误 2
```

解决方案 ： 添加 glib库的环境变量

```
1 CMakeLists.txt 中增加链接库
link_libraries(glib-2.0 gio-2.0 ${OpenCV_LIBS} ${gflags_LIBRARIES} )

2 系统文件中设置永久环境变量
```

`LD_LIBRARY_PATH`是一个环境变量，用于指定运行时动态链接器搜索共享库时的目录列表。要确保程序使用正确的库版本，可以将该库的目录添加到`LD_LIBRARY_PATH`。

以下是如何设置`LD_LIBRARY_PATH`的步骤：

1. **找到库的正确路径**：`pkg-config --libs glib-2.0`

2. **临时设置LD_LIBRARY_PATH**：你可以临时地为当前的终端会话设置`LD_LIBRARY_PATH`：

    在编译程序前，终端运行

    ```bash
    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/lib/x86_64-linux-gnu
    ```

3. **永久设置LD_LIBRARY_PATH**：如果你希望永久地更改`LD_LIBRARY_PATH`（例如，每次打开新的终端时），可以将上述`export`命令添加到你的`~/.bashrc`或`~/.bash_profile`文件中。然后，每次启动新的终端时，更改就会自动生效。

    打开文件：
    ```bash
    nano ~/.bashrc
    ```

    在文件的末尾添加：
    ```bash
    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/lib/x86_64-linux-gnu
    ctrl+o 报错  ctrl+x 退出
    ```

    保存并关闭文件。然后，为当前的终端会话加载更改：
    ```bash
    source ~/.bashrc
    ```

**警告**：过度或错误地设置`LD_LIBRARY_PATH`可能会导致系统行为异常或其他应用程序出错。因此，仅当确实需要时才更改它，并确保只添加必要的路径。

确保在更改后，你的程序运行正常，并且没有其他的不期望的副作用。



## 二、图片、视频、摄像头读取显示

### 2.1 读取图片并显示

```c++
// 使用imread函数读取图片，和Python用法类似
// 读取的数据保存在Mat类型的变量image中，Mat是opencv中的图像数据结构，类似numpy中的ndarray
cv::Mat image = cv::imread("图片路径");

// 输出数据，以numpy和Python list格式输出
std::cout << cv::format(image, cv::Formatter::FMT_NUMPY) << std::endl;
std::cout << cv::format(image, cv::Formatter::FMT_PYTHON) << std::endl;

// 判断图像是否读取成功，返回true表示失败
if (image.empty())
{
  std::cout << "无法读取图片"  << std::endl;
  return 1;
} 
// imshow显示图像
cv::imshow("opencv demo", image);
// 保存图像
cv::imwrite("./output/gray_image.jpg", gray_image);

// 等待按键
cv::waitKey(0); 
```

### 2.2 读取视频文件并显示

```c++
// 读取视频：创建了一个VideoCapture对象，参数为视频路径
cv::VideoCapture capture("视频路径");

// 判断视频是否读取成功，返回true表示成功
if (!capture.isOpened())
{
  std::cout << "无法读取视频"  << std::endl;
  return 1;
}

// 读取视频帧，使用Mat类型的frame存储返回的帧
cv::Mat frame;
// 循环读取视频帧
while (true)
{
  // 读取视频帧，使用 >> 运算符或者read()函数，他的参数是返回的帧
  capture.read(frame);
  // capture >> frame;
  
  // 显示视频帧
  cv::imshow("opencv demo", frame);
}
```

### 2.3 读取摄像头并写入文件

```c++
// 读取视频：创建了一个VideoCapture对象，参数为摄像头编号
cv::VideoCapture capture(0);

// 写入MP4文件，参数分别是：文件名，编码格式，帧率，帧大小  
cv::VideoWriter writer("record.mp4", cv::VideoWriter::fourcc('H', '2', '6', '4'), 20, cv::Size(640, 480));

// 写入视频
writer.write(frame);
```

## 三、图片基本操作

### 3.1 颜色转换

```c++
// BGR -> Gray
// 三个参数分别是输入图像、输出图像、转换方式
cv::cvtColor(src, gray, cv::COLOR_BGR2GRAY);
// BGR -> HSV，Hue(色调)、Saturation(饱和度)、Value(明度)
cv::cvtColor(src, hsv, cv::COLOR_BGR2HSV);
// BGR -> RGB
cv::cvtColor(src, rgb, cv::COLOR_BGR2RGB);
```

### 3.2 图像filtering

```c++
// 三个参数分别是输入图像、输出图像、卷积核大小
cv::GaussianBlur(src, blur, cv::Size(7, 7), 0);
// 膨胀
// 三个参数分别是输入图像、输出图像、卷积核大小
cv::dilate(src, dilate, cv::getStructuringElement(cv::MORPH_RECT, cv::Size(5, 5)));
// 腐蚀
// 三个参数分别是输入图像、输出图像、卷积核大小
cv::erode(src, erode, cv::getStructuringElement(cv::MORPH_RECT, cv::Size(5, 5)));
```

### 3.3 形状调整

```c++
// ======== resize ========
// 三个参数分别是输入图像、输出图像、输出图像大小
cv::resize(src, resize, cv::Size(320, 240));

// ======== copy ========
cv::Mat copy;
src.copyTo(copy);
// ======== ROI裁剪 ========
cv::Rect rect(100, 100, 200, 100); // x, y, width, height
cv::Mat roi = src(rect);
cv::imwrite("./output/3.roi.jpg", roi);

// ======== 拼接 ========
cv::Mat dog_img = cv::imread("./media/dog.jpg");
cv::Mat dog_resize;
cv::resize(dog_img, dog_resize, cv::Size(320, 240));

// 水平拼接，需要保证两张图片的高度（rows）一致
cv::Mat hconcat_img;
cv::hconcat(resize, dog_resize, hconcat_img);
cv::imwrite("./output/3.hconcat.jpg", hconcat_img);

// 或者使用vector方式
std::vector<cv::Mat> imgs{resize, dog_resize, resize, dog_resize};
cv::Mat hconcat_img2;
cv::hconcat(imgs, hconcat_img2);
cv::imwrite("./output/3.hconcat2.jpg", hconcat_img2);

// 数组方式
cv::Mat imgs_arr[] = {dog_resize, resize, dog_resize, resize};
cv::Mat hconcat_img3;
cv::hconcat(imgs_arr, 4, hconcat_img3); // 4是数组长度
cv::imwrite("./output/3.hconcat3.jpg", hconcat_img3);

// 垂直拼接，需要保证两张图片的宽度（cols）一致
cv::Mat vconcat_img;
cv::vconcat(resize, dog_resize, vconcat_img);
cv::imwrite("./output/3.vconcat.jpg", vconcat_img);

// ======== 翻转 ========
cv::Mat flip;
// 三个参数分别是输入图像、输出图像、翻转方向
cv::flip(src, flip, 1); // 1表示水平翻转，0表示垂直翻转，-1表示水平垂直翻转

// ======== 旋转 ========
cv::Mat rotate;
// 三个参数分别是输入图像、输出图像、旋转角度
cv::rotate(src, rotate, cv::ROTATE_90_CLOCKWISE); // 顺时针旋转90度
```

### 3.4 绘制

```c++
// 创建一个黑色图像，参数分别是图像大小、图像类型，CV_8UC3表示8位无符号整数，3通道
cv::Mat image = cv::Mat::zeros(cv::Size(600, 600), CV_8UC3);

// 绘制直线，参数分别是图像、起点、终点、颜色、线宽、线型
cv::line(image, cv::Point(50, 50), cv::Point(350, 250), cv::Scalar(0, 0, 255), 2, cv::LINE_AA);
// 绘制矩形，参数分别是图像、左上角、右下角、颜色、线宽、线型
cv::rectangle(image, cv::Point(50, 50), cv::Point(350, 250), cv::Scalar(0, 255, 0), 2, cv::LINE_AA);
// 绘制圆形，参数分别是图像、圆心、半径、颜色、线宽、线型
cv::circle(image, cv::Point(200, 150), 100, cv::Scalar(255, 0, 0), 2, cv::LINE_AA);
// 实心
cv::circle(image, cv::Point(200, 150), 50, cv::Scalar(255, 0, 0), -1, cv::LINE_AA);

// ================== 多边形 ==================
cv::Point points[2][4]; // 定义两个多边形的顶点数组
// 第一个多边形的顶点
points[0][0] = cv::Point(100, 115);
points[0][1] = cv::Point(255, 135);
points[0][2] = cv::Point(140, 365);
points[0][3] = cv::Point(100, 300);
// 第二个多边形的顶点
points[1][0] = cv::Point(300, 315);
points[1][1] = cv::Point(555, 335);
points[1][2] = cv::Point(340, 565);
points[1][3] = cv::Point(300, 500);
// ppt[] 要同时添加两个多边形顶点数组的地址）
const cv::Point *pts_v[] = {points[0], points[1]};
// npts_v[]要定义每个多边形的定点数
int npts_v[] = {4, 4};
// 绘制多边形，参数分别是图像、顶点数组、顶点数、是否闭合、颜色、线宽、线型
cv::polylines(image, pts_v, npts_v, 2, true, cv::Scalar(255, 0, 255), 2, 8, 0);

// ================== 使用vector绘制多边形 ==================
std::vector<cv::Point> points_v;
// 随机生成5个点
for (int i = 0; i < 5; i++)
{
  points_v.push_back(cv::Point(rand() % 600, rand() % 600));
}
// 绘制多边形，参数分别是图像、顶点数组、是否闭合、颜色、线宽、线型
cv::polylines(image, points_v, true, cv::Scalar(255, 0, 0), 2, 8, 0);


// ================== 绘制文字 ==================
// 参数分别是图像、文字、文字位置、字体、字体大小、颜色、线宽、线型
cv::putText(image, "Hello World!", cv::Point(400, 50), cv::FONT_HERSHEY_SIMPLEX, 1.0, cv::Scalar(255, 255, 255), 2, 8, 0);
```

![img](https://enpei-md.oss-cn-hangzhou.aliyuncs.com/img4.drawing.jpg?x-oss-process=style/wp)

## 四、RTSP 视频流

### 4.1 本机构造RTSP视频流（optional）

```shell
# Ubuntu安装ffmpeg
sudo apt-get install ffmpeg

# 赋予权限
chmod +x rtsp-simple-server
chmod +x start_server.sh
# 运行服务
./start_server.sh

# 退出服务
pkill rtsp-simple-server
pkill ffmpeg
```

### 4.2 使用ffmpeg作为视频解码

```c++
// CAP_FFMPEG：opencv 使用ffmpeg解码
cv::VideoCapture stream1 = cv::VideoCapture("rtsp地址", cv::CAP_FFMPEG);
```

## 五、人脸检测小例子

附件位置：`5.face_detection`

# 四 TensorRT

## 一、准备知识

NVIDIA® TensorRT™是一个用于高性能深度学习的推理框架。它可以与TensorFlow、PyTorch和MXNet等训练框架相辅相成地工作。

### 1.1 环境配置

#### AAA：若使用autodl不用配置，直接选择源安装,自动有cuda cudnn torch

![image-20240617154227814](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202406171542987.png)

#### A. CUDA Driver

- 使用CUDA前，要求GPU驱动与`cuda` 的版本要匹配，匹配关系如下：

  > 参考：https://docs.nvidia.com/cuda/cuda-toolkit-release-notes/index.html#cuda-major-component-versions__table-cuda-toolkit-driver-versions

![img](https://enpei-md.oss-cn-hangzhou.aliyuncs.com/img202302061153154.png?x-oss-process=style/wp)

- 检查安装机器建议的驱动

  ```shell
  // （不安装报错）
  root@autodl-container-cbb611a852-827cf0d2:~# nvidia-smi
  No devices were found
  ```

  ```shell
  $ ubuntu-drivers devices
  ```

  报错1：`bash: ubuntu-drivers: command not found`

  解决1：`sudo apt-get install ubuntu-drivers-common`

  报错2：`bash: ubuntu-drivers: command not found`

  解决2：`sudo apt-get update`

  ```bash
  $ ubuntu-drivers devices
  
  (base) enpei@enpei-ubutnu-desktop:~$ ubuntu-drivers devices
  == /sys/devices/pci0000:00/0000:00:01.0/0000:01:00.0 ==
  modalias : pci:v000010DEd00001C03sv000010DEsd000011D7bc03sc00i00
  vendor   : NVIDIA Corporation
  model    : GP106 [GeForce GTX 1060 6GB]
  driver   : nvidia-driver-525 - distro non-free recommended
  driver   : nvidia-driver-510 - distro non-free
  driver   : nvidia-driver-390 - distro non-free
  driver   : nvidia-driver-520 - third-party non-free
  driver   : nvidia-driver-515-server - distro non-free
  driver   : nvidia-driver-470 - distro non-free
  driver   : nvidia-driver-418-server - distro non-free
  driver   : nvidia-driver-470-server - distro non-free
  driver   : nvidia-driver-525-server - distro non-free
  driver   : nvidia-driver-515 - distro non-free
  driver   : nvidia-driver-450-server - distro non-free
  driver   : xserver-xorg-video-nouveau - distro free builtin
  ```

  上面信息提示了，当前我使用的GPU是[GeForce GTX 1060 6GB]，他推荐的（recommended）驱动是`nvidia-driver-525`。

- 安装指定版本

  ```bash
  $ sudo apt install nvidia-driver-525
  ```

- 重启

  ```bash
  $ sudo reboot
  ```

- 检查安装

  ```bash
  $ nvidia-smi
  
  (base) enpei@enpei-ubutnu-desktop:~$ nvidia-smi
  Mon Feb  2 12:23:45 2023
  +-----------------------------------------------------------------------------+
  | NVIDIA-SMI 525.78.01    Driver Version: 525.78.01    CUDA Version: 12.0     |
  |-------------------------------+----------------------+----------------------+
  | GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
  | Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
  |                               |                      |               MIG M. |
  |===============================+======================+======================|
  |   0  NVIDIA GeForce ...  Off  | 00000000:01:00.0  On |                  N/A |
  | 40%   29C    P8     9W / 120W |    239MiB /  6144MiB |      0%      Default |
  |                               |                      |                  N/A |
  +-------------------------------+----------------------+----------------------+
  
  +-----------------------------------------------------------------------------+
  | Processes:                                                                  |
  |  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
  |        ID   ID                                                   Usage      |
  |=============================================================================|
  |    0   N/A  N/A      1079      G   /usr/lib/xorg/Xorg                102MiB |
  |    0   N/A  N/A      1387      G   /usr/bin/gnome-shell              133MiB |
  +-----------------------------------------------------------------------------+
  ```

  可以看到当前安装的驱动版本是`525.78.01`，需要注意`CUDA Version: 12.0`指当前驱动支持的最高版本。

#### B. CUDA

* 查看显卡信息和支持cuda的最高版本

  ```shell
  nvidia-smi
  ```

  

- 选择对应版本：https://developer.nvidia.com/cuda-toolkit-archive

  

- 根据提示安装，如我选择的11.8 版本的：https://developer.nvidia.com/cuda-11-8-0-download-archive?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=20.04&target_type=deb_local

  

  ```bash
  wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin
  sudo mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600
  wget https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda-repo-ubuntu2004-11-8-local_11.8.0-520.61.05-1_amd64.deb
  sudo dpkg -i cuda-repo-ubuntu2004-11-8-local_11.8.0-520.61.05-1_amd64.deb
  sudo cp /var/cuda-repo-ubuntu2004-11-8-local/cuda-*-keyring.gpg /usr/share/keyrings/
  sudo apt-get update
  sudo apt-get -y install cuda
  ```

- 安装`nvcc`

  ```bash
  sudo apt install nvidia-cuda-toolkit
  // 使用nvcc检查cuda安装成功
  
  ```

- 重启

- ```shell
  nvcc -v
  ```

  

#### C. cuDNN

- 下载安装包：访问：https://developer.nvidia.com/zh-cn/cudnn，选择对应的版本，下载对应的安装包（建议使用Debian包安装）

  

  比如我下载的是：[Local Installer for Ubuntu20.04 x86_64 (Deb)](https://developer.nvidia.com/downloads/c118-cudnn-local-repo-ubuntu2004-8708410-1amd64deb)，下载后的文件名为`cudnn-local-repo-ubuntu2004-8.7.0.84_1.0-1_amd64.deb`。

- 安装：

  > 参考链接：https://docs.nvidia.com/deeplearning/cudnn/install-guide/index.html

  ```bash
  # 注意，运行下面的命令前，将下面的 X.Y和v8.x.x.x 替换成自己具体的CUDA 和 cuDNN版本，如我的CUDA 版本是11.8，cuDNN 版本是 8.7.0.84
  
  sudo dpkg -i cudnn-local-repo-${OS}-8.x.x.x_1.0-1_amd64.deb
  # 我的：sudo dpkg -i cudnn-local-repo-ubuntu2004-8.7.0.84_1.0-1_amd64.deb
  
  sudo cp /var/cudnn-local-repo-*/cudnn-local-*-keyring.gpg /usr/share/keyrings/
  sudo apt-get update
  
  
  sudo apt-get install libcudnn8=8.x.x.x-1+cudaX.Y
  # 我的：sudo apt-get install libcudnn8=8.7.0.84-1+cuda11.8
  
  
  sudo apt-get install libcudnn8-dev=8.x.x.x-1+cudaX.Y
  # 我的：sudo apt-get install libcudnn8-dev=8.7.0.84-1+cuda11.8
  
  
  sudo apt-get install libcudnn8-samples=8.x.x.x-1+cudaX.Y
  # 我的：sudo apt-get install libcudnn8-samples=8.7.0.84-1+cuda11.8
  ```

- 验证

  ```bash
  # 复制文件
  cp -r /usr/src/cudnn_samples_v8/ $HOME
  cd  $HOME/cudnn_samples_v8/mnistCUDNN
  make clean && make
  ./mnistCUDNN
  ```

  > 可能报错：test.c:1:10: fatal error: FreeImage.h: No such file or directory
  >
  > 解决办法：sudo apt-get install libfreeimage3 libfreeimage-dev

#### D. TensorRT

- 访问：https://developer.nvidia.com/nvidia-tensorrt-8x-download 下载对应版本的TensorRT

  

  比如我选择的是 8.5.3版本，下载完文件名为：`nv-tensorrt-local-repo-ubuntu2004-8.5.3-cuda-11.8_1.0-1_amd64.deb`

- 安装：

  > 参考地址：https://docs.nvidia.com/deeplearning/tensorrt/install-guide/index.html#installing-debian

  ```bash
  # 替换成自己的OS 和 版本信息
  os="ubuntuxx04"
  tag="8.x.x-cuda-x.x"
  sudo dpkg -i nv-tensorrt-local-repo-${os}-${tag}_1.0-1_amd64.deb
  # 我的：sudo dpkg -i nv-tensorrt-local-repo-ubuntu2004-8.5.3-cuda-11.8_1.0-1_amd64.deb
  sudo cp /var/nv-tensorrt-local-repo-${os}-${tag}/*-keyring.gpg /usr/share/keyrings/
  # 我的：sudo cp /var/nv-tensorrt-local-repo-ubuntu2004-8.5.3-cuda-11.8/*-keyring.gpg /usr/share/keyrings/
  
  sudo apt-get update
  sudo apt-get install tensorrt
  ```

- 验证：

  ```bash
  dpkg -l | grep TensorRT
  
  # 输出
  ii  libnvinfer-bin                                    8.5.3-1+cuda11.8                    amd64        TensorRT binaries
  ii  libnvinfer-dev                                    8.5.3-1+cuda11.8                    amd64        TensorRT development libraries and headers
  ii  libnvinfer-plugin-dev                             8.5.3-1+cuda11.8                    amd64        TensorRT plugin libraries
  ii  libnvinfer-plugin8                                8.5.3-1+cuda11.8                    amd64        TensorRT plugin libraries
  ii  libnvinfer-samples                                8.5.3-1+cuda11.8                    all          TensorRT samples
  ii  libnvinfer8                                       8.5.3-1+cuda11.8                    amd64        TensorRT runtime libraries
  ii  libnvonnxparsers-dev                              8.5.3-1+cuda11.8                    amd64        TensorRT ONNX libraries
  ii  libnvonnxparsers8                                 8.5.3-1+cuda11.8                    amd64        TensorRT ONNX libraries
  ii  libnvparsers-dev                                  8.5.3-1+cuda11.8                    amd64        TensorRT parsers libraries
  ii  libnvparsers8                                     8.5.3-1+cuda11.8                    amd64        TensorRT parsers libraries
  ii  tensorrt                                          8.5.3.1-1+cuda11.8                  amd64        Meta package for TensorRT
  ```

  > 如果遇到`unmet dependencies`的问题, 一般是cuda cudnn没有安装好。TensorRT的`INCLUDE` 路径是 `/usr/include/x86_64-linux-gnu/`, `LIB`路径是`/usr/lib/x86_64-linux-gnu/`,Sample code在`/usr/src/tensorrt/samples`, `trtexec`在`/usr/src/tensorrt/bin`下。

### 1.2 编程模型

TensorRT分两个阶段运行

- 构建（`Build`）阶段：你向TensorRT提供一个模型定义，TensorRT为目标GPU优化这个模型。这个过程可以离线运行。
- 运行时（`Runtime`）阶段：你使用优化后的模型来运行推理。

构建阶段后，我们可以将优化后的模型保存为模型文件，模型文件可以用于后续加载，以省略模型构建和优化的过程。

## 二、构建阶段

> *样例代码：`6.trt_basic/src/build.cpp`*

构建阶段的最高级别接口是 `Builder`。`Builder`负责优化一个模型，并产生`Engine`。通过如下接口创建一个`Builder` 。

```cpp
nvinfer1::IBuilder* builder = nvinfer1::createInferBuilder(logger);
```

要生成一个可以进行推理的`Engine`，一般需要以下三个步骤：

- 创建一个网络定义
- 填写`Builder`构建配置参数，告诉构建器应该如何优化模型
- 调用`Builder`生成`Engine`

### 2.1 创建网络定义

`NetworkDefinition`接口被用来定义模型。如下所示：

```cpp
// bit shift，移位：y左移N位，相当于 y * 2^N
// kEXPLICIT_BATCH（显性Batch）为0，1U << 0 = 1
// static_cast：强制类型转换
const auto explicitBatch = 1U << static_cast<uint32_t>(nvinfer1::NetworkDefinitionCreationFlag::kEXPLICIT_BATCH);
nvinfer1::INetworkDefinition* network = builder->createNetworkV2(explicitBatch);
```

接口`createNetworkV2`接受配置参数，参数用按位标记的方式传入。比如上面激活`explicitBatch`，是通过`1U << static_cast<uint32_t>(nvinfer1::NetworkDefinitionCreationFlag::kEXPLICIT_BATCH);` 将explicitBatch对应的配置位设置为1实现的。在新版本中，请使用`createNetworkV2`而非其他任何创建`NetworkDefinition` 的接口。

将模型转移到TensorRT的最常见的方式是以ONNX格式从框架中导出（将在后续课程进行介绍），并使用TensorRT的ONNX解析器来填充网络定义。同时，也可以使用TensorRT的`Layer`和`Tensor`等接口一步一步地进行定义。通过接口来定义网络的代码示例如下：

- 添加输入层

```cpp
nvinfer1::ITensor* input = network->addInput("data", nvinfer1::DataType::kFLOAT, nvinfer1::Dims4{1, input_size, 1, 1});
```

- 添加全连接层

```cpp
nvinfer1::IFullyConnectedLayer* fc1 = network->addFullyConnected(*input, output_size, fc1w, fc1b);
```

- 添加激活层

```cpp
nvinfer1::IActivationLayer* relu1 = network->addActivation(*fc1->getOutput(0), nvinfer1::ActivationType::kRELU);
```

通过调用`network`的方法，我们可以构建网络的定义。

无论你选择哪种方式，你还必须定义哪些张量是网络的输入和输出。没有被标记为输出的张量被认为是瞬时值，可以被构建者优化掉。输入和输出张量必须被命名，以便在运行时，TensorRT知道如何将输入和输出缓冲区绑定到模型上。示例代码如下：

```cpp
// 设置输出名字
relu1->getOutput(0)->setName("output");
// 标记输出
network->markOutput(*relu1->getOutput(0));
```

TensorRT的网络定义不会复制参数数组（如卷积的权重）。因此，在构建阶段完成之前，你不能释放这些数组的内存。

### 2.2 配置参数

下面我们来添加相关`Builder` 的配置。`createBuilderConfig`接口被用来指定TensorRT应该如何优化模型。如下：

```cpp
nvinfer1::IBuilderConfig* config = builder->createBuilderConfig();
```

在可用的配置选项中，你可以控制TensorRT降低计算精度的能力，控制内存和运行时执行速度之间的权衡，并限制CUDA®内核的选择。由于构建器的运行可能需要几分钟或更长时间，你也可以控制构建器如何搜索内核，以及缓存搜索结果以用于后续运行。在我们的示例代码中，我们仅配置`workspace`（workspace 就是 tensorrt 里面算子可用的内存空间 ）大小和运行时`batch size` ，如下：

```cpp
// 配置运行时batch size参数
builder->setMaxBatchSize(1);
// 配置运行时workspace大小
std::cout << "Workspace Size = " << (1 << 28) / 1024.0f / 1024.0f << "MB" << std::endl; // 256Mib
config->setMaxWorkspaceSize(1 << 28);
```

### 2.3 生成Engine

在你有了网络定义和`Builder`配置后，你可以调用`Builder`来创建`Engine`。`Builder`以一种称为`plan`的序列化形式创建`Engine`，它可以立即反序列化，也可以保存到磁盘上供以后使用。需要注意的是，由TensorRT创建的`Engine`是特定于创建它们的TensorRT版本和创建它们的GPU的，当迁移到别的GPU和TensorRT版本时，不能保证模型能够被正确执行。生成`Engine`的示例代码如下：

```cpp
nvinfer1::ICudaEngine* engine = builder->buildEngineWithConfig(*network, *config);
```

### 2.4 保存为模型文件

当有了`engine`后我们可以将其保存为文件，以供后续使用。代码如下：

```cpp
// 序列化
nvinfer1::IHostMemory* engine_data = engine->serialize();
// 保存至文件
std::ofstream engine_file("mlp.engine", std::ios::binary);
engine_file.write((char*)engine_data->data(), engine_data->size());
```

### 2.5 释放资源

```cpp
// 理论上，前面申请的资源都应该在这里释放，但是这里只是为了演示，所以只释放了部分资源
file.close();             // 关闭文件
delete serialized_engine; // 释放序列化的engine
delete engine;            // 释放engine
delete config;            // 释放config
delete network;           // 释放network
delete builder;           // 释放builder
```

## 三、运行时阶段

> 样例代码: *`6.trt_basic/src/runtime.cu`*

TensorRT运行时的最高层级接口是`Runtime` 如下：

```cpp
nvinfer1::IRuntime *runtime = nvinfer1::createInferRuntime(looger);
```

当使用`Runtime`时，你通常会执行以下步骤：

- 反序列化一个计划以创建一个`Engine`。
- 从引擎中创建一个`ExecutionContext`。

然后，重复进行：

- 为Inference填充输入缓冲区。
- 在`ExecutionContext`调用`enqueueV2()`来运行Inference

### 3.1 反序列化并创建Engine

通过读取模型文件并反序列化，我们可以利用runtime生成`Engine`。如下：

```cpp
nvinfer1::ICudaEngine *engine = runtime->deserializeCudaEngine(engine_data.data(), engine_data.size(), nullptr);
```

`Engine`接口代表一个优化的模型。你可以查询`Engine`关于网络的输入和输出张量的信息，如：预期尺寸、数据类型、数据格式等。

### 3.2 创建一个`ExecutionContext`

有了Engine后我们需要创建`ExecutionContext` 以用于后面的推理执行。

```cpp
nvinfer1::IExecutionContext *context = engine->createExecutionContext();
```

从`Engine`创建的`ExecutionContext`接口是调用推理的主要接口。`ExecutionContext`包含与特定调用相关的所有状态，因此你可以有多个与单个引擎相关的上下文，且并行运行它们，在这里我们暂不展开了解，仅做介绍。

### 3.3 为推理填充输入

我们首先创建CUDA Stream用于推理的执行。

> stream 可以理解为一个任务队列，调用以 async 结尾的 api 时，是把任务加到队列，但执行是异步的，当有多个任务且互相没有依赖时可以创建多个 stream 分别用于不同的任务，任务直接的执行可以被 cuda driver 调度，这样某个任务做 memcpy时 另外一个任务可以执行计算任务，这样可以提高 gpu利用率。

```cpp
cudaStream_t stream = nullptr;
// 创建CUDA Stream用于context推理
cudaStreamCreate(&stream);
```

然后我们同时在CPU和GPU上分配输入输出内存，并将输入数据从CPU拷贝到GPU上。

```cpp
// 输入数据
float* h_in_data = new float[3]{1.4, 3.2, 1.1};
int in_data_size = sizeof(float) * 3;
float* d_in_data = nullptr;
// 输出数据
float* h_out_data = new float[2]{0.0, 0.0};
int out_data_size = sizeof(float) * 2;
float* d_out_data = nullptr;
// 申请GPU上的内存
cudaMalloc(&d_in_data, in_data_size);
cudaMalloc(&d_out_data, out_data_size);
// 拷贝数据
cudaMemcpyAsync(d_in_data, h_in_data, in_data_size, cudaMemcpyHostToDevice, stream);
// enqueueV2中是把输入输出的内存地址放到bindings这个数组中，需要写代码时确定这些输入输出的顺序（这样容易出错，而且不好定位bug，所以新的接口取消了这样的方式，不过目前很多官方 sample 也在用v2）
float* bindings[] = {d_in_data, d_out_data};
```

### 3.4 调用enqueueV2来执行推理

将数据从CPU中拷贝到GPU上后，便可以调用`enqueueV2` 进行推理。代码如下：

```cpp
// 执行推理
bool success = context->enqueueV2((void**)bindings, stream, nullptr);
// 把数据从GPU拷贝回host
cudaMemcpyAsync(h_out_data, d_out_data, out_data_size, cudaMemcpyDeviceToHost, stream);
// stream同步，等待stream中的操作完成
cudaStreamSynchronize(stream);
// 输出
std::cout << "输出信息: " << host_output_data[0] << " " << host_output_data[1] << std::endl;
```

### 3.5 释放资源

```cpp
cudaStreamDestroy(stream);
cudaFree(device_input_data_address);
cudaFree(device_output_data_address);   
delete[] host_input_data;
delete[] host_output_data;

delete context;
delete engine;
delete runtime;
```

## 四、编译和运行

> 样例代码: *`6.trt_basic/CMakeLists.txt`*

利用我们前面cmake课程介绍的添加自定义模块的方法，创建`cmake/FindTensorRT.cmake`文件，我们运行下面的命令以编译示例代码：

```bash
cmake -S . -B build 
cmake --build build
```

然后执行下面命令，build将生成mlp.engine，而runtime将读取mlp.engine并执行：

```bash
./build/build
./build/runtime
```

最后将看到输出结果：

```bash
输出信息: 0.970688 0.999697
```

# 五 项目一 YOLOV5 人员检测项目

![image-20231015180228401](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015180228401.png)

## 一、安装Pytorch 及 YOLO v5

### AAAA 若使用autodl

1. 使用源镜像，则自动有torch

2. github拉取yolo到服务器

   ```git
   git clone https://github.com/ultralytics/ultralytics.git
   ```

   ```cpp
   // 修改远程仓库到自己仓库
   // 为减少冲突，创建新仓库时候不要加readme.md
   // 查看当前项目远程地址
   git remot -v
   // 删除远程地址
   git remote rm origin
   // 添加自己的新地址
   git remote add origin 新地址
   // 检查是否添加成功
   git remote -v
   // 提交代码
   git add .
   git commit -m "first"
   git push origin main
   ```

3. 安装yolo运行的py依赖，opencv等

   ```cpp
   // 关闭梯子
   // 进入conda base环境
   pip install ultralytics -i https://pypi.mirrors.ustc.edu.cn/simple
   // 安装成功
   Successfully installed opencv-python-4.10.0.84 pandas-2.0.3 py-cpuinfo-9.0.0 scipy-1.10.1 seaborn-0.13.2 tqdm-4.66.4 tzdata-2024.1 ultralytics-8.2.35 ultralytics-thop-2.0.0
   ```

4. 测试yolo环境安装

   ```cpp
   // 命令行输入
   yolo predict model=yolov8n.pt imgsz=640 conf=0.25
   ```

   ![image-20240619144703511](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202406191447351.png)

   ![image-20240619144734284](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202406191447504.png)

   

### 1.1 安装GPU版 pytorch

- conda虚拟环境，手动安装

  首先，请参考上一节课将`GPU driver, cuda, cudnn`先安装完毕。

* 选择版本, [pythorch安装包](https://download.pytorch.org/whl/torch_stable.html)

  ```shell
  cu118/torch-2.2.0%2Bcu118-cp38-cp38-linux_x86_64.whl
  cuda版本  torch版本  cppython版本3.8  linux安装
  ```

  下载安装包后导入到conda创建的环境内

  ```shell
  安装包放入： \Anaconda3\envc\我的环境\Scripts>
  pip安装
  \Anaconda3\envc\我的环境\Scripts> pip install "torch-1.6.0+cu101=cp36-cp36m-win_amd64.whl"
  ```

  

* 检测安装成功

  ```python
  python
  >> import torch
  // 是否调用gpu
  >> print(torch.cuda.is_available())
  >> True
  // torch版本
  >>print(torch.__version__)
  2.0.0+cu118
  // gpu个数
  >>print(torch.cuda.device_count())
  1
  // cudnn版本
  >>print(torch.backends.cudnn.version())
  8799
  // cuda版本
  >>print(torch.version.cuda)
  11.8
  ```
  
  

### 1.2 安装YOLO v5所需依赖

- 安装

```shell
# 克隆地址
git clone https://github.com/ultralytics/yolov5.git
# 进入目录
cd yolov5
# 选择分支，这里使用了特定版本的yolov5，主要是避免出现兼容问题
git checkout a80dd66efe0bc7fe3772f259260d5b7278aab42f

# 安装依赖（如果是docker环境，要进入容器环境后再安装）
pip3 install -r requirements.txt
```

- 下载预训练权重文件

下载地址：https://github.com/ultralytics/yolov5，附件位置：`3.预训练模型/`，将权重文件放到`weights`目录下：

- 测试是否安装成功

```shell
python detect.py --source ./data/images/ --weights weights/yolov5s.pt --conf-thres 0.4
```

> docker容器内部可能报错：AttributeError: partially initialized module 'cv2' has no attribute '_registerMatType' (most likely due to a circular import)，使用`pip3 install "opencv-python-headless<4.3"`

如果一切配置成功，则可以看到以下检测结果

![image-20231015180259938](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015180259938.png)

## 二、YOLO v5训练自定义数据

### 2.1 标注数据

#### 2.1.1 安装labelImg

需要在有界面的主机上安装，远程ssh无法使用窗口

```shell
# 建议使用conda虚拟环境
# 安装
pip install labelImg
# 启动
labelImg
```

#### 2.1.2 标注

![image-20231015180319272](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015180319272.png)

按照视频示例教程进行标注，保存路径下会生成`txt` YOLO格式标注文件。

![image-20231015180330955](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015180330955.png)

- 一张图片对应一个txt标注文件（如果图中无所要物体，则无需txt文件）；
- txt每行一个物体（一张图中可以有多个标注）；
- 每行数据格式：`类别id、x_center y_center width height`；
- **xywh**必须归一化（0-1），其中`x_center、width`除以图片宽度，`y_center、height`除以画面高度；
- 类别id必须从0开始计数。

### 2.2 准备数据集

#### 2.2.1 组织目录结构

```bash
. 工作路径
├── datasets
│   └── person_data
│       ├── images
│       │   ├── train
│       │   │   └── demo_001.jpg
│       │   └── val
│       │       └── demo_002.jpg
│       └── labels
│           ├── train
│           │   └── demo_001.txt
│           └── val
│               └── demo_002.txt
└── yolov5
```

**要点：**

- `datasets`与`yolov5`同级目录；
- 图片 `datasets/person_data/images/train/{文件名}.jpg`对应的标注文件在 `datasets/person_data/labels/train/{文件名}.txt`，YOLO会根据这个映射关系自动寻找（`images`换成`labels`）；
- 训练集和验证集
  - `images`文件夹下有`train`和`val`文件夹，分别放置训练集和验证集图片;
  - `labels`文件夹有`train`和`val`文件夹，分别放置训练集和验证集标签(yolo格式）;

#### 2.2.2 创建 dataset.yaml

复制`yolov5/data/coco128.yaml`一份，比如为`coco_person.yaml`

```yaml
# Train/val/test sets as 1) dir: path/to/imgs, 2) file: path/to/imgs.txt, or 3) list: [path/to/imgs1, path/to/imgs2, ..]
path: ../datasets/person_data  # 数据所在目录
train: images/train  # 训练集图片所在位置（相对于path）
val:  images/val # 验证集图片所在位置（相对于path）
test:  # 测试集图片所在位置（相对于path）（可选）

# 类别
nc: 5  # 类别数量
names: ['pedestrians','riders','partially-visible-person','ignore-regions','crowd'] # 类别标签名
```

### 2.3 选择合适的预训练模型

官方权重下载地址：https://github.com/ultralytics/yolov5

![image-20231015180358127](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015180358127.png)

复制`models`下对应模型的`yaml`文件，重命名，比如课程另存为`yolov5s_person.yaml`，并修改其中：

```shell
# nc: 80  # 类别数量
nc: 5  # number of classes
```

### 2.4 训练

下载对应的预训练模型权重文件，可以放到`weights`目录下，设置本机最好性能的各个参数，即可开始训练，课程中训练了以下参数：

```shell
# yolov5s 
python ./train.py --data ./data/coco_person.yaml --cfg ./models/yolov5s_person.yaml --weights ./weights/yolov5s.pt --batch-size 32 --epochs 120 --workers 0 --name s_120 --project yolo_person_s
```

> 更多参数见`train.py`；
>
> 训练结果在`yolo_person_s/`中可见，一般训练时间在几个小时以上。

### 2.5 可视化

#### 2.5.1 wandb

YOLO官网推荐使用https://wandb.ai/。

- 去官网注册账号；
- 获取`key`秘钥，地址：https://wandb.ai/authorize
- 使用`pip install wandb`安装包；
- 使用`wandb login`粘贴秘钥后登录；
- 打开网站即可查看训练进展。

![image-20231015180416602](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015180416602.png)

#### 2.5.2 Tensorboard

```
tensorboard --logdir=./yolo_person_s
```

![image-20231015180456661](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015180456661.png)

### 2.6 测试评估模型

#### 2.6.1 测试

> 测试媒体位置：`4.老师训练结果/`

```shell
# 如                                                         
python detect.py --source ./000057.jpg --weights ./yolo_person_s/s_120/weights/best.pt --conf-thres 0.3
# 或
python detect.py --source ./c3.mp4 --weights ./yolo_person_s/s_120/weights/best.pt --conf-thres 0.3
```

检测前后结果：

![image-20231015180517193](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015180517193.png)

![image-20231015180527630](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015180527630.png)

#### 2.6.2 评估

```shell
# s 模型

# python val.py --data  ./data/coco_person.yaml  --weights ./yolo_person_s/s_120/weights/best.pt --batch-size 12
# 15.8 GFLOPs
                   Class     Images     Labels          P          R     mAP@.5 mAP@.5:.95: 
                     all       1000      28027      0.451      0.372      0.375      0.209
             pedestrians       1000      17600      0.738      0.854      0.879      0.608
                  riders       1000        185      0.546      0.492      0.522      0.256
 artially-visible-person       1000       9198      0.461      0.334      0.336      0.125
          ignore-regions       1000        391       0.36      0.132      0.116     0.0463
                   crowd       1000        653      0.152     0.0468     0.0244    0.00841
```

## 三、yolov5模型导出ONNX

### 3.1 工作机制

在本项目中，我们将使用`tensort decode plugin`来代替原来yolov5代码中的decode操作，如果不替换，这部分运算将影响整体性能。

为了让`tensorrt`能够识别并加载我们额外添加的`plugin operator`，我们需要修改Yolov5代码中导出onnx模型的部分。

> onnx是一种开放的模型格式，可以用来表示深度学习模型，它是由微软开发的，目前已经成为了深度学习模型的标准格式。可以简单理解为各种框架模型转换的一种桥梁。

流程如图所示：

![image-20231015180549650](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015180549650.png)

### 3.2 修改yolov5 代码，输出ONNX

> 修改之前，建议先使用`python export.py --weights weights/yolov5s.pt --include onnx --simplify --dynamic`导出一份原始操作的onnx模型，以便和修改后的模型进行对比。

使用课程附件提供的`git patch`批量修改代码，代码位置：`1.代码/export.patch`

```shell
# 将patch复制到yolov5文件夹
cp export.patch yolov5/
# 进入yolov5文件夹
cd yolov5/
# 应用patch
git am export.patch
```

> 在理解代码逻辑后，也可以根据自己的需要在最新版本上的yolov5上进行修改。

首先根据上文自行根据yolov5的要求安装相关依赖，然后再执行下面命令安装导出onnx需要的依赖：

```bash
pip install seaborn
pip install onnx-graphsurgeon
pip install onnx-simplifier==0.3.10

apt update
apt install -y libgl1-mesa-glx
```

安装完成后，准备好训练好的模型文件，这里默认为`yolov5s.pt`，然后执行：

```shell
python export.py --weights weights/yolov5s.pt --include onnx --simplify --dynamic
```

以生成对应的onnx文件。

### 3.3 具体修改细节

在`models/yolo.py`文件中54行，我们需要修改`class Detect`的forward方法，以删除其box decode运算，以直接输出网络结果。在后面的tensorrt部署中，我们将利用decode plugin来进行decode操作，并用gpu加速。修改内容如下：

```python
-            bs, _, ny, nx = x[i].shape  # x(bs,255,20,20) to x(bs,3,20,20,85)
-            x[i] = x[i].view(bs, self.na, self.no, ny, nx).permute(0, 1, 3, 4, 2).contiguous()
-
-            if not self.training:  # inference
-                if self.onnx_dynamic or self.grid[i].shape[2:4] != x[i].shape[2:4]:
-                    self.grid[i], self.anchor_grid[i] = self._make_grid(nx, ny, i)
-
-                y = x[i].sigmoid()
-                if self.inplace:
-                    y[..., 0:2] = (y[..., 0:2] * 2 + self.grid[i]) * self.stride[i]  # xy
-                    y[..., 2:4] = (y[..., 2:4] * 2) ** 2 * self.anchor_grid[i]  # wh
-                else:  # for YOLOv5 on AWS Inferentia https://github.com/ultralytics/yolov5/pull/2953
-                    xy, wh, conf = y.split((2, 2, self.nc + 1), 4)  # y.tensor_split((2, 4, 5), 4)  # torch 1.8.0
-                    xy = (xy * 2 + self.grid[i]) * self.stride[i]  # xy
-                    wh = (wh * 2) ** 2 * self.anchor_grid[i]  # wh
-                    y = torch.cat((xy, wh, conf), 4)
-                z.append(y.view(bs, -1, self.no))
-
-        return x if self.training else (torch.cat(z, 1),) if self.export else (torch.cat(z, 1), x)
+            y = x[i].sigmoid()
+            z.append(y)
+        return z
```

可以看到这里删除了主要的运算部分，将模型输出直接作为list返回。修改后，onnx的输出将被修改为三个原始网络输出，我们需要在输出后添加decode plugin的算子。首先我们先导出onnx，再利用nvidia的graph surgeon来修改onnx。首先我们修改onnx export部分代码：

> GraphSurgeon 是nvidia提供的工具，可以方便的用于修改、添加或者删除onnx网络图中的节点，并生成新的onnx。参考链接：https://github.com/NVIDIA/TensorRT/tree/master/tools/onnx-graphsurgeon。

```python
torch.onnx.export(
        model,
        im,
        f,
        verbose=False,
        opset_version=opset,
        training=torch.onnx.TrainingMode.TRAINING if train else torch.onnx.TrainingMode.EVAL,
        do_constant_folding=not train,
        input_names=['images'],
        output_names=['p3', 'p4', 'p5'],
        dynamic_axes={
            'images': {
                0: 'batch',
                2: 'height',
                3: 'width'},  # shape(1,3,640,640)
            'p3': {
                0: 'batch',
                2: 'height',
                3: 'width'},  # shape(1,25200,4)
            'p4': {
                0: 'batch',
                2: 'height',
                3: 'width'},
            'p5': {
                0: 'batch',
                2: 'height',
                3: 'width'}
        } if dynamic else None)
```

将onnx的输出改为3个原始网络输出。输出完成后，我们再加载onnx，并simplify：

```python
model_onnx = onnx.load(f)
model_onnx = onnx.load(f)  # load onnx model
onnx.checker.check_model(model_onnx)  # check onnx model

# Simplify
if simplify:
    # try:
    check_requirements(('onnx-simplifier',))
    import onnxsim

    LOGGER.info(f'{prefix} simplifying with onnx-simplifier {onnxsim.__version__}...')
    model_onnx, check = onnxsim.simplify(model_onnx,
        dynamic_input_shape=dynamic,
        input_shapes={'images': list(im.shape)} if dynamic else None)
    assert check, 'assert check failed'
    onnx.save(model_onnx, f)
```

然后我们再将onnx加载回来，用nvidia surgeon进行修改:

```python
import onnx_graphsurgeon as onnx_gs
import numpy as np
yolo_graph = onnx_gs.import_onnx(model_onnx)
```

首先我们获取原始的onnx输出p3,p4,p5：

```python
p3 = yolo_graph.outputs[0]
p4 = yolo_graph.outputs[1]
p5 = yolo_graph.outputs[2]
```

然后我们定义新的onnx输出，由于decode plugin中，有4个输出，所以我们将定义4个新的输出。其名字需要和下面的代码保持一致，这是decode_plugin中预先定义好的。

```python
decode_out_0 = onnx_gs.Variable(
  "DecodeNumDetection",
  dtype=np.int32
)
decode_out_1 = onnx_gs.Variable(
  "DecodeDetectionBoxes",
  dtype=np.float32
)
decode_out_2 = onnx_gs.Variable(
  "DecodeDetectionScores",
  dtype=np.float32
)
decode_out_3 = onnx_gs.Variable(
  "DecodeDetectionClasses",
  dtype=np.int32
)
```

然后我们需要再添加一些decode参数，定义如下：

```python
decode_attrs = dict()

decode_attrs["max_stride"] = int(max(model.stride))
decode_attrs["num_classes"] = model.model[-1].nc
decode_attrs["anchors"] = [float(v) for v in [10,13, 16,30, 33,23, 30,61, 62,45, 59,119, 116,90, 156,198, 373,326]]
decode_attrs["prenms_score_threshold"] = 0.25
```

在定义好了相关参数后，我们创建一个onnx node，用作decode plugin。由于我们的tensorrt plugin的名称为`YoloLayer_TRT`,因此这里我们需要保持op的名字与我们的plugin名称一致。通过如下代码，我们创建了一个node：

```python
decode_plugin = onnx_gs.Node(
        op="YoloLayer_TRT",
        name="YoloLayer",
        inputs=[p3, p4, p5],
        outputs=[decode_out_0, decode_out_1, decode_out_2, decode_out_3],
        attrs=decode_attrs
    )
```

然后我们将这个node添加了网络中：

```python
yolo_graph.nodes.append(decode_plugin)
    yolo_graph.outputs = decode_plugin.outputs
    yolo_graph.cleanup().toposort()
    model_onnx = onnx_gs.export_onnx(yolo_graph)
```

最后添加一些meta信息后，我们导出最终的onnx文件，这个文件可以用于后续的tensorrt部署和推理。

```python
d = {'stride': int(max(model.stride)), 'names': model.names}
    for k, v in d.items():
        meta = model_onnx.metadata_props.add()
        meta.key, meta.value = k, str(v)

    onnx.save(model_onnx, f)
    LOGGER.info(f'{prefix} export success, saved as {f} ({file_size(f):.1f} MB)')
    return f
```

## 四、TensorRT部署

使用`TensorRT` docker容器：

```shell
docker run --gpus all -it --name env_trt -v $(pwd):/app nvcr.io/nvidia/tensorrt:22.08-py3
```

### 4.1 模型构建

> 代码位置：`1.代码/tensorrt_cpp/build.cu`

和我们之前课程中的TensorRT构建流程一样，yolov5转到onnx后，也是通过相同的流程进行模型构建，并保存序列化后的模型为文件。

1. **创建builder**。这里我们使用了`std::unique_ptr`只能指针包装我们的builder，实现自动管理指针生命周期。

```cpp
// =========== 1. 创建builder ===========
auto builder = std::unique_ptr<nvinfer1::IBuilder>(nvinfer1::createInferBuilder(sample::gLogger.getTRTLogger()));
if (!builder)
{
  std::cerr << "Failed to create builder" << std::endl;
  return -1;
}
```

1. **创建网络。**这里指定了explicitBatch

```cpp
// ========== 2. 创建network：builder--->network ==========
// 显性batch
const auto explicitBatch = 1U << static_cast<uint32_t>(nvinfer1::NetworkDefinitionCreationFlag::kEXPLICIT_BATCH);
// 调用builder的createNetworkV2方法创建network
auto network = std::unique_ptr<nvinfer1::INetworkDefinition>(builder->createNetworkV2(explicitBatch));
if (!network)
{
  std::cout << "Failed to create network" << std::endl;
  return -1;
}
```

1. **创建config。**用于模型构建的参数配置

```cpp
// ========== 3. 创建config配置：builder--->config ==========
auto config = std::unique_ptr<nvinfer1::IBuilderConfig>(builder->createBuilderConfig());
if (!config)
{
  std::cout << "Failed to create config" << std::endl;
  return -1;
}
```

1. **创建onnx 解析器，**并进行解析

```cpp
// 创建onnxparser，用于解析onnx文件
auto parser = std::unique_ptr<nvonnxparser::IParser>(nvonnxparser::createParser(*network, sample::gLogger.getTRTLogger()));
// 调用onnxparser的parseFromFile方法解析onnx文件
auto parsed = parser->parseFromFile(onnx_file_path, static_cast<int>(sample::gLogger.getReportableSeverity()));
if (!parsed)
{
  std::cout << "Failed to parse onnx file" << std::endl;
  return -1;
}
```

1. **配置网络构建参数。**这里由于我们导出onnx时并没有指定输入图像的batch，height，width。因此在构建时，我们需要告诉tensorrt我们最终运行时，输入图像的范围，batch size的范围。这样tensorrt才能对应为我们进行模型构建与优化。这里我们将输入指定到了1,3,640,640，这样tensorrt就会为这个尺寸的输入搜索最优算子并构建网络。其中设置pofile参数，即是我们用来指定输入大小搜索范围的。

```cpp
auto input = network->getInput(0);
auto profile = builder->createOptimizationProfile();
profile->setDimensions(input->getName(), nvinfer1::OptProfileSelector::kMIN, nvinfer1::Dims4{1, 3, 640, 640});
profile->setDimensions(input->getName(), nvinfer1::OptProfileSelector::kOPT, nvinfer1::Dims4{1, 3, 640, 640});
profile->setDimensions(input->getName(), nvinfer1::OptProfileSelector::kMAX, nvinfer1::Dims4{1, 3, 640, 640});
// 使用addOptimizationProfile方法添加profile，用于设置输入的动态尺寸
config->addOptimizationProfile(profile);

// 设置精度，不设置是FP32，设置为FP16，设置为INT8需要额外设置calibrator
config->setFlag(nvinfer1::BuilderFlag::kFP16);

builder->setMaxBatchSize(1);

// 设置最大工作空间（最新版本的TensorRT已经废弃了setWorkspaceSize）
config->setMemoryPoolLimit(nvinfer1::MemoryPoolType::kWORKSPACE, 1 << 30);

// 7. 创建流，用于设置profile
auto profileStream = samplesCommon::makeCudaStream();
if (!profileStream) { return -1; }
config->setProfileStream(*profileStream);
```

1. **将模型序列化**，并进行保存

```cpp
// ========== 4. 创建engine：builder--->engine(*nework, *config) ==========
// 使用buildSerializedNetwork方法创建engine，可直接返回序列化的engine（原来的buildEngineWithConfig方法已经废弃，需要先创建engine，再序列化）
auto plan = std::unique_ptr<nvinfer1::IHostMemory>(builder->buildSerializedNetwork(*network, *config));
if (!plan)
{
  std::cout << "Failed to create engine" << std::endl;
  return -1;
}
// ========== 5. 序列化保存engine ==========
std::ofstream engine_file("./model/yolov5.engine", std::ios::binary);
assert(engine_file.is_open() && "Failed to open engine file");
engine_file.write((char *)plan->data(), plan->size());
engine_file.close();
```

### 4.2 模型的推理

> 代码位置：`1.代码/tensorrt_cpp/build.cu`

如同之前的TensorRT课程介绍一样，推理过程将读取模型文件，并对输入进行预处理，然后读取模型输出后，再进行后处理。

1. **创建运行时**

```cpp
// ========= 1. 创建推理运行时runtime =========
auto runtime = std::unique_ptr<nvinfer1::IRuntime>(nvinfer1::createInferRuntime(sample::gLogger.getTRTLogger()));
if (!runtime)
{
  std::cout << "runtime create failed" << std::endl;
  return -1;
}
```

1. **反序列化**模型得到推理**Engine**

```cpp
// ======== 2. 反序列化生成engine =========
// 加载模型文件
auto plan = load_engine_file(engine_file);
// 反序列化生成engine
auto mEngine = std::shared_ptr<nvinfer1::ICudaEngine>(runtime->deserializeCudaEngine(plan.data(), plan.size()));
```

1. **创建执行上下文**

```cpp
// ======== 3. 创建执行上下文context =========
auto context = std::unique_ptr<nvinfer1::IExecutionContext>(mEngine->createExecutionContext());
```

1. **创建输入输出缓冲区管理器**，这里我们使用的是tensorrt sample code中的buffer管理器，以方便我们进行内存的分配和cpu gpu之间的内存拷贝。

```cpp
samplesCommon::BufferManager buffers(mEngine);
```

1. 我们读取视频文件，并逐帧读取图像，送入模型中，进行推理

```cpp
auto cap = cv::VideoCapture(input_video_path);

while(cap.isOpened()) {
  cv::Mat frame;
  cap >> frame;
  if (frame.empty()) break;
  ...
```

1. 首先对输入图像进行预处理，这里我们使用`preprocess.cu`中的代码，其中实现了对输入图像处理的gpu 加速（后续再进行讲解）。

```cpp
// 输入预处理
process_input(frame, (float *)buffers.getDeviceBuffer(kInputTensorName));
```

1. 预处理完成后，我们调用推理api `executeV2`，进行模型推理，并将模型输出拷贝到cpu

```cpp
context->executeV2(buffers.getDeviceBindings().data());
buffers.copyOutputToHost();
```

1. 最后我们从buffer manager中获取模型输出，并执行nms，得到最后的检测框

```cpp
// 获取模型输出
int32_t *num_det = (int32_t *)buffers.getHostBuffer(kOutNumDet); // 检测到的目标个数
int32_t *cls = (int32_t *)buffers.getHostBuffer(kOutDetCls);     // 检测到的目标类别
float *conf = (float *)buffers.getHostBuffer(kOutDetScores);     // 检测到的目标置信度
float *bbox = (float *)buffers.getHostBuffer(kOutDetBBoxes);     // 检测到的目标框
// 后处理
std::vector<Detection> bboxs;
yolo_nms(bboxs, num_det, cls, conf, bbox, kConfThresh, kNmsThresh);
```

1. 我们依次将检测框画到图像上，再打印对应的fps和推理时间。并显示图像

```cpp
// 结束时间
auto end = std::chrono::high_resolution_clock::now();
auto elapsed = std::chrono::duration_cast<std::chrono::milliseconds>(end - start).count();
auto time_str = std::to_string(elapsed) + "ms";
auto fps_str = std::to_string(1000 / elapsed) + "fps";

// 遍历检测结果
for (size_t j = 0; j < bboxs.size(); j++)
{
  cv::Rect r = get_rect(frame, bboxs[j].bbox);
  cv::rectangle(frame, r, cv::Scalar(0x27, 0xC1, 0x36), 2);
  cv::putText(frame, std::to_string((int)bboxs[j].class_id), cv::Point(r.x, r.y - 10), cv::FONT_HERSHEY_PLAIN, 1.2, cv::Scalar(0x27, 0xC1, 0x36), 2);
}
cv::putText(frame, time_str, cv::Point(50, 50), cv::FONT_HERSHEY_PLAIN, 1.2, cv::Scalar(0xFF, 0xFF, 0xFF), 2);
cv::putText(frame, fps_str, cv::Point(50, 100), cv::FONT_HERSHEY_PLAIN, 1.2, cv::Scalar(0xFF, 0xFF, 0xFF), 2);

cv::imshow("frame", frame);
```

### 4.3 INT8、FP16量化对比

> 首先需要确保你的GPU支持INT8计算（如jetson nano不支持INT8）

#### 4.3.1 简介

深度学习量化就是将深度学习模型中的参数（例如权重和偏置）从浮点数转换成整数或者定点数的过程。这样做可以减少模型的存储和计算成本，从而达到模型压缩和运算加速的目的。如int8量化，让原来模型中32bit存储的数字映射到8bit再计算（范围是[-128,127]）。

- 加快推理速度：访问一次32位浮点型可以访问4次int8整型数据；
- 减少存储空间和内存占用：在边缘设备（如嵌入式）上部署更实用。

当然，提升速度的同时，量化也会带来精度的损失，为了能尽可能减少量化过程中精度的损失，需要使用各种校准方法来降低信息的损失。TensorRT 中支持两种 INT8 校准算法：

- 熵校准 (Entropy Calibration)
- 最小最大值校准 (Min-Max Calibration)

> 熵校准是一种动态校准算法，它使用 KL 散度 (KL Divergence) 来度量推理数据和校准数据之间的分布差异。在熵校准中，校准数据是从实时推理数据中采集的，它将 INT8 精度量化参数看作概率分布，根据推理数据和校准数据的 KL 散度来更新量化参数。这种方法的优点是可以更好地反映实际推理数据的分布。
>
> 最小最大值校准使用最小最大值算法来计算量化参数。在最小最大值校准中，需要使用一组代表性的校准数据来生成量化参数，首先将推理中的数据进行统计，计算数据的最小值和最大值，然后根据这些值来计算量化参数。

这两种校准方法都需要准备一些数据用于在校准时执行推理，以统计数据的分布情况。**一般数据需要有代表性，即需要符合最终实际落地场景的数据。**实际应用中一般准备500-1000个数据用于量化。

#### 4.3.2 TensorRT中实现

在 TensorRT 中，可以通过实现 `IInt8EntropyCalibrator2` 接口或 `IInt8MinMaxCalibrator` 接口来执行熵校准或最小最大值校准，并且需要实现几个虚函数方法：

- `getBatch() `方法：用于提供一批校准数据；
- `readCalibrationCache()` 和 `writeCalibrationCache()` 方法：实现缓存机制，以避免在每次启动时重新加载校准数据。

课程附件中`build.cu`代码实现了 `IInt8MinMaxCalibrator` 接口，用于对 INT8 模型进行离线静态校准（你可以替换`IInt8EntropyCalibrator2`换成熵校准进行结果对比）。

```C++
// 定义校准数据读取器
// 如果要用entropy的话改为：IInt8EntropyCalibrator2
class CalibrationDataReader : public IInt8MinMaxCalibrator
{
  ....
}
```

- 在构造函数中，需要传递数据目录、数据列表和BatchSize等参数。数据目录是指包含校准数据的文件夹路径，数据列表是指校准数据文件的名称列表。构造函数还会初始化输入张量的维度和大小，以及在设备上分配内存。

```cpp
CalibrationDataReader(const std::string &dataDir, const std::string &list, int batchSize = 1)
        : mDataDir(dataDir), mCacheFileName("weights/calibration.cache"), mBatchSize(batchSize), mImgSize(kInputH * kInputW)
    {
        mInputDims = {1, 3, kInputH, kInputW}; // 设置网络输入尺寸
        mInputCount = mBatchSize * samplesCommon::volume(mInputDims);
        cuda_preprocess_init(mImgSize);
        cudaMalloc(&mDeviceBatchData, kInputH * kInputW * 3 * sizeof(float));
        // 加载校准数据集文件列表
        std::ifstream infile(list);
        std::string line;
        while (std::getline(infile, line))
        {
            sample::gLogInfo << line << std::endl;
            mFileNames.push_back(line);
        }
        mBatchCount = mFileNames.size() / mBatchSize;
        std::cout << "CalibrationDataReader: " << mFileNames.size() << " images, " << mBatchCount << " batches." << std::endl;
    }
```

- `getBatch()` 方法用于提供一批校准数据。在该方法中，需要将当前批次的校准数据读取到内存中，并将其复制到设备内存中。然后，将数据指针传递给 TensorRT 引擎，以供后续的校准计算使用。

```cpp
bool getBatch(void *bindings[], const char *names[], int nbBindings) noexcept override
    {
        if (mCurBatch + 1 > mBatchCount)
        {
            return false;
        }

        int offset = kInputW * kInputH * 3 * sizeof(float);
        for (int i = 0; i < mBatchSize; i++)
        {
            int idx = mCurBatch * mBatchSize + i;
            std::string fileName = mDataDir + "/" + mFileNames[idx];
            cv::Mat img = cv::imread(fileName);
            int new_img_size = img.cols * img.rows;
            if (new_img_size > mImgSize)
            {
                mImgSize = new_img_size;
                cuda_preprocess_destroy();      // 释放之前的内存
                cuda_preprocess_init(mImgSize); // 重新分配内存
            }
            process_input_gpu(img, mDeviceBatchData + i * offset);
        }
        for (int i = 0; i < nbBindings; i++)
        {
            if (!strcmp(names[i], kInputTensorName))
            {
                bindings[i] = mDeviceBatchData + i * offset;
            }
        }

        mCurBatch++;
        return true;
    }
```

- `readCalibrationCache()` 方法用于从缓存文件中读取校准缓存，返回一个指向缓存数据的指针，以及缓存数据的大小。如果没有缓存数据，则返回`nullptr`。

```cpp
const void* readCalibrationCache(std::size_t& length) noexcept override {
    // read from file
    mCalibrationCache.clear();

    std::ifstream input(mCacheFileName, std::ios::binary);
    input >> std::noskipws;

    if (input.good())
    {
        std::copy(std::istream_iterator<char>(input), std::istream_iterator<char>(),
                  std::back_inserter(mCalibrationCache));
    }

    length = mCalibrationCache.size();

    return length ? mCalibrationCache.data() : nullptr;
}
```

- `writeCalibrationCache()` 方法用于将校准缓存写入到缓存文件中。在该方法中，需要将缓存数据指针和缓存数据的大小传递给文件输出流，并将其写入到缓存文件中。

```cpp
void writeCalibrationCache(const void* cache, std::size_t length) noexcept override {
    // write tensorrt calibration cache to file
    std::ofstream output(mCacheFileName, std::ios::binary);
    output.write(reinterpret_cast<const char*>(cache), length);
}
```

在业务代码中，首先会检查当前平台是否支持 INT8 推理，如果不支持，则打印一条警告信息，并设置引擎为 `FP16` 模式。否则，创建一个 `CalibrationDataReader` 类型的对象 `calibrator`，并将其设置为 INT8 校准器，然后将 INT8 模式标志设置到配置对象 config 中。

```cpp
// 设置精度，不设置是FP32，设置为FP16，设置为INT8需要额外设置calibrator
if (!builder->platformHasFastInt8())
{
  sample::gLogInfo << "设备不支持int8." << std::endl;
  config->setFlag(nvinfer1::BuilderFlag::kFP16);
}
else
{
  // 设置calibrator量化校准器
  auto calibrator = new CalibrationDataReader(calib_dir, calib_list_file);
  config->setFlag(nvinfer1::BuilderFlag::kINT8);
  config->setInt8Calibrator(calibrator);
}
```

运行

```bash
# 进入media目录，在视频中随机挑选200帧画面作为校准图片
ffmpeg -i c3.mp4 sample%04d.png
ls *.png | shuf -n 200 > filelist.txt

# build后的参数分别是onnx未知、校准集目录（用于拼接完整图片路径）、文件列表路径
./build/build weights/yolov5s_person.onnx ./media/ ./media/filelist.txt
```

### 4.4 预处理和后处理

#### 4.4.1 预处理（Preprocess）

Yolov5图像预处理步骤主要如下：

1. **lettorbox**：即保持原图比例（图像直接resize到输入大小效果不好），将图片放在一个正方形的画布中，多余的部分用黑色填充。
2. **Normalization（归一化）**：将像素值缩放至`[0,1]`间；
3. **颜色通道顺序调整**：BGR2RGB
4. **NHWC 转为 NCHW**

**Letterbox** 示例：原图为：`960 x 540 `的图片，处理后变成`640 x 640`的正方形图片：

![image-20231015180635320](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015180635320.png)

我们可以使用`opencv`的`cv::warpAffine`函数，对图片进行仿射变换，来实现`letterbox`（在CPU上操作）：

> 参考代码`demo_test/letterbox.cpp`

```c++
// 对输入图片进行letterbox处理，即保持原图比例，将图片放在一个正方形的画布中，多余的部分用黑色填充
// 使用cv::warpAffine，将图片进行仿射变换，将图片放在画布中
// 这里使用inline关键字，表示该函数在编译时会被直接替换到调用处，不会生成函数调用，提高效率
inline cv::Mat letterbox(cv::Mat &src)
{
  float scale = std::min(kInputH / (float)src.rows, kInputW / (float)src.cols);

  int offsetx = (kInputW - src.cols * scale) / 2;
  int offsety = (kInputH - src.rows * scale) / 2;

  cv::Point2f srcTri[3]; // 计算原图的三个点：左上角、右上角、左下角
  srcTri[0] = cv::Point2f(0.f, 0.f);
  srcTri[1] = cv::Point2f(src.cols - 1.f, 0.f);
  srcTri[2] = cv::Point2f(0.f, src.rows - 1.f);
  cv::Point2f dstTri[3]; // 计算目标图的三个点：左上角、右上角、左下角
  dstTri[0] = cv::Point2f(offsetx, offsety);
  dstTri[1] = cv::Point2f(src.cols * scale - 1.f + offsetx, offsety);
  dstTri[2] = cv::Point2f(offsetx, src.rows * scale - 1.f + offsety);
  cv::Mat warp_mat = cv::getAffineTransform(srcTri, dstTri);       // 计算仿射变换矩阵
  cv::Mat warp_dst = cv::Mat::zeros(kInputH, kInputW, src.type()); // 创建目标图
  cv::warpAffine(src, warp_dst, warp_mat, warp_dst.size());        // 进行仿射变换
  return warp_dst;
}
```

为了对比`CUDA`加速效果，在`runtime.cu`中，使用参数`mode`可以选择不同的处理模式：

```c++
// 选择预处理方式
if (mode == 0)
{
  // 使用CPU做letterbox、归一化、BGR2RGB、NHWC to NCHW
  process_input_cpu(frame, (float *)buffers.getDeviceBuffer(kInputTensorName));
}
else if (mode == 1)
{
  // 使用CPU做letterbox，GPU做归一化、BGR2RGB、NHWC to NCHW
  process_input_cv_affine(frame, (float *)buffers.getDeviceBuffer(kInputTensorName));
}
else if (mode == 2)
{
  // 使用cuda预处理所有步骤
  process_input_gpu(frame, (float *)buffers.getDeviceBuffer(kInputTensorName));
}
```

##### 4.4.1.1 使用CPU做letterbox、归一化、BGR2RGB、NHWC to NCHW

```C++
// 使用CPU做letterbox、归一化、BGR2RGB、NHWC to NCHW
void process_input_cpu(cv::Mat &src, float *input_device_buffer)
{

  auto warp_dst = letterbox(src);                      // letterbox
  warp_dst.convertTo(warp_dst, CV_32FC3, 1.0 / 255.0); // normalization
  cv::cvtColor(warp_dst, warp_dst, cv::COLOR_BGR2RGB); // BGR2RGB
  // NHWC to NCHW：rgbrgbrgb to rrrgggbbb：
  std::vector<cv::Mat> warp_dst_nchw_channels;
  cv::split(warp_dst, warp_dst_nchw_channels); // 将输入图像分解成三个单通道图像：rrrrr、ggggg、bbbbb

  // 将每个单通道图像进行reshape操作，变为1x1xHxW的四维矩阵
  for (auto &img : warp_dst_nchw_channels)
  {
    // reshape参数分别是cn：通道数，rows：行数
    // 类似[[r,r,r,r,r]]或[[g,g,g,g,g]]或[[b,b,b,b,b]]，每个有width * height个元素
    img = img.reshape(1, 1);
  }
  // 将三个单通道图像拼接成一个三通道图像，即rrrrr、ggggg、bbbbb拼接成rrrgggbbb
  cv::Mat warp_dst_nchw;
  cv::hconcat(warp_dst_nchw_channels, warp_dst_nchw);
  // 将处理后的图片数据拷贝到GPU
  CUDA_CHECK(cudaMemcpy(input_device_buffer, warp_dst_nchw.ptr(), kInputH * kInputW * 3 * sizeof(float), cudaMemcpyHostToDevice));
}
```

##### 4.4.1.2 使用CPU做letterbox，GPU做归一化、BGR2RGB、NHWC to NCHW

```C++
// 使用CPU做letterbox，GPU做归一化、BGR2RGB、NHWC to NCHW
void process_input_cv_affine(cv::Mat &src, float *input_device_buffer)
{
  auto warp_dst = letterbox(src);
  cuda_pure_preprocess(warp_dst.ptr(), input_device_buffer, kInputW, kInputH);
}

// GPU做归一化、BGR2RGB、NHWC to NCHW
void cuda_pure_preprocess(
    uint8_t *src, float *dst, int dst_width, int dst_height)
{

  int img_size = dst_width * dst_height * 3;
  CUDA_CHECK(cudaMemcpy(img_buffer_device, src, img_size, cudaMemcpyHostToDevice));

  int jobs = dst_height * dst_width;
  int threads = 256;
  int blocks = ceil(jobs / (float)threads);

  preprocess_kernel<<<blocks, threads>>>(
      img_buffer_device, dst, dst_width, dst_height, jobs);
}
```

##### 4.4.1.3 使用GPU预处理所有步骤

```c++
// 使用cuda预处理所有步骤
void process_input_gpu(cv::Mat &src, float *input_device_buffer)
{
  cuda_preprocess(src.ptr(), src.cols, src.rows, input_device_buffer, kInputW, kInputH);
}
```

#### 4.4.2 后处理（Postprocess）

```C++
// 执行nms（非极大值抑制），得到最后的检测框
std::vector<Detection> bboxs;
yolo_nms(bboxs, num_det, cls, conf, bbox, kConfThresh, kNmsThresh);

// 遍历检测结果
for (size_t j = 0; j < bboxs.size(); j++)
{
  cv::Rect r = get_rect(frame, bboxs[j].bbox);
  cv::rectangle(frame, r, cv::Scalar(0x27, 0xC1, 0x36), 2);
  cv::putText(frame, std::to_string((int)bboxs[j].class_id), cv::Point(r.x, r.y - 10), cv::FONT_HERSHEY_PLAIN, 1.2, cv::Scalar(0x27, 0xC1, 0x36), 2);
}
```

### 4.5人员闯入、聚众的应用开发

#### 4.5.1 RTMP推流

> 代码位置：1.opencv_rtmp

为了将渲染后的画面传输出去，可以结合推流工具，步骤如下：

1. 启动`rtsp-simple-server`, 开启`RTMP服务器`
2. 使用`ffmpeg`将视频流推送到`RTMP服务器`中
3. 通过`vlc`等客户端读取`rtmp://127.0.0.1:1935/live/mystream` 即可获取显示视频流

> RTMP服务器：[rtsp-simple-server / MediaMTX](https://github.com/aler9/rtsp-simple-server) 是一个现成的、零依赖的服务器和代理，允许用户发布、读取和代理实时视频和音频流；
>
> `ffmpeg`推流工具：[opencv_ffmpeg_streaming](https://github.com/andreanobile/opencv_ffmpeg_streaming)。

如果在docker内运行，需要将端口映射出去：

```bash
# 映射端口并启动（注意主机端口不一样）
# 1935 是RTMP端口
# 8554 是RTSP端口
docker run --gpus all -it --name env_trt -p 1936:1935 -p 8556:8554 -v $(pwd):/app env_trt_img
# 为了能利用之前的容器（容器内部可能已经安装好了很多组件）

# 之前的启动命令（未映射端口）
docker run --gpus all -it --name env_trt -v $(pwd):/app nvcr.io/nvidia/tensorrt:22.08-py3
# 停止容器
docker stop env_trt
# 创建自定义镜像
docker commit env_trt env_trt_img
# 重新启动
```

可以将上节课代码做一些改动（`代码位置：2.yolo_trt_rtmp`），将`docker`容器内的数据推出来查看，为了演示真实IPC读取场景，我们让`rtsp-simple-server`也模拟了一个永不结束的`RTSP`视频流。

```bash
# 进入rtmp_server目录
cd rtmp_server
# 开启RTSP模拟IPC以及RTMP服务器
./start_server.sh
```

> 如果你使用的是AUTO DL等云服务，请确保对应端口开启或者使用VS Code的端口映射功能查看。



![image-20231015180657911](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015180657911.png)

#### 4.5.2 人员闯入应用开发

> 代码位置：`3.yolo_trt_app/task/border_cross.cpp`

![image-20231015180727445](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015180727445.png)

人员闯入的应用是利用判断一个点是否在多边形内来实现的，多边形和点的定义如下：

```cpp
// Point Struct Definitiono
struct Point {
    int x;
    int y;
};

// Polygon Struct Definition
struct Polygon {
    std::vector<Point> points;
};
```

在代码中实现了**射线法**（Ray Casting）算法，用于判断一个点是否在一个多边形内部。该算法的基本思路是从给定的点出发沿任意方向画一条射线，然后计算这条射线与多边形相交的次数。如果交点个数是奇数，则该点在多边形内部；否则，它在多边形外部。

函数 isInside 接受一个 Polygon 和一个 Point 作为输入，并返回一个布尔值，指示该点是否在多边形内部。函数首先检查多边形是否至少有三个顶点，因为不到三个顶点的图形不能被视为多边形。

然后，函数创建一个 extreme 点，它的 x 坐标非常大，y 坐标与给定点相同。这个点用于从给定点向右绘制一条水平射线。

然后，函数循环遍历多边形的所有边，检查每个边是否与射线相交。这是使用 doIntersect 函数完成的，该函数检查两条线段是否相交。如果找到一个交点，则函数使用 orientation 函数检查交点相对于边的方向。如果方向为零，则表示交点在边上。该函数然后使用 onSegment 函数检查交点是否在边上。如果交点在边上，则函数返回 true。

如果交点不在边上，则函数增加 count 变量的值。最后，如果 count 是奇数，则函数返回 true，表示该点在多边形内部；否则，它返回 false，表示该点在多边形外部。

**总之，给定的代码通过从给定点向右绘制一条水平射线，并计算它与多边形边的交点数来判断点是否在多边形内部。如果交点数是奇数，则该点在多边形内部；如果是偶数，它在多边形外部。**

```cpp
bool isInside(Polygon polygon, Point p) {
    int n = polygon.points.size();
    if (n < 3) {
        return false;
    }
    Point extreme = {10000, p.y};
    int count = 0, i = 0;
    do {
        int next = (i + 1) % n;
        if (doIntersect(polygon.points[i], polygon.points[next], p, extreme)) {
            if (orientation(polygon.points[i], p, polygon.points[next]) == 0) {
                return onSegment(polygon.points[i], p, polygon.points[next]);
            }
            count++;
        }
        i = next;
    } while (i != 0);
    return count % 2 == 1;
}
```

通过`isInside`函数我们可以判断一个点是否在多边形内，从而判断是否有人员闯入。

#### 4.5.3 人员聚众应用开发

> 代码位置：`3.yolo_trt_app/task/gather.cpp`

`gather.cpp` 中`gather`函数实现了**K-means聚类算法**，可以将一组点分为多个聚类。通过计算每个聚类中点的标准差，可以确定每个聚类中点之间是否聚集在一起。以下是函数如何使用来确定是否有人员聚集的步骤：

1. 首先，我们需要获取一组点的数据，这些点代表人员的位置。
2. 将这些点作为参数传递给 kMeans 函数，该函数需要指定聚类数 k 和最大迭代次数。
3. kMeans 函数将返回一组聚类，每个聚类都是一组点。
4. 将这些聚类作为参数传递给 isGather 函数，该函数需要指定一个阈值，该阈值表示允许的最大标准差。
5. isGather 函数将返回一组聚类，其中每个聚类都被认为是人员聚集的聚类。

调用 isGather 函数，将聚类数据和阈值作为参数传递。如果 gatherPoints 向量非空，则表示存在人员聚集。如果 gatherPoints 向量为空，则表示不存在人员聚集。

`gather_rule`功能是将给定的点集points按照一定的**距离阈值**threshold进行聚类，即将距离小于threshold的点归为一类。具体解释如下：

首先定义了一个阈值threshold和一个二维的vector容器gatherPoints，用于存储聚类后的点集。 然后对于points中的每个点进行遍历。 在遍历gatherPoints之前，需要先定义一个函数averagePoint，该函数用于计算一个点集的平均点。接下来对于gatherPoints中的每个点集pts，计算该点集的平均点与当前点的距离dist。 如果dist小于阈值threshold，则将当前点加入到该点集中。 如果dist大于等于阈值threshold，则将当前点作为一个新的点集加入到gatherPoints中。 最后返回聚类后的点集gatherPoints。 总体来说，这段代码通过遍历点集并计算点之间的距离，将距离小于阈值的点归为一类，得到了聚类后的点集。最后再通过点集的大小来判断是否属于人员聚集。目前有3人及以上聚集则当作人员聚集。

#### 4.5.4 多线程流水线

多线程知识参考附录：`5.3 多线程pipeline Demo`

当前我们程序的大致步骤可以分为：

1. 从文件或RTSP视频流读取画面帧
2. 输入数据的预处理
3. 推理inference
4. NMS后处理
5. 绘制画面，及人员闯入及聚众应用
6. 推流

其实`runtime.cu`中画面显示的FPS是根据`输入数据的预处理 -->推理-->NMS后处理 `（2、3、4）这三步的耗时，老师机器参考耗时输出如下：

```bash
# 参数：<engine_file> <input_path_path> <preprocess_mode> <dist_threshold> <stream> <bitrate>

# 720P 文件，开启推流
# ./build/runtime ./weights/yolov5.engine rtmp_server/c3_720.mp4  2 100 1 8000000
each step time(ms): 1.316,0.349,3.939,0.404,0.798,9.293
each step fps: 759.878,2865.33,253.872,2475.25,1253.13,107.608
method 1 all steps time(ms): 16.102, fps: 62.1041
method 2 all steps time(ms): 1003.58, fps: 60.7826,frame count: 61

# 720P 文件，关闭推流
# ./build/runtime ./weights/yolov5.engine rtmp_server/c3_720.mp4  2 100 0 8000000
each step time(ms): 1.376,0.283,3.365,0.336,0.604,0
each step fps: 726.744,3533.57,297.177,2976.19,1655.63,inf
method 1 all steps time(ms): 5.967, fps: 167.588
method 2 all steps time(ms): 1004.79, fps: 157.247,frame count: 158

# 1080P 文件，开启推流
#  ./build/runtime ./weights/yolov5.engine rtmp_server/c3_1080.mp4  2 100 1 8000000
each step time(ms): 2.976,0.667,3.945,0.413,0.916,15.577
each step fps: 336.021,1499.25,253.485,2421.31,1091.7,64.1972
method 1 all steps time(ms): 24.497, fps: 40.8213
method 2 all steps time(ms): 1014.25, fps: 40.4239,frame count: 41

# 1080P 文件，关闭推流
# ./build/runtime ./weights/yolov5.engine rtmp_server/c3_1080.mp4  2 100 0 8000000
each step time(ms): 2.921,0.614,3.366,0.396,0.891,0
each step fps: 342.349,1628.66,297.089,2525.25,1122.33,inf
method 1 all steps time(ms): 8.191, fps: 122.085
method 2 all steps time(ms): 1004.57, fps: 119.454,frame count: 120

# 1080p rstp视频流，开启推流
#  ./build/runtime ./weights/yolov5.engine rtsp  2 100 1 8000000
each step time(ms): 23.183,0.732,3.961,0.446,0.494,10.165
each step fps: 43.1351,1366.12,252.462,2242.15,2024.29,98.3768
method 1 all steps time(ms): 38.985, fps: 25.6509
method 2 all steps time(ms): 1002.46, fps: 24.9388,frame count: 25

# 1080p rstp视频流，关闭推流
#  ./build/runtime ./weights/yolov5.engine rtsp  2 100 0 8000000
each step time(ms): 30.315,1.508,4.181,1.561,2.567,0
each step fps: 32.987,663.13,239.177,640.615,389.56,inf
method 1 all steps time(ms): 40.138, fps: 24.914
method 2 all steps time(ms): 1013.76, fps: 24.6607,frame count: 25
```

> method 1 ：计算单张图片的总耗时
>
> method 2 : 计算超过 1s 一共处理了多少张图片 (计算平均帧率)

你可以调整各种参数，可以看到：

- 耗时最高的部分是：
  - 从文件或RTSP视频流读取画面帧（1）
  - 推理inference（3）
  - 推流（6）
- 分辨率越高耗时越高
- RTSP视频流的读流速度低于读取文件的方式（设备帧率限制），所以RTSP整体帧率基本上无法超过相机帧率
- 推流比特率也会影响整体速度
- 另外，如果画面目标较多，耗时也会增加

在`runtime_thread.cu`中，我们使用多线程流水线的方式来进行优化，一共分为四个线程：

1. `readFrame`：从文件或RTSP视频流读取画面帧（1）
2. `inference`：输入数据的预处理、推理inference、NMS后处理（2、3、4）
3. `postprocess`： 和 绘制画面，及人员闯入及聚众应用（5）
4. `streamer`：推流（6）

老师机器参考耗时输出如下：

```bash
# 1080P 文件，开启推流
#  ./build/runtime_thread ./weights/yolov5.engine rtmp_server/c3_1080.mp4  2 100 1 8000000
step1: 3.099ms, fps: 322.685
step2: 5.077ms, fps: 196.967
step3 time: 0.925ms, fps: 1081.08
step4 time: 14.309ms, fps: 69.8861
method 2 all steps time(ms): 1004.54, fps: 57.738,frame count: 58

# 1080p rstp视频流，开启推流
#  ./build/runtime_thread ./weights/yolov5.engine rtsp  2 100 1 8000000
step1: 39.843ms, fps: 25.0985
step2: 5.342ms, fps: 187.196
step3 time: 1.137ms, fps: 879.508
step4 time: 12.741ms, fps: 78.4868
method 2 all steps time(ms): 1038.47, fps: 25.0367,frame count: 26
```

可以看到：

- 读取文件方式，所有步骤的帧率由单线程的40多提高到57；
- 读取rtsp方式，所有步骤的帧率无明显变化（仍然受限于相机帧率）。

### 4.6 jetson nano 和 jetson xavier NX部署

#### 4.6.1 jetson nx

> 附件代码位置：`jetson代码/nx.zip`
>
> ! 代码相对于PC有微小改动

老师硬件环境参考信息（使用`jtop`得到）：

> 如要刷机，镜像归档参考：https://developer.nvidia.com/embedded/jetpack-archive

![img](https://enpei-md.oss-cn-hangzhou.aliyuncs.com/img20230311175736.png?x-oss-process=style/wp)

编译项目准备：

```bash
# 如果出现No CMAKE_CUDA_COMPILER could be found，修改一下环境变量：
export PATH=$PATH:/usr/local/cuda/bin
# 安装依赖包
sudo apt-get install libavutil-dev libavfilter-dev libavformat-dev libsdl2-dev libavcodec-dev libx264-dev libxvidcore-dev libvdpau-dev libva-dev libxcb-shm0-dev libwavpack-dev libvpx-dev libvorbis-dev libogg-dev libvidstab-dev libspeex-dev libopus-dev libopencore-amrnb-dev libopencore-amrwb-dev libmp3lame-dev libfreetype6-dev libfdk-aac-dev libass-dev libbz2-dev libsoxr-dev
```

**YOLOv5 S 模型**

- 单线程

```bash
# 参数：<engine_file> <input_path_path> <preprocess_mode> <dist_threshold> <stream> <bitrate>

# 720P 文件，开启推流
# ./build/runtime ./weights/yolov5s.engine rtmp_server/c3_720.mp4  2 100 1 2000000
method 2 all steps time(ms): 1027.08, fps: 15.5781,frame count: 16

# 720P 文件，关闭推流
# ./build/runtime ./weights/yolov5s.engine rtmp_server/c3_720.mp4  2 100 0 2000000
method 2 all steps time(ms): 1003.74, fps: 59.7762,frame count: 60

# 720P RTSP，开启推流
# ./build/runtime ./weights/yolov5s.engine rtsp  2 100 1 2000000
method 2 all steps time(ms): 1032.3, fps: 14.5307,frame count: 15

# 720P RTSP，关闭推流
# ./build/runtime ./weights/yolov5s.engine rtsp  2 100 0 2000000
method 2 all steps time(ms): 1034.82, fps: 25.1251,frame count: 26
```

- 多线程

```bash
# 参数：<engine_file> <input_path_path> <preprocess_mode> <dist_threshold> <stream> <bitrate>

# 720P 文件，开启推流
# ./build/runtime_thread ./weights/yolov5s.engine rtmp_server/c3_720.mp4  2 100 1 2000000
method 2 all steps time(ms): 1046.31, fps: 20.0705,frame count: 21

# 720P 文件，关闭推流
# ./build/runtime_thread ./weights/yolov5s.engine rtmp_server/c3_720.mp4  2 100 0 2000000
method 2 all steps time(ms): 1003.24, fps: 76.7516,frame count: 77

# 720P RTSP，开启推流
# ./build/runtime_thread ./weights/yolov5s.engine rtsp  2 100 1 2000000
method 2 all steps time(ms): 1005.82, fps: 19.8843,frame count: 20

# 720P RTSP，关闭推流
# ./build/runtime_thread ./weights/yolov5s.engine rtsp  2 100 0 2000000
method 2 all steps time(ms): 1005.57, fps: 24.8616,frame count: 25
```

**YOLOV5 N 模型**

- 单线程

```bash
# 参数：<engine_file> <input_path_path> <preprocess_mode> <dist_threshold> <stream> <bitrate>

# 720P 文件，开启推流
# ./build/runtime ./weights/yolov5n.engine rtmp_server/c3_720.mp4  2 100 1 2000000
method 2 all steps time(ms): 1029.93, fps: 16.5059,frame count: 17

# 720P 文件，关闭推流
# ./build/runtime ./weights/yolov5n.engine rtmp_server/c3_720.mp4  2 100 0 2000000
method 2 all steps time(ms): 1007.66, fps: 74.4296,frame count: 75

# 720P RTSP，开启推流
# ./build/runtime ./weights/yolov5n.engine rtsp  2 100 1 2000000
method 2 all steps time(ms): 1013.58, fps: 14.799,frame count: 15

# 720P RTSP，关闭推流
# ./build/runtime ./weights/yolov5n.engine rtsp  2 100 0 2000000
method 2 all steps time(ms): 1003.79, fps: 24.9057,frame count: 25
```

- 多线程

```bash
# 参数：<engine_file> <input_path_path> <preprocess_mode> <dist_threshold> <stream> <bitrate>

# 720P 文件，开启推流
# ./build/runtime_thread ./weights/yolov5n.engine rtmp_server/c3_720.mp4  2 100 1 2000000
method 2 all steps time(ms): 1046.23, fps: 19.1162,frame count: 20

# 720P 文件，关闭推流
# ./build/runtime_thread ./weights/yolov5n.engine rtmp_server/c3_720.mp4  2 100 0 2000000
method 2 all steps time(ms): 1003.65, fps: 94.655,frame count: 95

# 720P RTSP，开启推流
# ./build/runtime_thread ./weights/yolov5n.engine rtsp  2 100 1 2000000
method 2 all steps time(ms): 1029.55, fps: 18.4546,frame count: 19

# 720P RTSP，关闭推流
# ./build/runtime_thread ./weights/yolov5n.engine rtsp  2 100 0 2000000
method 2 all steps time(ms): 1005.57, fps: 24.8616,frame count: 25
```

#### 4.6.2 jetson nano

> 附件代码位置：附件代码位置：`jetson代码/nano.zip`
>
> ! 代码相对于PC有改动
>
> 主要修改点：NANO GPU 是Maxwell 架构（[参考这里](https://arnon.dk/matching-sm-architectures-arch-and-gencode-for-various-nvidia-cards/) ），修改了`CMakeLists.txt`；

老师硬件环境参考信息（使用`jtop`得到）：

![img](https://enpei-md.oss-cn-hangzhou.aliyuncs.com/img20230311202948.png?x-oss-process=style/wp)

**YOLOv5 S 模型**

- 单线程

```bash
# 参数：<engine_file> <input_path_path> <preprocess_mode> <dist_threshold> <stream> <bitrate>

# 720P 文件，开启推流
# ./build/runtime ./weights/yolov5s.engine rtmp_server/c3_720.mp4  2 100 1 2000000
method 2 all steps time(ms): 1115.41, fps: 7.17228,frame count: 8

# 720P 文件，关闭推流
# ./build/runtime ./weights/yolov5s.engine rtmp_server/c3_720.mp4  2 100 0 2000000
method 2 all steps time(ms): 1012.27, fps: 12.8424,frame count: 13

# 720P RTSP，开启推流
# ./build/runtime ./weights/yolov5s.engine rtsp  2 100 1 2000000
method 2 all steps time(ms): 1038.04, fps: 8.67019,frame count: 9

# 720P RTSP，关闭推流
# ./build/runtime ./weights/yolov5s.engine rtsp  2 100 0 2000000
method 2 all steps time(ms): 1061.26, fps: 13.1919,frame count: 14
```

- 多线程

```bash
# 参数：<engine_file> <input_path_path> <preprocess_mode> <dist_threshold> <stream> <bitrate>

# 720P 文件，开启推流
# ./build/runtime_thread ./weights/yolov5s.engine rtmp_server/c3_720.mp4  2 100 1 2000000
method 2 all steps time(ms): 1065.54, fps: 13.1389,frame count: 14

# 720P 文件，关闭推流
# ./build/runtime_thread ./weights/yolov5s.engine rtmp_server/c3_720.mp4  2 100 0 2000000
method 2 all steps time(ms): 1045.08, fps: 13.3961,frame count: 14

# 720P RTSP，开启推流
# ./build/runtime_thread ./weights/yolov5s.engine rtsp  2 100 1 2000000
method 2 all steps time(ms): 1007.5, fps: 13.8958,frame count: 14

# 720P RTSP，关闭推流
# ./build/runtime_thread ./weights/yolov5s.engine rtsp  2 100 0 2000000
method 2 all steps time(ms): 1011.88, fps: 13.8356,frame count: 14
```

**YOLOV5 N 模型**

- 单线程

```bash
# 参数：<engine_file> <input_path_path> <preprocess_mode> <dist_threshold> <stream> <bitrate>

# 720P 文件，开启推流
# ./build/runtime ./weights/yolov5n.engine rtmp_server/c3_720.mp4  2 100 1 2000000
method 2 all steps time(ms): 1059.62, fps: 9.43736,frame count: 10

# 720P 文件，关闭推流
# ./build/runtime ./weights/yolov5n.engine rtmp_server/c3_720.mp4  2 100 0 2000000
method 2 all steps time(ms): 1025.55, fps: 23.402,frame count: 24

# 720P RTSP，开启推流
# ./build/runtime ./weights/yolov5n.engine rtsp  2 100 1 2000000
method 2 all steps time(ms): 1044, fps: 11.4942,frame count: 12

# 720P RTSP，关闭推流
# ./build/runtime ./weights/yolov5n.engine rtsp  2 100 0 2000000
method 2 all steps time(ms): 1039.09, fps: 25.0219,frame count: 26
```

- 多线程

```bash
# 参数：<engine_file> <input_path_path> <preprocess_mode> <dist_threshold> <stream> <bitrate>

# 720P 文件，开启推流
# ./build/runtime_thread ./weights/yolov5n.engine rtmp_server/c3_720.mp4  2 100 1 2000000
method 2 all steps time(ms): 1038.55, fps: 14.4432,frame count: 15

# 720P 文件，关闭推流
# ./build/runtime_thread ./weights/yolov5n.engine rtmp_server/c3_720.mp4  2 100 0 2000000
method 2 all steps time(ms): 1023.37, fps: 26.3835,frame count: 27

# 720P RTSP，开启推流
# ./build/runtime_thread ./weights/yolov5n.engine rtsp  2 100 1 2000000
method 2 all steps time(ms): 1032.58, fps: 19.3689,frame count: 20

# 720P RTSP，关闭推流
# ./build/runtime_thread ./weights/yolov5n.engine rtsp  2 100 0 2000000
method 2 all steps time(ms): 1026.91, fps: 27.2662,frame count: 28
```

## 五、附录：

### 5.1 CUDA quickstart

#### 5.1.1 简介

CUDA是一种并行计算平台和编程模型，由NVIDIA推出，它可以利用GPU（图形处理器）进行高效的并行计算。使用CUDA编程可以提高计算密集型应用程序的性能，例如图像处理、科学计算、机器学习、深度学习等。相比于使用CPU进行串行计算，使用GPU并行计算可以大大提高计算速度和效率（如图像数据归一化，需要对每个像素值进行操作）。

CUDA编程的基本步骤可以概括为以下几个部分：

1. **定义kernel核函数**：首先需要定义一个kernel函数，用于在GPU上执行并行计算任务。使用`__global__`关键字来标记kernel函数，表示它将在GPU上执行。
2. **分配内存并初始化数据**：接下来需要在主机端分配内存，并初始化数据。然后，使用`cudaMalloc()`函数在GPU上分配相同大小的内存，并使用`cudaMemcpy()`函数将数据从主机端复制到GPU上。
3. **启动kernel函数**：使用`<<<...>>>`语法启动kernel函数，将线程块的数量和大小作为参数传递给kernel函数。线程块的数量和大小通常需要根据计算任务的特点进行调整，以最大化利用GPU的计算能力。
4. **将结果从GPU上复制回主机端**：执行kernel函数后，需要使用`cudaMemcpy()`函数将结果从GPU上复制回主机端。这样我们就可以在主机端访问并处理这些数据了。
5. **释放内存**：最后需要使用`cudaFree()`函数释放在GPU上分配的内存，并使用标准的C或C++语言函数释放在主机端分配的内存。

#### 5.1.2 线程块 block、线程thread

在CUDA编程中，一个CUDA Kernel 是由众多的线程（threads）组成的，这些线程可以被组织成一个或多个block（块），而这些block又可以被组织成一个或多个grid（网格），如下图：

![image-20231015180755532](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015180755532.png)

- **Thread**：线程是CUDA中最基本的执行单元，每个线程都执行相同的操作，但操作的数据不同。
- **BLock**：线程块是线程的集合，所有线程共享同一线程块的共享内存，并且可以通过线程块内同步方式进行通信。
- **Grid**：网格是线程块的集合，网格中的所有线程块可以同时执行，每个线程块的线程都相互独立，块之间不能直接通信。

一个grid可以包含多个block，block可以是一维、二维或三维的，block中的thread也可以是一维、二维或三维的。每个线程都有一个唯一的线程ID，可以用来访问不同的数据和内存位置。在同一个线程块中，线程ID是从0开始连续编号的，可以通过内置变量 `threadIdx` 来获取：

```C++
// 获取本线程的索引，blockIdx 指的是线程块的索引，blockDim 指的是线程块的大小，threadIdx 指的是本线程块中的线程索引
int tid = blockIdx.x * blockDim.x + threadIdx.x;
```

在CUDA编程中，block和thread的数量和大小通常需要根据计算任务的特点进行调整，以最大化利用GPU的计算能力。例如，对于大规模的并行计算任务，可以使用更多的线程和线程块来充分利用GPU的并行处理能力。而对于计算量较小的任务，使用更少的线程和线程块可能会更高效。

```C++
// 计算需要的线程总量（高度 x 宽度）:640*640=409600
int jobs = dst_height * dst_width;
// 一个线程块包含256个线程
int threads = 256;
// 计算线程块的数量
int blocks = ceil(jobs / (float)threads);

// 调用kernel函数
preprocess_kernel<<<blocks, threads>>>(
  img_buffer_device, dst, dst_width, dst_height, jobs); // 函数的参数
```

#### 5.1.3 kernel 函数

在CUDA编程中，kernel函数是在GPU上执行的函数，用于实现并行计算任务。当启动kernel函数时，GPU上的每个线程都会执行相同的程序代码，从而实现高效的并行计算。

在CUDA中，我们可以使用`__global__`关键字来标记一个函数，使之成为kernel函数。`__global__`关键字告诉编译器这个函数将在GPU上执行，而不是在CPU上执行。除此之外，kernel函数和普通的函数并没有太大区别，可以有输入参数和输出参数，可以有本地变量和控制流程语句，甚至可以调用其他函数。

在kernel函数中，我们可以使用一些内置的变量和函数来获取当前线程的信息，例如`threadIdx、blockIdx、blockDim`等。这些变量和函数可以帮助我们确定当前线程的位置和执行流程，从而更好地调度并行计算任务的执行。

启动kernel函数需要使用`<<<...>>>`语法。`<<<...>>>`中第一个参数一般是一个整数，用于指定线程块的数量。第二个参数是一个整数或一个`dim3`类型，用于指定每个线程块中的线程数量。`dim3`类型是一个三维向量，可以分别指定每个线程块中`x、y、z`方向的线程数量。如果只指定了一个整数，那么默认使用这个整数作为x方向的线程数量，而y和z方向的线程数量默认为1。

```C++
// 向量加法
__global__ void add(int *a, int *b, int *c, int N)
{   
    // 获取本线程块的索引，blockIdx 指的是线程块的索引，blockDim 指的是线程块的大小，threadIdx 指的是线程的索引
    int tid = blockIdx.x * blockDim.x + threadIdx.x;  
    if (tid < N)
        c[tid] = a[tid] + b[tid];
}
// 调用kernel函数
add<<<n_blocks, n_threads>>>(dev_a, dev_b, dev_c, N);
```

#### 5.1.4 代码解释

`simple.cu`演示了如何使用CUDA在GPU上进行向量加法，并比较使用CPU和GPU的时间。

### 5.2 TensorRT plugin

> TensorRT插件的编写涉及CUDA、网络操作细节知识较多，本节是YOLOV5 decode的样例，仅作参考。
>
> 在实现插件时，需要根据插件的具体功能来设计相应的计算逻辑，更多介绍请参考：https://docs.nvidia.com/deeplearning/tensorrt/developer-guide/index.html#extending

#### 5.2.1 Yolov5 decode流程

将YOLOv5 COCO预训练模型（80个类别）导出ONNX，可查看到3个head（shape分别是`[255,80,80], [255,40,40], [255,20,20]`），经过decode后变成最终的输出output （`[25200,85]`），再经过NMS就可以得到最终的检测框。

![image-20231015180846829](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015180846829.png)

**decode、后处理的大致流程：**

- 输入图片推理得到3个head的特征图

![image-20231015180904594](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015180904594.png)

将每个head 变形，下图是其中`[255,80,80]` 这个head的变形

- 因为有3种anchor，`[255,80,80]`可以转换为3个`[85,80,80]`的Tensor，即`[3,85,80,80]`

- 取出其中一个Tensor的一个cell，即一个网格的预测结果，大小为

  ```
  [85,1,1]
  ```

  - 其中1,1表示网格的横纵坐标位置
  - 85表示：`(tx,ty,tw,th,score, [0,0,1,...,0,0,0] )`即检测框的`xywh`和`score`，80个类别独热编码的`classes`
  - decode的核心流程就是根据`tx,ty,tw,th`计算`bx,by,bw,bh`

![image-20231015180928322](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015180928322.png)

计算`bx,by,bw,bh`

![image-20231015180950630](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015180950630.png)

- > bx, by取值范围 (-0.5,1.5) 负责一个网格一定范围内中心点的预测
  >
  > bw,bh取值范围(0,4) ，即是anchor宽度高度调节范围的0~4倍

- 最后三个特征图，每个特征图3种anchor，转换下来：

  - `[255,80,80]` --> `[3,80,80,85]` --> `[19200,85]`
  - `[255,40,40]` --> `[3,40,40,85]` --> `[4800,85]`
  - `[255,20,20]` --> `[3,20,20,85]` --> `[1200,85]`
  - 最终组合到一起，最终的输出为`[25200,85]` ，85中80是类别数量

- NMS筛选最终的检测框

#### 5.2.2 plugin基本流程介绍

在我们之前的介绍中提到，我们使用了`YoloLayer_TRT`插件，其功能是`decode onnx`模型的输出，这里的`decode`算子用GPU实现并加速了，以提高模型吞吐量。

> 参考：3.3 具体修改细节

![image-20231015181014779](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015181014779.png)

实现TensorRT Plugin需要实现插件类，和插件工厂类，并对插件进行注册。步骤如下：

1. 定义插件版本和插件名:

   > 位置：`yoloPlugins.h` 第51行

```cpp
// 定义插件版本和插件名
namespace
{
    const char *YOLOLAYER_PLUGIN_VERSION{"1"};
    const char *YOLOLAYER_PLUGIN_NAME{"YoloLayer_TRT"};
} // namespace
```

1. 实现插件类

   > 位置：`yoloPlugins.h` 第58行

   插件类需要继承`IPluginV2DynamicExt`类。这份代码中定义的插件类名是`YoloLayer`，其中实现了`IPluginV2DynamicExt`中的虚函数和一些成员变量和函数。

```cpp
class YoloLayer : public nvinfer1::IPluginV2DynamicExt
{
public:
    .....
private:
    ......
};
```

1. 实现插件创建类

   > 位置：`yoloPlugins.h` 第112行

   插件创建类需要继承`IPluginCreator`类，并实现其中的虚函数。这份代码中定义的插件创建类名是`YoloLayerPluginCreator`，其中实现了`IPluginCreator`中的虚函数和一些成员变量和函数。

```cpp
class YoloLayerPluginCreator : public nvinfer1::IPluginCreator
{
public:
    ......

private:
    ......
};
```

上述代码定义在头文件`yoloPlugins.h`中，具体的函数实现放在了`yoloPlugins.cpp`文件中，同时核心的计算部分由cuda进行实现，放在了`yoloForward_nc.cu`中。

1. 注册插件

   > 位置：`yoloPlugins.cpp` 第341行

   在实现了各个类方法后，需要调用宏对plugin进行注册。以方便TensorRT识别并找到对应的Plugin。

```cpp
REGISTER_TENSORRT_PLUGIN(YoloLayerPluginCreator);
```

1. 编译插件库并使用

```cmake
add_library(yolo_plugin SHARED
    plugins/yoloPlugins.cpp
    plugins/yoloForward_nc.cu
)
add_executable(build
    build.cu
    ${TensorRT_SAMPLE_DIR}/common/logger.cpp
    ${TensorRT_SAMPLE_DIR}/common/sampleUtils.cpp
)
# 这里需要注意加上-Wl,--no-as-needed，否则可能连接失败
target_link_libraries(build PRIVATE -Wl,--no-as-needed yolo_plugin) # -Wl,--no-as-needed is needed to avoid linking errors
```

#### 5.2.3 Plugin中需要实现的方法介绍

核心需要实现的方法有`configurePlugin`, `enqueue`, 还有用于序列化和反序列的方法。

1. `configurePugin`用于配置相关参数的信息：

```cpp
void YoloLayer::configurePlugin(
    const nvinfer1::DynamicPluginTensorDesc *in, int nbInputs, const nvinfer1::DynamicPluginTensorDesc *out, int nbOutputs) noexcept
{
  ......
}
```

1. `enqueue`方法则是进行模型推理，需要调用对应的推理代码。

```C++
int YoloLayer::enqueue(const nvinfer1::PluginTensorDesc *inputDesc, const nvinfer1::PluginTensorDesc *outputDesc, const void *const *inputs,
                       void *const *outputs, void *workspace, cudaStream_t stream) noexcept
{
	  .......
    return 0;
}
```

1. 另外一个比较重要的是序列化，序列化需要把plugin的参数存入序列化数据中，如下代码所示：

```cpp
void YoloLayer::serialize(void* buffer) const noexcept
{
    char *d = static_cast<char*>(buffer);

    write(d, m_NetWidth);
    write(d, m_NetHeight);
    write(d, m_MaxStride);
    write(d, m_NumClasses);
    write(d, m_ScoreThreshold);
    write(d, m_OutputSize);

    // write anchors:
    for (int i = 0; i < m_Anchors.size(); i++){
        write(d, m_Anchors[i]);
    }

    // write feature size:
    uint yoloTensorsSize = m_FeatureSpatialSize.size();
    for (uint i = 0; i < yoloTensorsSize; ++i)
    {
        write(d, m_FeatureSpatialSize[i].h());
        write(d, m_FeatureSpatialSize[i].w());
    }
}
```

其中write函数把plugin的参数写到对应的内存位置，在后续将模型序列化存入磁盘时，这些数据也会被存入模型文件中。在反序列化的过程中，模型序列化数据又会被解析出来用于创建plugin。如下：

```cpp
YoloLayer::YoloLayer (const void* data, size_t length)
{
    const char *d = static_cast<const char*>(data);

    read(d, m_NetWidth);
    read(d, m_NetHeight);
    read(d, m_MaxStride);
    read(d, m_NumClasses);
    read(d, m_ScoreThreshold);
    read(d, m_OutputSize);

    m_Anchors.resize(NFEATURES * NANCHORS * 2);
    for(uint i = 0; i < m_Anchors.size(); i++){
        read(d, m_Anchors[i]);
    }

    for(uint i = 0; i < NFEATURES; i++){
        int height;
        int width;
        read(d, height);
        read(d, width);
        m_FeatureSpatialSize.push_back(nvinfer1::DimsHW(height, width));
    }
};
```

在上面的构造函数中实现了从序列化数据中读取参数的功能，以构造plugin。Plugin需要实现的核心函数包括：

- `getOutputDimensions()`：计算并返回插件的输出张量的尺寸。
- `enqueue()`：执行插件的前向传播计算。
- `configurePlugin()`：设置插件的参数和输入/输出张量的数据类型等信息。
- `getSerializationSize()`和`serialize()`：用于插件的序列化。
- ` deserialize()`：用于插件的反序列化。

在实现插件时，需要根据插件的具体功能来设计相应的计算逻辑，并在`enqueue()`函数中实现。同时，还需要根据插件的输入/输出张量的数据类型等信息来设置插件的参数，在`configurePlugin()`函数中实现。最后,通过宏注册`plugin`，并和主程序一起编译即可。

```C++
// 注册插件。 在实现了各个类方法后，需要调用宏对plugin进行注册。以方便TensorRT识别并找到对应的Plugin。
REGISTER_TENSORRT_PLUGIN(YoloLayerPluginCreator);
```

### 5.3 多线程pipeline Demo

> 附件位置：`4.thread_pipeline `

示例代码实现了一个生产者-消费者模型，使用队列作为共享资源来存储生产者生产的数据，消费者从队列中取出数据进行消费。在这个模型中，生产者和消费者是两个不同的线程，共享同一个队列。

- 定义了一个全局变量 buffer 代表队列，大小为 `buffer_size`，设置为 10。
- 使用互斥锁 `buffer_mutex` 来保护对队列的访问，以确保生产者和消费者不能同时访问队列。
- `not_full` 和 `not_empty` 是条件变量，用于在队列满时阻塞生产者线程，在队列为空时阻塞消费者线程。
- 生产者线程的函数是 `produce()`，它将数字 1 到 20 添加到队列中。生产者线程首先尝试获取互斥锁，然后在条件变量 `not_full` 上等待，直到队列不再满。一旦队列未满，生产者线程将数字添加到队列中，并发送信号给条件变量 `not_empty`，通知消费者线程队列中已有数据可以消费。
- 消费者线程的函数是 `consume()`，它从队列中取出数字并进行消费。消费者线程也首先尝试获取互斥锁，然后在条件变量 `not_empty` 上等待，直到队列中有数据可供消费。一旦有数据可供消费，消费者线程将数字从队列中删除，并发送信号给条件变量 `not_full`，通知生产者线程队列中已有空间可以继续生产数据。
- 在主函数 main() 中，我们创建了两个线程，一个用于生产者函数 `producer()`，另一个用于消费者函数 `consumer()`。然后我们等待两个线程执行完毕，使用 `join()` 函数来等待线程完成执行。

这段代码演示了如何使用互斥锁和条件变量实现生产者-消费者模型，实现了线程之间的同步，以确保生产者和消费者在访问共享资源时不会发生竞争条件问题。

使用`g++ main.cpp -std=c++14 -pthread`编译代码，并执行`./a.out`执行代码查看运行结果。

# 六 项目二 车人流量统计

## 一、Deepstream

### 1.1 简介

> https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_Overview.html

DeepStream是一个基于NVIDIA GPU和TensorRT的开源视频分析框架。它提供了一个端到端的、可扩展的平台，可以处理多个视频和图像流，并支持实时的人脸识别、车辆识别、物体检测和跟踪、行为分析等视觉分析任务。DeepStream可以通过在不同的节点上进行分布式部署来实现高吞吐量和低延迟的处理，从而满足各种应用场景的需求，如智能城市、智能交通、工业自动化等。

简单来说，就是一个开发套件，让我们可以更快地开发视觉AI相关的应用，本节课使用它主要考虑两点：

- Deepstream稳定高效的读流和推流能力；
- Deepstream内置的目标追踪算法（deepsort等）

特性：

- 支持输入：USB/CSI 摄像头, 文件, RTSP流
- 示例代码：
  - C++: https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_C_Sample_Apps.html
  - python: https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_Python_Sample_Apps.html
- 硬件加速插件：VIC, GPU, DLA, NVDEC, and NVENC
- 使用软件SDK： CUDA, TensorRT, NVIDIA® Triton™ （Deepstream将它们抽象为插件）
- 支持平台：Jetson , 各种 GPU, [container](https://catalog.ngc.nvidia.com/orgs/nvidia/containers/deepstream)

### 1.2 图架构（Graph architecture）

> 图示：
>
> - 典型的视频分析应用：都是从读取视频开始，从视频中抽取有价值信息，最后输出
> - 上半部分：用到的所有插件
> - 下半部分：整个App链路中用到的硬件引擎

图架构：

- Deepstream基于开源 [GStreamer](https://enpeicv.com/) 框架开发；
- 优化了内存管理：pipeline上插件之间没有内存拷贝，并且使用了各种加速器来保证最高性能；

插件（plugins）：

- input→ decode: [Gst-nvvideo4linux2](https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_plugin_gst-nvvideo4linux2.html)
- preprocessing:
  - [Gst-nvdewarper](https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_plugin_gst-nvdewarper.html): 对鱼眼或360度相机的图像进行反扭曲
  - [Gst-nvvideoconvert](https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_plugin_gst-nvvideoconvert.html): 颜色格式的调整
  - [Gst-nvstreammux](https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_plugin_gst-nvstreammux.html): 多路复用器，从多个输入源形成一批缓冲区（帧）
  - inference:
    - [Gst-nvinfer](https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_plugin_gst-nvinfer.html): TensorRT
    - [Gst-nvinferserver](https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_plugin_gst-nvinferserver.html): Triton inference server: native frameworks such as TensorFlow or PyTorch
  - [Gst-nvtracker](https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_plugin_gst-nvtracker.html): 目标追踪
  - [Gst-nvdsosd](https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_plugin_gst-nvdsosd.html): 可视化：bounding boxes, segment masks, labels
- output:
  - 格式： 窗口显示，保存到文件，流通过RTSP，发送元数据到云
  - [Gst-nvmsgconv](https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_plugin_gst-nvmsgconv.html) ：将元数据metadata转换为数据结构
  - [Gst-nvmsgbroker](https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_plugin_gst-nvmsgbroker.html)：向服务器发送遥测数据(如Kafka, MQTT, AMQP和Azure IoT)

### 1.3 应用架构（Application Architecture）

> https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_ref_app_deepstream.html#reference-application-configuration
>
> ![image-20231015181421263](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015181421263.png)

- 包含了一系列的`GStreamer`插件

- 英伟达开发的插件有：

  - Gst-nvstreammux: 从多个输入源形成一批缓冲区（帧）

  - Gst-nvdspreprocess: 对预先定义的roi进行预处理，进行初步推理

  - Gst-nvinfer: TensorRT推理引擎（可用来检测和分类、分割）

  - Gst-nvtracker: 使用唯一ID来跟踪目标物体

  - Gst-nvmultistreamtiler: 拼接多个输入视频源显示

  - Gst-nvdsosd: 使用生成的元数据在合成视频帧上绘制检测框、矩形和文本等

  - Gst-nvmsgconv, Gst-nvmsgbroker: 将分析数据发送到云服务器。

  - ## 二、配置文件方式运行Deepstream

    ### 2.1 环境准备

    > https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_Quickstart.html#dgpu-setup-for-ubuntu

    ```bash
    # 对着官网将依赖准备装好：包括卸载老版本、装依赖包、安装好驱动、CUDA、TensorRT、librdkafka
    
    # 使用Debian package 安装，下载地址：https://developer.nvidia.com/downloads/deepstream-62-620-1-amd64-deb
    # 或者使用附件：3.PC/deepstream-6.2_6.2.0-1_amd64.deb
    
    $ sudo apt-get install ./deepstream-6.2_6.2.0-1_amd64.deb
    ```

    ### 2.2 主机运行

    > 代码位置：3.PC/代码

    - 生成engine文件：

      - 之前课程训练的是只有`person`这一类的模型，现在需要加上`car`车辆类别，我们使用`coco`预训练模型即可（共80类，附件位置：`1.预训练模型`）

      - 比如使用`yolov5s.pt`，需要按照之前课程流程处理：修改网络结构 --> 导出onnx文件 --> build engine （注意量化需要提供校准集）

        ```bash
        # 进入目录
        cd 3.yolo_trt_app
        
        # 构建
        # build engine
        # 用法: ./build [onnx_file_path] [use_int8] [calib_dir] [calib_list_file]
        
        # 比如我不开启INT8量化构建
        ./build/build weights/yolov5s.onnx 0 null null
        ```

    - 运行

      ```bash
      # 进入目录
      cd 1.deep_stream
      
      # 编译plugin library
      /usr/local/cuda/bin/nvcc -Xcompiler -fPIC -shared -o lib/yolov5_decode.so ./src/yoloForward_nc.cu ./src/yoloPlugins.cpp ./src/nvdsparsebbox_Yolo.cpp -isystem /usr/include/x86_64-linux-gnu/ -L /usr/lib/x86_64-linux-gnu/ -I /opt/nvidia/deepstream/deepstream/sources/includes -lnvinfer 
      
      # 把类别标签文件labels.txt放到config下
      
      # 将build好的yolov5 engine 文件放到weights下
      # 修改配置文件config_infer_primary_yoloV5.txt中engine的路径
      
      # 修改配置文件deepstream_app_config_windows_display_write.txt 中读取视频的地址，以及保存视频的地址
      
      # 读取文件 --> 检测 --> 窗口显示、保存文件、推流（注意看老师演示）
      deepstream-app -c config/deepstream_app_config_windows_display_write.txt
      
      # `rtsp`推流的链接为`rtsp://127.0.0.1:8554/ds-test`。可以通过vlc捕获并查看
      ```

    ### 2.3 配置文件解析

    > 参考链接：https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_ref_app_deepstream.html

    ```bash
    # deepstream_app_config_windows_display_write.txt
    
    [application]
    enable-perf-measurement=1
    perf-measurement-interval-sec=1
    
    [tiled-display]
    enable=0
    rows=1
    columns=1
    width=1280
    height=720
    gpu-id=0
    nvbuf-memory-type=0
    
    [source0]
    enable=1
    type=3
    uri=file:///home/enpei/Documents/course_cpp_tensorrt/course_10/1.deep_stream/media/sample_720p.mp4
    num-sources=1
    gpu-id=0
    cudadec-memtype=0
    
    
    
    [sink0]
    enable=1
    type=4
    sync=0
    gpu-id=0
    codec=1
    bitrate=5000000
    rtsp-port=8554
    udp-port=5400
    nvbuf-memory-type=0
    
    
    [sink1]
    enable=1
    type=2
    sync=0
    gpu-id=0
    codec=1
    width=1280
    height=720
    nvbuf-memory-type=0
    
    [sink2]
    enable=1
    type=3
    sync=1
    gpu-id=0
    codec=1
    container=1
    bitrate=5000000
    output-file=/home/enpei/Documents/course_cpp_tensorrt/course_10/1.deep_stream/media/output.mp4
    nvbuf-memory-type=0
    
    [osd]
    enable=1
    gpu-id=0
    border-width=5
    border-color=0;1;0;1
    text-size=30
    text-color=1;1;1;1;
    text-bg-color=0.3;0.3;0.3;1
    font=Serif
    show-clock=0
    clock-x-offset=800
    clock-y-offset=820
    clock-text-size=12
    clock-color=1;0;0;0
    nvbuf-memory-type=0
    
    [streammux]
    gpu-id=0
    live-source=0
    batch-size=1
    batched-push-timeout=40000
    width=1920
    height=1080
    enable-padding=0
    nvbuf-memory-type=0
    
    [primary-gie]
    enable=1
    gpu-id=0
    gie-unique-id=1
    nvbuf-memory-type=0
    config-file=config_infer_primary_yoloV5.txt
    
    [tests]
    file-loop=1
    ```

    以上配置文件解释如下：

- **[application]**

  - `enable-perf-measurement=1`：启用性能测量。
  - `perf-measurement-interval-sec=5`：性能测量间隔。

- **[tiled-display]**

  > 多个输入源显示在同一个窗口中

  - `enable=0`：是否启用Tiled Display。
  - `rows=1`：Tiled Display中的行数。
  - `columns=1`：Tiled Display中的列数。
  - `width=1280`：Tiled Display中每个小窗口的宽度。
  - `height=720`：Tiled Display中每个小窗口的高度。
  - `gpu-id=0`：Tiled Display所在的GPU ID。
  - `nvbuf-memory-type=0`：NvBufSurface的内存类型。

- **源属性 source**

  > Deepstream支持输入多个输入源，对于每个源需要单独命名为`source%d`，并且添加相应配置信息，类似：

  ```
  [source0]
  key1=value1
  key2=value2
  ...
  
  [source1]
  key1=value1
  key2=value2
  ...
  ```

  - `enable=1`：是否启用源。

  - `type=3`：源类型，
    - 1: Camera (V4L2)
    - 2: URI（统一资源标识符）
    - 3: MultiURI
    - 4: RTSP
    - 5: Camera (CSI) (Jetson only)
  - `uri`：媒体文件的URI，可以是文件（`file:///app/2.ds_tracker/media/sample_720p.mp4`），也可以是`http, RTSP `流。
  - `num-sources=1`：源数量。
  - `gpu-id=0`：源所在的GPU ID。
  - `cudadec-memtype=0`：解码器使用的内存类型。

- **sink**

  > sink组件用于控制显示的渲染、编码、文件存储，pipeline可以支持多个sink，命名为`[sink0],[sink1]...`

  - `enable=1`：是否启用。

  - `type=4`：类型，4表示RTSP流，更多类型如下：
    - 1: Fakesink
    - 2: EGL based windowed nveglglessink for dGPU and nv3dsink for Jetson （窗口显示）
    - 3: Encode + File Save (encoder + muxer + filesink) （文件）
    - 4: Encode + RTSP streaming; Note: sync=1 for this type is not applicable; （推流）
    - 5: nvdrmvideosink (Jetson only)
    - 6: Message converter + Message broker
  - `sync=0`：流渲染速度，0: As fast as possible 1: Synchronously
  - `gpu-id=0`：汇所在的GPU ID。
  - `codec=1`：编码器类型，1: H.264 (hardware)，2: H.265 (hardware)
  - `bitrate=5000000`：比特率。
  - `rtsp-port=8554`：RTSP端口号。
  - `udp-port=5400`：UDP端口号。
  - `nvbuf-memory-type=0`：NvBufSurface的内存类型。

- **osd**

  > 启用On-Screen Display (OSD) 屏幕绘制

  - `enable=1`：是否启用OSD。
  - `gpu-id=0`：OSD所在的GPU ID。
  - `border-width=5`：检测框宽度（像素值）。
  - `border-color=0;1;0;1`：检测框颜色（R;G;B;A Float, 0≤R,G,B,A≤1）。
  - `text-size=15`：文本大小。
  - `text-color=1;1;1;1;`：文本颜色。
  - `text-bg-color=0.3;0.3;0.3;1`：文本背景颜色。
  - `font=Serif`：字体。
  - `show-clock=1`：是否显示时钟。
  - `clock-x-offset=800`：时钟的X方向偏移量。
  - `clock-y-offset=820`：时钟的Y方向偏移量。
  - `clock-text-size=12`：时钟文本大小。
  - `clock-color=1;0;0;0`：时钟文本颜色。
  - `nvbuf-memory-type=0`：NvBufSurface的内存类型。

- **Streammux属性**

  > 设置流多路复用器

  - `gpu-id=0`：Streammux所在的GPU ID。
  - `live-source=0`：是否使用实时源。
  - `batch-size=1`：批大小。
  - `batched-push-timeout=40000`：批处理推送超时时间。
  - `width=1920`：流的宽度。
  - `height=1080`：流的高度。
  - `enable-padding=0`：是否启用填充。
  - `nvbuf-memory-type=0`：NvBufSurface的内存类型。

- **Primary GIE属性**

  > GIE （GPU Inference Engines）图像推理引擎，支持1个主引擎和多个次引擎，例如：

  ```
  [primary-gie]
  key1=value1
  key2=value2
  ...
  
  [secondary-gie1]
  key1=value1
  key2=value2
  ...
  
  [secondary-gie2]
  key1=value1
  key2=value2
  ...
  ```

  - `enable=1`：是否启用Primary GIE。
  - `gpu-id=0`： GIE所在的GPU ID。
  - `gie-unique-id=1`： GIE的唯一ID。
  - `nvbuf-memory-type=0`：NvBufSurface的内存类型。
  - `config-file=config_infer_primary_yoloV5.txt`：引擎的配置文件路径，参考后文介绍，可以包含 [这个表格](https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_ref_app_deepstream.html#primary-gie-and-secondary-gie-group) 所有属性（除`config-file`）

- **Tests属性**

  > 用于调试

  `file-loop=1`：是否启用文件循环。

对应我们也需要对gie进行配置，配置文件为`config_infer_primary_yoloV5.txt`

```bash
[property]
gpu-id=0
net-scale-factor=0.0039215697906911373
model-color-format=0
onnx-file=../weights/yolov5s.onnx
model-engine-file=../weights/yolov5.engine
infer-dims=3;640;640
labelfile-path=labels.txt
batch-size=1
workspace-size=1024
network-mode=2
num-detected-classes=80
interval=0
gie-unique-id=1
process-mode=1
network-type=0
cluster-mode=2
maintain-aspect-ratio=1
parse-bbox-func-name=NvDsInferParseYolo
custom-lib-path=../lib/yolov5_decode.so

[class-attrs-all]
nms-iou-threshold=0.45
pre-cluster-threshold=0.25
topk=300
```

每个参数的详细解释：

> 原始参考链接：https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_plugin_gst-nvinfer.html#gst-nvinfer-file-configuration-specifications

- ```
  [property]
  ```

  ：指定GIE的各种属性和参数：

  - `gpu-id=0`：使用的GPU ID。
  - `net-scale-factor=0.0039215697906911373`：输入图像归一化因子，为1/255。
  - `model-color-format=0`：输入图像颜色格式，0: RGB 1: BGR 2: GRAY
  - `onnx-file=yolov5s.onnx`：输入的ONNX模型文件路径（如果`model-engine-file`指向的文件不存在，则会用onnx 生成一个，并且结合`network-mode`调整精度）
  - `model-engine-file=yolov5.engine`：TensorRT模型engine文件路径（如果指向文件不存在，参考上一步，如果存在，`network-mode`不起作用）
  - `infer-dims=3;640;640`：输入图像的维度，格式为`通道数;宽度;高度`。
  - `labelfile-path=labels.txt`：类别标签文件路径。
  - `batch-size=1`：推理时的批大小。
  - `workspace-size=1024`：TensorRT内部使用的工作空间大小。
  - `network-mode=2`：推理模式，0: FP32 1: INT8 2: FP16
  - `num-detected-classes=80`：模型可检测的类别数。
  - `interval=0`：推理时图像的采样间隔，0表示不采样。
  - `gie-unique-id=1`：TensorRT引擎的唯一ID。
  - `process-mode=1`：推理时使用的处理模式，1表示同步处理。
  - `network-type=0`：**神经网络类型，0: Detector，1: Classifier，2: Segmentation，3: Instance Segmentation**
  - `cluster-mode=2`：推理时的集群模式，0: OpenCV groupRectangles() 1: DBSCAN 2: Non Maximum Suppression 3: DBSCAN + NMS Hybrid 4: No clustering （for instance segmentation）
  - `maintain-aspect-ratio=1`：是否保持输入图像的宽高比，1表示保持。
  - `parse-bbox-func-name=NvDsInferParseYolo`：解析边界框的函数名（这里用的是NvDsInferParseYolo）
  - `custom-lib-path=yolov5_decode.so`：自定义解码库路径（使用了一个自定义库文件yolov5_decode.so来解码推理输出。）

- ```
  [class-attrs-all]
  ```

  ：指定目标检测的属性和参数：

  - `nms-iou-threshold=0.45`：非极大值抑制的IOU阈值，低于阈值的候选框会丢弃
  - `pre-cluster-threshold=0.25`：聚类前的阈值。
  - `topk=300`：按置信度排序，保留前K个目标。

更多配置文件运行：

```bash
# 读取文件 --> 检测 --> 窗口显示、保存文件、推流（注意看老师演示）
deepstream-app -c config/deepstream_app_config_windows_display_write.txt

# 2个输入（RTSP、文件）--> 检测 --> 推流
deepstream-app -c config/deepstream_app_config_stream.txt

# 文件 -> 检测 -> 追踪 -> 推流
deepstream-app -c config/deepstream_app_config_stream_tracking.txt
```

### 2.4 docker运行

- 启动镜像

  ```bash
  # 运行deepstream容器
  docker run --gpus all -v `pwd`:/app -p 8556:8554  --name deepstream_env -it nvcr.io/nvidia/deepstream:6.1.1-devel bash
  ```

- 生成engine文件：

  - 安装Deepstream容器缺的包：

    ```bash
    # 先安装当前镜像缺少的包
    apt install libopencv-dev
    apt reinstall libavcodec58 libavformat58 libavutil56
    
    # 进入之前课程项目文件：
    cd 3.yolo_trt_app
    
    # build
    cmake . -B build
    cmake --build build
    
    # create engine
    ```

  - 之前课程训练的是只有`person`这一类的模型，现在需要加上`car`车辆类别，我们使用`coco`预训练模型即可（80类，附件位置：`1.预训练模型`）

  - 比如使用`yolov5s.pt`，需要按照之前课程流程处理：修改网络结构 --> 导出onnx文件 --> build engine （注意量化需要提供校准集）

- 运行

  ```bash
  # 进入目录
  cd 2.deep_stream_docker
  
  # 编译plugin library
  /usr/local/cuda/bin/nvcc -Xcompiler -fPIC -shared -o lib/yolov5_decode.so ./src/yoloForward_nc.cu ./src/yoloPlugins.cpp ./src/nvdsparsebbox_Yolo.cpp -isystem /usr/include/x86_64-linux-gnu/ -L /usr/lib/x86_64-linux-gnu/ -I /opt/nvidia/deepstream/deepstream/sources/includes -lnvinfer 
  
  # 把类别标签文件labels.txt放到config下
  
  # 将build好的yolov5 engine 文件放到config下
  # 修改配置文件config_infer_primary_yoloV5.txt中engine的路径
  
  # 修改配置文件deepstream_app_config_windows_display_write.txt 中读取视频的地址，以及保存视频的地址
  
  
  # 2个输入（RTSP、文件）--> 检测 --> 推流
  deepstream-app -c config/deepstream_app_config_stream.txt
  
  # 文件 -> 检测 -> 追踪 -> 推流
  deepstream-app -c config/deepstream_app_config_stream_tracking.txt
  
  
  # `rtsp`推流的链接为`rtsp://127.0.0.1:8554/ds-test`。可以通过vlc捕获并查看（注意容器端口映射）
  ```

## 三、代码方式运行Deepstream

### 3.1 开发一个Deepstream应用

> https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_C_Sample_Apps.html

建议在官方例子的基础上进行开发，代码位置：`/opt/nvidia/deepstream/deepstream-{版本号}/sources/apps/sample_apps`，本课程就是基于`test3`的例子改进开发的。

### 3.2 Metadata

> - https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_plugin_metadata.html
> - https://docs.nvidia.com/metropolis/deepstream/sdk-api/index.html （优先）

![image-20231015181609973](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015181609973.png)

核心数据：

- NvDsBatchMeta：`Gst-nvstreammux`处理后的批次数据
- 次级结构：
  - frame
  - object
  - classifier
  - label data

### 3.3 GStreamer 核心概念

> gstreamer是一种基于流的多媒体框架，可用于创建、处理和播放音频和视频流。它是一个开源项目，可以在Linux、Windows、macOS等多个平台上使用。gstreamer提供了一系列的库和插件，使开发者可以构建自定义的流媒体应用程序，包括音频和视频编辑器、流媒体服务器、网络摄像头应用程序等等。gstreamer具有高度的可扩展性和灵活性，可以通过插件的方式支持各种不同的编解码器、协议和设备。

#### 3.3.1 GstElement

> https://gstreamer.freedesktop.org/documentation/application-development/basics/elements.html?gi-language=c

- 媒体应用pipeline基本的构建模块（可以看成一个有输入输出的黑箱）
  - 输入：编码数据
  - 输出：解码数据
- 类型：
  - source element：没有输入，不接受数据，只产生数据（比如从文件中读取视频）

![image-20231015181623482](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015181623482.png)

Filters, convertors, demuxers（分流器）, muxers（混流器） and codecs：可以有多个输入输出（source pad、sink pad）

![image-20231015181634040](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015181634040.png)

- - Sink pad: 接受，消费数据（图左）
  - Source pad：输出，生产数据（图右）
- sink element：没有输出，不生产数据，只消费数据（比如写入磁盘、推流）

![image-20231015181639940](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015181639940.png)

- 创建元素：

  ```c++
  GstElement *element;
  
  /* init GStreamer */
  gst_init (&argc, &argv);
  
  /* create element */
  element = gst_element_factory_make ("fakesrc", "source");
  if (!element) {
    g_print ("Failed to create element of type 'fakesrc'\n");
    return -1;
  }
  // unref 
  gst_object_unref (GST_OBJECT (element));
  ```

- 获取元素属性、设置元素属性、查询元素属性

  ```c++
  // get properties
  g_object_get()
  // set properties
  g_object_set()
  
  // query properties (bash command)
  gst-inspect element
  ```

- 常见元素：

  - filesrc
  - h264parse
  - nv412decoder
  - nvstreammux
  - nvinfer
  - nvtracker
  - nvvideoconvert
  - nvdsosd

- 链接元素

  ![img](https://enpei-md.oss-cn-hangzhou.aliyuncs.com/img202303271527901.png)

  ```c++
  GstElement *pipeline;
  GstElement *source, *filter, *sink;
  
  /* create pipeline */
  pipeline = gst_pipeline_new ("my-pipeline");
  
  /* create elements */
  source = gst_element_factory_make ("fakesrc", "source");
  filter = gst_element_factory_make ("identity", "filter");
  sink = gst_element_factory_make ("fakesink", "sink");
  
  /* must add elements to pipeline before linking them */
  gst_bin_add_many (GST_BIN (pipeline), source, filter, sink, NULL);
  
  
  // more specific behavior 
  gst_element_link () and gst_element_link_pads ()
  ```

- 元素状态：

  - GST_STATE_NULL

  - GST_STATE_READY

  - GST_STATE_PAUSED

  - GST_STATE_PLAYING

  - 设置函数：

    ```c++
    /* Set the pipeline to "playing" state */
    gst_element_set_state(pipeline, GST_STATE_PLAYING);
    ```

#### 3.3.2 bin

> https://gstreamer.freedesktop.org/documentation/application-development/basics/bins.html?gi-language=c

![image-20231015181719569](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015181719569.png)

- 一串链接起来的元素的集合（bin其实一种element）

- 创建方式：

  ```C++
  /* create */
  pipeline = gst_pipeline_new ("my_pipeline");
  bin = gst_bin_new ("my_bin");
  source = gst_element_factory_make ("fakesrc", "source");
  sink = gst_element_factory_make ("fakesink", "sink");
  
  /* First add the elements to the bin */
  gst_bin_add_many (GST_BIN (bin), source, sink, NULL);
  /* add the bin to the pipeline */
  gst_bin_add (GST_BIN (pipeline), bin);
  
  /* link the elements */
  gst_element_link (source, sink);
  ```

#### 3.3.3 pipeline

![image-20231015181731340](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015181731340.png)

- 所有的元素都必须添加进pipeline后才能被使用（pipeline需要调整时钟、消息传递等）

- pipeline也是一种特殊的bin，所以也是element

- 创建方式

  ```C++
  GstElement *pipeline;
  // create 
  pipeline = gst_pipeline_new (const gchar * name)
  
  // add elements to the pipeline
  gst_bin_add_many (GST_BIN (pipeline), source, sink, NULL);
  ```

#### 3.3.4 pads

> [https://gstreamer.freedesktop.org/documentation/application-development/basics/pads.html?gi-language=chttps://gstreamer.freedesktop.org/documentation/application-development/basics/pads.html?gi-language=c](https://gstreamer.freedesktop.org/documentation/application-development/basics/pads.html?gi-language=c)

![image-20231015181740779](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015181740779.png)

- pads是元素对外服务的接口
- 数据从一个元素的source pad流向下一个元素的sink pad。

### 3.4 课程应用

> 代码：4.ds_tracker

在课程的例子中，我们主要通过构建了整条pipeline，并传入gie以及nvtracker的配置，以搭建了一条满足我们应用的流水线。

其中`gie`的配置文件类似上文配置文件介绍：

```bash
# pgie_config.txt
[property]
gpu-id=0
net-scale-factor=0.0039215697906911373
model-color-format=0
onnx-file=yolov5s.onnx
model-engine-file=../weights/yolov5.engine
labelfile-path=../weights/labels.txt
infer-dims=3;640;640
batch-size=1
workspace-size=1024
network-mode=2
num-detected-classes=80
interval=0
gie-unique-id=1
process-mode=1
network-type=0
cluster-mode=2
maintain-aspect-ratio=1
parse-bbox-func-name=NvDsInferParseYolo
custom-lib-path=../build/libyolo_decode.so

[class-attrs-all]
nms-iou-threshold=0.45
pre-cluster-threshold=0.25
topk=300
```

`nvtracker`的配置文件也类似：

```
[tracker]
tracker-width=640
tracker-height=384
gpu-id=0
ll-lib-file=/opt/nvidia/deepstream/deepstream/lib/libnvds_nvmultiobjecttracker.so
ll-config-file=./config_tracker_IOU.yml
enable-batch-process=1
```

在docker容器内运行，示例如下：

- 仅检测

  pipeline流程：

![image-20231015181756614](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015181756614.png)

```
# file
./build/ds_detect file:///app/4.ds_tracker/media/sample_720p.mp4
# rtsp
./build/ds_detect rtsp://localhost:8555/live1.sdp

```

![image-20231015181814656](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015181814656.png)

- > 绘制信息
  >
  > - 左上角：当前帧人员和车辆统计
  > - 检测框label：类别+置信度
  >
  > 推流地址：`rtsp://{ip}:{port}/ds-test`

- 检测+追踪

  Pipeline:（增加了tracker）

![image-20231015181832697](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015181832697.png)

```cpp
# file 
./build/ds_track file:///app/4.ds_tracker/media/sample_720p.mp4

# rtsp
./build/ds_track rtsp://localhost:8555/live1.sdp

```

![image-20231015181845080](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015181845080.png)

- > 绘制信息
  >
  > - 左上角：当前帧人员和车辆统计
  > - 检测框label：类别+ track_id

- 应用：越界 + 人流量 + 车流量

  Pipeline：（probe位置变化）

![image-20231015181855200](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015181855200.png)

```# file
./build/ds_app file:///app/4.ds_tracker/media/sample_720p.mp4
# RTSP
./build/ds_app rtsp://localhost:8555/live1.sdp
```

![image-20231015181910556](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015181910556.png)

![image-20231015181916568](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015181916568.png)

应用：越界 + 人流量 + 车流量 + 多源输入

Pipeline：（增加了nvmultistreamtiler）

![image-20231015181930542](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015181930542.png)

```# 文件 + RTSP 多个输入源
./build/ds_app_multi rtsp://localhost:8555/live1.sdp file:///app/4.ds_tracker/media/sample_720p.mp4
```

![image-20231015181949363](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015181949363.png)

![image-20231015181955919](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015181955919.png)

### 3.5 jetson NX 运行

- 安装 `deepstream`

  > 参考文档：https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_Quickstart.html

  ```bash
  # 安装库
  sudo apt install \
  libssl1.1 \
  libgstreamer1.0-0 \
  gstreamer1.0-tools \
  gstreamer1.0-plugins-good \
  gstreamer1.0-plugins-bad \
  gstreamer1.0-plugins-ugly \
  gstreamer1.0-libav \
  libgstreamer-plugins-base1.0-dev \
  libgstrtspserver-1.0-0 \
  libjansson4 \
  libyaml-cpp-dev
  
  # 安装librdkafka
  git clone https://github.com/edenhill/librdkafka.git
  cd librdkafka
  git reset --hard 7101c2310341ab3f4675fc565f64f0967e135a6a
  ./configure
  make
  sudo make install
  
  # 复制文件
  sudo mkdir -p /opt/nvidia/deepstream/deepstream-6.2/lib
  sudo cp /usr/local/lib/librdkafka* /opt/nvidia/deepstream/deepstream-6.2/lib
  
  
  
  # 下载SDK，并复制到jetson： 
  下载地址：https://developer.nvidia.com/downloads/deepstream-sdk-v620-jetson-tbz2
  
  # 附件位置：2.Jetson/deepstream_sdk_v6.2.0_jetson.tbz2
  
  # 解压DeepStream SDK
  sudo tar -xvf deepstream_sdk_v6.2.0_jetson.tbz2 -C /
  
  # 安装
  cd /opt/nvidia/deepstream/deepstream-6.2
  sudo ./install.sh
  sudo ldconfig
  ```

- 生成engine文件：

  - 之前课程训练的是只有`person`这一类的模型，现在需要加上`car`车辆类别，我们使用`coco`预训练模型即可（80类，附件位置：`1.预训练模型`）
  - 比如使用`yolov5s.pt`，需要按照之前课程流程处理：修改网络结构 --> 导出onnx文件 --> build engine （注意量化需要提供校准集）

- 编译运行程序，同PC

### 3.6 Jetson nano

Nano：不支持Deepstream 6.2

![image-20231015182013808](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231015182013808.png)

```# 安装依赖
sudo apt install \
libssl1.0.0 \
libgstreamer1.0-0 \
gstreamer1.0-tools \
gstreamer1.0-plugins-good \
gstreamer1.0-plugins-bad \
gstreamer1.0-plugins-ugly \
gstreamer1.0-libav \
libgstrtspserver-1.0-0 \
libjansson4=2.11-1

#安装librdkafka
git clone https://github.com/edenhill/librdkafka.git
cd librdkafka
git reset --hard 7101c2310341ab3f4675fc565f64f0967e135a6a
./configure
make
sudo make install

# 复制文件
sudo mkdir -p /opt/nvidia/deepstream/deepstream-6.0/lib
sudo cp /usr/local/lib/librdkafka* /opt/nvidia/deepstream/deepstream-6.0/lib


# 下载SDK，并复制到jetson nano上： https://developer.nvidia.com/deepstream_sdk_v6.0.1_jetsontbz2

# 附件位置：2.Jetson/deepstream_sdk_v6.0.1_jetson.tbz2  (Nano：不支持Deepstream 6.2)

# 解压DeepStream SDK
sudo tar -xvf deepstream_sdk_v6.0.1_jetson.tbz2 -C /
# 安装
cd /opt/nvidia/deepstream/deepstream-6.0
sudo ./install.sh
sudo ldconfig