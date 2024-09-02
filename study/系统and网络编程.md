[课程列表_牛客网 (nowcoder.com)](https://www.nowcoder.com/study/live/504/1/27)

[课程列表_牛客网 (nowcoder.com)](https://www.nowcoder.com/study/live/690/4/4?autoplay=1)第四章

 系统编程 2023/4/28-- 2023/5/23 

秋招复习：2024/7/17

# 0 linux命令

```py
https://github.com/gaojingcome/WebServer
// 下载
sudo apt install xx
// 清屏
ctrl + l
// 编译文件为可执行文件
gcc test.c -o test
// 执行可执行文件
./test
// 查看文件执行中的系统调用
strace ./test
// 查进程id
ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.2 168684  9564 ?        Ss   Sep01   0:04 /sbin/init
root         2  0.0  0.0      0     0 ?        S    Sep01   0:00 [kthreadd]
tty: ？表示没有终端，


ps ajx
    PID    PPID    PGID     SID TTY        TPGID STAT   UID   TIME COMMAND
   1686       1    1686    1686 ?             -1 Ssl      0   0:02 
   1732       1    1732    1732 ?             -1 Ssl      0   0:00 /usr/sbin/cron -f

// 关闭进程
ps aux|grep 程序名    kill -9 pid
// 查看端口使用
netstat -anp | grep 9527
```

```
// man 2
open
read
write
fork
accept
connect
wait
```

```
// man 7
ip
```

## 0.1系统调用

系统调用（System Call）是操作系统提供给应用程序的一种接口，应用程序通过系统调用请求操作系统内核执行特权操作或获取操作系统提供的服务。它允许应用程序访问底层操作系统的功能，如文件操作、进程管理、网络通信、设备控制等。

应用程序通常运行在用户态（User Mode）下，而操作系统内核运行在核心态（Kernel Mode）下，具有更高的权限和访问底层资源的能力。为了保证系统的安全性和稳定性，操作系统限制了应用程序的直接访问内核空间和底层资源的能力。通过系统调用，应用程序可以向操作系统发起请求，由操作系统代表应用程序执行特权操作或提供服务。

系统调用的调用方式通常是通过特定的指令或软中断来触发，从用户态切换到核心态，进入操作系统内核的上下文中执行相应的操作。系统调用的参数和返回值的传递通常是通过寄存器或栈来完成。

常见的系统调用包括：

- 文件操作：如打开文件、读取文件、写入文件、关闭文件等。
- 进程管理：如创建进程、终止进程、进程间通信等。
- 内存管理：如申请内存、释放内存、修改内存权限等。
- 网络通信：如建立网络连接、发送数据、接收数据等。
- 设备控制：如设备打开、设备关闭、设备读取、设备写入等。

系统调用是操作系统与应用程序之间的重要接口，它使应用程序能够利用操作系统提供的功能和资源，实现更复杂的任务和操作。通过系统调用，应用程序可以与底层系统进行交互，从而实现文件操作、网络通信、进程管理等功能。

## 0.2 man指令

在Linux系统中，`man`是一个用于查看系统手册页（Manual Page）的命令。它提供了对系统命令、库函数、系统调用以及配置文件等的详细文档和说明。

使用`man`命令可以通过终端查看特定命令或函数的手册页，以获取关于其使用方法、参数、选项和示例等方面的信息。`man`命令以分页的方式显示文档内容，可以使用键盘上的方向键、Page Up、Page Down等来浏览文档。

`man`命令通常提供了多个手册节（Sections），每个节包含了不同类型的文档。常见的手册节包括：

- Section 1: 用户命令（User Commands）：包含常见的命令和工具的说明，如ls、cp、grep等。
- Section 2: 系统调用（System Calls）：包含操作系统提供的系统调用的文档，如open、read、write等。
- Section 3: C库函数（C Library Functions）：包含C语言标准库提供的函数的文档，如printf、malloc、strcpy等。
- Section 4: 特殊文件（Special Files）：包含设备文件、文件系统等的文档。
- Section 5: 文件格式（File Formats）：包含文件格式、配置文件等的文档。
- Section 8: 系统管理命令（System Administration Commands）：包含系统管理和配置相关的命令的文档，通常需要管理员权限才能运行。



## 0.3 头文件

### 1 stdlib

`stdlib`是C和C++编程语言中的一个标准库（Standard Library），提供了一系列的函数和类型，用于处理常见的任务和操作，包括内存管理、字符串操作、随机数生成、排序算法等。

在C语言中，`stdlib.h`是相应的头文件，而在C++语言中，相关函数和类型位于`<cstdlib>`头文件中。

`stdlib`库中的一些常用函数和类型包括：

1. 内存管理函数：
   - `malloc()`：分配指定字节数的动态内存空间。
   - `free()`：释放先前分配的内存空间。
   - `calloc()`：分配并清零指定数量的元素空间。
   - `realloc()`：重新分配先前分配的内存空间。
2. 字符串转换函数：
   - `atoi()`、`atol()`、`atof()`：将字符串转换为整数、长整数、浮点数。
   - `itoa()`、`ltoa()`、`ftoa()`：将整数、长整数、浮点数转换为字符串。
   - `sprintf()`、`sscanf()`：格式化输出和输入字符串。
3. 随机数函数：
   - `rand()`：生成伪随机数。
   - `srand()`：设置随机数种子。
4. 环境函数：
   - `system()`：执行操作系统命令。
   - `getenv()`：获取环境变量的值。
5. 排序和查找算法：
   - `qsort()`：快速排序算法。
   - `bsearch()`：二分查找算法。

此外，`stdlib`库还包括其他一些有用的函数，如时间和日期处理、进程控制等。具体的函数和类型可根据编程语言和具体的标准进行查阅和使用。

### 2 stdio

`stdio`是C和C++编程语言中的标准库（Standard Library）之一，提供了对输入和输出操作的支持。它定义了一系列的函数和类型，用于处理标准输入、输出和文件操作。

在C语言中，`stdio.h`是相应的头文件，而在C++语言中，相关函数和类型位于`<cstdio>`头文件中。

`stdio`库中的一些常用函数和类型包括：

1. 标准输入输出函数：
   - `printf()`：格式化输出到标准输出流。
   - `scanf()`：格式化从标准输入流读取输入。
   - `getchar()`：从标准输入流读取一个字符。
   - `putchar()`：向标准输出流写入一个字符。
2. 文件操作函数：
   - `fopen()`、`fclose()`：打开和关闭文件。
   - `fgets()`、`fputs()`：读取和写入字符串到文件。
   - `fscanf()`、`fprintf()`：格式化读取和写入文件。
   - `fseek()`、`ftell()`：文件定位和查询当前位置。
   - `feof()`、`ferror()`：判断文件结束和错误状态。
3. 标准流：
   - `stdin`、`stdout`、`stderr`：标准输入、输出和错误流。
4. 格式化输入输出：
   - `sprintf()`、`sscanf()`：格式化输出和输入字符串。
   - `fprintf()`、`fscanf()`：格式化输出和输入文件。

`stdio`库中的函数和类型提供了方便和灵活的输入输出操作，使开发者能够进行格式化的输入输出、文件操作和标准流的处理。具体的函数和类型可以根据编程语言和标准进行查阅和使用。

## 0.4 错误处理函数

```
if(ret == -1){
	perror("read error!");
	exit(1); // 异常退出
}
```



# 1 配置linux环境

## 1.1 配置环境

```
vmware中安装ubuntu
镜像位置："D:\VM\Ubuntu18\ubuntu-18.04.6-desktop-amd64.iso"
```

```
安装成功后，图形化界面很小，安装vmtools,重启
zhang 123456
```

```
更新下载源
sudo apt upgrage
sudo apt-get upgrade
下载必要软件
sudo apt install net-tools
sudo apt install vim
//ssh远程连接
sudo apt install openssh-server
// 安装gcc/g++/make
sudo apt install build-essential
```

## 1.2 vscode远程登录

```
下载插件：remote development
```

```
打开远程连接，打开文件连接
```

![image-20230422170909406](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230422170909406.png)

```
给服务器安装插件：c/c++
```

## 1.3 设置ssh免密登录

```
windows cmd :C:\Users\zhang>ssh-keygen -t rsa
生成公钥私钥位置：C:\Users\zhang/.ssh/
```

```
ubuntu cmd :ssh-keygen -t rsa
生成公钥私钥位置：/home/zhang/.ssh
 /root/.ssh/id_rsa.pub.  (aliyun)

在.ssh 下创建文件：authorized_keys
vim打开写入windows的公钥地址：C:\Users\zhang/.ssh\id_rsa.pub 中内容
```

### 1.4 linux安装mysql

安装

```
sudo apt-get install mysql-server 
sudo apt-get install mysql-client 
sudo apt-get install libmysqlclient-dev
```

查看默认信息

```
sudo cat /etc/mysql/debian.cnf
```

默认信息登录

```
mysql -u xxx -p xxx       // 用户名以自己的配置文件为准
```

更改密码

```
use mysql; 
// 下一行，密码改为了yourpassword，可以设置成其他的 
update mysql.user set authentication_string=password('123456') where user='root' and Host ='localhost'; 

update user set plugin="mysql_native_password"; 

flush privileges; 

quit;
```

重启

```
sudo service mysql restart 
mysql -u root -p 新密码123456
```

### 1.5 mysql数据库配置项目信息

```
// 建立webserver库
create database webserver;

// 创建user表
USE webserver;
CREATE TABLE user(
    username char(50) NULL,
    password char(50) NULL
)ENGINE=InnoDB;

// 添加数据
INSERT INTO user(username, password) VALUES('zhang', 'zhang'); //vm里
INSERT INTO user(username, password) VALUES('root', 'root'); // aliyun
quit;
```

### 1.6 跑项目

```
// 编译生成可执行文件 到 bin
zhang@zhang:~/WebServer-master$ make
// 执行文件
zhang@zhang:~/WebServer-master$ bin/server
// web访问
http://47.115.215.93:1316/   //aliyin开启1316端口
http://4192.168.88.128:1316/
```

# 2 GCC

## 2.1 简介

![image-20230423102836929](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230423102836929.png)

![image-20230423102854788](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230423102854788.png)

## 2.2 执行流程

![image-20230423103158768](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230423103158768.png)

1、预处理：将头文件拷贝过来，将宏替换为值, 删掉注释

```
gcc -E test.c -o test.i
```

2、编译：变为汇编代码

```
gcc -S test.i -o test.S
```

3、汇编: 为目标文件

```
gcc -c test.S -o test.O
```

4、链接：生成可执行文件

```
gcc test.o a.o b.o -o test.out
```

## 2.3 其余参数

![image-20230423104633885](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230423104633885.png)

![image-20230423104656023](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230423104656023.png)

# 3 makefile

## 3.1 简介

![image-20230423110847913](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230423110847913.png)

## 3.2 makefile文件命名和规则

![image-20230423110925915](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230423110925915.png)

```
gcc test.c -o test

// mikefile
test:test.c
	gcc test.c -o test
```

* 使用

```
在目标文件下生成目标文件 test.out
/xx/xx/>>make
执行
/xx/xx/>>./test
```



## 3.3 基本原理

![image-20230423111049032](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230423111049032.png)

* 例：

<img src="C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230423111257240.png" alt="image-20230423111257240" style="zoom: 50%;" />

## 3.4 变量

* 简化写的操作

  1、自定义变量

  ```
  变量名 = 变量值
  var = test.c
  target = test
  $(target)获取值
  
  ```

  2、默认变量

  ```
  AR:归档维护程序的明证，默认 ar
  CC：C编译器名称，默认 gcc
  CXX：c++编译器名称，默认 g++
  $@ : 目标的完整名称
  $<：第一个依赖文件名称
  $^: 所有依赖的名称
  ```

  ```
  app:main.c a.c b.c
  	gcc-c main.c a.c b.c -o app
  
  // 默认变量--用来定义命令
  app:main.c a.c b.c
  	$(CC)-c $^ -o $@
  	
  // 自变量--用来定义目标、依赖文件
  src = main.c a.c b.c
  target = app
  $(target)t:$(src)
  	$(CC)-c $(src) -o $(target)
  ```

## 3.5 模式匹配

  避免写出多个重复类型的规则

  * 将相同类型的规则可以用匹配符代替

  ```
  a.o:a.c
  	gcc -E a.c -o a.o
  ab.o:b.c
  	gcc -E b.c -o b.o
  t.o:t.c
  	gcc -E t.c -o t.o
  	
  //%通配符，两个%匹配的字符一样
  %.o:%.c
  	$(CC) -E $< -o $@
  ```

## 3.6 函数

  避免规则中的依赖函数全部写出来

  * wildcard

  ```
  // 查找后缀名的所有文件
  src = $(wildcard ./*.c ./*.i)  // 查找当前目录下所有的以c和i结尾的文件
  ```

  * patsubst

  ```
  // 替换文件后缀 
  objs = $(patsubst %.c %.o $(src)) // 将src里的所有.c结尾文件替换为.o结尾
  ```

  ## 3.7 clean

* 删除中间产生的依赖

```
.PHONY:clean
clean:
	rm $(objs) -f
```



  # 4 GDB

# 5 静态库和动态库

## 5.1 静态库

* 在程序的链接阶段被复制到程序中
* 静态库的文件是目标文件（.o结尾二进制代码文件）

### 5.1.1 静态库命名

```
linux：libxxx.a
// lib 前缀
// xxx库名
// .a后缀

window: libxxx.lib
```

### 5.1.2 创建静态库

```
// 库文件
mylib：
a.c
b.c
mylib.h
```

* 静态库的文件是目标文件（.o结尾二进制代码文件）

```
1、gcc将 .c 文件编译为 .o 后缀文件
gcc a.c b.c -c
2、使用 ar 工具将.o后缀文件打包
ar rcs libmylib.a *.o
-r 将文件插入备份文件中
-c 建立备存文件
-s 索引
```

### 5.1.3 使用静态库

<img src="C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230423173029337.png" alt="image-20230423173029337" style="zoom:50%;" />

```cpp
// main.c文件
#include <stdio.h>
#include "header.h"
```

```
1// 编译为可执行文件
gcc main.c -o app
```

* 报错找不到头文件位置

![image-20230423172805687](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230423172805687.png)

```
2//指定头文件
gcc main.c -o app -I ../include/
```

* 找不到定义的库文件位置

![image-20230423172921724](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230423172921724.png)

```
3// 指定库文件及其位置
gcc main.c -o app -I ../include/ -l calc -L ../lib/ 
```

### 5.1.4 静态库使用

* 注意静态库文件名libxxx.a
* 静态库名：xxx

```
gcc main.c -o app -I /静态库头文件位置/ -l /静态库名/ -L /库文件位置/
./app
```



## 5.2 动态库

* 在程序运行时将库动态加载到内存中供库使用

### 5.2.1 动态库命名

```
linux：libxxx.so
// lib 前缀
// xxx库名
// .s0后缀

window: libxxx.dll
```



### 5.2.2 创建动态库

```
1、打包得到.o文件，得到和位置无关的代码
gcc -c -fpic a.c b.c

2、gcc打包得到动态库
gcc -shared *.o -o libmylib.so
```



### 5.2.3 使用动态库

* 程序启动后，动态库会被动态加载到内存中
* 通过  ldd+可执行文件  检查动态库依赖关系

```
gcc main.c -o app -I /静态库头文件位置/ -l /静态库名/ -L /库文件位置/
./app 
```

* 报错

  ![image-20230423203648502](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230423203648502.png)

* 配置环境变量，告诉程序从哪里寻找动态库

```
1// 临时配置
export LD_LIBRARY-PATH=$LD_LIBRARY-PATH:/绝对路径/libxxx.so
// $获取原先的值  ：拼接新的值

2// 在.bash中永久配置
vim /root/.bashrc

3// 刷新
. .bashrc
```

```
//再次执行
./app
```

## 5.3 对比

![image-20230423204930749](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230423204930749.png)

![image-20230423204248240](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230423204248240.png)

![image-20230423204056205](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230423204056205.png)

# 6 进程

## 6.1 MMU

![img](file:///C:/Users/zhang/AppData/Local/Temp/msohtmlclip1/01/clip_image002.jpg)

```
程序 a.out             进程  ./a.out
占用磁盘				占用内存和cpu
```

* 当程序变为进程时候 ，相关数据   磁盘 --> 虚拟内存 -->  MMU  -->  实际内存

* MMU大小4k，寄存器大小4B，虚拟地址分页映射，页大小4k

* 作用1：虚拟内存与物理内存映射

* 作用2：调整指令访问内存的级别（实际内存条不分用户区和内核区，通过访问级别界定）

  ---------



## 6.2 虚拟内存

![image-20230511180713726](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230511180713726.png)

* 一个进程最大占用4g内存，实际占用很小

* 0-3G用户区，3-4G内核区，具体映射到内存是根据其指令级别划分

* windows划分4个等级，linux划分2个等级

* 内核空间

* 栈：局部变量、函数调用、函数返回值地址

* 堆

* 代码段：存放可执行程序的机器指令

* 数据段：全局变量和静态变量

  

## 6.3 进程映射

![image-20230511181451976](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230511181451976.png)

* 不同进程的用户区分开映射，不会存在同一块内存区域（用户空间各自独立）
* 不同进程的内核区，映射在同一块内存区域，即内存条的一块区域存在多个不同的pcb（内核区域共享）
* 虚拟内存上的连续区域，在实际内存上分块存储

## 6.4 进程控制块PCB

* 本质：结构体

\* 进程id。系统中每个进程有唯一的id，在C语言中用pid_t类型表示，其实就是一个非负整数。

\* 进程的状态，有就绪、运行、挂起、停止等状态。

\* 文件描述符表，包含很多指向file结构体的指针。

\* 用户id和组id。



\* 进程切换时需要保存和恢复的一些CPU寄存器。

\* 当前工作目录（Current Working Directory）。



\* 描述虚拟地址空间的信息。（进程和线程的区别）

\* 描述控制终端的信息。

\* umask掩码。

\* 和信号相关的信息。

\* 会话（Session）和进程组。

\* 进程可以使用的资源上限（Resource Limit）。

## 6.5 文件描述符fd

![image-20230526143419415](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230526143419415.png)

![image-20230424213923798](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230424213923798.png)

* 0-4G内核区，有很多与进程有关的文件，PCB进程块是其中一个
* PCB中有一个指针，指向文件描述符表
* 文件描述符表中存文件描述符的id和指针，指针指向file文件结构体
* os屏蔽指针的操作，所以我们用fd接收文件描述符id
* 通过控制fd来操作文件
* fd序号为0，1，2的文件固定不变，固定1023
* 新打开一个文件，赋予其可用文件描述符最小的文件描述符 

#### 6.5.1 打开文件

在 Linux 下，可以使用 open() 函数来打开文件或设备。open() 函数是一个系统调用，用于在程序中打开文件或创建新文件。

```cpp
#include <fcntl.h>
#include <stdio.h>

int main() {
    int fd = open("example.txt", O_RDONLY);
    if (fd == -1) {
        perror("Failed to open the file");
        return 1;
    }

    // 文件打开成功，可以在这里进行读取操作

    // 关闭文件
    close(fd);

    return 0;
}

```

open() 函数的第一个参数是文件路径名，指定要打开的文件或设备的路径。

第二个参数是一个整数标志，用于指定打开文件的模式。常见的标志包括：

- O_RDONLY：只读模式
- O_WRONLY：只写模式
- O_RDWR：读写模式
- O_CREAT：如果文件不存在，则创建文件
- O_APPEND：以追加方式打开文件
- O_TRUNC：如果文件已存在，则将其截断为零长度

open() 函数会返回一个非负整数的文件描述符（File Descriptor），如果打开文件失败，则返回 -1。文件描述符可以用于后续的读写操作。

#### 6.5.2 读写文件

```c
//read
ssize_t read(int fd, void *buf, size_t count);
参数1：从哪个文件中读，用fd文件描述符指定
参数2：写到指定 的buf缓冲区（102、4096）
参数3：缓冲区的大小sizeof(buf)
    成功：返回num读取的字节数大小
    失败：-1，设置error
    文件读完：0

```

```c
//write
ssize_t write(int fd, const void *buf, size_t count);
参数1：往指定文件写，用fd指定
参数2：将指定buf中的数据写入
参数3：写入的实际数据大小（缓冲区一般设置1024，但实际数据没这么多）
    成功：写入的字节数
    失败：-1，设置error
```

```c
// 实现拷贝
int fd1 = open("text1",O_RDONLY);
int fd2 = open("text2",O_RDWR | O_CREAT);

char buf[1024];
int num = 0;
while( num = read(fd1,buf,1024) != 0){  // fd文件大小可能超过1024，一次读不完，循环依次读取，读取结束后，再次读取num=0
	write(fd2,buf,num);
}

close(fd1);
close(fd2);
```



#### 6.5.3 复制文件描述符

```cpp
int dup(int oldfd);
dup() 函数通过复制现有的文件描述符 oldfd，返回一个新的文件描述符。新的文件描述符与原来的文件描述符指向相同的文件表项，也就是说它们共享同一个文件偏移量和文件状态标志。
```

```cpp
#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>

int main() {
    int fd = open("example.txt", O_WRONLY | O_CREAT, 0644);
    if (fd == -1) {
        perror("Failed to open the file");
        return 1;
    }

    int new_fd = dup(fd);
    if (new_fd == -1) {
        perror("Failed to duplicate file descriptor");
        close(fd);
        return 1;
    }

    // 使用 new_fd 进行写操作
    write(new_fd, "Hello, World!", 13);

    // 关闭文件描述符
    close(fd);
    close(new_fd);

    return 0;
}
在上述示例中，首先使用 open() 函数打开了一个文件，并获得了一个文件描述符 fd。然后，使用 dup() 函数复制了该文件描述符，得到了一个新的文件描述符 new_fd。最后，可以使用 new_fd 进行写操作，写入数据到文件中。

需要注意的是，复制的文件描述符与原来的文件描述符是相互独立的，可以分别进行读写操作。在程序结束时，需要使用 close() 函数关闭文件描述符，以释放资源。
```

--------

```cpp
int dup2(int oldfd, int newfd);

dup2() 函数将 oldfd 的文件描述符复制到 newfd，并关闭 newfd 所指向的文件描述符（如果已经打开）。如果 newfd 等于 oldfd，则不进行复制，而是返回 newfd
```

```cpp
#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>

int main() {
    int fd = open("example.txt", O_WRONLY | O_CREAT, 0644);
    if (fd == -1) {
        perror("Failed to open the file");
        return 1;
    }

    int new_fd = dup2(fd, STDOUT_FILENO);
    if (new_fd == -1) {
        perror("Failed to duplicate file descriptor");
        close(fd);
        return 1;
    }

    // 使用 new_fd 进行写操作
    write(new_fd, "Hello, World!", 13);

    // 关闭文件描述符
    close(fd);
    close(new_fd);

    return 0;
}

在上述示例中，首先使用 open() 函数打开一个文件，并获得一个文件描述符 fd。然后，使用 dup2() 函数将 fd 复制到标准输出文件描述符 STDOUT_FILENO。这样，后续的写操作将会输出到该文件中。

需要注意的是，dup2() 函数会关闭 newfd 所指向的文件描述符（如果已经打开），并将 oldfd 复制到 newfd。在程序结束时，需要使用 close() 函数关闭文件描述符，以释放资源。
```

#### 6.5.4 阻塞和非阻塞

* 阻塞是 ==设备文件==和==网络文件==的特性

* 读取一般的文件，基本上都是非阻塞

* 设备文件：STDIN_FILENO : 文件阻塞等待键盘输入

  ​					STDOUT_FILENO : 文件阻塞，等待读取信息输出屏幕

* 网络文件：

* 更改文件的阻塞模式

```cpp
int flag = fcntl(fd, F_GETFL, 0);
fcntl(fd, F_SETFL, flags | O_NONBLOCK);
```

* read返回值：
  * -1  读取失败
  * -1  并且 errno为EAGAIN或者EWOULDBLOCK，则说明设备文件或者网络文件被设置为非阻塞模式，且没有读到任何数据
  * 0  文件读到末尾/文件关闭
  * num：读到的字节数

## 6.6 shell和bash

![image-20230512155745156](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230512155745156.png)

![image-20230512155829719](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230512155829719.png)

![image-20230512155908275](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230512155908275.png)

==命令解释行内运行的所有父程序的父程序pid=1==

==bash的pid = 1==

# 7 多进程

## 7.1 多进程定义

```cpp
//创建子进程，pid标识父进程or子进程
pid_t pid = fork();
	成功： 父进程fork返回 --> 子进程pid
          子进程fork返回 --> 0
    失败： 返回-1

// 查看当前进程的pid和父亲的pid，组id
getpid()  
getppid()  
getpgid();  
```

![image-20230512103709367](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230512103709367.png)

* a.out执行到fork
* copy所有a.out代码，一分为二，同时执行
* 子进程拥有fork前的代码，但是不执行
* fork（）返回两个值

```
// 注意
父子相同处: 全局变量、.data、.text、栈、堆、环境变量、用户ID、宿主目录、进程工作目录、信号处理方式...
父子不同处: 1.进程ID   2.fork返回值   3.父进程ID    4.进程运行时间    5.闹钟(定时器)   6.未决信号集

父子进程：读时共享，写时复制
不共享全局变量
共享：文件描述符、mmap建立的映射区
```





## 7.1 循环创建多进程

```cpp
#include <sys/types.h>
#include <unistd.h>
#include <stdio.h>

int main()
{
    printf("the main process begin~\n");
    pid_t pid;
    int i = 0;
    for (i; i < 5; i++) // 让父程序循环创建子程序
    {
        pid = fork();
        if (pid == 0) // 子程序
        {
            break;
        }
    }
    if (i == 5)
    {
        printf("father, id: %d , ppid: %d \n", getpid(), getppid());
    }
    else
    {
        printf("child : %d , id: %d , ppid: %d \n", i + 1, getpid(), getppid());
    }

    return 0;
}


```

```
root@iZf8zc70s5qi0tygukf9wdZ:/home/zhang/many# ./fork
the main process begin~
father, id: 26638 , ppid: 10915     // ppid位bash的pid
child : 3 , id: 26641 , ppid: 1 	// 父进程结束，子进程被init进程收养，init的pid=1
root@iZf8zc70s5qi0tygukf9wdZ:/home/zhang/many# child : 4 , id: 26642 , ppid: 1 
child : 1 , id: 26639 , ppid: 1 
child : 2 , id: 26640 , ppid: 1 
child : 5 , id: 26643 , ppid: 1 
```

```
// 我的理解
循环创建5个进程，系统层面上看： 5个进程同时建立，与父程序一块执行下面的程序，抢占cpu
当父亲结束，子进程还未结束时，bash出现，出现child 4 的情况
```



## 7.3 孤儿/僵尸进程

![image-20230426145535480](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230426145535480.png)

### 7.3.1 解决孤儿进程

* 让父程序睡眠等待子程序结束

```cpp
if (i == 5)
    {	
    	sleep(5);
        printf("father, id: %d , ppid: %d \n", getpid(), getppid());
    }
    else
    {
    	sleep(i); // 保证子程序按照创建顺序输出
        printf("child : %d , id: %d , ppid: %d \n", i + 1, getpid(), getppid());
    }
```

### 7.3.2 解决僵尸进程

* 杀死父进程

* wait

  ```cpp
  // man 2 wait
  // 父函数调用
  pid_t wait(int *wstatus); // 传出参数
  	成功：回收的进程号
      失败：-1
  ```

  wait作用

  ① 阻塞等待子进程退出   （父子进程争夺从cpu，父进程得到后，wait阻塞，知道子进程死掉，回收）

  ② 回收子进程残留资源 

  ③ 获取子进程结束状态(退出原因)。

  可使用wait函数传出参数status来保存进程的退出状态。借助宏函数来进一步判断进程终止的具体原因。宏函数可分为如下三组：

   \1. WIFEXITED(status) 为非0   → 进程正常结束

  ​     WEXITSTATUS(status) 如上宏为真，使用此宏 → 获取进程退出状态 (exit的参数)

   \2.  WIFSIGNALED(status) 为非0 → 进程异常终止

  ​     WTERMSIG(status) 如上宏为真，使用此宏 → 取得使进程终止的那个信号的编号。

  *3.  WIFSTOPPED(status) 为非0 → 进程处于暂停状态

  ​     WSTOPSIG(status) 如上宏为真，使用此宏 → 取得使进程暂停的那个信号的编号。

  ​     WIFCONTINUED(status) 为真 → 进程暂停后已经继续运行

* waitpid



## 7.4 waitpid

```cpp
if (i == 5)
    {	
    	pid_t wpid;
    // 使用阻塞方式回收子进程（回收完一直返回-1）
        wpid = waitpid(-1, NULL, 0);
        while (wpid)
        {
            printf("wait pid: %d \n", wpid);
        }
    }
	// 使用非阻塞方式执行（回收完退出）
		wpid = waitpid(-1, NULL, WNOHANG); // would no hang
        while (wpid != -1)
        {
            if (wpid > 0)
            {
                printf("wait child %d \n", wpid);
            }
            else if (wpid == 0)
            {
                sleep(1);
                continue;
            }
        }


    else
    {
    	sleep(i); // 保证子程序按照创建顺序输出
        printf("child : %d , id: %d , ppid: %d \n", i + 1, getpid(), getppid());
    }
```



## 7.4 进程通信

我们先来说说进程间通信（IPC）的一般目的，大概有数据传输、共享数据、通知事件、资源共享和进程控制等。

但是我们知道，对于每一个进程来说这个进程看到属于它的一块内存资源，这块资源是它所独占的，所以进程之间的通信就会比较麻烦。

原理就是需要让不同的进程间能够看到一份公共的资源。

所以交换数据必须通过内核,在内核中开辟一块缓冲区,进程1把数据从用户空间 拷到内核缓冲区,进程2再从内核缓冲区把数据读走,内核提供的这种机制称为进程间通信。

一般我们采用的进程间通信方式有

1. 管道（pipe）和有名管道（FIFO）
2. 信号（signal）
3. 消息队列
4. 共享内存
5. 信号量
6. 套接字（socket)

我们先来从最简单的通信方式来说起；

### 1 管道通信

#### 匿名管道

**管道的创建**

管道是一种最基本的进程间通信机制。管道由pipe函数来创建：

![img](https://images2015.cnblogs.com/blog/932246/201609/932246-20160909083826535-913822489.png)

调用pipe函数，会在内核中开辟出一块缓冲区用来进行进程间通信，这块缓冲区称为管道，它有一个读端和一个写端。

pipe函数接受一个参数，是包含两个整数的数组，如果调用成功，会通过pipefd[2]传出给用户程序两个文件描述符，需要注意pipefd [0]指向管道的读端, pipefd [1]指向管道的写端，那么此时这个管道对于用户程序就是一个文件，可以通过read(pipefd [0]);或者write(pipefd [1])进行操作。pipe函数调用成功返回0，否则返回-1..

那么再来看看通过管道进行通信的步骤：

》父进程创建管道，得到两个文件描述符指向管道的两端

![img](https://images2015.cnblogs.com/blog/932246/201609/932246-20160909083943691-1511040684.png)

》利用fork函数创建出子进程，则子进程也得到两个文件描述符指向同一管道

![img](https://images2015.cnblogs.com/blog/932246/201609/932246-20160909083954504-660747163.png)

》父进程关闭读端（pipe[0]）,子进程关闭写端pipe[1]，则此时父进程可以往管道中进行写操作，子进程可以从管道中读，从而实现了通过管道的进程间通信。

   ![img](https://images2015.cnblogs.com/blog/932246/201609/932246-20160909084013707-2039185528.png)

```c
// 实例
#include<stdio.h>
#include<unistd.h>
 #include<string.h>
int main()
{
int _pipe[2];
int ret=pipe(_pipe);
    if(ret<0)
    {
         perror("pipe\n");
    }
  pid_t id=fork();
  if(id<0)
{
       perror("fork\n");
   }
   else if(id==0)  // child
    {
        close(_pipe[0]);
        int i=0;
        char *mesg=NULL;
       while(i<100)
       {
           mesg="I am child";
           write(_pipe[1],mesg,strlen(mesg)+1);
           sleep(1);
           ++i;
        }
     }
    else  //father
   {
       close(_pipe[1]);
         int j=0;
        char _mesg[100];
         while(j<100)
        {
          memset(_mesg,'\0',sizeof(_mesg ));
          read(_pipe[0],_mesg,sizeof(_mesg));
          printf("%s\n",_mesg);
          j++;
        }
    }
   return 0;

```

* 匿名管道特点

\1. 只能单向通信

\2. 只能血缘关系的进程进行通信

\3. 依赖于文件系统

4、生命周期随进程

\5. 面向字节流的服务

\6. 管道内部提供了同步机制

说明：因为管道通信是单向的，在上面的例子中我们是通过子进程写父进程来读，如果想要同时父进程写而子进程来读，就需要再打开另外的管道；

管道的读写端通过打开的文件描述符来传递,因此要通信的两个进程必须从它们的公共祖先那里继承管道的件描述符。 上面的例子是父进程把文件描述符传给子进程之后父子进程之 间通信,也可以父进程fork两次,把文件描述符传给两个子进程,然后两个子进程之间通信, 总之 需要通过fork传递文件描述符使两个进程都能访问同一管道,它们才能通信。

#### 有名管道

* 在管道中，只有具有血缘关系的进程才能进行通信，对于后来的命名管道，就解决了这个问题。

* FIFO不同于管道之处在于它提供一个路径名与之关联，以FIFO的文件形式存储于文件系统中。

* 命名管道是一个设备文件，因此，即使进程与创建FIFO的进程不存在亲缘关系，只要可以访问该路径，就能够通过FIFO相互通信。

* 值得注意的是， FIFO(first input first output)总是按照先进先出的原则工作，第一个被写入的数据将首先从管道中读出

```
// 创建fifo文件（有名管道）
int ret = access("fifo",F_OK); // 判断文件是否存在
if(ret == -1){
	printf(“管道不存在！);
	ret = mkfifo("fifo",0664); // 权限
}
```

```
//进程1 读  
// 只读方式打开管道
int fd = open("fifo"，O_RDONLY); // 通过操作符来控制fifo
if(fd == -1){
	perror("open");
	exit(0);
}
// 读数据
while(1){
	char buf[1024] = {0};
	int len = read(fd,buf,sizeof(buf));
	}
close(fd);
```

```
// 进程2 写
// 只写方式打开
int fd = open("fifo"，O_WRONLY; // 通过操作符来控制fifo
if(fd == -1){
	perror("open");
	exit(0);
}
// 写数据
for(int i = 0;i<100;i++){
	char buf[1024];
	write(fd,buf,strlen(buf))
	sleep(1);
}
close(fd);
```

#### 总结

![image-20230427143058092](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230427143058092.png)



### 2 共享内存

![image-20230427144438832](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230427144438832.png)

```cpp
int main(){
    // 获取共享内存
	int shmid = shmget(100,0,IPC_CREAT);
    // 当前进程关联
    void *ptr = shmat(shmid,NULL,0);
    // 读数据
    printf("%s\n",(char*)ptr);
    getchar();
    // 解除关联
    shmdt(ptr);
    // 删除共享内存
    shmctl(shmid,IPC_RMID,NULL)
}
```

```
// shell 命令
ipcs  查看当前进程通信信息

------ Message Queues --------
key        msqid      owner      perms      used-bytes   messages    

------ Shared Memory Segments --------  "ipcs-m"
key        shmid      owner      perms      bytes      nattch     status      

------ Semaphore Arrays --------
key        semid      owner      perms      nsems     
```





### 3  信号

* 简单
* 满足条件才能发送

特质：

* 软件层面"中断"。一旦信号产生，无论程序执行到什么位置，都必须立即停止运行，处理完信号，再执行后续的指令
* 所有信号处理，均由==内核== 完成

#### 3.0 信号四要素

* 编号
* 名称
* 事件
* 默认处理

```
Trem 终止进程
Ign 忽略信号
Core 终止进程，生成core文件
Stop 停止 暂停进程
Cont 继续运行
```





#### 3.1 信号产生方式

1、按键产生 ctrl c

2、 系统调用产生 kill

```
// man 7 signal
// kill -l
// 中文一览表
1) SIGHUP: 当用户退出 shell 时，由该 shell 启动的所有进程将收到这个信号，默认动作为终止进程
2) SIGINT：当用户按下了<Ctrl+C>组合键时，用户终端向正在运行中的由该终端启动的程序发出此信号。默认动
作为终止进程。
3) SIGQUIT：当用户按下<ctrl+\>组合键时产生该信号，用户终端向正在运行中的由该终端启动的程序发出些信
号。默认动作为终止进程。
4) SIGILL：CPU 检测到某进程执行了非法指令。默认动作为终止进程并产生 core 文件
5) SIGTRAP：该信号由断点指令或其他 trap 指令产生。默认动作为终止里程 并产生 core 文件。
6) SIGABRT: 调用 abort 函数时产生该信号。默认动作为终止进程并产生 core 文件。
7) SIGBUS：非法访问内存地址，包括内存对齐出错，默认动作为终止进程并产生 core 文件。
8) SIGFPE：在发生致命的运算错误时发出。不仅包括浮点运算错误，还包括溢出及除数为 0 等所有的算法错误。
默认动作为终止进程并产生 core 文件。
9) SIGKILL：无条件终止进程。本信号不能被忽略，处理和阻塞。默认动作为终止进程。它向系统管理员提供了
可以杀死任何进程的方法。
10) SIGUSE1：用户定义 的信号。即程序员可以在程序中定义并使用该信号。默认动作为终止进程。
11) SIGSEGV：指示进程进行了无效内存访问。默认动作为终止进程并产生 core 文件。
12) SIGUSR2：另外一个用户自定义信号，程序员可以在程序中定义并使用该信号。默认动作为终止进程。
13) SIGPIPE：Broken pipe 向一个没有读端的管道写数据。默认动作为终止进程
14) SIGALRM: 定时器超时，超时的时间 由系统调用 alarm 设置。默认动作为终止进程。
15) SIGTERM：程序结束信号，与 SIGKILL 不同的是，该信号可以被阻塞和终止。通常用来要示程序正常退出。
执行 shell 命令 Kill 时，缺省产生这个信号。默认动作为终止进程。
16) SIGSTKFLT：Linux 早期版本出现的信号，现仍保留向后兼容。默认动作为终止进程。
17) SIGCHLD：子进程状态发生变化时，父进程会收到这个信号。默认动作为忽略这个信号。
18) SIGCONT：如果进程已停止，则使其继续运行。默认动作为继续/忽略。
19) SIGSTOP：停止进程的执行。信号不能被忽略，处理和阻塞。默认动作为暂停进程。
20) SIGTSTP：停止终端交互进程的运行。按下<ctrl+z>组合键时发出这个信号。默认动作为暂停进程。
21) SIGTTIN：后台进程读终端控制台。默认动作为暂停进程。
22) SIGTTOU: 该信号类似于 SIGTTIN，在后台进程要向终端输出数据时发生。默认动作为暂停进程。
23) SIGURG：套接字上有紧急数据时，向当前正在运行的进程发出些信号，报告有紧急数据到达。如网络带外
数据到达，默认动作为忽略该信号。
24) SIGXCPU：进程执行时间超过了分配给该进程的 CPU 时间 ，系统产生该信号并发送给该进程。默认动作为
终止进程。
25) SIGXFSZ：超过文件的最大长度设置。默认动作为终止进程。
26) SIGVTALRM：虚拟时钟超时时产生该信号。类似于 SIGALRM，但是该信号只计算该进程占用 CPU 的使用时
间。默认动作为终止进程。
27) SGIPROF：类似于 SIGVTALRM，它不公包括该进程占用 CPU 时间还包括执行系统调用时间。默认动作为终止
进程。
28) SIGWINCH：窗口变化大小时发出。默认动作为忽略该信号。
29) SIGIO：此信号向进程指示发出了一个异步 IO 事件。默认动作为忽略。
30) SIGPWR：关机。默认动作为终止进程。
31) SIGSYS：无效的系统调用。默认动作为终止进程并产生 core 文件。
34) SIGRTMIN ～ (64) SIGRTMAX：LINUX 的实时信号，它们没有固定的含义（可以由用户自定义）。所有的实时
信号的默认动作都为终止进程。
```



3、 软件条件产生 sleep、定时器alarm

```cpp
// alarm
// 每一个进程有且只有唯一个定时器
// 设置定时器。内核给当前进程发送，14，SINGALARM信号，进程默认终止
alarm（4）；
// 设置进程执行时间，返回上一段闹钟的剩余值，下一次的时间与上一次的时间无关

time ./alarm
// 查看程序执行时间
// 实际时间= 系统时间(sys)+用户时间(user)+等待(IO)时间
// 优化程序重点在IO
```

 ```cpp
 // setitimer()
 // man setitimer
 // 1、可以设置两个定时器，先执行第一个，后循环执行第二个
 // 2、周期性，可以循环执行第二个闹钟
  int setitimer(int which, 
                const struct itimerval *new_value,// 传入参数，需要初始化数值
                struct itimerval *old_value);    //传出参数，返回上个闹钟剩余时间，不用设置
 // which
 // 1、自然定时 ITIMER_REAL === 14 SIGLARM               自然事件
 // 2、虚拟空间计时（用户空间） ITIMER_VIRTUAL====26			只计算进程占用cpu时间
 // 3、运行时计时（用户+内核）ITIMER_PROF=====27				计算占用cpu和执行系统调用的时间
 
 struct itimerval {
                struct timeval it_interval; /* 第一个闹钟 */  // 后执行，n次
                struct timeval it_value;    /* 第二个闹钟 */  // 先执行，1次
            };
 
  struct timeval {
                time_t      tv_sec;         /* 秒 */
                suseconds_t tv_usec;        /* 微秒 */   // 一般二选一，一个设置数值，一个为0
            };
 
 // 成功 0；失败-1
 
 
 //e.g
 #include <stdio.h>
 #include <sys/time.h>
 #include <signal.h>
 
 void fun(int singgo)
 {
     printf("hello\n");
 }
 
 int main()
 {
     struct itimerval it, oldit;
 
     signal(SIGALRM, fun);
 
     it.it_interval.tv_sec = 2;   // 第一个闹钟2s，循环执行
     it.it_interval.tv_usec = 0;
 
     it.it_value.tv_sec = 5;  // 闹钟5s,执行1次
     it.it_value.tv_usec = 0;
 
     while (1)
         ;
     return 0;
 }
 ```



4、 硬件异常产生

5、命令产生 kill

#### 3.2 信号状态

* 产生
* 递达  到达进程
* 未决 未到达进程，由于阻塞  (信号里9和19kill -9 必须执行，不能被阻塞)

#### 3.3 信号的处理方式

1、 执行默认动作

2、 忽略丢弃

3、 信号捕捉，调用户处理函数

#### 3.4 未决/阻塞信号集 

* 未决信号集：用来记录信号的处理状态，默认为0
* 阻塞信号集：用来记录信号的屏蔽状态，一旦被屏蔽，只能一直处于未决状态

![image-20230516180349409](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230516180349409.png)

#### 3.5 屏蔽/解除信号

![image-20230517161302794](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230517161302794.png)

```cpp
// 设置自定义信号集
sigset_t set;

sigemptyset( &set );			//将某个信号集清0		 		成功：0；失败：-1
sigfillset( &set );				//将某个信号集置1		  		成功：0；失败：-1
sigaddset(&set, SIGINT);	//将某个信号加入信号集 ，例如SIGINT信号 		成功：0；失败：-1
sigdelset(&set, int signum);	//将某个信号移除信号集 
sigismember(const sigset_t *set, int signum); //判断某个信号是否在信号集中	返回值：在集合：1；不在：0；
```

```cpp
// 设置信号屏蔽字和解除
int sigprocmask(int how, const sigset_t *set, sigset_t *oldset);	成功：0；失败：-1，设置errno
参数：
	
	how参数取值：	假设当前的信号屏蔽字为mask
		1.	SIG_BLOCK: 屏蔽
		2.	SIG_UNBLOCK: 解除屏蔽
		3.	SIG_SETMASK: 用于替代原始屏蔽及的新屏蔽集。
    set：自定义屏蔽集。
	oldset：旧有的屏蔽集，用于执行完进程后恢复。
           If  oldset is non-NULL, the previous value of the signal mask is stored in old‐set.
		   If set is NULL, then the signal mask is unchanged 
    
// e.g
// 自定义屏蔽集
sigset_t set;
sigemptyset(&set);
sigaddset(&set, SIGCHLD);
// 屏蔽信号
sigprocmask(SIG_BLOCK, &set, NULL);
// 解除屏蔽
sigprocmask(SIG_UNBLOCK, &set, NULL);
```

```cpp
// 查看未决信号集
int sigpending(sigset_t *set);
```

```cpp
// e.g
int main(){
	sigset_t set,oldset,pedset;
    
    sigemptyset(&set);
    sigaddset(&set,SIGINT); // 信号变1
    sigprocmask(SIG_BLOCK,&set,&oldset);  // 异或两个集合
    
    while(1){
		sigpending(&pedset); // 将未决集导入到pedset集合
        print_set(&pedset); // 自定义打印函数
        sleep(1);
    }
    return 0;
}
```

#### 3.6 信号捕捉

* signal  注册一个信号捕捉函数，捕捉由内核完成

 ```cpp
 typedef void (*sighandler_t)(int); //定义一个参数为int、返回值为void的指针函数
 sighandler_t signal(int signum,  // 信号名
                     sighandler_t handler); // 处理函数
 
 // e.g
 void catch(int sig){   // sig为捕捉到的信号的编号
 	printf("catch you %d\n",sig)
 }
 int main(){
 	signal(SIGINT,catch);  // 当捕捉到SIGIN信号时，执行catch函数
     while(1);
     
     return 0;
 }
 ```

* sigaction（常用）

```cpp
int sigaction(int signum,  // 信号名
              const struct sigaction *act, // 新的处理方式
              struct sigaction *oldact); // 返回，旧的处理方式, oldact可以为NULL
 struct sigaction {
               void  (*sa_handler)(int); // 处理函数
               sigset_t sa_mask; //信号屏蔽字，作用域为执行处理信号的过程中，不同于全局的mask,用sigemptyset( &set );
               int sa_flags; // 设置信号屏蔽，默认0，
     								// 防止在执行处理函数的时候，再来一个捕捉信号，在处理过程中，将其阻塞
           };

// e.g
void catch(int sig){   // sig为捕捉到的信号的编号
	printf("catch you %d\n",sig)
}
int main(){
    
    struct sigaction act,oldact;
    act.sa_handler = catch;        // 捕捉函数
    sigemptyset(&act.sa_mask);	   // 初始化信号屏蔽字为空	
    act.sa_flags = 0;   		   // 将捕捉的信号设置堵塞
    sigaddset(&act.sa_mask, SIGINT); // (可以设置)在执行捕捉函数期间，将其他信号阻塞
    
	sigaction(SIGINT,&act,&oldact);  // 当捕捉到SIGIN信号时，执行catch函数
    //oldact可以为空
    sigaction(SIGINT,&act,NULL); 
    while(1);  						// 模拟后续操作
    
    return 0;
}
```

* 信号捕捉特性

```
1、捕捉函数执行期间，信号屏蔽字由 mask -> sa_mask，捕捉函数结束后，sa_mask -> mask
2、捕捉函数执行期间，本信号自动屏蔽（sa_flags = 0）
3、捕捉函数执行期间，被屏蔽信号如果多次发送，解除屏蔽后只执行1次回调函数  (在捕捉函数中，用while循环处理 )
```

#### 3.7 利用信号捕捉回收子进程

```cpp
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>
#include <signal.h>
#include <string.h>
#include <sys/wait.h>
#include <pthread.h>

void catch_child(int signo)
{
    pid_t wpid;
    int status;
    // 1、在执行捕捉函数时，发来多个信号，最后只会一次回调
    // 若回调期间，发送多个sigchld信号，会产生多个僵尸进程
    // 回调函数内部，用while循环处理，一次回调，多次处理
    // 旧：1次回调中，调用1次waitpid,回收一个子进程
    // 新：1次回调中，循环调用n次waitpid,回收一个n个子进程
    // 解决信号处理无排队机制问题
    while ((wpid = waitpid(-1, &status, 0)) != -1)
    {
        if (WIFEXITED(status))
        {
            printf("-------------catch child id %d, ret=%d \n", wpid, WEXITSTATUS(status));
        }

        return;
    }
}

int main()
{
    // 2、设置阻塞
    // 防止父进程捕捉信号尚未注册完毕，子进程结束
    sigset_t set;
    sigemptyset(&set);
    sigaddset(&set, SIGCHLD);

    sigprocmask(SIG_BLOCK, &set, NULL);
    // 创建子进程
    int i = 0;
    for (i; i < 10; i++)
    {
        pid_t pid;
        pid = fork();
        if (pid == 0)
        {
            break;
        }
    }
    if (i == 10)
    {
        // 父进程
        printf("i am parent, pid %d \n", getpid());
        // 回收子进程
        struct sigaction act;

        act.sa_handler = catch_child; // 设置回调函数
        sigemptyset(&act.sa_mask);    // 设置捕捉期间信号屏蔽字
        act.sa_flags = 0;             // 本信号自动屏蔽

        sigaction(SIGCHLD, &act, NULL); // 注册捕捉信号函数

        // 2、解除屏蔽，处理子进程结束信号
        sigprocmask(SIG_UNBLOCK, &set, NULL);

        while (1)
            ; // 模拟父进程继续处理之后的事情
    }
    else if (i < 10)
    {
        // 子进程
        printf("i am child %d, pid %d \n", i, getpid());
    }

    return 0;
}
```









# 8 网络编程

## 8.1 CS/BS模型

![image-20230509121939040](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230509121939040.png)

## 8.2 协议

### 8.2.1 ARP协议

![image-20230509122603029](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230509122603029.png)

### 8.2.1 IP协议  

* 网络中，标识一台唯一的主机

![image-20230509122216627](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230509122216627.png)

![image-20230509122351186](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230509122351186.png)

### 8.2.3 TCP协议

* 主机中，标识一个唯一进程

![image-20230509122648315](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230509122648315.png)

![image-20230509122912342](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230509122912342.png)

## 8.3 socket

### 8.3.1 设置网络套接字



![image-20230509121633607](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230509121633607.png)

* 套接字是成对出现的
* 一个套接字有一个fd文件描述符，控制两个缓冲区
* sfd写到发送端后，系统自动发送到cfd的接收端内，不用用户操作

------------------------

* struct linger

  ```cpp
  // 设置套接字选项
  struct linger
    {
      int l_onoff;	 // 是否启用延迟关闭选项(1是，0否)
      int l_linger;	 // 设置延迟关闭的时间 (秒为单位)
    };
  ```

  1. `l_onoff`：用于控制是否启用延迟关闭选项。如果将 `l_onoff` 设置为非零值（通常为 1），表示启用延迟关闭，即在关闭套接字之前等待未发送的数据发送完毕。如果将 `l_onoff` 设置为零，表示禁用延迟关闭，即立即关闭套接字，不管是否还有未发送的数据。
  2. `l_linger`：用于设置延迟关闭的时间。当 `l_onoff` 设置为非零值时，`l_linger` 表示等待未发送数据发送完毕的时间（以秒为单位）。在等待的时间内，套接字会保持打开状态。超过指定的延迟时间后，无论数据是否发送完毕，套接字都会被强制关闭。
  3. 套接字默认会在调用 `close()` 函数后立即关闭。只有在需要特殊处理延迟关闭的情况下，才需要显式设置 `struct linger` 结构体并应用于套接字选项。

---------------------------

* 设置套接字属性

  ```cpp
  int setsockopt(int sockfd, int level, int optname, const void *optval, socklen_t optlen);
  ```

  参数说明如下：

  - `sockfd`：表示要设置选项的套接字描述符。

  - `level`：表示选项所属的协议级别或套接字级别。

    ==`SOL_SOCKET`----socket==

    `IPPROTO_TCP`----tcp协议

    `IPPROTO_IP` -----ip协议

  - `optname`：表示要设置的选项的名称。它指定了要设置的特定选项。

  - `optval`：是一个指向存储选项值的缓冲区的指针。根据选项的类型，`optval` 可以是不同类型的指针，如 `int*`、`char*`、`struct linger*` 等。

  - `optlen`：表示选项值的长度，即缓冲区的大小。

  - 成功，返回值为 0；

  - 失败，返回值为 -1，并设置相应的错误码（通过 `errno` 变量获取）

    -------------

    下面是关于SOL_SOCKET	选项的说明：

  1. `SO_REUSEADDR`：（端口复用）
    - 级别：`SOL_SOCKET`
     - 作用：允许在同一端口上快速重用处于 `TIME_WAIT` 状态的套接字。通常在服务器程序中使用，以便在绑定新套接字之前，允许关闭的套接字释放端口。这样可以避免在套接字关闭后一段时间内无法绑定相同地址和端口的问题。
  
  2. `SO_LINGER`：（延迟关闭）
     - 级别：`SOL_SOCKET`
     - 作用：控制套接字的延迟关闭行为。使用 `struct linger` 结构体来设置延迟关闭的属性，包括 `l_onoff` 和 `l_linger`。当 `l_onoff` 为非零值时，表示启用延迟关闭，套接字在关闭时会等待未发送完的数据发送完毕。`l_linger` 则指定等待的时间（以秒为单位）。如果 `l_onoff` 为零，表示禁用延迟关闭，套接字关闭时会立即关闭，丢弃未发送的数据。
  
3. `SO_RCVBUF`：
     - 级别：`SOL_SOCKET`
     - 作用：设置接收缓冲区的大小。通过设置接收缓冲区大小，可以影响接收数据的效率和性能。较大的接收缓冲区可以容纳更多的数据，适用于高速数据传输或者需要处理大量数据的场景。
  
4. `SO_SNDBUF`：
     - 级别：`SOL_SOCKET`
     - 作用：设置发送缓冲区的大小。通过设置发送缓冲区大小，可以影响发送数据的效率和性能。较大的发送缓冲区可以容纳更多的数据，适用于高速数据发送或者需要一次发送大量数据的场景。

这些选项可以通过 `setsockopt()` 函数来设置。根据具体的需求，选择适当的选项和设置合适的参数值，以达到所需的网络通信效果和性能要求。

-----------------

* 设置延迟关闭

```cpp
struct linger lfd_linger;
ret = setsockopt(listen_fd, SOL_SOCKET, SO_LINGER, &lfd_linger,sizeof(lfd_linger))
```

* 设置端口复用

```cpp
int optval = 1;
ret = setsockopt(listenFd_, SOL_SOCKET, SO_REUSEADDR, (const void *)&optval, sizeof(int));
```



### 8.3.2 网络字节序

* 电脑： 小端法

高位存高地址、低位存低地址

`int a = 0x12345678`

![image-20230429174045286](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230429174045286.png)

  

* 网络：大端法

高位存低地址，地位存高地址

 ```
 // 转换函数（host->net ）(传入2进制)
 htonl   本地->网络 (IP)32位 //不用
 htons   本地->网络(port)16位
 ntohl   网络->本地(IP)32位  // 不用
 ntohs   网络->本地(port)16位
 ```

```
192.168.11.12(点分十进制，string)-> atoi ->int类型 -> htonl -> 网络数据流
// 过于麻烦
inet_pton函数： 直接将主机stringip转为网络2进制ip
inet_ntop函数： 直接将网络2进制ip转为 主机stringip
```

```
// man inet_pton
int inet_pton(int af, const char *src, void *dst);
  af :AF_INET or AF_INET6 
  src:"192.168.11.12"主机字节序的ip
  dst:大端法写的二进制地址，定义int dst，使用强转void*
  返回值：1 成功； 0 异常； -1 失败

// 例子
inet_pton(AF_INET, "192.168.11.12",addr_server.sin_addr.s_addr);
```

```
// man inet_ntop
const char *inet_ntop(int af, const void *src,char *dst, socklen_t size);
	af :AF_INET or AF_INET6 
	src:网络字节序的ip
	det:本地字节序
	size：det大小
	返回值：det：成功； NULL 失败
	
// 例子
char clientIP[1024];
inet_ntop(AF_INET,&addr_client.sin_addr.s_addr,clientIP,sizeof(clientIP))
```



### 8.3.3 struct sockaddr

* 结构体地址（IP+port）

![image-20230509125124662](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230509125124662.png)

```
// 常用sockaddr_in类型，但是接口早已定好，因此，用的时候需要强转类型
struct sockaddr_in addr;
bind(fd, (strcut sockaddr *)&addr,size)
```

```cpp
// man 7 ip  查看 struct sockaddr_in 结构
struct sockaddr_in {
               sa_family_t    sin_family; // AF_INET  AF_INET 6  -->ipv4 ipv6
               in_port_t      sin_port;   // 存放网络字节序 port(htons转换)*/
               struct in_addr sin_addr;    //  存放网络字节序ip(inet_pton获得)
           };

/* Internet address. */
struct in_addr {
   uint32_t       s_addr;     /* 网络字节序 ip */
};
```

```cpp
// 例子
struct sockaddr_in addr;

// 初始化结构体
addr.sin_family = AF_INET;
addr.sin_port = htons(9527);
// 法1
inet_pton(AF_INET, "192.168.11.12", addr.sin_addr.s_addr)
// 法2
addr.sin_addr.s_addr = htonl(INADDR_ANY) // 宏INADDR_ANY：取出系统中所有有效的任意IP地址，[2进制类型]，用htonl转为网络字节序

bind(fd, (strcut sockaddr *)&addr,size)
```

### 8.3.4 socket模型

![image-20230703174141597](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230703174141597.png)



<img src="https://cdn.xiaolincoding.com//mysql/other/format,png-20230309230545997.png" alt="基于 TCP 协议的客户端和服务端工作" style="zoom:50%;" />

- 服务端和客户端初始化 `socket`，得到文件描述符；
- 服务端调用 `bind`，将 socket 绑定在指定的 IP 地址和端口;
- 服务端调用 `listen`，进行监听；
- 服务端调用 `accept`，等待客户端连接；
- 客户端调用 `connect`，向服务端的地址和端口发起连接请求；
- 服务端 `accept` 返回用于传输的 `socket` 的文件描述符；
- 客户端调用 `write` 写入数据；服务端调用 `read` 读取数据；
- 客户端断开连接时，会调用 `close`，那么服务端 `read` 读取数据的时候，就会读取到了 `EOF`，待处理完数据后，服务端调用 `close`，表示连接关闭。

这里需要注意的是，服务端调用 `accept` 时，连接成功了会返回一个已完成连接的 socket，后续用来传输数据。

所以，监听的 socket 和真正用来传送数据的 socket，是「两个」 socket，一个叫作**监听 socket**，一个叫作**已完成连接 socket**。

成功连接建立之后，双方开始通过 read 和 write 函数来读写数据，就像往一个文件流里面写东西一样。

<img src="https://cdn.xiaolincoding.com/gh/xiaolincoder/ImageHost/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/TCP-%E5%8D%8A%E8%BF%9E%E6%8E%A5%E5%92%8C%E5%85%A8%E8%BF%9E%E6%8E%A5/3.jpg" alt="半连接队列与全连接队列" style="zoom:50%;" />

**没有accept也可以进行tcp连接**

accpet 系统调用并不参与 TCP 三次握手过程，它只是负责从 TCP 全连接队列取出一个已经建立连接的 socket，用户层通过 accpet 系统调用拿到了已经建立连接的 socket，就可以对该 socket 进行读写操作了。

```cpp
//man socktet
int socket(int domain, int type, int protocol);
	domain: AF_INET、AF_INET6、AF_UNIX // 创建ipv4 ir or  ipv6
	type:SOCK_STREAM、SOCK_DGRAM (数据流/数据报)
	protocol：0 （默认根据上方type选择   TCP/UDP）
	成功：文件描述符sockfd
	失败：-1 errno
//例
int conn_fd = socket(AF_INET,SOCK_STREAM,0); // 连接socket
```

```cpp
// man bind
int bind(int sockfd, const struct sockaddr *addr,socklen_t addrlen);// 长度直接sizeof
	sockfd:socket()的返回值
	addr：传入参数，结构体地址
	addrlen：sizeof(addr)
	返回值：成功 0 ； 
		  失败：-1；
	
// 例
struct sockaddr_in addr;

addr.som_family = AF_INET;
addr.sin_port = htons(9527);
addr.sin_addr.s_addr = htonl(INADDR_ANY)

bind(cfd, (strcut sockaddr *)&addr,sizeof(addr)) // 结构体大小固定，直接传值
```

```cpp
// man 2 listen设置同时进行3次握手的客户端数量
int listen(int sockfd, int backlog);
	sockfd:socket()的返回值
	backlog：上限数值，最大128
	返回值：成功0；
		   失败-1

// 例
int ret = listen(cfd,12);  
	
```

```cpp
// man 2 accept
int accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen);  // 长度单独定义
	sockfd:socket()的返回值
	addr：传出参数：与服务器建立连接的客户端的地址结构（ip+端口号）
	addrlen：传入：addr大小  出：addr的实际大小
	返回值：成功：能与服务器通信的socket的文件描述符 
		  失败：-1
	
// 例
// 定义客户端及长度
struct sockaddr_in addr;
socklen_t addrlen = sizeof(addr_clint);
int listen_fd = accept(fd, (struct sockaddr *)addr, &addrlen); // 传入传出长度，传入地址// 返回listen_socket
```

```cpp
// man 2 connect
int connect(int sockfd, const struct sockaddr *addr,socklen_t addrlen);
	sockfd:socket()的返回值
	addr:服务器的地址结构
	addrlen：sizeof(addr)

// 例
// 绑定服务器地址
struct sockaddr_in addr_server;
addr_server.sin_family = AF_INET;
addr_server.sin_port = htons(PORT_SERVER);
inet_pton(AF_INET, "172.16.108.62", &addr_server.sin_addr.s_addr); // 指出服务器地址，不能INADDR_ANY

// 连接服务器
int ret = connect(cfd, (const struct sockaddr *)&addr_server, sizeof(addr_server));
```

### 8.3.5 server—client

```c
// server
#include <stdio.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <netinet/ip.h>
#include <stdlib.h>
#include <unistd.h> //write(STDOUT_FILENO,buf,ret);
#include <errno.h>
#include <pthread.h>
#include <ctype.h>
#include <string.h>
#include <arpa/inet.h>
#define PORT_SERVER 9527
void sys_err(const char *str)
{
    perror(str);
    exit(1);
}

int main()
{
    // 1、套接字
    int sfd = 0;
    sfd = socket(AF_INET, SOCK_STREAM, 0);
    if (sfd == -1)
    {
        sys_err("socket error");
    }

    // 服务器地址结构
    struct sockaddr_in addr_server;
    addr_server.sin_family = AF_INET;
    addr_server.sin_port = htons(PORT_SERVER);
    addr_server.sin_addr.s_addr = htonl(INADDR_ANY); // 网络字节序、二进制
    // inet_pton(AF_INET, "172.16.108.62", &addr_server.sin_addr.s_addr); // 网络字节序、二进制

    // 2、绑定
    bind(sfd, (const struct sockaddr *)&addr_server, sizeof(addr_server));

    // 3、监听
    listen(sfd, 128);

    // 客户端地址结构，客户端访问服务器，系统自动填充信息
    struct sockaddr_in addr_clint;
    socklen_t addrlen_client = sizeof(addr_clint);

    // 4、接收客户端
    int cfd = 0;
    cfd = accept(sfd, (struct sockaddr *)&addr_clint, &addrlen_client);
    if (cfd == -1)
    {
        sys_err("accept error");
    }

    // 连接成功
    // 打印服务器的ip+port
    char serverIP[16];
    inet_ntop(AF_INET, &addr_server.sin_addr.s_addr, serverIP, sizeof(serverIP));
    unsigned short serverPort = ntohs(addr_server.sin_port);
    printf("server ip : %s ,port : %d \n", serverIP, serverPort);
    // 打印客户端信息
    char clientIP[16];
    inet_ntop(AF_INET, &addr_clint.sin_addr.s_addr, clientIP, sizeof(clientIP));
    unsigned short clientPort = ntohs(addr_clint.sin_port);
    printf("client ip : %s ,port : %d \n", clientIP, clientPort);

    // 读操作
    while (1)
    {
        // 读1次数据
        int num = 0;      // 读到的字节数
        char buf[BUFSIZ]; // 4096
        num = read(cfd, buf, sizeof(buf));
        if (num == -1)
        {
            perror("read");
            exit(-1);
        }
        else if (num > 0)
        {
            printf("recv client data : \n %s\n", buf);
        }
        else if (num == 0)
        {
            printf("client closed..");
            break;
        }

        // 写1次数据
        char *data = " hello i am server....\n";
        write(cfd, data, strlen(data));
    }
    close(sfd);
    close(cfd);

    return 0;
}
```

```c
// client
#include <stdio.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <netinet/ip.h>
#include <stdlib.h>
#include <unistd.h> //write(STDOUT_FILENO,buf,ret);
#include <errno.h>
#include <pthread.h>
#include <ctype.h>
#include <string.h>
#include <arpa/inet.h>
#define PORT_SERVER 9527
void sys_err(const char *str)
{
    perror(str);
    exit(1);
}

int main()
{
    // 1、套接字
    int cfd = 0;
    cfd = socket(AF_INET, SOCK_STREAM, 0);
    if (cfd == -1)
    {
        sys_err("socket error");
    }
    
	// 2、绑定客户端地址（系统隐式绑定，无需操作）
    
    // 服务器地址
    struct sockaddr_in addr_server;
    addr_server.sin_family = AF_INET;
    addr_server.sin_port = htons(PORT_SERVER);
    inet_pton(AF_INET, "172.16.108.62", &addr_server.sin_addr.s_addr); // 指出服务器地址，不能INADDR_ANY

    // 2、连接服务器
    int ret = connect(cfd, (const struct sockaddr *)&addr_server, sizeof(addr_server));
    if (ret == -1)
    {
        perror("connect");
        exit(-1);
    }

    // 通讯
    while (1)
    {
        // 写3次数据                                  // 写三次的时候，时间间隔2s，服务器，读1次，写一些，读完3次，管道内写有3条数据
        char *data = "i am client";                 // 若写的时间过快，则服务器一次性全部读出3条数据
        for (int i = 0; i < 3; i++)
        {
            write(cfd, data, strlen(data));
            sleep(2);
        }

        // 读1次数据                                 // 管道内含有3条数据，1次读出全部3条数据
        char recvBuf[1024];
        int len = read(cfd, recvBuf, sizeof(recvBuf));
        if (len == -1)
        {
            perror("read");
            exit(-1);
        }
        else if (len > 0)
        {
            printf("receive data is: %s \n", recvBuf);
        }
        else if (len == 0)
        {
            printf("server closed...");
            break;
        }
        sleep(5);
    }
    close(cfd);

    return 0;
}
```

### 8.3.6 端口复用

```cpp
// bind之前
int optval = 1;
setsockopt(lfd, SOL_SOCKET,SO_REUSEPORT,&optval, sizeof(optval));
```



## 8.4 客户端--bind

很多人觉得只有服务器程序可以调用 bind 函数绑定一个端口号，其实不然，在一些特殊的应用中，我们需要客户端程序以指定的端口号去连接服务器，此时我们就可以在客户端程序中调用 bind 函数绑定一个具体的端口。

1. socket后不绑定bind

   默认客户端端口由系统随机分配

2. 绑定bind，port=0

   端口号仍然是系统随机分配的，也就是说绑定 **0** 号端口和没有绑定效果是一样的

3. 绑定bind，port=固定端口

   **client** 进程确实使用 固定端口连接到 **server** 进程上去了

   这个时候如果我们再开启一个 **client** 进程，我们猜想由于端口号已经被占用，新启动的 **client** 会由于调用 **bind** 函数出错而退出

   

## 8.5 异步connect

在 socket 是阻塞模式下 connect 函数会一直到有明确的结果才会返回（或连接成功或连接失败），如果服务器地址“较远”，连接速度比较慢，connect 函数在连接过程中可能会导致程序阻塞在 connect 函数处好一会儿（如两三秒之久），虽然这一般也不会对依赖于网络通信的程序造成什么影响，但在实际项目中，我们一般倾向使用所谓的**异步的 connect** 技术，或者叫**非阻塞的 connect**。这个流程一般有如下步骤：

```
1. 创建socket，并将 socket 设置成非阻塞模式；
2. 调用 connect 函数，此时无论 connect 函数是否连接成功会立即返回；如果返回-1并不表示连接出错，如果此时错误码是EINPROGRESS
3. 接着调用 select 函数，在指定的时间内判断该 socket 是否可写，如果可写说明连接成功，反之则认为连接失败。
```

按上述流程编写代码如下：

```cpp
/**
 * 异步的connect写法，nonblocking_connect.cpp
 * zhangyl 2018.12.17
 */
#include <sys/types.h> 
#include <sys/socket.h>
#include <arpa/inet.h>
#include <unistd.h>
#include <iostream>
#include <string.h>
#include <stdio.h>
#include <fcntl.h>
#include <errno.h>

#define SERVER_ADDRESS "127.0.0.1"
#define SERVER_PORT     3000
#define SEND_DATA       "helloworld"

int main(int argc, char* argv[])
{
    //1.创建一个socket
    int clientfd = socket(AF_INET, SOCK_STREAM, 0);
    if (clientfd == -1)
    {
        std::cout << "create client socket error." << std::endl;
        return -1;
    }

    //============连接成功以后，我们再将 clientfd 设置成非阻塞模式，=============
    //不能在创建时就设置，这样会影响到 connect 函数的行为
    int oldSocketFlag = fcntl(clientfd, F_GETFL, 0);
    int newSocketFlag = oldSocketFlag | O_NONBLOCK;
    if (fcntl(clientfd, F_SETFL,  newSocketFlag) == -1)
    {
        close(clientfd);
        std::cout << "set socket to nonblock error." << std::endl;
        return -1;
    }

    //2.连接服务器
    struct sockaddr_in serveraddr;
    serveraddr.sin_family = AF_INET;
    serveraddr.sin_addr.s_addr = inet_addr(SERVER_ADDRESS);
    serveraddr.sin_port = htons(SERVER_PORT);
    for (;;)
    {
        // ====================判断出错情况======================
        int ret = connect(clientfd, (struct sockaddr *)&serveraddr, sizeof(serveraddr));
        if (ret == 0)
        {
            std::cout << "connect to server successfully." << std::endl;
            close(clientfd);
            return 0;
        } 
        else if (ret == -1) 
        {
            if (errno == EINTR)
            {
                //connect 动作被信号中断，重试connect
                std::cout << "connecting interruptted by signal, try again." << std::endl;
                continue;
            } else if (errno == EINPROGRESS)
            {
                //连接正在尝试中
                break;
            } else {
                //真的出错了，
                close(clientfd);
                return -1;
            }
        }
    }

   // 执行操作

    //5. 关闭socket
    close(clientfd);

    return 0;
}
```

## 8.5 nc命令

```cpp
[root@localhost testsocket]# nc -v -p 9999 127.0.0.1 3000
Ncat: Version 6.40 ( http://nmap.org/ncat )
Ncat: Connected to 127.0.0.1:3000.
....
                    
```

**-v** 选项表示输出 **nc** 命令连接的详细信息，这里连接成功以后，会输出“**Ncat: Connected to 127.0.0.1:3000.**” 提示已经连接到服务器的 **3000** 端口上去了。

**-p** 选项的参数值是 **9999** 表示，我们要求 **nc** 命令本地以端口号 **9999** 连接服务器，注意不要与端口号 **3000** 混淆，**3000** 是服务器的侦听端口号，也就是我们的连接的目标端口号，**9999** 是我们客户端使用的端口号。我们用 **lsof** 命令来验证一下我们的 **nc** 命令是否确实以 **9999** 端口号连接到 **server** 进程上去了。








## 8.6 三握四挥

![image-20230510171103222](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230510171103222.png)

### 8.4.1 tcp数据报

![image-20230510172554005](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230510172554005.png)

* SYN标志位：建立连接----用于三次握手
* ACK标志位：收到了xx之前所有的。----用于每一次通信
* FIN标志位： 断开连接

### 8.4.2 三次握手

![image-20230510182030114](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230510182030114.png)

* 客户端发起--SYN--1000号的数据报
* 服务器--ACK收到1001号前的所有报，发起SYN确认报8000
* 客户端收到，发起ACK确认收到8001前所有报

宏观代码上看： accept()与connect() 成功执行 == 三次挥手建立完成

### 8.4.3 四次挥手

![image-20230510182239046](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230510182239046.png)



* 客户端发起FIN断开连接，服务器ACK响应，完成一次半关闭---> 客户端的写缓冲断开，只能接受，不能发送

![image-20230510185522507](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230510185522507.png)

* 服务器发起FIN断开连接，客户端ACK响应，完成全关闭----> 服务器写缓冲关闭

# 9 多并发服务器

![image-20230516163054818](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230516163054818.png)

```cpp
#include <stdio.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <netinet/ip.h>
#include <stdlib.h>
#include <unistd.h> //write(STDOUT_FILENO,buf,ret);
#include <errno.h>
#include <pthread.h>
#include <ctype.h>
#include <string.h>
#include <arpa/inet.h>
#include <signal.h>
#include <sys/wait.h>

#define PORT_SERVER 9527
void sys_err(const char *str)
{
    perror(str);
    exit(1);
}
void catch_child(int signo)
{
    pid_t wpid;
    while ((wpid = waitpid(-1, NULL, WNOHANG)) != -1)
    {
        printf("-------------catch child id %d -------------\n", wpid);

        return;
    }
}

int main()
{
    // 1、套接字
    int sfd = 0;
    conn_fd = socket(AF_INET, SOCK_STREAM, 0);
    if (sfd == -1)
    {
        sys_err("socket error");
    }

    // 服务器地址结构
    struct sockaddr_in addr_server;
    bzero(&addr_server, sizeof(addr_server)); // 地址结构清零

    addr_server.sin_family = AF_INET;
    addr_server.sin_port = htons(PORT_SERVER);
    addr_server.sin_addr.s_addr = htonl(INADDR_ANY); // 网络字节序、二进制
    // inet_pton(AF_INET, "172.16.108.62", &addr_server.sin_addr.s_addr); // 网络字节序、二进制

    // 2、绑定
    bind(sfd, (const struct sockaddr *)&addr_server, sizeof(addr_server));

    // 3、设置监听参数,阻塞
    listen(sfd, 128);

    // 服务器地址
    struct sockaddr_in addr_clint;
    socklen_t addrlen_client = sizeof(addr_clint);

    // 设置阻塞
    sigset_t set;
    sigemptyset(&set);
    sigaddset(&set, SIGCHLD);

    sigprocmask(SIG_BLOCK, &set, NULL);

    pid_t pid;
    int cfd = 0;
    int ret;
    char buf[BUFSIZ];
    while (1)
    {
        // 4、接收客户端,获取客户端IP+port
        lisfd = accept(sfd, (struct sockaddr *)&addr_clint, &addrlen_client);
        char clientIP[16];
        inet_ntop(AF_INET, &addr_clint.sin_addr.s_addr, clientIP, sizeof(clientIP));
        unsigned short clientPort = ntohs(addr_clint.sin_port);
        if (cfd == -1)
        {
            sys_err("accept error");
        }

        pid = fork();
        if (pid == 0)
        {
            // 子进程
            close(sfd);

            printf("client ip : %s ,port : %d \n", clientIP, clientPort);

            break;
        }
        else if (pid > 0)
        {
            // 父进程
            close(cfd);

            struct sigaction act;

            act.sa_handler = catch_child; // 设置回调函数
            sigemptyset(&act.sa_mask);    // 设置捕捉期间信号屏蔽字
            act.sa_flags = SA_RESTART;    // 解决慢速系统调用

            sigaction(SIGCHLD, &act, NULL); // 注册捕捉信号函数

            // 2、解除屏蔽，处理子进程结束信号
            sigprocmask(SIG_UNBLOCK, &set, NULL);
            continue;
        }
    }
    if (pid == 0)
    {
        while (1)
        {
            ret = read(cfd, buf, sizeof(buf));
            if (ret == 0)
            {
                close(cfd);
                exit(1);
            }

            // 1、打印客户端地址
            char clientIP[16];
            inet_ntop(AF_INET, &addr_clint.sin_addr.s_addr, clientIP, sizeof(clientIP));
            unsigned short clientPort = ntohs(addr_clint.sin_port);
            printf("client ip : %s ,port : %d \n", clientIP, clientPort);
            // 2、打印客户端读取的内容
            write(STDOUT_FILENO, buf, ret);

            for (int i = 0; i < ret; i++)
            {
                buf[i] = toupper(buf[i]);
            }

            write(cfd, buf, ret);
        }
    }

    return 0;
}

```

# 10 进程组和会话 

## 1 进程组

1、 组长进程可以创建一个进程组，且pgid = pid

2、只要进程组中有一个进程存在，进程组就存在，与组长进程是否终止无关。

## 2 会话

1. 调用进程不能是进程组组长，该进程变成新会话首进程(session header)

2. 会长的 pid = pgid = sid

3. 新会话丢弃原有的控制终端，该会话没有控制终端 (运行在后端)

4. 建立新会话时，先调用fork, 父进程终止，子进程调用setsid

## 3 守护进程

守护进程（Daemon）是在操作系统后台运行的一种特殊类型的进程，它独立于终端并没有与之关联的控制终端。守护进程的作用是在系统启动时启动并一直运行，提供一种持续性的服务。

下面是守护进程的几个主要作用：

1. 后台服务：守护进程通常用于提供后台服务，例如网络服务（如Web服务器、FTP服务器、DNS服务器）、数据库服务、邮件服务等。它们在系统启动时自动启动，一直运行在后台，等待来自其他程序或网络的请求，并提供相应的功能和服务。
2. 无人值守任务：守护进程经常用于执行无人值守任务，这些任务可以在没有用户交互的情况下运行。例如，系统备份、日志记录、定时任务等。通过将这些任务作为守护进程运行，可以确保它们在系统启动后一直运行，并按计划或需要执行任务。
3. 资源管理：守护进程还可以负责系统资源的管理和分配。例如，操作系统中的内存管理守护进程可以监控和管理系统内存的分配和释放，确保系统中的各个进程能够正常运行并使用适当的资源。
4. 监控和恢复：守护进程可以监控其他进程或系统状态，并在必要时采取措施进行恢复。例如，监控进程可能会检测到某个关键进程崩溃或系统资源不足的情况，然后采取相应的措施，如重新启动进程、清理资源等，以保持系统的稳定性和可靠性。

总之，守护进程在操作系统中扮演着重要角色，它们作为后台服务运行，提供持续性的服务、无人值守任务、资源管理和监控恢复等功能，使系统能够在长时间运行期间保持稳定和可靠。

### 4 创建守护进程

```cpp
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <sys/stat.h>
#include <stdlib.h>

int main()
{
    pid_t pid;
    pid = fork();
    if (pid > 0)
        exit(0); // 1 父进程终止

    pid = setsid(); // 子进程创建会话
    if (pid == -1)
        perror("setsid error");

    int ret, fd;
    ret = chdir("/home/zhang/Daemon"); // 2 改变工作目录
    if (ret == -1)
        perror("chdir error");

    umask(0022); // 3 改变文件访问权限掩码

    close(STDIN_FILENO);            // 4 关闭0号fd，重定向到/dev/null
    fd = open("/dev/null", O_RDWR); // fd-->0
    if (pid == -1)
        perror("open error");

    dup2(fd, STDOUT_FILENO); // 1号2号重定向
    dup2(fd, STDERR_FILENO);

    while (1)
        ; // 5 模拟守护进程业务

    return 0;
}
```

```
    PPID   PID  PGID   SID TTY      TPGID STAT   UID   TIME COMMAND
   1 26911 26911 26911 ?           -1 Rs       0   0:24 ./creat
```

```
通过 
kill -9 
结束会话进程
```

## 4 线程

进程和线程的创建，底层都是调用clone机制，复制pcb



进程：独立地址空间(0~4G)，拥有PCB 

​			pcb复制父进程pcb，但是其中的《描述虚拟地址的空间信息》指针不同，因此，进程拥有独立的内存空间

线程：有独立的PCB

​			pcb复制进程，但是《描述虚拟地址的空间信息》指针相同，指向同一个三级页表

​			因此，没有独立空间



Linux下：  线程：最小的执行单位

​                   进程：最小分配资源单位，可看成是只有一个线程的进程。

```
ps -Lf pid// 查看同一进程下不同线程的线程号
```

![image-20230519184234342](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230519184234342.png)

线程下：

线程id：在进程内部区分线程

线程号：（轻量级进程LWP）给cpu用以划分时间轮片

#### 4.1 共享资源

​     1.文件描述符表 

​     2.每种信号的处理方式 

​     3.当前工作目录

​     4.用户ID和组ID

​     5.内存地址空间 (.text/.data/.bss/heap/共享库)

#### 4.2 非共享资源

​     1.线程id

​     2.处理器现场和栈指针(内核栈)

​     3.独立的栈空间(用户空间栈)

​     4.errno变量

​     5.信号屏蔽字

​     6.调度优先级 



## 5 线程控制函数

```
// linux 指令
// 编译线程时候，需要添加链接库
gcc more_pthread -o pth -pthread
```

```cpp
// 子线程（回调函数）
void *tfn(void *arg){
    printf("thread: pid:%d, tid: %d \n", getpid(),pthread_self());
	return NULL;
}

// 主线程
int main(){
    pthread_t = tid;
    int ret = pthread_create(&tid,NULL,tfn,NULL);
    if(ret !=0){
        perror("create error");
	}
    sleep(1);
    return 0;
        
}

```

```cpp
1、创建线程
pthread_t = tid; // 返回线程id
int ret = pthread_create(&tid,NULL,tfn,NULL); // 创建成功为0, tfn为线程回调函数，执行子线程的内容
	参数1：传出参数，保存系统为我们分配好的线程ID
	参数2：通常传NULL，表示使用线程默认属性。若想使用具体属性也可以修改该参数。
	参数3：函数指针，指向线程主函数(线程体)，该函数运行结束，则线程结束。
	参数4：回调函数执行期间所使用的参数。（传入参数强转(void *)(intptr_t) i）
        为保证 整数<-->指针 互相转换时候精度不丢失，int -> intptr_t -> void *
2、子线程回调函数
void *tfn(void *arg){ return NULL;}

// 接收void * arg
// 使用 intptr_t i = (intptr_t) arg 强转为int类型 ,用 %d 接收

tfn 是一个函数，它接受一个指向未指定类型的数据的指针 arg，并返回一个指向未指定类型的数据的指针。

void* 类型作为函数的参数和返回类型，通常用于处理不同类型的指针或在函数之间传递通用的指针。
    
由于 void* 是一种无类型指针，它可以接受任何类型的指针，并且在函数内部可以使用类型转换操作将其转换为特定类型的指针进行操作。

2、查看线程id
pthread_self()
// 返回 pthread_t 类型，一般为无符号长整数
// 用 %lu 接收
// pid_t为 int类型，用%d 接收
```

 #### 5.1 循环创立子线程

```cpp
#include <stdio.h>
#include <pthread.h>
#include <sys/types.h>
#include <unistd.h>

void *t_fun(void *arg)
{

    intptr_t num = (intptr_t)arg;
    sleep(num); 				// 子线程按顺序输出
    printf("id: %ld ,pid: %d ,tid: %lu \n", num + 1, getpid(), pthread_self());

    return NULL;
}

int main()
{

    int ret, i;
    pthread_t tid;

    for (i = 0; i < 5; i++)
    {
        ret = pthread_create(&tid, NULL, t_fun, (void *)(intptr_t)i);
    }

    printf("i am father thread, pid: %d \n", getpid());
    
    //sleep(i);  // 等待子线程结束，主线程结束/主进程结束
    //return 0;
    pthread_exit((void*)0);
}
```

#### 5.2 退出线程

```
exit(0): 退出进程
return 
return 0; 
return NULL; : 结束线程/结束函数，返回到主函数
```

```
// 结束当前线程
pthread_exit((void*)0);
```

#### 5.3 回收指定线程

```cpp
int pthread_join(pthread_t thread, void **retval);
参数1：指定收回的线程id
参数2：用于保存子线程回调函数的返回值，为void**类型，retval为一级指针的地址
```



```cpp
#include <stdio.h>
#include <pthread.h>
#include <string.h>
#include <stdlib.h>

struct thrd
{
    int var;
    char str[256];
};

void *pfun(void *arg)
{
    struct thrd *tp = malloc(sizeof(tp));
    tp->var = 521;
    strcpy(tp->str, "hello world");

    return (void *)tp;
}

int main()
{
    int ret;
    pthread_t tid;
    // 创建线程
    ret = pthread_create(&tid, NULL, pfun, NULL);

    // 回收子线程，返回值保存在tp2指针内
    struct thrd *tp2;
    pthread_join(tid, (void **)&tp2);

    printf("child thread exit with var = %d, str = %s\n", tp2->var, tp2->str);

    pthread_exit((void *)0);
}
```

---------

```cpp
// 循环回收子进程
#include <stdio.h>
#include <pthread.h>
#include <sys/types.h>
#include <unistd.h>

void *t_fun(void *arg)
{

    intptr_t num = (intptr_t)arg;
    sleep(num);
    printf("id: %ld ,pid: %d ,tid: %lu \n", num + 1, getpid(), pthread_self());

    return NULL;
}

int main()
{

    int ret, i, j;
    pthread_t tid[5];

    for (i = 0; i < 5; i++)
    {
        ret = pthread_create(&tid[i], NULL, t_fun, (void *)(intptr_t)i);
    }
    for (j = 0; j < 5; j++)
    {
        pthread_join(tid[j], NULL);
        printf("exit %d \n", (int)tid[j]);
    }

    printf("i am father thread, pid: %d \n", getpid());
    pthread_exit((void *)0);
}
```

#### 5.4 杀死线程

```cpp
// 方法
// 子线程自身设置
1、return NULL;
2、exit(0);


// 主线程设置
3、pthread_exit((void *)0)
4、 pthread_testcancel(); // 子线程设置  
    pthread_cancel(tid);
// 系统调用，进内核处理
// 若无契机进入内核，手动添加取消点

```

# 11 线程同步

## 0 同步和异步

1. 线程间同步：
   - 线程间同步是指多个线程之间协调和同步它们的执行顺序或共享资源的访问，以确保数据的一致性和避免竞态条件等问题。
   - 通过使用同步机制（如互斥锁、条件变量、信号量等），线程可以相互通信、同步和协作，以保证数据的正确性和可靠性。
   - 线程间同步的目的是在多线程环境中实现有序、安全的操作，以避免数据竞争和不确定性的结果。

2. 主线程和子线程之间的异步操作：
   - 主线程可以启动一个或多个子线程，子线程可以在后台执行一些耗时的任务，而主线程可以继续执行其他任务或响应用户操作，而不需要等待子线程完成。

     
   

​	3.多个子线程之间的异步操作：在多线程环境下，不同的子线程可以并发执行各自的任务，它们之间可以独立地执行，互不影响。


​	4.异步回调：一个线程可以发起某个操作，并在该操作完成后，通过回调机制通知其他线程。这样，发起操作的线程不需要等待操作完成，可以继续执行其他任务。



同步关注的是多线程环境下的数据同步和协作，确保数据的正确性。

异步操作关注的是任务的并行执行，提高程序的性能和并发能力。



## 1 互斥锁mutex

```cpp
// 创建互斥锁  ----定义在头文件下面，所有函数之前
pthread_mutex_t mutex;    pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;
// 初始化     -----在创建线程之前初始化好
pthread_mutex_init(&mutex,NULL); 
// 上锁      ------线程访问共享资源之前上锁
pthread_mutex_lock(&mutex);
// 解锁      -------线程结束访问后+++立刻++++解锁，注意防止一个线程一直占用锁
pthread_mutex_unlock(&mutex);
// 销毁      ------所有线程结束后，销毁
pthread_mutex_destroy(&mutex);
```

##  2 独占锁


在常见的多线程编程中，"互斥锁"（Mutex）和"独占锁"（Exclusive Lock）可以用来实现对共享资源的互斥访问，但它们有一些区别：

1. 概念：
   - 互斥锁：互斥锁是一种同步原语，用于确保在给定时间只有一个线程可以访问共享资源。线程在访问共享资源之前会请求互斥锁，如果锁已经被其他线程持有，则线程将被阻塞，直到获得锁为止。
   - 独占锁：独占锁是一种特定类型的互斥锁，它保证在给定时间只有一个线程可以持有锁。线程在持有独占锁期间具有对共享资源的独占访问权。
2. 用途：
   - 互斥锁：用于保护共享资源，确保同时只有一个线程可以访问该资源，从而避免竞态条件（Race Condition）和数据不一致问题。
   - 独占锁：通常是指针对特定的资源或代码段进行独占访问，以确保在给定时间只有一个线程可以执行该代码段或访问该资源。
3. 并发性：
   - 互斥锁：多个线程可以竞争同一个互斥锁，但只有一个线程能够获得锁，其他线程会被阻塞。当持有锁的线程释放锁时，其他线程可以竞争获得锁。
   - 独占锁：在给定时间内，只有一个线程可以获得独占锁。其他线程如果请求独占锁，则会被阻塞，直到持有锁的线程释放锁。
4. 灵活性：
   - 互斥锁：互斥锁可以被多个线程轮流获取和释放，不要求持有锁的线程必须是同一个线程，可以实现线程间的同步和互斥。
   - 独占锁：独占锁一般由特定的线程获取，并且只有该线程能够释放锁，以确保特定的代码段或资源在给定时间内只有一个线程可以访问。

总结来说，互斥锁用于保护共享资源的访问，确保同一时间只有一个线程可以访问该资源。而独占锁是互斥锁的一种特定类型，用于确保在给定时间内只有一个线程可以持有锁，并独占访问某个代码段或资源

## 3 死锁

两种情况：

* 一个线程，对同一个锁重复lock
* 两个线程，各自持有一把，请求另一把

```cpp
// 第二种死锁
#include <stdio.h>
#include <pthread.h>
#include <unistd.h>

pthread_mutex_t mutex1;
pthread_mutex_t mutex2;

void *t1_fun(void *arg)
{
    pthread_mutex_lock(&mutex1);
    printf("Thread 1 acquired mutex1\n");
    sleep(2);
    pthread_mutex_lock(&mutex2);
    printf("Thread 1 acquired mutex2\n");

    // 释放锁
    pthread_mutex_unlock(&mutex2);
    pthread_mutex_unlock(&mutex1);
    return NULL;
}
void *t2_fun(void *arg)
{
    // 线程2先获取mutex2，然后尝试获取mutex1
    pthread_mutex_lock(&mutex2);
    printf("Thread 2 acquired mutex2\n");

    sleep(2); // 模拟一些处理时间

    pthread_mutex_lock(&mutex1);
    printf("Thread 2 acquired mutex1\n");

    // 释放锁
    pthread_mutex_unlock(&mutex1);
    pthread_mutex_unlock(&mutex2);
    return NULL;
}

int main()
{
    pthread_mutex_init(&mutex1, NULL);
    pthread_mutex_init(&mutex2, NULL);
    // 创建两个线程
    pthread_t tid1, tid2;
    pthread_create(&tid1, NULL, t1_fun, NULL);
    pthread_create(&tid2, NULL, t2_fun, NULL);

    // 回收
    pthread_join(tid1, NULL);
    pthread_join(tid2, NULL);

    pthread_mutex_destroy(&mutex1);
    pthread_mutex_destroy(&mutex2);
    printf("main....\n");

    pthread_exit((void *)0);
}
```

## 4 读写锁wrlock

* 当读线程多的时候，提高访问效率

```cpp
// 读共享，写独占，读写排队写在前
// 1、r-lock   rr  -->rrr共享
// 2、r-lock   rrw  -->阻塞，r-unlock w-lock,阻塞，w-unlock,rr共享
```

```cpp
// 创建互斥锁  ----定义在头文件下面，所有函数之前
pthread_rwlock_t lock;   pthread_rwlock_t rwlock = PTHREAD_RWLOCK_INITIALIZER;
// 初始化（动态）     -----在创建线程之前初始化好
pthread_rwlock_init(&wrlock,NULL); 
//（静态）--直接man pthread_rwlock_init查

// 上读锁      ------线程访问共享资源之前上锁
pthread_rwlock_rlock(&rwlock);
// 上写锁      ------线程访问共享资源之前上锁
pthread_rwlock_wlock(&rwlock);
// 解锁      -------线程结束访问后+++立刻++++解锁，注意防止一个线程一直占用锁
pthread_rwlock_unlock(&rwlock);
// 销毁      ------所有线程结束后，销毁
pthread_rwlock_destroy(&rwlock);
```

## 5 共享锁

共享锁（Shared Lock）和读写锁（Read-Write Lock）是用于多线程环境下的锁机制，用于实现对共享资源的访问控制。它们有以下区别：

1. 访问模式：
   - 共享锁：多个线程可以同时持有共享锁并访问共享资源。共享锁用于读取共享资源，多个线程可以同时读取，互不干扰。
   - 读写锁：与共享锁类似，多个线程可以同时持有读锁并读取共享资源。但当有线程持有写锁时，其他线程无法获取读锁或写锁，写锁具有排他性，用于修改共享资源。
2. 写锁特性：
   - 共享锁：没有写锁的概念，共享锁之间是相互兼容的，可以共存。
   - 读写锁：写锁是排他的，当一个线程持有写锁时，其他线程无法获取读锁或写锁。这是为了确保在修改共享资源时的互斥性。
3. 冲突：
   - 共享锁：共享锁与共享锁之间没有冲突，可以并发持有。
   - 读写锁：写锁与任何其他锁（读锁或写锁）之间存在冲突，即写锁是互斥的。这是为了保证写操作的原子性和一致性。
4. 性能：
   - 共享锁：适用于读多写少的场景，多个线程可以同时读取共享资源，提高并发性能。
   - 读写锁：适用于读写频繁的场景，写操作会独占资源，但读操作可以并发进行，提高读操作的并发性能。

综上所述，共享锁适用于读多写少的场景，多个线程可以同时读取共享资源，互不干扰。而读写锁适用于读写频繁的场景，读操作可以并发进行，但写操作需要互斥执行，以保证数据的一致性。选择合适的锁机制取决于具体的并发访问模式和性能需求

## 6 条件变量

![image-20230523154305743](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230523154305743.png)

```
一般的互斥锁
上锁--执行--解锁
问题： 执行过程中，因为缺少某些条件无法执行，一直阻塞无法解锁

条件变量
上锁--执行--{wait（缺少条件，则解锁，让给其他程序执行，阻塞等待条件）--条件满足，signal发送信号--重新上锁，执行}---执行完毕解锁
```

```cpp
// 全局定义
pthread_cond_t cond = PTHREAD_COND_INITIALIZER;

// 阻塞
while( 条件不满足){
    pthread_cond_wait(&cond, &mutex);
}

// 唤醒1个
pthread_cond_signal(&cond);
// 唤醒所有阻塞线程
pthread_cond_broadcast(&cond);
```

在生产者消费者模型中，条件变量的使用是为了实现线程间的协调和同步。虽然在互斥锁之前判断条件是否存在看起来是一种简单的解决方案，但这种方法存在一些问题，其中最主要的问题是**竞态条件（race condition）**的产生。

竞态条件是指多个线程在访问共享资源时，由于执行顺序的不确定性而导致的问题。在生产者消费者模型中，如果不使用条件变量，而是在互斥锁之前判断条件是否存在，可能会导致以下情况发生：

1. 虚假唤醒（spurious wakeup）：即使条件没有满足，也可能会发生线程被唤醒的情况。这是由于线程被唤醒的原因不仅仅是其他线程的信号，还可能是由于操作系统的调度或其他内部因素导致的。这会导致线程在没有实际工作可做时被唤醒，从而浪费系统资源和时间。
2. 竞态条件：在没有条件变量的情况下，生产者线程在获取互斥锁后可能会判断条件并发现条件不满足，于是释放锁并进入等待状态。但在此期间，消费者线程也可能获取到互斥锁，消费掉了数据，然后再释放锁。如果此时生产者线程被唤醒，它会假设条件已满足，但实际上数据已被消费，导致错误的操作。

综上所述，使用条件变量是为了解决上述问题。条件变量提供了一种线程间的通信机制，允许线程在等待某个条件满足时进入等待状态，并且只有当条件满足时才会被唤醒。通过使用条件变量，生产者可以在生产数据后发出信号，通知消费者线程有数据可用，消费者线程在消费完数据后发出信号，通知生产者线程有空闲缓冲区可用。这样可以避免虚假唤醒和竞态条件的问题，确保线程在正确的时间进行等待和唤醒。

总结起来，使用条件变量可以更可靠地控制线程间的同步和通信，避免了竞态条件和虚假唤醒的问题，保证了生产者和消费者线程在正确的时间进行等待和唤醒操作。

## 7 生产者消费者模型

```cpp
#include <stdio.h>
#include <pthread.h>
#include <stdlib.h>
#include <unistd.h>

// 共享区域
struct msg
{
    int num;
    struct msg *next;
};
// 定义头指针
struct msg *head = NULL;

// 互斥锁、条件变量
pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;
pthread_cond_t cond = PTHREAD_COND_INITIALIZER;

void *producer(void *arg)
{
    while (1)
    {
        // 模拟生产数据(创建一个结点)
        struct msg *mp = malloc(sizeof(struct msg));
        mp->num = rand() % 1000 + 1;
        printf("-----producer-----%d\n", mp->num);

        pthread_mutex_lock(&mutex);
        mp->next = head; // 加入链表（模拟放入共享区域）
        head = mp;
        pthread_mutex_unlock(&mutex);

        pthread_cond_signal(&cond); // 发送信号，条件满足

        sleep(rand() % 3);
    }
    return NULL;
}
void *consumer(void *arg)
{
    while (1)
    {
        struct msg *mp = malloc(sizeof(struct msg));

        pthread_mutex_lock(&mutex);
        // while() 在多个消费者存在时，避免  上锁-条件阻塞、条件解锁-条件满足、条件上锁（可能被别人用，期间消费了条件）-执行（此时条件又不满足）  因此，要循环判断条件是否满足
        while (head == NULL)		
        {
            pthread_cond_wait(&cond, &mutex); // 若条件不满足，则wait等待
        }
        mp = head; // 摘走节点（模拟消费）
        head = mp->next;
        pthread_mutex_unlock(&mutex);
        printf("---------------------cousmer----------%d\n", mp->num);
        free(mp);
        sleep(rand() % 3);
    }

    return NULL;
}

int main()
{
    // 随机种子
    srand(time(NULL));

    pthread_t tid1, tid2;
    pthread_create(&tid1, NULL, producer, NULL);
    pthread_create(&tid2, NULL, consumer, NULL);

    pthread_join(tid1, NULL);
    pthread_join(tid2, NULL);

    pthread_mutex_destroy(&mutex);
    pthread_cond_destroy(&cond);

    pthread_exit(NULL);
}
```

## 8 信号量

* 进阶版的mutex，解决串行执行问题

* 初始化定义N个mutex

* 应用于线程、进程

```cpp
sem_t sem;
sem_init(&sem,0,N)   // 0线程间同步，1进程间同步,N指定访问的线程数目
sem_destory(&sem)
    
sem_wait(&sem) // 做一次N--操作,N=0再次调用会阻塞
sem_post(&sem) // 做一次N++操作，N=N时候再次调用，会阻塞
```

* 生产者消费者模型

![image-20230523195150193](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230523195150193.png)

```cpp
#include <stdio.h>
#include <pthread.h>
#include <stdlib.h>
#include <unistd.h>
#include <semaphore.h>
#define NUM 5

// 公共区域
int queue[NUM];

sem_t product, blank;

void *producer(void *arg)
{
    int i = 0;
    while (1)
    {
        sem_wait(&blank);
        queue[i] = rand() % 1000 + 1;
        printf("------------------------produce--------%d\n", queue[i]);
        sem_post(&product);
        i = (i + 1) % NUM; // 下表实现循环
        sleep(rand() % 1);
    }
    return NULL;
}
void *consumer(void *arg)
{
    int i = 0;
    while (1)
    {
        sem_wait(&product);
        printf("---------consume--------%d\n", queue[i]);
        queue[i] = 0;
        sem_post(&blank);
        i = (i + 1) % NUM;
        sleep(rand() % 2);
    }

    return NULL;
}
int main()
{
    // 随机种子
    srand(time(NULL));

    sem_init(&blank, 0, NUM);
    sem_init(&product, 0, 0);

    pthread_t tid1, tid2;
    pthread_create(&tid1, NULL, producer, NULL);
    pthread_create(&tid2, NULL, consumer, NULL);

    pthread_join(tid1, NULL);
    pthread_join(tid2, NULL);

    sem_destroy(&blank);
    sem_destroy(&product);

    pthread_exit(NULL);
}
```

# 12 epoll多路IO转接

epoll作用：

无epoll（传统阻塞+轮询）：服务器轮回检查是否有请求，若有请求，立刻处理，其余请求等待，处理完毕，再处理其余请求

epoll（epoll+线程池）：服务器沉默，epoll循环等待是否有请求，若有请求，唤醒服务器，服务器将任务放工作队列后继续沉默等待唤醒，工作线程获取工作

![image-20230605173728140](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230605173728140.png)

## 12.0 wait监听的触发模式

1. 水平触发模式（Level-Triggered）：

   - 手机接收短信：当手机处于开启状态时，每当有新的短信到达，手机会一直通知用户，直到用户主动查看并处理短信。
   - 电子邮件通知：当电子邮件客户端处于开启状态时，每当有新的邮件到达，客户端会持续通知用户，直到用户主动查看并处理邮件。

2. 边缘触发模式（Edge-Triggered）：

   - 定时器触发事件：当定时器到达预定的时间点时，系统只会触发一次事件通知，应用程序需要立即对事件进行处理。如果应用程序无法及时处理，可能会错过事件。
   - 鼠标移动事件：当鼠标从静止状态开始移动时，系统会触发一次鼠标移动事件通知应用程序。应用程序需要立即响应并处理鼠标移动事件，直到鼠标再次停止移动。

3. 一次触发模式（One-Shot）：

   - 红绿灯控制：当红灯变为绿灯时，控制器将触发一次绿灯开启的事件通知，然后需要重新设置事件以准备下一次红灯到绿灯的切换。这样可以确保只在红灯变为绿灯时进行一次事件处理，避免重复处理。
   - 文件上传完成通知：当文件上传完成后，服务器会触发一次文件上传完成的事件通知，然后需要重新设置事件以等待下一次文件上传。

   水平触发模式适合处理长时间处理的任务，边缘触发模式适合高效处理并发连接，而一次触发模式适合确保事件只触发一次的场景。

比较边缘触发<-->水平触发：

* 当事件设置水平触发

  ```cpp
  uint32_t connEvent // 默认
  ```

  wait只会在文件就绪时候，返回文件就绪队列

  * 可读
  * 可写
  * 连接关闭
  * 新建连接
  * 异常
  * 当文件描述符的输入缓冲区有数据可读时，文件描述符被认为是就绪的，但状态可能没有发生改变。
  * 当文件描述符的输出缓冲区有空闲空间可写入时，文件描述符被认为是就绪的，但状态可能没有发生改变。

* 事件设置边缘触发

  ```cpp
  uint32_t  connEvent & EPOLLEP;
  ```

  wait只会在文件状态发生改变时，返回状态改变的文件队列（更加的精细，舍弃掉了水触发中无意义的事件，相当于一个过滤机制）

  * 可读
  * 可写
  * 连接关闭
  * 新建连接
  * 异常
  
* 使用

```cpp
// 将 EPOLLET 标志位添加到 listenEvent_ 变量中。
listenEvent_ |= EPOLLET;

// 检查 listenEvent_ 变量中是否包含 EPOLLET 标志位。
listenEvent_ & EPOLLET
```



## 12.2 wait监听的模式

由`epoll_wait`的第三个参数 `timeout`决定

* timeout>0 超时阻塞，作为 `epoll_wait()` 函数的超时时间。

  如果超过了设置的超时时间，即使没有文件描述符就绪，`epoll_wait()` 函数也会返回，并且返回一个空的文件描述符列表。

  

* 如果 `timeoutMS_` 小于零，则 `timeMS` 保持为默认值 `-1`，即永久阻塞。

  如果有文件描述符就绪（满足了注册的事件条件），`epoll_wait()` 函数会立即返回，并返回就绪的文件描述符列表。

  
  
* timeoutMS_ == 0,非阻塞
  
  

1、永久阻塞 + 水平触发

2、永久阻塞 + 边缘触发

##12.1 对epoll理解

* epoll相当于一个监听的红黑树
* lfd和cfd都作为树的节点，受到epoll_wait()的监听读操作
* 多进程处理：accept循环监听，有连接请求，创建进程，单独处理
* epoll处理：epoll_wait循环监听，（1）连接请求，建立cfd，加入红黑树（2）读写请求，执行读写操作
* 单个线程处理多个连接：通过 `epoll` 的监听机制，一个线程可以同时监听和处理多个连接的 I/O 事件，而不需要为每个连接创建一个线程。这样可以大大减少线程的数量和线程切换的开销，提高并发能力。
* 高效的事件就绪通知：`epoll` 使用 `epoll_wait` 函数进行事件的等待和获取，它可以等待多个事件同时就绪，而不需要遍历所有的文件描述符，从而提高了效率。
* `epoll` 的本质仍然是串行处理每个事件。虽然 `epoll` 能够同时监听和处理多个连接的事件，但在应用程序的角度看，它仍然是以事件为单位进行处理的。
* 虽然 `epoll` 在处理多个事件时是串行进行的，但由于使用了高效的事件通知机制和非阻塞 I/O 模型，能够快速地切换和处理多个事件，从而实现高并发的效果。同时，可以通过使用多个线程或进程来处理 `epoll` 的事件，进一步提高并发能力。

## 12.2 epoll API 的事件标志

具体来说，`events` 的类型是 `uint32_t`，它是一个无符号整数类型，用于存储 epoll 事件的标志位。

在 Linux 的 epoll 机制中，通过 `epoll_wait` 函数等待事件时，当有事件发生时，会将相应的事件类型放入一个 `epoll_event` 结构体中，并将多个 `epoll_event` 结构体存储在一个数组中返回给调用者。其中，每个 `epoll_event` 结构体包含了一个 `events` 字段，用于表示该事件的类型。

在代码中，通过 `epoller_->GetEvents(i)` 获取到第 `i` 个事件的类型，并将其赋值给 `events` 变量。后续代码根据 `events` 的值来判断事件的类型，进而执行相应的处理逻辑。

需要注意的是，具体的事件类型是通过位运算来判断的，例如使用 `events & EPOLLIN` 判断是否包含读事件，`events & EPOLLOUT` 判断是否包含写事件等。这些事件类型的取值在 epoll 相关的头文件中定义。

- `EPOLLIN`：表示关联的文件描述符可读。
- `EPOLLOUT`：表示关联的文件描述符可写。
- 出错
- `EPOLLRDHUP`：表示关联的文件描述符的对端已关闭连接或关闭了写操作。
- `EPOLLERR`：表示关联的文件描述符发生错误（真正错）。
- `EPOLLHUP`：表示关联的文件描述符被挂断。
- `EPOLLONESHOT`：将文件描述符设置为一次性触发模式。在事件被触发并处理后，需要重新将其添加到 epoll 实例中才能继续监听事件。
- 触发监听返回的模式
- `epollET`





## 12.2 epoll函数（3个）

* 创建一颗监听红黑树fd，一个树根 

![image-20230525164720628](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230525164720628.png)

* 操作监听红黑树

![image-20230525164759001](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230525164759001.png)

删除节点：最后不用传入结构体，传NULL

* 监听

![image-20230525171732615](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230525171732615.png)

##12.3 epoll（LT）实现并发服务器

```cpp
#include <stdio.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <netinet/ip.h>
#include <stdlib.h>
#include <unistd.h> //write(STDOUT_FILENO,buf,ret);
#include <errno.h>
#include <pthread.h>
#include <ctype.h>
#include <string.h>
#include <arpa/inet.h>
#include <sys/epoll.h>
#define PORT_SERVER 9527
#define OPEN_MAX 500
void sys_err(const char *str)
{
    perror(str);
    exit(1);
}

int main()
{
    // 1、套接字
    int lfd, cfd = 0;
    lfd = socket(AF_INET, SOCK_STREAM, 0);
    if (lfd == -1)
    {
        sys_err("socket error");
    }

    // 服务器地址结构
    struct sockaddr_in addr_server;
    addr_server.sin_family = AF_INET;
    addr_server.sin_port = htons(PORT_SERVER);
    addr_server.sin_addr.s_addr = htonl(INADDR_ANY); // 网络字节序、二进制
    // inet_pton(AF_INET, "172.16.108.62", &addr_server.sin_addr.s_addr); // 网络字节序、二进制

    // 2、绑定
    bind(lfd, (const struct sockaddr *)&addr_server, sizeof(addr_server));

    // 3、监听
    listen(lfd, 128);

    // 客户端地址结构，客户端访问服务器，系统自动填充信息
    struct sockaddr_in addr_clint;
    socklen_t addrlen_client = sizeof(addr_clint);
    // ============================================

    // 4、实现epollIO多路复用
    // (1)创建红黑树根节点，用efd控制
    int efd = epoll_create(OPEN_MAX);
    if (efd == -1)
    {
        sys_err("efd error");
    }
    // （2）创建一个树节点结构体
    struct epoll_event tep, ep[OPEN_MAX];

    // （3）添加第一个lfd监听节点
    tep.events = EPOLLIN; // 监听读
    tep.data.fd = lfd;    // 监听lfd;

    int ret;
    ret = epoll_ctl(efd, EPOLL_CTL_ADD, lfd, &tep);
    if (ret == -1)
    {
        sys_err("add error");
    }

    // (4)阻塞监听节点是否有读操作（lfd连接请求/cfd读写操作）
    char buf[1024]; // 读写缓冲区
    while (1)
    {
        ret = epoll_wait(efd, ep, OPEN_MAX, -1); // ep返回值数组，保存有读操作的节点，-1为永久阻塞，
        if (ret == -1)
        { // 成功返回ret为监听到读操作的总个数
            sys_err("wait erorr");
        }
        // 监听到读操作
        for (int i = 0; i < ret; i++)
        {
            if (!(ep[i].events & EPOLLIN))
            {
                continue; // 若不是读操作，则继续循环（一般都是读操作，可以不用判断）
            }
            // 【1】若ep数组内有lfd连接请求
            if (ep[i].data.fd == lfd)
            {
                // 创建cfd
                socklen_t addr_clint_len = sizeof(addr_clint);
                cfd = accept(lfd, (struct sockaddr *)&addr_clint, &addr_clint_len);
                if (cfd == -1)
                {
                    sys_err("efd error");
                }

                // cfd加入监听红黑树
                tep.events = EPOLLIN;
                tep.data.fd = cfd;
                ret = epoll_ctl(efd, EPOLL_CTL_ADD, cfd, &tep);
                if (ret == -1)
                {
                    sys_err("add error");
                }
                // 客户端信息
                char clientIP[16];
                inet_ntop(AF_INET, &addr_clint.sin_addr.s_addr, clientIP, sizeof(clientIP));
                unsigned short clientPort = ntohs(addr_clint.sin_port);
                printf("client ip : %s ,port : %d login success!! \n", clientIP, clientPort);
            }
            // 【2】ep数组中的cfd发出读写请求
            else
            {
                int num = read(ep[i].data.fd, buf, 1024);
                if (num == 0)
                {
                    // 客户端关闭,删除监听节点
                    ret = epoll_ctl(efd, EPOLL_CTL_DEL, ep[i].data.fd, NULL);
                    if (ret == -1)
                    {
                        sys_err("del error");
                    }
                    close(ep[i].data.fd);

                    // 客户端信息
                    char clientIP[16];
                    inet_ntop(AF_INET, &addr_clint.sin_addr.s_addr, clientIP, sizeof(clientIP));
                    unsigned short clientPort = ntohs(addr_clint.sin_port);
                    printf("client ip : %s ,port : %d logout!! \n", clientIP, clientPort);
                }
                // 读取信息
                else
                {
                    for (int j = 0; j < num; j++)
                    {
                        buf[j] = toupper((unsigned char)buf[j]);
                    }
                    write(STDOUT_FILENO, buf, num);
                    write(ep[i].data.fd, buf, num);
                }
            }
        }
    }
    close(lfd);

    return 0;
}
```



## 12.5 文件的非阻塞读

文件描述符的非阻塞读（Non-blocking read）是指在读取文件描述符时，如果没有数据可用，读取操作不会阻塞等待，而是立即返回。

通常情况下，读取文件描述符时，如果没有数据可用，读取操作会一直阻塞，直到有数据到达或者发生错误。这种情况下，应用程序会一直等待数据的到来，造成阻塞。

而非阻塞读操作通过将文件描述符设置为非阻塞模式，在没有数据可用时，立即返回，不会阻塞等待。这样，应用程序可以继续执行其他操作，而不需要一直等待数据的到来。

非阻塞读操作的特点如下：

1. 立即返回：如果文件描述符上没有数据可用，非阻塞读操作会立即返回，不会阻塞等待。
2. 错误处理：非阻塞读操作返回时，需要根据返回值和错误码来判断读取操作的结果。
3. 循环读取：由于非阻塞读操作可能只读取到部分数据，需要在循环中进行多次读取，直到读取到所需的数据或者遇到结束条件。

非阻塞读操作通常与多路复用（如 `epoll`、`select`）或异步 I/O 操作配合使用，以便在读取操作期间可以同时处理其他事件或任务。它在网络编程中特别有用，可以实现高效的事件驱动模型，提高程序的并发性能。

* 设置方法

```cpp
//获取文件描述符的当前状态标志：
int flag = fcntl(fd, F_GETFL, 0);

// 将文件描述符设置为非阻塞模式
fcntl(fd, F_SETFL, flags | O_NONBLOCK);
```

```cpp
if (fcntl(clientfd, F_SETFL,  newSocketFlag) == -1)
{
    close(clientfd);
    std::cout << "set socket to nonblock error." << std::endl;
    return -1;
}

```



## 12.4 epoll的ET模式

* ET模式只支持文件的非阻塞读取模式

  在epoll的ET（边缘触发）模式下，为了最大化利用其高效的事件通知机制，通常建议将读操作设置为非阻塞模式。

  ET模式是一种边缘触发模式，它只在状态发生变化时通知应用程序。对于I/O操作来说，ET模式要求应用程序在接收到读就绪或写就绪的事件通知后，必须一直读取或写入数据直到返回EAGAIN（表示暂时没有更多数据可读或写）。这与水平触发模式（LT）不同，水平触发模式只要求应用程序在有数据可读或写时进行读写操作。

  在ET模式下，如果读操作设置为阻塞模式，即使应用程序只读取了一部分数据，仍然会一直阻塞等待更多数据到达。这样会导致应用程序无法及时响应其他事件和请求，造成资源浪费和性能下降。

  而将读操作设置为非阻塞模式，则可以保证在读取完所有已就绪的数据后立即返回，即使没有读取到足够的数据也不会阻塞。这样，应用程序可以及时返回处理其他事件，提高了处理并发请求的效率。

  总结来说，将读操作设置为非阻塞模式能够使得在ET模式下，应用程序尽快读取完就绪的数据并立即返回，避免了阻塞等待更多数据的情况发生。这样可以充分利用epoll的高效事件通知机制，提高服务器的响应性能和吞吐能力。

  

* ```cpp
  //1、ET模式
  uint32_t events = EPOLLIN | EPOLLET
  ```
  
* ```cpp
  //2、 非阻塞模式
  int flag = fcntl(fd, F_GETFL, 0);
  fcntl(fd, F_SETFL, flag | O_NONBLOCK);
  ```
  
* ```cpp
  // 加入监听树
  ev.data.fd = fd;
  ev.evebts = events'
  ```
  
* ```cpp
  // 非阻塞轮询读数据(确保一次性读完所有数据)
  do{
      len = read(cfd,buf,sizeof(buf));
      if(len<0){
  		break;
      }
  	write(STDOUT_FILENO,buf,len);
  }while(events & EPOLLET)
  ```



## 12.5 LT 模式和 ET 模式

 ![image-20230706172642053](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230706172642053.png)

-----------

 ![image-20230706172742276](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230706172742276.png)

与 poll 的事件宏相比，epoll 新增了一个事件宏 **EPOLLET**，这就是所谓的**边缘触发模式**（**E**dge **T**rigger，ET），而默认的模式我们称为 **水平触发模式**（**L**evel **T**rigger，LT）。这两种模式的区别在于：

- 对于水平触发模式，一个事件只要有，就会一直触发；
- 对于边缘触发模式，只有一个事件从无到有才会触发。

对于水平模式，只要 socket 上有未读完的数据，就会一直产生 POLLIN 事件；而对于边缘模式，socket 上第一次有数据会触发一次，后续 socket 上存在数据也不会再触发，除非把数据读完后，再次产生数据才会继续触发。

对于 socket 写事件，如果 socket 的 TCP 窗口一直不饱和，会一直触发 POLLOUT 事件；而对于边缘模式，只会触发一次，除非 TCP 窗口由不饱和变成饱和再一次变成不饱和，才会再次触发 POLLOUT 事件。

**socket 可读事件水平模式触发条件：**

```
1. socket上无数据 => socket上有数据
2. socket上有数据 => socket上有数据
```

**socket 可读事件边缘模式触发条件：**

```
1. socket上无数据 => socket上有数据
```

**socket 可写事件水平模式触发条件：**

```
1. socket可写   => socket可写
2. socket不可写 => socket可写
```

**socket 可写事件边缘模式触发条件：**

```
1. socket不可写 => socket可写
```

也就是说，如果对于一个非阻塞 socket，如果使用 epoll 边缘模式去检测数据是否可读，触发可读事件以后，一定要一次性把 socket 上的数据收取干净才行，也就是一定要循环调用 recv 函数直到 recv 出错，错误码是**EWOULDBLOCK**（**EAGAIN** 一样）；如果使用水平模式，则不用，你可以根据业务一次性收取固定的字节数，或者收完为止。边缘模式下收取数据的代码示例如下：

```cpp
bool TcpSession::RecvEtMode()
{
    char buff[256];
    while (true)
    {       
        int nRecv = ::recv(clientfd_, buff, 256, 0);
        if (nRecv == -1)
        {
            if (errno == EWOULDBLOCK)
                return true;
            else if (errno == EINTR)
                continue;

            return false;
        }
        //对端关闭了socket
        else if (nRecv == 0)
            return false;

        inputBuffer_.add(buff, (size_t)nRecv);
    }

    return true;
}
```

最后，我们来看一个 epoll 模型的完整例子：

```cpp
/**
 * 演示 epoll 通信模型，epoll_server.cpp
 */
#include <sys/types.h> 
#include <sys/socket.h>
#include <arpa/inet.h>
#include <unistd.h>
#include <fcntl.h>
#include <sys/epoll.h>
#include <poll.h>
#include <iostream>
#include <string.h>
#include <vector>
#include <errno.h>

int main(int argc, char* argv[])
{
    //创建一个侦听socket
    int listenfd = socket(AF_INET, SOCK_STREAM, 0);
    if (listenfd == -1)
    {
        std::cout << "create listen socket error." << std::endl;
        return -1;
    }

    //将侦听socket设置为非阻塞读
    int oldSocketFlag = fcntl(listenfd, F_GETFL, 0);
    int newSocketFlag = oldSocketFlag | O_NONBLOCK;
    if (fcntl(listenfd, F_SETFL,  newSocketFlag) == -1)
    {
        close(listenfd);
        std::cout << "set listenfd to nonblock error." << std::endl;
        return -1;
    }

    //初始化服务器地址
    struct sockaddr_in bindaddr;
    bindaddr.sin_family = AF_INET;
    bindaddr.sin_addr.s_addr = htonl(INADDR_ANY);
    bindaddr.sin_port = htons(3000);
    if (bind(listenfd, (struct sockaddr *)&bindaddr, sizeof(bindaddr)) == -1)
    {
        std::cout << "bind listen socket error." << std::endl;
        close(listenfd);
        return -1;
    }

    //启动侦听
    if (listen(listenfd, SOMAXCONN) == -1)
    {
        std::cout << "listen error." << std::endl;
        close(listenfd);
        return -1;
    }

    //复用地址和端口号
    int on = 1;
    setsockopt(listenfd, SOL_SOCKET, SO_REUSEADDR, (char *)&on, sizeof(on));
    setsockopt(listenfd, SOL_SOCKET, SO_REUSEPORT, (char *)&on, sizeof(on));

    //创建epollfd红黑树根节点
    int epollfd = epoll_create(1);
    if (epollfd == -1)
    {
        std::cout << "create epollfd error." << std::endl;
        close(listenfd);
        return -1;
    }

    epoll_event listen_fd_event;
    listen_fd_event.events = POLLIN;
    listen_fd_event.data.fd = listenfd;

    //将侦听socket绑定到epollfd监听树上去，作为根节点（listenfd）
    if(epoll_ctl(epollfd, EPOLL_CTL_ADD, listenfd, &listen_fd_event) == -1)
    {
        std::cout << "epoll_ctl error." << std::endl;
        close(listenfd);
        return -1;
    }

    int n;
    while (true)
    {       
        epoll_event epoll_events[1024];
        n = epoll_wait(epollfd, epoll_events, 1024, 1000);
        if (n < 0)
        {
            //被信号中断，再次连接
            if (errno == EINTR)
                continue;

            //出错，退出
            break;
        }
        else if (n == 0)
        {
            //超时，继续
            continue;
        }

        // 读取数组内的事件，进行处理
        for (size_t i = 0; i < n; ++i)
        {
            // 事件可读
            if (epoll_events[i].events & POLLIN)
            {
                // 创建新连接，判断该事件的socket是否是listenfd
                if (epoll_events[i].data.fd == listenfd)
                {
                    //侦听socket，接受新连接
                    struct sockaddr_in clientaddr;
                    socklen_t clientaddrlen = sizeof(clientaddr);
                    //接受客户端连接, 并加入到fds集合中
                    int clientfd = accept(listenfd, (struct sockaddr *)&clientaddr, &clientaddrlen);
                    if (clientfd != -1)
                    {
                        //将客户端socket设置为非阻塞读
                        int oldSocketFlag = fcntl(clientfd, F_GETFL, 0);
                        int newSocketFlag = oldSocketFlag | O_NONBLOCK;
                        if (fcntl(clientfd, F_SETFL,  newSocketFlag) == -1)
                        {
                            close(clientfd);
                            std::cout << "set clientfd to nonblock error." << std::endl;                        
                        }
                        else
                        {
                            epoll_event client_fd_event;
                            client_fd_event.events = POLLIN;
                            client_fd_event.data.fd = clientfd;                         
                            if(epoll_ctl(epollfd, EPOLL_CTL_ADD, clientfd, &client_fd_event) != -1)
                            {
                                std::cout << "new client accepted, clientfd: " << clientfd << std::endl;
                            }
                            else
                            {
                                std::cout << "add client fd to epollfd error." << std::endl;
                                close(clientfd);                            
                            }
                        }       
                    }
                }
                else 
                {
                    //普通读写clientfd,收取数据（红黑树其他的节点有信息需求）
                    char buf[64] = { 0 };
                    int m = recv(epoll_events[i].data.fd, buf, 64, 0);
                    if (m == 0)
                    {
                        //对端关闭了连接，从epollfd上移除clientfd
                        if(epoll_ctl(epollfd, EPOLL_CTL_DEL, epoll_events[i].data.fd, NULL) != -1)
                        {
                            std::cout << "client disconnected, clientfd: " << epoll_events[i].data.fd << std::endl;
                        }
                        close(epoll_events[i].data.fd);
                    }
                    else if (m < 0)                          
                    {                                           
                        //出错，从epollfd上移除clientfd
                        if (errno != EWOULDBLOCK && errno != EINTR)
                        {
                            if(epoll_ctl(epollfd, EPOLL_CTL_DEL, epoll_events[i].data.fd, NULL) != -1)
                            {
                                std::cout << "client disconnected, clientfd: " << epoll_events[i].data.fd << std::endl;
                            }
                            close(epoll_events[i].data.fd);
                        }
                    }
                    else
                    {
                        //正常收到数据
                        std::cout << "recv from client: " << buf << ", clientfd: " << epoll_events[i].data.fd << std::endl;
                    }
                }
            }
            else if (epoll_events[i].events & POLLERR)
            {
                //TODO: 暂且不处理
            }

        }// end  outer-for-loop
    }// end  while-loop


    //关闭侦听socket
    //（理论上应该关闭包括所有clientfd在内的fd，但这里只是为了演示问题，就不写额外的代码来处理啦）
    close(listenfd);            

    return 0;
}
```



# 12 项目





![image-20230524150626047](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230524150626047.png)

![image-20230524151517138](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230524151517138.png)

![image-20230524151453222](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230524151453222.png)

 ![image-20230524151545177](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230524151545177.png)









# 13 C++中的网络编程实现

## 13.1 线程

thread是c++提供的线程类

1、`std::thread`: 用于创建和管理线程的类。它的构造函数接受一个可调用对象（函数指针、函数对象或 lambda 表达式）作为参数，并创建一个新的线程来执行该可调用对象。

示例：

```cpp
#include <iostream>
#include <thread>

void myFunction() {
    std::cout << "Thread running!" << std::endl;
}

int main() {
    std::thread t(myFunction); // 创建新线程t并执行 myFunction
    t.join(); // 等待线程执行完毕
    return 0;
}

```

* 匿名创建线程

```cpp
int main(){
    std::thread([]{std::cout << "Thread running!" << std::endl})
}
```

* 线程分离

```cpp
for(int i =0; i<10;++i){
    
}
```







2、`std::this_thread::sleep_for`: 使当前线程暂停执行一段时间。它接受一个 `std::chrono::duration` 对象作为参数，表示暂停的时间段。

示例

```cpp
#include <iostream>
#include <chrono>
#include <thread>

int main() {
    std::cout << "Start" << std::endl;
    std::this_thread::sleep_for(std::chrono::seconds(2)); // 暂停 2 秒
    std::cout << "End" << std::endl;
    return 0;
}

```

3、`std::thread::join`: 阻塞当前线程，等待指定的线程执行完毕

```cpp
#include <iostream>
#include <thread>

void myFunction() {
    std::cout << "Thread running!" << std::endl;
}

int main() {
    std::thread t(myFunction); // 创建新线程并执行 myFunction
    t.join(); // 等待线程执行完毕
    std::cout << "Main thread" << std::endl;
    return 0;
}

```

4、`std::thread::detach`: 分离当前线程，使其成为一个独立的线程，不再与主线程同步。

```cpp
#include <iostream>
#include <thread>

void myFunction() {
    std::cout << "Thread running!" << std::endl;
}

int main() {
    std::thread t(myFunction); // 创建新线程并执行 myFunction
    t.detach(); // 分离线程
    std::cout << "Main thread" << std::endl;
    return 0;
}

```



## 13.2 锁

* 使用 `std::lock_guard` 模板类进行上锁和解锁操作
* lock_guard是一个上锁的模板函数（看作对象）
* `<std::mutex>` 具体到是互斥锁上锁的模板函数 (指定类型)
* locker（） 是实例化一个具体使用锁的对象，传入参数mtx，可以上锁，可以解锁

```cpp
#include <mutex>
#include <shared_mutex>

// 初始化互斥锁
std::mutex mtx;

// 当 locker 对象被创建,会自动调用 locker.lock() 来上锁。
// 当 locker 对象的生命周期结束时，它会自动调用 locker.unlock() 来解锁
std::lock_guard<std::mutex> locker(mtx); // 实例化一个locker,自动上锁解锁

std::unique_lock<std::mutex> locker(mtx); // 更加高级，可以手动上锁解锁
locker.unlock(); // 解锁
locker.lock(); // 上锁

```

```
`std::lock_guard`, `std::unique_lock`, 和 `std::shared_lock` 是C++标准库中用于线程同步的互斥锁包装器。它们提供了不同的功能和灵活性，以适应不同的多线程场景。

1. `std::lock_guard`:
   - `std::lock_guard`是最简单的锁包装器，它使用了一种称为RAII（Resource Acquisition Is Initialization）的技术，确保在作用域结束时自动释放锁资源。
   - `std::lock_guard`被设计为在获取锁时构造，在作用域结束时析构并释放锁。
   - `std::lock_guard`提供了一种简化的方式来管理锁的生命周期，但不提供额外的灵活性，如手动释放锁或条件变量的支持。

2. `std::unique_lock`:
   - `std::unique_lock`提供了比`std::lock_guard`更高级的锁管理功能。
   - `std::unique_lock`可以手动获得和释放锁，也可以延迟锁的获取。
   - `std::unique_lock`还提供了与条件变量一起使用的功能，可以在满足特定条件之前暂时释放锁，并在条件满足时重新获取锁。
   - `std::unique_lock`相比于`std::lock_guard`更加灵活，但也更加复杂。

3. `std::shared_lock`:
   - `std::shared_lock`是C++14引入的，它是`std::unique_lock`的一个变体，用于支持共享所有权的锁。
   - `std::shared_lock`允许多个线程共享同一个锁资源，以提高并发性能。
   - `std::shared_lock`提供了共享（读）锁和排他（写）锁之间的转换，以及延迟获取共享锁的能力。
   - `std::shared_lock`适用于读多写少的场景，可以提供更好的性能。

总结：
- `std::lock_guard`提供了最简单的锁封装，适用于简单的互斥操作。
- `std::unique_lock`提供了更高级的锁管理功能，适用于复杂的互斥操作和条件变量的使用。
- `std::shared_lock`是`std::unique_lock`的变体，适用于读多写少的场景，提供了共享锁的能力。

根据具体的需求和场景，选择适当的锁包装器可以使多线程编程更加灵活和高效。
```

* 作用域结束自动释放

作用域用{}控制，表示一个代码块

```c
{
        lock_guard<mutex> locker(mtx_);
        buff_.RetrieveAll(); // 清空日志缓冲区，将其内部日志全部取出
        if (fp_)
        {
            flush();     // 刷新日志，将缓冲区写入
            fclose(fp_); // 关闭当前日志文件，fp_指向nullptr（标准库函数，底层调用close关闭文件描述符）
        }

        fp_ = fopen(fileName, "a");
        if (fp_ == nullptr)
        {
            mkdir(path_, 0777);
            fp_ = fopen(fileName, "a");
        }
        assert(fp_ != nullptr);
    }
```



## 13.3 条件变量

```cpp
#include <condition_variable>

// 定义+初始化全局条件变量
std::condition_variable cond;

// 阻塞等待,locker 是一个已经上锁的互斥锁对象，用于保护条件变量
cond.wait(locker);
// 设置最长等待时间。如果超过指定的时间还没有收到通知，则函数会自动唤醒当前线程
wait_for(locker, timeout): 

// 唤醒至少一个线程
cond.notify_one();
// 唤醒所有等待的线程
cond.notify_all();
```

```cpp
// 使用
while(true){ // 循环内可以进行多种判断
    if(条件不满足){
        cond.wait(locker); // 等待唤醒，重新进入循环判断
    }else if(其他判断){
        xxx
    }else{
        条件满足，访问共享资源;
    }
}

```



## 13.4 epoll

（自己封装）将linux系统提供的API封装为一个类

* epoll_create
* epoll_ctl   (add、mod、del)
* epoll_wait

* 创建一颗监听红黑树fd，一个树根 

![image-20230525164720628](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230525164720628.png)

* 操作监听红黑树

![image-20230525164759001](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230525164759001.png)

删除节点：最后不用传入结构体，传NULL

* 阻塞监听

![image-20230525171732615](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230525171732615.png)

```cpp
// 封装API为类
#include <sys/epoll.h>
class Epoller{
public:
    Epoller(){
        // 创建树根
        efd = epoll_creat(1024);
    };
    ~Epoller(){};
    
    // 添加节点
    bool addFd(int fd,unit32_t events){    // 添加节点的文件fd，该文件的读取模式
        epoll_event ev;
        ev.events = events;
        ev.data.fd = fd;
        return epoll.ctl(efd,EPOLL_CTRL_ADD,fd,&ev) == 0;
    }
    // 修改节点
    bool modFd(int fd,uint32_t events){
        epoll_event ev;
        ev.events = events;
        ev.data.fd = fd;
        return epoll.ctl(efd,EPOLL_CTRL_MOD,fd,&ev) == 0;
    }
    // 删除节点
     bool delFd(int fd){
        return epoll.ctl(efd,EPOLL_CTRL_DEL,fd,nullptr) == 0;
    }
    // 阻塞监听
    int wait(epoll_events* events,int max_events,int timeout){
		return epoll_wait(efd,events,max_events,timeout)
    }
private:
    int efd; // 根节点fd
	
}
```

--------

* 使用

```cpp
Epoller epoller;

// 加入listen_fd
int listen_fd;
epoll_event listen_events;
listen_events.events = EPOLLIN | EPOLLET; // 文件设置为 监听可读模式 和 边缘触发模式
epoller.addFd(listen_fd,events);

// 创建wait输出的有读信号的数组
const int MAX_EVENTS = 10;
epoll_event evs[MAX_EVENTS];

while(1){
	int event_count = epoller.wait(evs,MAX_EVENTS,-1); // 阻塞监听
    for(int i =0;i<event_count;i++){
		int fd = evs[i].data.fd;
        uint_t events = evs[i].events;
        // 处理连接请求
        if(fd == listen_fd){
            // 客户端结构
            struct sockaddr_in addr_clint;
            socklen_t addr_clint_len = sizeof(addr_clint);
            // 连接套接字
            conn_fd = accept(listen_fd, (struct sockaddr *)&addr_clint, &addr_clint_len);
            if (conn_fd == -1)
            {
                sys_err("cfd error");
            }

            // cfd加入监听红黑树
            epoll_event conn_event;
            conn_event.events = EPOLLIN;
            conn_event.data.fd = conn_fd;
            
            epoller.addFd(conn_fd,conn_event);
                
        }else{
			// 处理读请求
            
        }
    }
    
}
```



## 13.5 socket

```cpp
/**
 * TCP服务器通信基本流程
 * zhangyl 2018.12.13
 */
#include <sys/types.h> 
#include <sys/socket.h>
#include <arpa/inet.h>
#include <unistd.h>
#include <iostream>
#include <string.h>
#include <vector>

int main(int argc, char* argv[])
{
    //1.创建一个侦听socket
    int listenfd = socket(AF_INET, SOCK_STREAM, 0);
    if (listenfd == -1)
    {
        std::cout << "create listen socket error." << std::endl;
        return -1;
    }

    //2.初始化服务器地址
    struct sockaddr_in bindaddr;
    bindaddr.sin_family = AF_INET;
    bindaddr.sin_addr.s_addr = htonl(INADDR_ANY);
    bindaddr.sin_port = htons(3000);
    if (bind(listenfd, (struct sockaddr *)&bindaddr, sizeof(bindaddr)) == -1)
    {
        std::cout << "bind listen socket error." << std::endl;
        return -1;
    }

    //3.启动侦听
    if (listen(listenfd, SOMAXCONN) == -1)
    {
        std::cout << "listen error." << std::endl;
        return -1;
    }

    //记录所有客户端连接的容器
    std::vector<int> clientfds;
    while (true)
    {
        struct sockaddr_in clientaddr;
        socklen_t clientaddrlen = sizeof(clientaddr);
        //4. 接受客户端连接
        int clientfd = accept(listenfd, (struct sockaddr *)&clientaddr, &clientaddrlen);
        if (clientfd != -1)
        {             
            char recvBuf[32] = {0};
            //5. 从客户端接受数据
            int ret = recv(clientfd, recvBuf, 32, 0);
            if (ret > 0) 
            {
                std::cout << "recv data from client, data: " << recvBuf << std::endl;
                //6. 将收到的数据原封不动地发给客户端
                ret = send(clientfd, recvBuf, strlen(recvBuf), 0);
                if (ret != strlen(recvBuf))
                    std::cout << "send data error." << std::endl;

                std::cout << "send data to client successfully, data: " << recvBuf << std::endl;
            } 
            else 
            {
                std::cout << "recv data error." << std::endl;
            }

            //close(clientfd);
            clientfds.push_back(clientfd);
        }
    }

    //7.关闭侦听socket
    close(listenfd);

    return 0;
}
```



# 14 系统调用

## 14.1 读写write


用于实现一次性读取或写入多个缓冲区的操作。这些函数主要是在Unix/Linux系统中提供的，它们的命名规则一般是以`v`结尾，表示向量（vector）操作。

以下是一些常见的与`readv()`类似的系统调用函数：

1. `preadv()`：类似于`readv()`，但从指定文件偏移量处读取数据。
2. `readv()`：一次性读取多个缓冲区的数据。
3. `preadv2()`：类似于`preadv()`，但可以提供更多的标志和选项。
4. `recvmmsg()`：类似于`readv()`，用于一次性接收多个消息。
5. `read()`：一次性读取单个缓冲区的数据。

以下是一些常见的与`writev()`类似的系统调用函数：

1. `pwritev()`：类似于`writev()`，但写入到指定文件偏移量处。
2. `writev()`：一次性写入多个缓冲区的数据。
3. `pwritev2()`：类似于`pwritev()`，但可以提供更多的标志和选项。
4. `sendmmsg()`：类似于`writev()`，用于一次性发送多个消息。
5. `write()`：一次性写入单个缓冲区的数据。

---------------

1. read/writre   见6.5.2

2. readv/writev

   * ```cpp
     #include <sys/uio.h>
     ssize_t readv(int fd, const struct iovec* iov, int iovcnt);
     ```

     - `fd`是文件描述符，表示要写入数据的文件或套接字。
     
     - `iov`是一个指向`struct iovec`数组的指针，每个`struct iovec`元素描述一个缓冲区。
     
     - `iovcnt`表示`iov`数组中`struct iovec`元素的数量。
     
     - 从第一个缓冲区开始读取数据，直到达到该缓冲区的长度（或遇到文件末尾），然后继续读取下一个缓冲区的数据，以此类推
     

 ```cpp
 #include <sys/uio.h>
 ssize_t writev(int fd, const struct iovec* iov, int iovcnt);
 
 ```

 `writev()`函数将按顺序将`iov`数组中的缓冲区数据依次写入到文件描述符中。函数返回值是实际写入的字节数，如果出现错误，则返回-1。

 这两个函数的优点在于可以减少系统调用的次数，从而提高数据传输的效率。通过一次系统调用读取或写入多个缓冲区，可以减少用户空间和内核空间之间的上下文切换开销，提高数据传输的速度。特别是在处理大量数据时，这种效率提升是非常显著的。

 需要注意的是，`readv()`和`writev()`函数所操作的缓冲区是通过`struct iovec`结构来描述的，

 例子

   * ```cpp
     struct iovec {
         void* iov_base; // 数据缓冲区的起始地址
         size_t iov_len; // 数据缓冲区的长度
     };
     
     ```

     ```cpp
     #include <sys/uio.h>
     #include <unistd.h>
     
     int main() {
         struct iovec iov[2];
         char buf1[] = "Hello, ";
         char buf2[] = "world!";
         
         iov[0].iov_base = buf1;
         iov[0].iov_len = sizeof(buf1) - 1;
         iov[1].iov_base = buf2;
         iov[1].iov_len = sizeof(buf2) - 1;
         
         // 从两个缓冲区内写出到控制台
         ssize_t bytes_written = writev(STDOUT_FILENO, iov, 2);
         // 将fd内的数据，读入到iov的两个缓冲区中
         ssize_t bytes_read = readv(fd, iov, 2);
         
         // 检查写入是否成功
         if (bytes_written == -1) {
             // 错误处理
         }
         
         return 0;
     }
     
     ```

     

# 高级补充

## 1 进程

### 1.1 进程的状态

进程有不同的状态，本质上是进程pcb在不同的队列当中

* 运行态：当前进程PCB在==cpu所管理的执行队列==里，就是运行态，并非只是进程正在执行

* 阻塞态：当进程访问外设，将PCB放入==外设管理的wait阻塞队列==中，即阻塞

* 挂起态：当进程阻塞时，由于长期不执行，仍占据内存，将其二进制代码换入到磁盘中，pcb仍处理阻塞队列，此时成为挂起态

  挂起一定阻塞，阻塞不一定挂起

linux中进程的状态通过结构体 task_state_array管理

* 执行态 R   阻塞态 S D T t
* 死亡态 D
* 僵尸态 Z

![image-20240320144553504](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240320144553504.png)

### 1.2 僵尸进程、孤儿进程

进程是通过父进程创建的，子进程在创建新的进程。任何一个子进程(init除外)在exit()之后，并非马上就消失掉，而是留下一个称为[僵尸进程](https://so.csdn.net/so/search?q=僵尸进程&spm=1001.2101.3001.7020)(Zombie)的数据结构，等待父进程处理。 

孤儿进程：一个父进程退出，而它的一个或多个子进程还在运行，那么那些子进程将成为孤儿进程。孤儿进程将被init进程(进程号为1)所收养，并由init进程对它们完成状态收集工作。 

僵尸状态是一个比较特殊的状态，当进程退出父进程（使用wait()系统调用）没有读取到子进程退出的返回代码时就会产生僵尸进程。僵尸进程会在以终止状态保持在进程表中，并且会一直等待父进程读取退出状态代码。 

僵尸进程与孤儿进程的区别： 
孤儿进程是子进程还在运行，而父进程挂了，子进程被init进程收养。僵尸进程是父进程还在运行但是子进程挂了，但是父进程却没有使用wait来清理子进程的进程信息，导致子进程虽然运行实体已经消失，但是仍然在内核的进程表中占据一条记录，这样长期下去对于系统资源是一个浪费。僵尸进程将会导致资源浪费，而孤儿则不会。 
那么如何避免僵尸进程呢 
（1）fork两次 
原理是将子进程成为孤儿进程，从而其的父进程变为init进程，通过init进程可以处理僵尸进程 
（2）通过信号机制 
子进程退出时向父进程发送SIGCHILD信号，父进程处理SIGCHILD信号。在信号处理函数中调用wait进行处理僵尸进程

### 1.3 进程优先级

* 优先级通过pcb中的两个整数控制,PRI(priority), NI(nice)，优先级=PRI + NI
* 用户可以自定义NI调整进程优先级，使用top命令进入，按r 输入调整的进程pid， 输入NI值
* PRI初始值大小80， NI自定义范围[-20, 19] 40个级别

# 16 Windows网络编程

## 16.1 winsock2.h库

`WSASend` 和 `WSARecv` 是用于在 Windows Socket API（Winsock）中发送和接收数据的函数。以下是每个函数的参数及其解释：

### WSASend

```c
int WSASend(
  SOCKET s,           // 要发送数据的套接字
  LPWSABUF lpBuffers, // 包含要发送的数据缓buffer
  DWORD dwBufferCount,// 数据的个数
  LPDWORD lpNumberOfBytesSent,   // 接收发送的数据字节数，可以是 `NULL`，如果使用异步重叠操作，则必须为 `NULL`
  DWORD dwFlags, // 1、0：标准发送， 2、MSG_DONTROUTE:数据不会通过路由
  LPWSAOVERLAPPED lpOverlapped,  // 1、null：同步阻塞发送socket  2、指向overlapped：使用异步发送数据
  LPWSAOVERLAPPED_COMPLETION_ROUTINE lpCompletionRoutine  // 1、null:不使用  2、异步完成后调用函数
);
```



### WSARecv

```c
int WSARecv(
  SOCKET s,                        // 接收数据的套接字
  LPWSABUF lpBuffers,              // 接收数据的buffer
  DWORD dwBufferCount,             // buffer大小
  LPDWORD lpNumberOfBytesRecvd,    // 接收实际接收到的数据字节数，若使用异步，则为null
  LPDWORD lpFlags,
  LPWSAOVERLAPPED lpOverlapped,    // 指向overlapped，用于异步操作
  LPWSAOVERLAPPED_COMPLETION_ROUTINE lpCompletionRoutine  // 异步完成时调用
);
```



### WSABUF 缓冲区

* 专门用于socket通信发送数据使用

```c
typedef struct _WSABUF {
  ULONG len;  // 缓冲区的长度
  CHAR FAR *buf;  // 指向缓冲区的指针
} WSABUF, *LPWSABUF;
```



### WSAOVERLAPPED 结构体

```c
typedef struct _WSAOVERLAPPED {
  DWORD Internal;
  DWORD InternalHigh;
  DWORD Offset;
  DWORD OffsetHigh;
  HANDLE hEvent;
} WSAOVERLAPPED, *LPWSAOVERLAPPED;
```

**字段解释：**

1. **Internal (DWORD)**
   - 用于 Winsock 内部使用。

2. **InternalHigh (DWORD)**
   - 用于 Winsock 内部使用。

3. **Offset (DWORD)**
   - 文件偏移量，用于文件 I/O 操作。

4. **OffsetHigh (DWORD)**
   - 高位文件偏移量。

5. **hEvent (HANDLE)**
   - 用于通知操作完成的事件句柄。

这些函数和结构体用于处理高性能网络 I/O 操作，特别是在需要异步（非阻塞）处理的情况下非常有用。

## 16.2 IO完成端口

**异步 I/O 操作机制**

1. **I/O 请求初始化**
   - 当 `WriteFile` 函数被调用，并传入一个 `OVERLAPPED` 结构体时，操作系统知道这是一个异步操作。
   - `OVERLAPPED` 结构体中包含的信息（如文件偏移量和事件句柄）会被用于标识和管理这个特定的 I/O 请求。
2. **I/O 请求投递**
   - `WriteFile` 将 I/O 请求投递给操作系统的 I/O 管理器。
   - 如果设备驱动程序支持异步 I/O，它将立即返回，通常返回 `FALSE` 并设置 `GetLastError` 为 `ERROR_IO_PENDING`，表示操作正在进行中。
   - 这些请求会被添加到一个队列中，并由 I/O 管理器和设备驱动程序进行调度和处理。
3. **I/O 请求处理**
   - 操作系统内核会异步地处理这些 I/O 请求。当设备（如磁盘或网络设备）准备好执行 I/O 操作时，驱动程序会处理这些请求。
   - 处理过程中，设备驱动程序会将数据写入设备，或从设备读取数据。
4. **I/O 完成通知**
   - 一旦 I/O 操作完成，设备驱动程序会通知操作系统内核，==内核会更新== `OVERLAPPED` 结构体中的状态信息。
   - 如果 `OVERLAPPED` 结构体中包含一个事件句柄（`hEvent`），这个事件会被设置为有信号状态，通知等待该事件的线程 I/O 操作已经完成。
   - 同时，I/O 完成端口（如果存在）会收到一个完成包，==通知与该 I/O 操作相关的线程==。
5. **获取操作结果**
   - 应用程序可以通过 `GetOverlappedResult` 函数来获取 I/O 操作的结果，包括实际写入或读取的字节数。
   - `GetOverlappedResult` 函数会检查 `OVERLAPPED` 结构体的状态，如果操作已经完成，会返回操作结果；否则可以选择等待操作完成。

1. 创建完成端口、连接句柄到完成端口`CreateIoCompletionPort()`

```cpp
HANDLE WINAPI CreateIoCompletionPort(
  _In_     HANDLE    // 文件句柄： 串口h，网络socket ，INVALID_HANDLE_VALUE新完成端口
  _In_opt_ HANDLE    // ,带连接的完成端口
  _In_     ULONG_PTR CompletionKey,
  _In_     DWORD     NumberOfConcurrentThreads // 完成端口允许创建的线程数： 适合 threads = cores, 经验 threads = 2*cores + 2
);

```

```cpp

// 功能1：创建一个新的完成端口
HANDLE hCompletionPort = CreateIoCompletionPort(INVALID_HANDLE_VALUE, NULL, 0, 0);
if (hCompletionPort == NULL) {
    std::cerr << "CreateIoCompletionPort failed with error: " << GetLastError() << std::endl;
    return 1;
}
// 创建一个文件句柄（例如网络套接字）
HANDLE hFile = CreateFile(
    "example.txt",
    GENERIC_READ | GENERIC_WRITE,
    0,
    NULL,
    OPEN_EXISTING,
    FILE_FLAG_OVERLAPPED, // 指定采用异步的方式
    NULL
);
if (hFile == INVALID_HANDLE_VALUE) {
    std::cerr << "CreateFile failed with error: " << GetLastError() << std::endl;
    CloseHandle(hCompletionPort);
    return 1;
}

// 功能2：将文件句柄与完成端口关联
if (CreateIoCompletionPort(hFile, hCompletionPort, (ULONG_PTR)hFile, 0) == NULL) {
    std::cerr << "CreateIoCompletionPort failed with error: " << GetLastError() << std::endl;
    CloseHandle(hFile);
    CloseHandle(hCompletionPort);
    return 1;
}
```

## 16.3 overlappend

`OVERLAPPED` 结构体是 Windows API 中用于支持异步（重叠）I/O 操作的关键数据结构。它包含用于描述异步 I/O 操作状态和信息的字段，并允许操作系统在 I/O 操作完成时通知应用程序。

允许应用程序在发起 I/O 请求后无需等待其完成，可以继续执行其他任务。当 I/O 操作完成时，操作系统通过 `OVERLAPPED` 结构体通知应用程序。

在 `Windows.h` 中，`OVERLAPPED` 结构体定义如下：

```cpp
typedef struct _OVERLAPPED {
    ULONG_PTR Internal;      // I/O 操作的是否完成的状态
    ULONG_PTR InternalHigh;  // I/O 操作完成时传输的字节数
    union {                  // 指定从文件的哪个位置开始进行 I/O 操作
        struct {
            DWORD Offset;  
            DWORD OffsetHigh;
        };
        PVOID Pointer; 
    }; 
    HANDLE hEvent;           // 当 I/O 操作完成时系统会设置此事件。用于通知应用程序操作完成
} OVERLAPPED, *LPOVERLAPPED;：
```

下面是一个简单的示例，展示了如何使用 `OVERLAPPED` 结构体进行异步文件读取操作：

```cpp
#include <windows.h>
#include <iostream>

void WriteDataAsync(HANDLE hFile, const char* data, DWORD size) {
    // 1 初始化 OVERLAPPED 结构体
    OVERLAPPED overlapped = {0};
    overlapped.Offset = 0;
    overlapped.OffsetHigh = 0;
    overlapped.hEvent = CreateEvent(NULL, TRUE, FALSE, NULL);

    if (overlapped.hEvent == NULL) {
        std::cerr << "Failed to create event, error: " << GetLastError() << std::endl;
        return;
    }

    // 2 启动异步写操作
    DWORD bytesWritten;
    if (!WriteFile(hFile, data, size, NULL, &overlapped)) {
        DWORD error = GetLastError();
        if (error != ERROR_IO_PENDING) {
            std::cerr << "WriteFile failed, error: " << error << std::endl;
            CloseHandle(overlapped.hEvent);
            return;
        }
    }

    // 3 等待写操作完成
    if (WaitForSingleObject(overlapped.hEvent, INFINITE) == WAIT_OBJECT_0) {
        // 4 结果完成，获取
        if (GetOverlappedResult(hFile, &overlapped, &bytesWritten, FALSE)) {
            std::cout << "Successfully wrote " << bytesWritten << " bytes asynchronously." << std::endl;
        } else {
            std::cerr << "GetOverlappedResult failed, error: " << GetLastError() << std::endl;
        }
    } else {
        std::cerr << "WaitForSingleObject failed, error: " << GetLastError() << std::endl;
    }

    // 清理
    CloseHandle(overlapped.hEvent);
}

int main() {
    // 打开文件，使用 FILE_FLAG_OVERLAPPED 标志
    HANDLE hFile = CreateFile(
        "example.txt",                  // 文件名
        GENERIC_WRITE,                  // 写权限
        0,                              // 共享模式
        NULL,                           // 安全属性
        CREATE_ALWAYS,                  // 创建模式
        FILE_FLAG_OVERLAPPED,           // 文件属性
        NULL                            // 模板文件句柄
    );

    if (hFile == INVALID_HANDLE_VALUE) {
        std::cerr << "Failed to open file, error: " << GetLastError() << std::endl;
        return 1;
    }

    // 要写入的数据
    const char data[] = "Hello, Async World!";
    DWORD size = sizeof(data);

    // 使用异步方式写数据
    WriteDataAsync(hFile, data, size);

    // 关闭文件句柄
    CloseHandle(hFile);
    return 0;
}

```

## 16.4 WSAIoctl获取扩展指针

* winsock2.h提供的socket功能不够用
* 需要适配更多的功能，需要通过WSAIoctl获取指向新功能的socket，由func指向

```cpp
WSAIoctl(
    sock,
    SIO_GET_EXTENSION_FUNCTION_POINTER,
    &guid,
    sizeof(guid),
    &func,
    sizeof(func),
    &bytes,
    nullptr,
    nullptr
);

```



```cpp
#include <winsock2.h>
#include <mswsock.h>
#include <iostream>

GUID guidAcceptEx = WSAID_ACCEPTEX;

int main() {
    WSADATA wsaData;
    SOCKET sock;
    int result;
    
// 初始化 Winsock
result = WSAStartup(MAKEWORD(2, 2), &wsaData);
if (result != 0) {
    std::cerr << "WSAStartup failed with error: " << result << std::endl;
    return 1;
}

// 创建套接字
sock = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
if (sock == INVALID_SOCKET) {
    std::cerr << "socket failed with error: " << WSAGetLastError() << std::endl;
    WSACleanup();
    return 1;
}

// 获取 AcceptEx 函数指针  // 同样可以获取 ConnectEx函数指针
LPFN_ACCEPTEX lpfnAcceptEx = NULL;
DWORD bytes;
result = WSAIoctl(
    sock,
    SIO_GET_EXTENSION_FUNCTION_POINTER,
    &guidAcceptEx,
    sizeof(guidAcceptEx),
    &lpfnAcceptEx,
    sizeof(lpfnAcceptEx),
    &bytes,
    NULL,
    NULL
);

// 判断扩展是否获取成功
if (result == SOCKET_ERROR) {
    std::cerr << "WSAIoctl failed with error: " << WSAGetLastError() << std::endl;
    closesocket(sock);
    WSACleanup();
    return 1;
}

// 确认获取到的函数指针
if (lpfnAcceptEx != NULL) {
    std::cout << "Successfully retrieved AcceptEx function pointer." << std::endl;
} else {
    std::cerr << "Failed to retrieve AcceptEx function pointer." << std::endl;
}

// 清理
closesocket(sock);
WSACleanup();
return 0;
```


# 17 Window下udp协议

``` cpp
// server
#include <winsock2.h>
#include <ws2tcpip.h>
#include <iostream>

#pragma comment(lib, "ws2_32.lib")

int main() {
    WSADATA wsaData;
    SOCKET serverSocket;
    sockaddr_in serverAddr, clientAddr;
    int clientAddrSize, recvLen;
    char recvBuf[1024];

    // 初始化Winsock
    if (WSAStartup(MAKEWORD(2, 2), &wsaData) != 0) {
        std::cerr << "WSAStartup failed." << std::endl;
        return 1;
    }

    // 创建UDP套接字
    serverSocket = socket(AF_INET, SOCK_DGRAM, IPPROTO_UDP);
    if (serverSocket == INVALID_SOCKET) {
        std::cerr << "Socket creation failed." << std::endl;
        WSACleanup();
        return 1;
    }

    // 配置服务器地址结构
    serverAddr.sin_family = AF_INET;
    serverAddr.sin_addr.s_addr = INADDR_ANY;  // 监听服务器上所有地址 0.0.0.0
    serverAddr.sin_port = htons(8888);

    // 绑定套接字
    if (bind(serverSocket, (sockaddr*)&serverAddr, sizeof(serverAddr)) == SOCKET_ERROR) {
        std::cerr << "Bind failed." << std::endl;
        closesocket(serverSocket);
        WSACleanup();
        return 1;
    }

    std::cout << "Server is running and waiting for incoming messages..." << std::endl;
	
    // bind后可以接收发送数据
    // 循环接收数据
    while (true) {
        clientAddrSize = sizeof(clientAddr);
        // 阻塞
        recvLen = recvfrom(serverSocket, recvBuf, 1024, 0, (sockaddr*)&clientAddr, &clientAddrSize);
        if (recvLen == SOCKET_ERROR) {
            std::cerr << "recvfrom() failed." << std::endl;
            break;
        }

        recvBuf[recvLen] = '\0'; // 确保字符串以空字符结尾
        std::cout << "Received message: " << recvBuf << std::endl;

        // 发送响应回客户端
        const char* response = "Message received";
        sendto(serverSocket, response, strlen(response), 0, (sockaddr*)&clientAddr, clientAddrSize);
    }

    // 关闭套接字和清理Winsock
    closesocket(serverSocket);
    WSACleanup();

    return 0;
}
```

```cpp
// client
#include <winsock2.h>
#include <ws2tcpip.h>
#include <iostream>

#pragma comment(lib, "ws2_32.lib")

int main() {
    WSADATA wsaData;
    SOCKET clientSocket;
    sockaddr_in serverAddr;
    char sendBuf[1024] = "Hello, Server!";
    char recvBuf[1024];
    int serverAddrSize, recvLen;

    // 初始化Winsock
    if (WSAStartup(MAKEWORD(2, 2), &wsaData) != 0) {
        std::cerr << "WSAStartup failed." << std::endl;
        return 1;
    }

    // 创建UDP套接字
    clientSocket = socket(AF_INET, SOCK_DGRAM, IPPROTO_UDP);
    if (clientSocket == INVALID_SOCKET) {
        std::cerr << "Socket creation failed." << std::endl;
        WSACleanup();
        return 1;
    }

    // 配置服务器地址结构
    serverAddr.sin_family = AF_INET;
    serverAddr.sin_addr.s_addr = inet_addr("127.0.0.1"); // 服务器IP地址
    serverAddr.sin_port = htons(8888); // 服务器端口

    // 发送数据到服务器
    if (sendto(clientSocket, sendBuf, strlen(sendBuf), 0, (sockaddr*)&serverAddr, sizeof(serverAddr)) == SOCKET_ERROR) {
        std::cerr << "sendto() failed." << std::endl;
        closesocket(clientSocket);
        WSACleanup();
        return 1;
    }

    std::cout << "Message sent to server." << std::endl;

    // 接收服务器的响应
    serverAddrSize = sizeof(serverAddr);
    recvLen = recvfrom(clientSocket, recvBuf, 1024, 0, (sockaddr*)&serverAddr, &serverAddrSize);
    if (recvLen == SOCKET_ERROR) {
        std::cerr << "recvfrom() failed." << std::endl;
        closesocket(clientSocket);
        WSACleanup();
        return 1;
    }

    recvBuf[recvLen] = '\0'; // 确保字符串以空字符结尾
    std::cout << "Received response from server: " << recvBuf << std::endl;

    // 关闭套接字和清理Winsock
    closesocket(clientSocket);
    WSACleanup();

    return 0;
}

```

