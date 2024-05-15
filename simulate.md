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

# 11

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



