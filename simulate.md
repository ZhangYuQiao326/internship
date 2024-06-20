# Cmake

* `CMAKE_SOURCE_DIR`

CMake内置的一个变量，表示正在处理的当前CMakeLists.txt文件所在的目录的路径。换句话说，它指的是包含当前CMakeLists.txt文件的目录。

```cmake
cmake_minimum_required(VERSION 3.5)

project(WDTech.CSM2020.Tools.Simulate)

# 没有定义系统变量QT_DIR  报错
if(NOT DEFINED ENV{QT_DIR})
	message("Not Define QT_DIR")
else()
	
	# D:\software\Perfessional\QT5.15.2\5.15.2\msvc2019_64
    message("QT_DIR: $ENV{QT_DIR}")

    set(CMAKE_PREFIX_PATH $ENV{QT_DIR}) # Qt Kit Dir

	# 查看下路径 D:/Work/333/sources
	message("CMAKE_SOURCE_DIR: ${CMAKE_SOURCE_DIR}")
	
	# 设置输出目录
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/../bins/${PROJECT_NAME})
    set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/../bins/${PROJECT_NAME})
    set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/../bins/${PROJECT_NAME})

    remove_definitions(-DUNICODE)

	# 启用了CMake的自动工具支持，用于处理UI文件、MOC文件和资源文件。
    set(CMAKE_AUTOUIC ON)
    set(CMAKE_AUTOMOC ON)
    set(CMAKE_AUTORCC ON)

	# 查找并添加Qt5 Widgets模块
    find_package(Qt5 COMPONENTS Widgets REQUIRED)

``	# 添加可执行文件
    add_executable(${PROJECT_NAME} WIN32
        main.cpp

        
        
        
        ${CMAKE_SOURCE_DIR}/includes/utils/create_dump.cpp
    )

    
	# 系统依赖库
    set(SYS_LIBS
        ws2_32

        Qt5::Widgets
    )

	# 第三方库
    set(3RD_LIBS
        zip/zlib1
        
    )
	# 本地库
    set(LOCAL_LIBS 
            WDTech.CSM2020.Utils

    WDTech.CSM2020.Coroutine.ThreadPool
        WDTech.CSM2020.Coroutine.Loop
        WDTech.CSM2020.Coroutine.Log

        WDTech.CSM2020.Framework
    )
	
	# 链接库
    target_link_libraries(${PROJECT_NAME} PRIVATE 

        ${SYS_LIBS}
        ${LOCAL_LIBS}
        ${3RD_LIBS}
    )
	
	# 插件库
    set(PLUGIN_LIBS
        WDTech.CSM2020.Plugin.Dispatcher

        WDTech.CSM2020.Tools.Simulate.Plugin.MainWindow

        WDTech.CSM2020.Tools.Simulate.Plugin.Emulator.Front

        WDTech.CSM2020.Tools.Simulate.Plugin.Emulator.CBI.CRCC
        WDTech.CSM2020.Tools.Simulate.Plugin.Emulator.CBIRBC.CRCC
        WDTech.CSM2020.Tools.Simulate.Plugin.Emulator.CTC.CRCC
        WDTech.CSM2020.Tools.Simulate.Plugin.Emulator.DCQK.CRCC
        WDTech.CSM2020.Tools.Simulate.Plugin.Emulator.DYP.CRCC
        WDTech.CSM2020.Tools.Simulate.Plugin.Emulator.JZ.CRCC
        WDTech.CSM2020.Tools.Simulate.Plugin.Emulator.QJK.CRCC
        WDTech.CSM2020.Tools.Simulate.Plugin.Emulator.TCC.CRCC
        WDTech.CSM2020.Tools.Simulate.Plugin.Emulator.ZPW2000.CRCC
        WDTech.CSM2020.Tools.Simulate.Plugin.Emulator.ZPW2000Host.CRCC
    )

	# 添加依赖,构建本项目先构建依赖
    add_dependencies(${PROJECT_NAME}
        ${PLUGIN_LIBS}
    )
	
	# 调用自定义的COPY_DLLS函数，将DLL文件复制到可执行文件所在目录。
    COPY_DLLS(PRJ_NAME ${PROJECT_NAME} 3RD_LIBS ${3RD_LIBS} LOCAL_LIBS ${LOCAL_LIBS} PLUGIN_LIBS ${PLUGIN_LIBS})
endif()
```



![image-20240515152143095](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202405151521143.png)

# 1 设计标准

* 设置全局字体大小

```cpp
QFont font("Arial", 10);
qApp->setFont(font);
```

* 选项卡字体大小：10

```cpp
QTabBar* tabBar = ui->tabWidget->tabBar();
tabBar->setFont(QFont("Arial", 10));
```



# 2

## 1 mainWindow

```cpp
// emulator是单个仿真组件
Coroutine<void> MainWindow::init()
{
    auto &emulators = EmulatorManager::getInstance()->emulators();
    for (auto &emulator : emulators)
    {
        auto btn = new QPushButton(QString::fromLocal8Bit(emulator->name()));
        // 获取emulator的widget
        auto widget = emulator->widget();
        
        
        ui->verticalLayoutMainPage->addWidget(btn);
        ui->stackedWidgetMainPage->addWidget(widget);

        // 当按钮被点击时，Lambda表达式会检查当前显示的widget是否与模拟器的widget相同，
        // 如果不同，则将堆叠窗口的当前widget切换为模拟器的widget。
        connect(btn, &QPushButton::clicked, this,
                [=]()
                {
                    if (widget != ui->stackedWidgetMainPage->currentWidget())
                    {
                        ui->stackedWidgetMainPage->setCurrentWidget(widget);
                    }
                });
    }

    co_return;
}
```

## 2 

这段代码实现了一个名为 `CBISetParam` 的类，用于加载和初始化配置参数。下面是对代码的整体功能和每个函数的详细解释。

### 整体功能
`CBISetParam` 类负责从网络或文件加载特定配置参数，并将其存储在内部数据结构中。它还包括一些辅助函数来处理和初始化这些数据。

### 详细解释

#### CBISetParam 类的定义和构造函数

```cpp
#include "CBISetParam.h"

struct CBISetParam::Impl
{
    ConfigCBISetParam data;
    std::vector<std::string> paths;
    WorkerQueue queue;
};

CBISetParam::CBISetParam()
{
    m_impl = new Impl();
}

CBISetParam::~CBISetParam()
{
    delete m_impl;
}
```
- **`Impl`**：`CBISetParam` 类的私有实现，包含了 `ConfigCBISetParam` 数据、路径列表和一个工作队列。
- **`CBISetParam::CBISetParam`**：构造函数，初始化 `m_impl` 成员。
- **`CBISetParam::~CBISetParam`**：析构函数，删除 `m_impl` 成员，释放内存。

#### init 函数

```cpp
Coroutine<bool> CBISetParam::init(uint16_t zmId, uint16_t index, int32_t timeout)
{
    auto protocol = NetworkConfigInterface::getInstance()->protocol();

    constexpr uint32_t cmdType = CONFIG_STRUCT_STATION_CBISET_PARAM;
    constexpr uint32_t rspType = CONFIG_STRUCT_STATION_CBISET_PARAM_RET;
    stConfigIndexCmd cmd;
    cmd.index = index;
    ConfigCBISetParam configData;
    bool success = co_await protocol->getResponse<cmdType, rspType>(protocol->channels(), zmId, 0, cmd, configData, timeout);
    if (!success)
    {
        co_return false;
    }

    m_impl->data = configData;

    initData();

    co_return true;
}
```
- **功能**：从网络加载配置参数。
- **参数**：
  - `zmId`：站点 ID。
  - `index`：配置索引。
  - `timeout`：超时时间。
- **流程**：
  - 获取协议实例。
  - 定义命令和响应类型。
  - 发送请求并等待响应，将结果存储在 `configData` 中。
  - 如果成功，将 `configData` 存储在 `m_impl->data` 中，并调用 `initData` 进行初始化。

#### load 函数

```cpp
Coroutine<bool> CBISetParam::load(const std::string &zm, uint16_t index)
{
    auto pFileTr = FileConfigInterface::getInstance();
    std::string dir = "车站配置文件\\" + zm + "\\jk\\CBISet" + std::to_string(index) + ".ini";
    auto path = pFileTr->path() + dir;
    if (m_impl->paths.empty())
    {
        m_impl->paths.emplace_back(dir);
    }
    m_impl->data = co_await co_sync(&m_impl->queue, &CBISetParam::loadFile, this, std::ref(path));

    initData();

    co_return true;
}
```
- **功能**：从文件加载配置参数。
- **参数**：
  - `zm`：站点名称。
  - `index`：配置索引。
- **流程**：
  - 构建文件路径。
  - 如果路径列表为空，添加路径。
  - 使用 `co_sync` 协程同步调用 `loadFile` 函数加载文件，并将结果存储在 `m_impl->data` 中。
  - 调用 `initData` 进行初始化。

#### path 函数

```cpp
const std::vector<std::string> &CBISetParam::path() const
{
    return m_impl->paths;
}
```
- **功能**：返回路径列表。
- **返回值**：包含路径的向量。

#### GetData 函数

```cpp
const ConfigCBISetParam &CBISetParam::GetData() const
{
    return m_impl->data;
}
```
- **功能**：返回配置数据。
- **返回值**：配置数据对象。

#### loadFile 函数

```cpp
ConfigCBISetParam CBISetParam::loadFile(const std::string &path)
{
    ConfigCBISetParam param;

    IniUtils ini;
    ini.load(path);

    param.linkStatus = loadLinkStatus(ini);
    param.explainTypes = loadExplainTypes(ini);

    {
        auto count = atoi(ini.getKeyValue("联锁码位", "总数").c_str());
        for (int i = 0; i < count; i++)
        {
            auto params = StringUtils::split(ini.getKeyValue("联锁码位", std::to_string(i + 1)));
            assert(params.size() >= 4);

            auto &data = param.codeBits.emplace_back();

            size_t pos = 0;
            data.name = params[pos++];
            data.kglAd = atoi(params[pos++].c_str());
            data.dkglAd = atoi(params[pos++].c_str());
            data.explainCode = atoi(params[pos++].c_str());
        }
    }

    return param;
}
```
- **功能**：从指定文件加载配置数据。
- **参数**：
  - `path`：文件路径。
- **流程**：
  - 创建 `ConfigCBISetParam` 对象 `param`。
  - 使用 `IniUtils` 加载文件。
  - 加载链接状态和解释类型。
  - 获取联锁码位的总数，遍历每个联锁码位，解析参数并存储在 `param` 的 `codeBits` 向量中。

#### initData 函数

```cpp
void CBISetParam::initData()
{
    initExplain(m_impl->data.explainTypes);
}
```
- **功能**：初始化解释类型数据。
- **流程**：
  - 调用 `initExplain`，传入解释类型数据进行初始化。

### 总结
- **CBISetParam 类** 负责管理配置参数的加载和初始化。
- **构造函数和析构函数**：负责资源的分配和释放。
- **init 和 load 函数**：从网络或文件加载配置数据。
- **path 和 GetData 函数**：提供访问路径列表和数据的方法。
- **loadFile 函数**：具体从文件解析配置数据。
- **initData 函数**：初始化解释类型数据。

通过这些函数，`CBISetParam` 类实现了从不同来源（网络和文件）加载配置参数，并对这些参数进行处理和初始化。



# 3 组包

## 3.1 读取配置

[配置文件地址](D:\Work\333\bins\配置文件\车站配置文件\ZJJ\jk)

读取配置插件：dlls - fileInterface - station - jk



```cpp

```

## 3.2 CBI

## 3.3 CBI-RBC

### 3.3.1 协议

![image-20240611095453414](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202406110954496.png)

![image-20240611100029384](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202406111000813.png)

#  4 串口通信

## 串口PCB设置

```cpp
// serialPort_channel
bool SerialPortChannel::open()
{
    if (state() == CHANNEL_STATE_CONNECTED)
    {
        return true;
    }

    if (!m_impl->serialport->open(m_impl->comm.c_str()))
    {
        return false;
    }

    auto handle = m_impl->serialport->handle();
    // timeout
    COMMTIMEOUTS timeouts;
    GetCommTimeouts(handle, &timeouts);
    timeouts.ReadIntervalTimeout = 200; // 读取间隔超时
    timeouts.ReadTotalTimeoutConstant = 0;  // 读取操作没有总超时
    timeouts.ReadTotalTimeoutMultiplier = 0;
    SetCommTimeouts(handle, &timeouts);

    // rw queue
    SetupComm(handle, 100 * 1024, 100 * 1024);

    // dcb
    DCB dcb;
    GetCommState(handle, &dcb);
    if (m_impl->baudRate < CBR_110)
    {
        dcb.BaudRate = CBR_110;
    }
    else if (m_impl->baudRate > CBR_256000)
    {
        dcb.BaudRate = CBR_256000;
    }
    else
    {
        dcb.BaudRate = m_impl->baudRate;
    }

    dcb.Parity = m_impl->parity;
    dcb.ByteSize = m_impl->dataBit;
    dcb.StopBits = m_impl->stopBit;
    SetCommState(handle, &dcb);

    PurgeComm(handle, PURGE_TXABORT | PURGE_RXABORT | PURGE_TXCLEAR | PURGE_RXCLEAR);

    setState(CHANNEL_STATE_CONNECTED);

    return true;
}
```

## 读取串口

```cpp
// 初始化
m_unpack(new LengthFieldUnpackEx(
    config.bufLen,           // 缓冲区长度
    config.maxLen,           // 最大长度
    15,                      // 长度字段的偏移量
    2,                       // 长度字段的大小
    UNPACK_CODING_LITTEL_ENDIAN, // 使用小端字节序
    17,                      // 长度调整
    6,                       // 初始字节去除
    {char(0xEF), char(0xEF), char(0xEF), char(0xEF)} // 魔术字节
))

```

![image-20240604161115852](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202406041611895.png)

```cpp
bool LengthFieldUnpack::unpack(UnpackParams *params) const
{
    char *const buf = params->buffer.get();
    uint32_t bodyLen = 0;
    do
    {
        // 检查帧头是否是0xEF 0xEF 0xEF 0xEF
        if (!m_impl->frameHeader.empty())
        {
            // 定位帧头校验
            uint32_t headOffset = 0;
            bool bResult = false;
            while (true)
            {
                // 检查消息大小
                if (params->head + headOffset + (m_impl->frameHeader.length() - 1) >= params->bufLen)
                {
                    break;
                }

                bResult = true;
                for (size_t i = 0; i < m_impl->frameHeader.length(); i++)
                {
                    if (buf[params->head + i + headOffset] != m_impl->frameHeader[i])
                    {
                        headOffset++;
                        bResult = false;
                        break;
                    }
                }

                if (bResult)
                    break;
            }

            if (!bResult)
            {
                // 未识别到帧头
                headOffset = 0;
            }

            params->head += headOffset;
        }
    // 检查封装的消息（0xEF0xEF0xEf0xEF+。。。+ 数据域 +CRC + 结尾）大小是否超过缓冲区最大长度
    
        while (params->head + m_impl->lenOffset + m_impl->lenBytes <= params->offset)
    {
        bodyLen = 0;
        // // 偏移15位，p指向data len的位置，占2位
        unsigned char *p = (unsigned char *)(buf + params->head + m_impl->lenOffset);
        switch (m_impl->lenCoding)
        {
		// 小端编码：逐字节读取长度字段，低字节在前。大端编码：逐字节读取长度字段，高字节在前。
        case UNPACK_CODING_LITTEL_ENDIAN:
            for (uint32_t i = 0; i < m_impl->lenBytes; i++)
            {
                // 获取2位表示的data字段长度
                bodyLen |= ((uint32_t)*p++) << (i * 8);
            }
            break;
        case UNPACK_CODING_BIG_ENDIAN:
            for (uint32_t i = 0; i < m_impl->lenBytes; i++)
            {
                bodyLen = (bodyLen << 8) | (uint32_t)*p++;
            }
            break;
        default:
            abort();
            break;
        }

        // 计算整个消息的总大小17+datalen+6,如果总大小超过允许的最大长度，返回 false，表示长度错误。
        const uint32_t size = m_impl->bodyOffset + bodyLen + m_impl->tailBytes;
        if (size > m_impl->maxLen)
        {
            // len error
            return false;
        }

        if (params->head + size > params->offset)
        {
            // buffer not enough
            break;
        }

        auto message = std::make_shared<ReadMessage>();
        message->channel = params->channel;
        message->buffer = params->buffer;
        message->data = buf + params->head;
        message->size = size;
        params->messages.emplace_back(std::move(message));

        params->head += size;
    }

    params->index = params->head;
    params->tail = params->head + bodyLen + m_impl->tailBytes;

    return true;
}
```

```cpp
现在有crc16函数如下
    static uint16_t calcCbiCRC16Code(uint16_t init, const uint8_t *buf, uint32_t len)
{
    uint16_t i, j, crc = init;

    if (buf == nullptr || len == 0)
    {
        return 0;
    }

    for (i = 0; i < len; i++)
    {
        j = (crc >> 8) ^ buf[i];
        crc = (crc << 8) ^ g_cbiCrcTable[j];
    }

    return crc;
}，现在有数据std::vector<uint8_t> data，如何通过crc函数计算值
```

# 报错修改

## 1 读取配置

### 1.1 front

```cpp
Coroutine<void> FrontEmulatorForm::initStation(const char *path)
{
    m_set = co_await FileConfigInterface::getInstance()->GetZmIndexConfigInterface<FrontCommParam>(path, 1);
    m_kglConfig = co_await FileConfigInterface::getInstance()->GetZmConfigInterface<ISingleKglConfig>(path);
    m_kglTypeConfig = co_await FileConfigInterface::getInstance()->GetZmConfigInterface<IKglTypeCfg>("ZJJ");  // 修改

    initTreeWidgetFenJis();
    initTableKGLs();

    co_return;
}
```

