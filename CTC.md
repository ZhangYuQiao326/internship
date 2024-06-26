要实现你描述的UDP通信协议，我们需要在C++中定义一些结构来封装数据帧的格式，然后使用UDP套接字进行数据的发送和接收。下面是一个基于你给出的数据帧格式的实现示例。

### 步骤 1: 定义数据帧结构

首先，我们需要定义一个结构体来表示数据帧的结构，包括序列化和反序列化的功能。

```cpp
#include <iostream>
#include <vector>
#include <cstdint>
#include <cstring>
#include <chrono>
#include <ctime>
#include <boost/crc.hpp>  // 使用Boost库进行CRC计算

struct Frame {
    uint32_t header = 0x40435443;  // 帧头@CTC
    std::vector<uint8_t> timestamp;  // 时间戳
    uint8_t frame_number;  // 帧序号
    uint8_t frame_type;  // 帧类型
    uint16_t frame_length;  // 帧长度
    std::vector<uint8_t> frame_content;  // 帧内容
    uint16_t crc;  // CRC校验

    // 序列化功能
    std::vector<uint8_t> serialize() const {
        std::vector<uint8_t> data;
        data.reserve(11 + frame_content.size());  // 预留空间

        // 添加帧头
        for (int i = 3; i >= 0; --i) {
            data.push_back((header >> (i * 8)) & 0xFF);
        }

        // 添加时间戳
        data.insert(data.end(), timestamp.begin(), timestamp.end());

        // 添加帧序号和帧类型
        data.push_back(frame_number);
        data.push_back(frame_type);

        // 添加帧长度
        data.push_back((frame_length >> 8) & 0xFF);
        data.push_back(frame_length & 0xFF);

        // 添加帧内容
        data.insert(data.end(), frame_content.begin(), frame_content.end());

        // 计算并添加CRC
        boost::crc_16_type crc_calculator;
        crc_calculator.process_bytes(data.data(), data.size());
        crc = crc_calculator.checksum();
        data.push_back((crc >> 8) & 0xFF);
        data.push_back(crc & 0xFF);

        return data;
    }
};
```

### 步骤 2: UDP 通信实现

接下来，我们需要创建UDP套接字来发送和接收数据。

```cpp
#include <boost/asio.hpp>

void send_udp_data(const std::vector<uint8_t>& data) {
    boost::asio::io_context io_context;
    boost::asio::ip::udp::socket socket(io_context);
    socket.open(boost::asio::ip::udp::v4());

    boost::asio::ip::udp::endpoint receiver_endpoint(
        boost::asio::ip::address::from_string("255.255.255.255"), 5551);

    socket.set_option(boost::asio::socket_base::broadcast(true));
    socket.send_to(boost::asio::buffer(data), receiver_endpoint);
}

int main() {
    Frame frame;
    frame.timestamp = { /* 适当的年月日时分秒格式化 */ };
    frame.frame_number = 1;
    frame.frame_type = 0x01;  // 心跳信息
    frame.frame_length = 1400;  // 假设内容长度
    frame.frame_content = std::vector<uint8_t>(1400, 0);  // 填充内容示例

    auto data = frame.serialize();
    send_udp_data(data);

    return 0;
}
```

### 说明：
1. **时间戳的处理**：这里我们留空了时间戳的具体实现。你需要根据实际需求生成当前的年月日时分秒格式。
2. **Boost库的使用**：示例中使用Boost库处理CRC计算和UDP套接字，你需要在你的开发环境中安装Boost库并正确配置。
3. **发送数据**：发送功能将数据广播到一个预设的端口，这里我们使用了全局广播地址`255.255.255.255`和默认端口`5551`。你可能需要根据实际情况调整这些设置。

这是一个基本的框架，你可以根据具体需求调



# CSM的信号处理

## CTC处理路径

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202405060924463.png" alt="image-20240506092411289" style="zoom:33%;" />



# windowsAPI

| API                            | 功能     |
| ------------------------------ | -------- |
| `PostQueuedCompletionStatus()` |          |
| `abort()`                      | 程序退出 |
| ``                             |          |
| ``                             |          |
| ``                             |          |
| ``                             |          |



```cpp
// loop_request.h
#define REQUEST_POST(_req, _loop)                                                  \
    do                                                                             \
    {                                                                              \
        if (!PostQueuedCompletionStatus((_loop)->iocp, 0, 0, &(_req)->overlapped)) \
        {                                                                          \
            abort();                                                               \
        }                                                                          \
    } while (0)
```

`PostQueuedCompletionStatus` 函数是 Windows API 中用于向 I/O 完成端口（IOCP）投递完成状态的函数。其原型为：

```c
BOOL PostQueuedCompletionStatus(
  HANDLE       CompletionPort,
  DWORD        dwNumberOfBytesTransferred,
  ULONG_PTR    dwCompletionKey,
  LPOVERLAPPED lpOverlapped
);
```

- `CompletionPort` 
- 指定了一个已经创建的 IOCP 的句柄，它是一个操作系统提供的对象，用于管理异步 I/O 完成状态的通知。
- 当某个异步 I/O 操作完成时，操作系统会将完成状态投递到指定的 IOCP 中，以便应用程序可以通过监听该 IOCP 来获取相关的完成状态并进行处理。
- `dwNumberOfBytesTransferred` 参数表示已经成功传输的字节数。对于某些操作，它可能不适用，可以将其设置为 0。
- `dwCompletionKey` 参数是一个用户定义的键值，它在投递完成状态时与完成状态一起传递。可以用它来标识完成状态的来源。可以设置为0
- `lpOverlapped` 参数是一个指向 OVERLAPPED 结构的指针，该结构包含了异步操作的相关信息。

`PostQueuedCompletionStatus` 的作用是将指定的完成状态异步地投递到指定的 IOCP 中，以便在异步操作完成时通知相关的线程。

### 2. abort 函数

`abort` 函数是 C 标准库中的一个函数，其原型为：

```c
void abort(void);
```

`abort` 函数的作用是立即终止当前程序的执行。当调用 `abort` 函数时，程序会立即退出，并且不会执行后续的代码。

```cpp
typedef struct _OVERLAPPED {
    // 这两个字段用于存储操作系统内部使用的数据
    ULONG_PTR Internal;
    ULONG_PTR InternalHigh;
    union {
        // 文件偏移量
        // 指定从文件中读取或写入数据的位置。
        struct {
            DWORD Offset;
            DWORD OffsetHigh;
        } DUMMYSTRUCTNAME;
        // 发起异步 I/O 操作时传递额外的数据给操作系统
        PVOID Pointer;
    } DUMMYUNIONNAME;

    // 在异步 I/O 操作中，应用程序可以选择等待一个事件以便在操作完成时得到通知。
    // 操作系统会在操作完成时将该事件设置为有信号状态。
    // 如果应用程序不需要等待操作完成，可以将该字段设置为 NULL。
    HANDLE  hEvent;
} OVERLAPPED, *LPOVERLAPPED;
```

## 高效windows网络编程

windows 高效网络编程 IOCP
1.  完成端口概述
2.  什么是重叠 IO
3.  IOCP 的工作原理
4.  同步 IO 和 异步 IO的区别
5.  windows 异步 IO 接口
6.  手撕 IOCP 网络编程案例



# 工作计划

5.13

下周任务：仔细阅读LoopWork剩余部分代码

以及：co_worker的所有代码

# executer调度框架

[同workflow](https://zhuanlan.zhihu.com/p/518265010)
