学习资料 [爱编程的大丙](https://subingwen.cn/)



QT下载网址：[Index of /new_archive/qt](https://download.qt.io/new_archive/qt/)

百度网盘：嵌入式->qt->第二章

qt账号 zhangyuqiao26@gmail.com   Vw3G7@K,zZYjq7g

zhangyuqiao26@outlook.com Zyq0326.

QT 5.14.2 版本  【阿里网盘】



vc2022 + qt5.14.2 （msvc 2017）+ tools 2.8.1.6 

【vc配置插件教程】

https://blog.csdn.net/m0_62083249/article/details/124700712

【解决vc中点击ui文件报错问题】

https://blog.csdn.net/dengjin20104042056/article/details/122160103

【kit可选中，有黄色感叹号报错】

version中qmake的路径错误，系统自动选择的路径修改方式：找到qtversion.xml    toolchains.xml两个文件，修改路径保存





修改主题 https://ryuzhihao123.blog.csdn.net/article/details/70412310?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-70412310-blog-131055971.235%5Ev38%5Epc_relevant_sort_base2&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-70412310-blog-131055971.235%5Ev38%5Epc_relevant_sort_base2&utm_relevant_index=2

## 1 代码介绍

```cpp
// 主窗口
#include "widget.h"
#include <QApplication>

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    Widget w;
    w.show();

    //exec() 方法进入 Qt 的事件循环，开始处理事件队列中的事件。事件循环是 GUI 应用程序的核心部分，	它等待和分派事件，例如用户输入、绘图请求、网络事件等。
	// 一直运行，直到应用程序退出
    return a.exec();
}
```

![image-20230718142235686](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230718142235686.png)

### 1.1 pro文件介绍

* 使用qmake来build项目

```cpp
# 项目底层模块
QT       += core gui

# 版本大于4，额外添加widgets模块
greaterThan(QT_MAJOR_VERSION, 4): QT += widgets

CONFIG += c++11

DEFINES += QT_DEPRECATED_WARNINGS

# 源文件
SOURCES += \
    ctc.cpp \
    main.cpp \
    mainwindow.cpp \
    newwgt.cpp \
    系统/ctc/sources/ctcdevicework.cpp \
    系统/ctc/sources/kk.cpp

# 头文件
HEADERS += \
    ctc.h \
    mainwindow.h \
    newwgt.h \ \
    系统/ctc/headers/ctcdevicework.h \
    系统/ctc/headers/kk.h \
    系统/ctc/public/public.h

FORMS += \
    mainwindow.ui \
    newwgt.ui \

# 头文件寻找路径
INCLUDEPATH += \
    $$PWD/系统/ctc/headers
# 库文件寻找路径
LIBS += $$PWD/ffmepg-4.2/bin/avformat.lib \

# Default rules for deployment.
qnx: target.path = /tmp/$${TARGET}/bin
else: unix:!android: target.path = /opt/$${TARGET}/bin
!isEmpty(target.path): INSTALLS += target

```

### 1.2 cmakelist文件介绍

* 使用cmake来build项目

```cmake
cmake_minimum_required(VERSION 3.5)

project(CSM VERSION 0.1 LANGUAGES CXX)

# 自动识别ui文件
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 找第三方库
find_package(QT NAMES Qt6 Qt5 REQUIRED COMPONENTS Widgets)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Widgets)

# 项目文件
set(PROJECT_SOURCES
        main.cpp
        mainwindow.cpp
        mainwindow.h
        mainwindow.ui
)

# 若是qt版本高于6，通过qt_add_executable创建exe文件
if(${QT_VERSION_MAJOR} GREATER_EQUAL 6)
    qt_add_executable(CSM
        MANUAL_FINALIZATION
        ${PROJECT_SOURCES}
    )
# Define target properties for Android with Qt 6 as:
#    set_property(TARGET CSM APPEND PROPERTY QT_ANDROID_PACKAGE_SOURCE_DIR
#                 ${CMAKE_CURRENT_SOURCE_DIR}/android)
# For more information, see https://doc.qt.io/qt-6/qt-add-executable.html#target-creation
else()
	# 如果是安卓，则生成动态库
    if(ANDROID)
        add_library(CSM SHARED
            ${PROJECT_SOURCES}
        )
# Define properties for Android with Qt 5 after find_package() calls as:
#    set(ANDROID_PACKAGE_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/android")
    else()
    	# 生成可执行文件
        add_executable(CSM
            ${PROJECT_SOURCES}

            CSM-CTC/csm_ctc.h CSM-CTC/csm_ctc.cpp CSM-CTC/csm_ctc.ui
            pagemanger.h pagemanger.cpp
            CSM-RBC/csm_rbc.h CSM-RBC/csm_rbc.cpp CSM-RBC/csm_rbc.ui
            CSM-TSRS/csm_tsrs.h CSM-TSRS/csm_tsrs.cpp CSM-TSRS/csm_tsrs.ui
            CSM_DHJC/csm_dhjc.h CSM_DHJC/csm_dhjc.cpp CSM_DHJC/csm_dhjc.ui
            CSM_LMD/csm_lmd.h CSM_LMD/csm_lmd.cpp CSM_LMD/csm_lmd.ui
            CSM_DMS/csm_dms.h CSM_DMS/csm_dms.cpp CSM_DMS/csm_dms.ui
        )
    endif()
endif()

# =========================== 自己设置
# 设置头文件查找目录
include_directories(${CMAKE_SOURCE_DIR}
    ${CMAKE_SOURCE_DIR}/CSM-CTC
    ${CMAKE_SOURCE_DIR}/CSM_DHJC
    ${CMAKE_SOURCE_DIR}/CSM_DMS
    ${CMAKE_SOURCE_DIR}/CSM-RBC
    ${CMAKE_SOURCE_DIR}/CSM-TSRS
    ${CMAKE_SOURCE_DIR}/CSM_CTC
    ${CMAKE_SOURCE_DIR}/CSM_LMD
)

# 链接库
target_link_libraries(CSM PRIVATE Qt${QT_VERSION_MAJOR}::Widgets)

# Qt for iOS sets MACOSX_BUNDLE_GUI_IDENTIFIER automatically since Qt 6.1.
# If you are developing for iOS or macOS you should consider setting an
# explicit, fixed bundle identifier manually though.
if(${QT_VERSION} VERSION_LESS 6.1.0)
  set(BUNDLE_ID_OPTION MACOSX_BUNDLE_GUI_IDENTIFIER com.example.CSM)
endif()
set_target_properties(CSM PROPERTIES
    ${BUNDLE_ID_OPTION}
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
    MACOSX_BUNDLE TRUE
    WIN32_EXECUTABLE TRUE
)

include(GNUInstallDirs)
install(TARGETS CSM
    BUNDLE DESTINATION .
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)

if(QT_VERSION_MAJOR EQUAL 6)
    qt_finalize_executable(CSM)
endif()

```



### 1.2 数据类型

| 类型    | 功能                                                         |
| ------- | ------------------------------------------------------------ |
| QWidget | 窗口类：  用于创建具有用户界面的可视化窗口，及各种控件       |
| QAction | 操作类：它可以在菜单、工具栏、快捷键等场景中使用，代表用户可以执行的一个操作当用户触发 QAction 时，它会发出 `triggered()` 信号，可以通过连接到该信号的槽函数来处理用户操作 |
| QMenu   | 菜单类：它可以用于创建弹出式菜单、下拉菜单等。QMenu 可以包含多个 QAction 对象，它们作为菜单的选项。 |
|         |                                                              |



| 类型    | 注意事项                                                     |
| ------- | ------------------------------------------------------------ |
| QString | 1、显示时候带   “ ”  2、转char*  ：s.toUtf8().data()         |
|         | 格式化字符串：int a = 12;     int b = 22;    QString str = QString("这俩数字,x = %1，y = %2").arg(a).arg(b); |
| char *  | 显示时候不带   “ ”                                           |
| int     | 2、int -> QString   QString::number(2)                       |



### 1.3 创建项目类信息

<img src="C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230719153939235.png" alt="image-20230719153939235" style="zoom:50%;" />





## 2 控件 （QWedget类下）

* 按钮

| 操作     | widget           | butten                                 |
| -------- | ---------------- | -------------------------------------- |
| 创建     | /                | QPushButten()     btn->setParent(this) |
| 移动     | move()           | btn->move()                            |
| 尺寸     | resize()         | btn->resize()                          |
| 固定尺寸 | setFixedSize()   | /                                      |
| 文字     | setWindowTitle() | btn->setText()                         |
|          |                  | btn->                                  |
|          |                  |                                        |

```cpp
#include "widget.h"
#include "ui_widget.h"
#include <QPushButton>

Widget::Widget(QWidget *parent) :
    QWidget(parent),
    ui(new Ui::Widget)
{
    ui->setupUi(this);

    resize(900,600);
    setWindowTitle("第一个窗口");

    // 创建按钮
    // 法1
    QPushButton *btn = new QPushButton;
    btn->setParent(this);
    btn->setText("开始");
    btn->resize(70,50);
    btn->move(325,450);
    // 法2
    QPushButton * btn2 = new QPushButton("取消",this);
    btn2->resize(70,50);
    btn2->move(475,450);
}

Widget::~Widget()
{
    delete ui;
}

```

* 自定义类

1. 必须设置父类，用于调用qt的回收机制

   ```cpp
   // 方式1: 通过构造函数
   // parent: 当前窗口的父对象, 找构造函数中的 parent 参数即可,没有设为nullptr
   QWidget::QWidget(QWidget *parent = Q_NULLPTR, Qt::WindowFlags f = Qt::WindowFlags());
   QTimer::QTimer(QObject *parent = nullptr);
   
   // 方式2: 通过setParent()方法
   // 假设这个控件没有在构造的时候指定符对象, 可以调用QWidget的api指定父窗口对象
   void QWidget::setParent(QWidget *parent);
   void QObject::setParent(QObject *parent);
   
   ```

2. 如果想要在QT类中自定义信号槽, 需要满足一些条件, 并且有些事项也需要注意:

​	要编写新的类并且让其继承Qt的某些标准类
​	这个新的子类必须从QObject类或者是QObject子类进行派生
​	在定义类的头文件中加入 Q_OBJECT 宏

```cpp
class mydate : public Object
{
    Q_OBJECT // 添加，

public:
    mydate(QWidget *parent = nullptr); // 父类
    ~Q_OBJECT();
single:
    void eat();
   
    
};
```



## 3 信号

### 3.1 信号和槽函数

api信号

![image-20230718164015667](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230718164015667.png)

api槽函数

![image-20230718164842608](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230718164842608.png)

### 3.2 连接

* ==connect连接放在构造函数内==, 只用connect一次

#### 3.2.1 连接系统api的信号和槽函数

* this 可以省略

```cpp
// 打开
connect(btn2,&QPushButton::clicked,this,&Widget::close);

// 关闭
disconnect(btn2,&QPushButton::clicked,this,&Widget::close);
```

-------

####3.2.2 连接自定义信号和槽函数

```cpp
// teacher.h
// 自定义信号 1、无返回值 2、只用声明，不需要实现 3、可以有参数，可以重载
signals:
    void downClass();

public slots:
```

```cpp
// student.h
// 自定义槽函数 1、无返回值 2、需要声明+实现 3、可以有参数，可以重载
signals:

public slots:
    void treat();

// student.cpp
void Student::treat(){
    qDebug()<<"下课啦，回家吃饭！";
}
```

```cpp
// 参数1.3 传入指针
// 参数2，4 传入信号和槽函数的地址
connect(te,&Teacher::downClass,st,&Student::treat);

// emit 关键字：使用 emit 关键字可以发送信号。当信号被发出时，与之连接的槽函数将会被调用。
emit te->downClass();
   			
```

#### 3.2.3 重载

* 存在重载信号和槽函数时候，用函数指针指明地址

```cpp
// 1、downClass()  treat()
void (Teacher::*tp1)(void) = &Teacher::downClass;
void (Student::*sp1)(void) = &Student::treat;
connect(te,tp1,st,sp1);
classIsOver();
```

```cpp
// 1、downClass(QString name)  treat(QString name)
void (Teacher::*tp1)() = &Teacher::downClass;
void (Student::*sp1)() = &Student::treat;
connect(te,tp1,st,sp1);
classIsOver("name");
```

#### 3.2.4 lambda表达式

* 可以同时执行多个操作
* lambda表达式可以直接作为槽函数，而无需传入其地址

```cpp
       QPushButten * bt = new QPushButten(this);
connect(bt,&QPushButten::clicked,[=]{
    this->closed();
    emit te->downClass();
    qDebug<<"执行多个操作";
})
```

## 4 QMainWindow主窗口

### 4.1 mainwindow

* 设置程序名

```cpp
#include "mainwindow.h"
#include <QApplication>
#include <QDebug>
int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    MainWindow w;

    w.setWindowTitle("仿真中心");
    w.show();
    qDebug() << "我是要成为海贼王的男人!!!";
    return a.exec();
}
```



菜单栏

```cpp
QMenuBar *bar = new QMenuBar();
setMenuBar(bar);
// 1 添加菜单
QMenu *file_menu = bar->addMenu("文件");

QMenu *begin_menu = bar->addMenu("开始");
// 2 添加行为(菜单项)
QAction *new_action = file_menu->addAction("新建");
// 3 添加分割线
file_menu->addSeparator();

QAction *open_action = file_menu->addAction("打开");
```

以下是以表格形式呈现的`QAction`类的信号，包含描述：

| 信号            | 描述                                                         |
| --------------- | ------------------------------------------------------------ |
| `changed()`     | 当`QAction`的状态（例如可用性、文本、图标等）发生变化时发出。 |
| `hovered()`     | 当鼠标光标悬停在`QAction`上时发出。                          |
| `toggled(bool)` | 当`QAction`的状态发生变化时发出，例如复选框或切换按钮的情况。参数`bool`表示新的状态。 |
| `trigger()`     | 当调用`QAction::trigger()`方法时发出，通常用于以编程方式手动触发操作。 |

* 工具栏
* 用来存放菜单中的功能，功能由菜单创建

```cpp
// 二、创建工具栏（可以多个）
QToolBar *toolBar = new QToolBar(this);
// 1.1 添加到窗口
addToolBar(Qt::LeftToolBarArea,toolBar);
// 1.2 设置是否允许拖动
toolBar->setMovable(true);
// 1.3 设置停靠范围
toolBar->setAllowedAreas(Qt::LeftToolBarArea | Qt::RightToolBarArea);
// 1.4 设置是否浮动
toolBar->setFloatable(false);

// 2.1 设置工具（注意只能放QAction类型、控件）
toolBar->addAction(open_action);
toolBar->addSeparator();
toolBar->addAction(new_action);

QPushButton *bt = new QPushButton("按钮",this);
toolBar->addWidget(bt);
```

* 状态栏

```cpp
QStatusBar * stBar = new QStatusBar();
setStatusBar(stBar);
// 3.2 放置标签
QLabel *lab1 = new QLabel("左侧提示信息",this);
QLabel *lab2 = new QLabel("右侧提示信息",this);

stBar->addWidget(lab1);
stBar->addPermanentWidget(lab2);
```

* 铆接部件

```cpp
QDockWidget *doc = new QDockWidget("浮动窗口",this);
addDockWidget(Qt::BottomDockWidgetArea,doc);
```

* 中心部件

```cpp
QTextEdit *edit = new QTextEdit(this);
setCentralWidget(edit);
```

---------

小结

| 类型         | 创建                             | 嵌入                     | 添加功能                    | 添加扩展                      |
| ------------ | -------------------------------- | ------------------------ | --------------------------- | ----------------------------- |
| 菜单栏 1个   | new QMenuBar(this)               | setMenuBar(bar)          | bar->addMenu()              | new = Menu->addAction(“新建”) |
| 工具栏 n个   | new QToolBar(this)               | addToolBar(Qt::, bar)    | bar->addAction(new_action)  |                               |
| 状态栏 1个   | new QStatusBar(this)             | setStatusBar(bar)        | new QLabel("提示信息",this) | bar->addWidget(lab1);         |
| 铆接部件 n个 | new QDockWidget("浮动窗口",this) | addDockWidget(Qt::, bar) |                             |                               |
| 中心部件 1个 | new QTextEdit(this)              | setCentralWidget(edit)   |                             |                               |

## 5 控件

### 5.1 QComboBox

* 下拉菜单

| 方法                                                         | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `addItem(const QString &text, const QVariant &userData = QVariant())` | 向 ComboBox 中添加一个文本项，并可选择关联一个自定义数据。   |
| `insertItem(int index, const QString &text, const QVariant &userData = QVariant())` | 在指定位置插入一个文本项，并可选择关联一个自定义数据。       |
| `removeItem(int index)`                                      | 移除指定索引处的项。                                         |
| `clear()`                                                    | 清空 ComboBox 中的所有项。                                   |
| `setCurrentIndex(int index)`                                 | 将当前选中项设置为指定索引处的项。                           |
| `currentIndex()`                                             | 返回当前选中项的索引。                                       |
| `currentText()`                                              | 返回当前选中的项的文本。                                     |
| `currentData()`                                              | 返回当前选中的项的关联数据（如果存在）                       |
| `count()`                                                    | 返回 ComboBox 中的项数。                                     |
| `itemText(int index)`                                        | 返回指定索引处项的文本。通过ui添加的值                       |
| `itemData(int index)`                                        | 返回指定索引处项关联的自定义数据。                           |
| `setItemText(int index, const QString &text)`                | 设置指定索引处项的文本。                                     |
| `setItemData(int index, const QVariant &userData)`           | 设置指定索引处项关联的自定义数据。                           |
| `setEditable(bool editable)`                                 | 设置 ComboBox 是否可编辑。                                   |
| `isEditable()`                                               | 返回 ComboBox 是否可编辑。                                   |
| `setEnabled(bool enabled)`                                   | 设置 ComboBox 是否可用。                                     |
| `isEnabled()`                                                | 返回 ComboBox 是否可用。                                     |
| `setToolTip(const QString &tip)`                             | 设置 ComboBox 的工具提示。                                   |
| `setIconSize(const QSize &size)`                             | 设置 ComboBox 中图标的大小。                                 |
| `setInsertPolicy(QComboBox::InsertPolicy policy)`            | 设置插入策略，指定如何插入新项。                             |
| `setMaxVisibleItems(int maxItems)`                           | 设置最大可见项数。                                           |
| `setMinimumContentsLength(int characters)`                   | 设置 ComboBox 的最小内容长度（以字符数为单位），以确保下拉框的大小适合显示内容。 |
| `setModel(QAbstractItemModel *model)`                        | 设置 ComboBox 的数据模型，用于提供数据。                     |
| `view()`                                                     | 返回 ComboBox 的下拉列表视图，可以用于自定义下拉列表的外观和行为。 |

-------

```cpp
QComboBox* comb = new QComboBox;
// 获取当前的索引
comb -> currentIndex();
// 设置当前的索引
comb -> setCurrentIndex(1);
// 填入选项
comb->addItems({ QString::fromLocal8Bit("占用"), QString::fromLocal8Bit("空闲") });

// 遍历数组插入选项
std::vector<QString> items = {"Option 1", "Option 2", "Option 3"};
for (const auto& item : items) {
    comboBox->addItem(item);
}
// combox插入单元格内
table->setCellWidget(row, col, box);


```

### 5.2 tableWidget

#### 5.2.1 基础设置

```cpp
// 表格操作
#include <QApplication>
#include <QTableWidget>
#include <QTableWidgetItem>
#include <QVBoxLayout>
#include <QWidget>

class TableDemo : public QWidget {
public:
    TableDemo(QWidget *parent = nullptr) : QWidget(parent) {
        // 创建一个QTableWidget
        QTableWidget *tableWidget = new QTableWidget(this);
        
        // 设置行数和列数
        tableWidget->setRowCount(10);  // 设置10行
        tableWidget->setColumnCount(3);  // 设置3列
        
        // 设置表头
        QStringList headers;
        headers << QString::fromLocal8Bit("序号") << QString::fromLocal8Bit("名称") << QString::fromLocal8Bit("状态");
        tableWidget->setHorizontalHeaderLabels(headers);
        
        // 插入行
        int row = tableWidget.rowCount();
        tableWidget.insertRow(row);
        
        // 填充表格项
        tableWidget->setItem(0, 0, new QTableWidgetItem("1"));
        tableWidget->setItem(0, 1, new QTableWidgetItem("240DG"));
        tableWidget->setItem(0, 2, new QTableWidgetItem("空闲"));
        
        tableWidget->setItem(1, 0, new QTableWidgetItem("2"));
        tableWidget->setItem(1, 1, new QTableWidgetItem("238DG"));
        tableWidget->setItem(1, 2, new QTableWidgetItem("空闲"));

        // 隐藏行号
        QHeaderView *header = tblList->verticalHeader();
		header->setHidden(true);
        

    }
};

int main(int argc, char *argv[]) {
    QApplication app(argc, argv);
    TableDemo demo;
    demo.show();
    return app.exec();
}

```

####  5.3.1 表格格式设计

##### 1 基础操作

下面是`ResizeMode`参数的几种常见取值及其作用：

- `QHeaderView::Interactive`：允许用户通过拖动调整部分的大小。
- `QHeaderView::Fixed`：固定大小，部分的大小不会改变。
- `QHeaderView::Stretch`：自动拉伸，部分会根据父控件的大小自动拉伸。
- `QHeaderView::ResizeToContents`：根据内容调整大小，部分的大小会根据其内容的大小自动调整。

【出现问题：ResizeToContents】、

设置该模式时，对表格一列进行修改，遍历表格时会非常慢，因为需要计算每个单元格的表格大小，不建议用

```cpp
// 设置表格的大小策略，表头最后一列扩展整个表格
tableWidget->horizontalHeader()->setStretchLastSection(true);
// 最后一行全部扩展
tableWidget->verticalHeader()->setStretchLastSection(true);
        
// 表头单元格大小均匀分布
tableWidget->horizontalHeader()->setSectionResizeMode(QHeaderView::Stretch);
tableWidget->verticalHeader()->setSectionResizeMode(QHeaderView::Stretch);

// 表头单元格随文本内容调节（列）
tableWidget->horizontalHeader()->
setSectionResizeMode(QHeaderView::ResizeToContents);
// 行大小随文本调节----卡死，不建议使用
//tableWidget->verticalHeader()->
//setSectionResizeMode(QHeaderView::ResizeToContents);

// 不允许修改单元格内容
tableWidget->setEditTriggers(QAbstractItemView::NoEditTriggers);
```

##### 2 部分列允许编辑

```cpp
QStringList str;
str << QString::number(index + 1) << QString::fromLocal8Bit(data.name.c_str()) << QString::number(data.kglAd) << QString::fromLocal8Bit(state.c_str())<< QString::number(0);

// 设置数据的时候修改单个单元格的编辑模式
// 不再使用 table->setEditTriggers(QAbstractItemView::NoEditTriggers);
for (int col = 0; col < str.size() && col < table->columnCount(); ++col)
{
	QTableWidgetItem* item = new QTableWidgetItem(str[col]);
	table->setItem(index, col, item);
	if (col == 4) {
		item->setFlags(item->flags() | Qt::ItemIsEditable); 
	}
	else {
		item->setFlags(item->flags() & ~Qt::ItemIsEditable); 
	}
}
index++;
```



#### 5.3.2 单元格操作

##### 1 基础操作

```cpp
// 创建单元格
QTableWidgetItem *item0 = new QTableWidgetItem("Item 1");
tableWidget.setItem(row, 0, item0);

// 获取存在的单元格
QTableWidgetItem* item = table->item(row, column);

// 删除单元格内容
table->takeItem(row, col); 
```

| 接口                                       | 描述                                           |
| ------------------------------------------ | ---------------------------------------------- |
| `setText(const QString &text)`             | 设置单元格的文本内容为给定的字符串 `text`。    |
| `text() const`                             | 返回单元格当前的文本内容。                     |
| `setData(int role, const QVariant &value)` | 设置单元格的特定角色的数据为给定的值 `value`。 |
| `data(int role) const`                     | 返回单元格的特定角色的数据。                   |
| `column() const`                           | 返回单元格所在的列索引。                       |
| `row() const`                              | 返回单元格所在的行索引。                       |

`setText` 和 `setData` 是 `QTableWidgetItem` 中的两个不同方法，它们在功能和用法上有一些区别。

```cpp
QTableWidgetItem *item = new QTableWidgetItem();
item->setText("Hello, World!");
// 等同于
item->setData(Qt::DisplayRole, "Hello, World!");
```

```cpp
QTableWidgetItem *item = new QTableWidgetItem();
item->setData(Qt::DisplayRole, "Hello, World!"); // 设置显示文本
item->setData(Qt::DecorationRole, QIcon("icon.png")); // 设置图标
item->setData(Qt::ToolTipRole, "This is a tooltip"); // 设置工具提示
```

##### 2 单元格添加下拉框

| 接口                                                         | 描述                   |
| ------------------------------------------------------------ | ---------------------- |
| `table.setCellWidget(row, col, comboBox)`                    | 单元格插入combobox     |
| `QComboBox *comboBox = qobject_cast<QComboBox *>(table.cellWidget(row, col));` | 获取单元格内的combobox |

```cpp
#include <QApplication>
#include <QTableWidget>
#include <QComboBox>
#include <QVBoxLayout>
#include <QHeaderView>

class ComboBoxTable : public QWidget {
    Q_OBJECT
public:
    ComboBoxTable(QWidget *parent = nullptr) : QWidget(parent) {
        QVBoxLayout *layout = new QVBoxLayout(this);

        // 创建表格，6行2列
        tableWidget = new QTableWidget(6, 2, this);
        tableWidget->setHorizontalHeaderLabels(QStringList() << "Label" << "ComboBox");
        tableWidget->horizontalHeader()->setStretchLastSection(true);

        // 插入第1种ComboBox到前两行
        for (int i = 0; i < 2; ++i) {
            QComboBox *comboBox1 = new QComboBox(this);
            comboBox1->addItems({"Option A1", "Option A2", "Option A3"});
            connect(comboBox1, QOverload<int>::of(&QComboBox::currentIndexChanged),
                    this, &ComboBoxTable::onComboBoxChanged);
            tableWidget->setCellWidget(i, 1, comboBox1);
        }

        // 插入第2种ComboBox到中两行
        for (int i = 2; i < 4; ++i) {
            QComboBox *comboBox2 = new QComboBox(this);
            comboBox2->addItems({"Option B1", "Option B2", "Option B3"});
            connect(comboBox2, QOverload<int>::of(&QComboBox::currentIndexChanged),
                    this, &ComboBoxTable::onComboBoxChanged);
            tableWidget->setCellWidget(i, 1, comboBox2);
        }

        // 插入第3种ComboBox到后两行
        for (int i = 4; i < 6; ++i) {
            QComboBox *comboBox3 = new QComboBox(this);
            comboBox3->addItems({"Option C1", "Option C2", "Option C3"});
            connect(comboBox3, QOverload<int>::of(&QComboBox::currentIndexChanged),
                    this, &ComboBoxTable::onComboBoxChanged);
            tableWidget->setCellWidget(i, 1, comboBox3);
        }

        layout->addWidget(tableWidget);
        setLayout(layout);
    }

private slots:
    void onComboBoxChanged(int index) {
        // 获取发送信号的ComboBox
        QComboBox *comboBox = qobject_cast<QComboBox*>(sender());
        if (comboBox) {
            // 获取ComboBox所在的行
            int row = -1;
            for (int i = 0; i < tableWidget->rowCount(); ++i) {
                if (tableWidget->cellWidget(i, 1) == comboBox) {
                    row = i;
                    break;
                }
            }

            if (row != -1) {
                QString selectedItem = comboBox->currentText();
                qDebug() << "Row" << row << "ComboBox changed to" << selectedItem;
            }
        }
    }

private:
    QTableWidget *tableWidget;
};

int main(int argc, char *argv[]) {
    QApplication app(argc, argv);
    ComboBoxTable window;
    window.show();
    return app.exec();
}

#include "main.moc"

```



#### 5.2.4 单元格信号

在 Qt 的 `QTableWidget` 中，单元格可以响应多种用户操作。以下是一些常见的单元格操作和对应的信号：

| 操作                           | 描述                                                 | 信号                                                         |
| ------------------------------ | ---------------------------------------------------- | ------------------------------------------------------------ |
| 单击                           | 用户单击单元格。                                     | `cellClicked(int row, int column)`                           |
| 双击                           | 用户双击单元格。                                     | `cellDoubleClicked(int row, int column)`                     |
| 编辑开始                       | 用户开始编辑单元格内容。                             | `cellActivated(int row, int column)`                         |
| 编辑结束                       | 用户完成对单元格的编辑。                             | `cellChanged(int row, int column)`                           |
| 单元格被选中                   | 单元格被选中（可能是通过鼠标或键盘操作）。           | `cellEntered(int row, int column)`                           |
| 单元格被选择                   | 用户选择单元格（可能是通过鼠标拖动选择多个单元格）。 | `itemSelectionChanged()`                                     |
| 进入单元格（悬停）             | 鼠标悬停在单元格上。                                 | `cellEntered(int row, int column)`                           |
| 单元格获得焦点                 | 单元格获得焦点。                                     | `cellActivated(int row, int column)`                         |
| 单元格文本编辑完成（失去焦点） | 用户完成对单元格文本的编辑并离开该单元格。           | `itemChanged(QTableWidgetItem *item)`                        |
| 右键点击单元格                 | 用户右键点击单元格，通常用于显示上下文菜单。         | 通常通过 `QTableWidget::customContextMenuRequested` 信号处理 |
| 拖动单元格                     | 用户拖动单元格（拖放操作）。                         | `cellPressed(int row, int column)`                           |



```cpp
#include <QApplication>
#include <QTableWidget>
#include <QVBoxLayout>
#include <QWidget>
#include <QDebug>

class MainWidget : public QWidget
{
    Q_OBJECT

public:
    MainWidget(QWidget *parent = nullptr);

private slots:
    void onCellClicked(int row, int column);
    void onCellDoubleClicked(int row, int column);
    void onCellEntered(int row, int column);
    void onCellChanged(int row, int column);

private:
    QTableWidget *table;
};

MainWidget::MainWidget(QWidget *parent)
    : QWidget(parent)
{
    table = new QTableWidget(5, 5, this);
    QVBoxLayout *layout = new QVBoxLayout;
    layout->addWidget(table);
    setLayout(layout);

    // 设置所有单元格的默认值为0
    for (int row = 0; row < table->rowCount(); ++row) {
        for (int column = 0; column < table->columnCount(); ++column) {
            table->setItem(row, column, new QTableWidgetItem("0"));
        }
    }

    // 连接信号到槽函数
    connect(table, &QTableWidget::cellClicked, this, &MainWidget::onCellClicked);
    connect(table, &QTableWidget::cellDoubleClicked, this, &MainWidget::onCellDoubleClicked);
    connect(table, &QTableWidget::cellEntered, this, &MainWidget::onCellEntered);
    connect(table, &QTableWidget::cellChanged, this, &MainWidget::onCellChanged);
}

void MainWidget::onCellClicked(int row, int column)
{
    qDebug() << "Cell clicked at (" << row << ", " << column << ")";
}

void MainWidget::onCellDoubleClicked(int row, int column)
{
    qDebug() << "Cell double-clicked at (" << row << ", " << column << ")";
}

void MainWidget::onCellEntered(int row, int column)
{
    qDebug() << "Cell entered at (" << row << ", " << column << ")";
}

void MainWidget::onCellChanged(int row, int column)
{
    qDebug() << "Cell changed at (" << row << ", " << column << ")";
}

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    MainWidget w;
    w.show();
    return a.exec();
}
```

```cpp
// 双击 
connect(ui->tableWidget_kglzt, &QTableWidget::cellDoubleClicked, this, &CBIEmulatorForm::on_CellDoubleClicked);
// slots
void CBIEmulatorForm::on_CellDoubleClicked(int row, int column)
{
    // 第五列双击有效
    if (column == 4) {
        QTableWidgetItem* item = ui->tableWidget_kglzt->item(row, column);
        if (item->text() == "0") {
            item->setText("1");
        }
        else if (item->text() == "1") {
            item->setText("0");
        }
    }
}
```



* 设置表头字体属性

  ```cpp
  QFont font ;//定义一个字体变量
  font.setBold(true);  //设置粗体
  table->horizontalHeader()->setFont(font);//把字体变量属性加进表头中
  ```

  

* 设置表头高度

  ```cpp
  table->horizontalHeader()->setFixedHeight(25); //设置表头的高度为25
  ```

* 设置表头宽度

  ```cpp
   table->horizontalHeader()->resizeSection(0,180); //设置表头第1列的宽度为180
  ```

* 设置表格行高

  ```cpp
  table->verticalHeader()->setDefaultSectionSize(10); //设置行高为10
  ```

* 设置表格列宽

  ```cpp
  table->horizontalHeader()->setDefaultSectionSize(15)
  ```

* 表格列宽自适应拉伸充满整个表格，且均匀分布

  ```cpp
  table->horizontalHeader()->setSectionResizeMode(QHeaderView::Stretch);
  ```

* 设置表大小

  ```cpp
  table->setFixedWidth(ui->tabwgt->width());
  ui->table1->setFixedHeight(tableHeight)
  ```

* 移动表位置

  ```cpp
  // 将表格的左边与tabWidget的左边重合（左边重合，）
  // move(x,y)将控件的左上角坐标点移动到x y处
  ui->table1->move(ui->tabwgt->geometry().left(), ui->table1->geometry().left());
  // 将表格的下边与tabWidget的下边重合
  ui->table1->move(ui->table1->geometry().left(), ui->tabwgt->geometry().bottom() - tableHeight);
  ```

* 无边框

  ```cp
  table->setFrameShape(QFrame::NoFrame); //设置无边框
  ```

####  5.2.5 模板

#####  1 调整表格样式：

![image-20240612115421868](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202406121154373.png)

```cpp
#include <QTableWidget>
void initPerTable(QTableWidget *table)
{
    // 设置表头前需要先设置行号
    table->setColumnCount(6);

	QStringList headers;
	headers << QString::fromLocal8Bit("序号") << QString::fromLocal8Bit("名称") << QString::fromLocal8Bit("开关量序号") << QString::fromLocal8Bit("多开关量序号") << QString::fromLocal8Bit("状态") << QString::fromLocal8Bit(" ");
    table->setHorizontalHeaderLabels(headers);

    table->setShowGrid(true);
	
    // 隐藏行号
	QHeaderView* header = table->verticalHeader();
	header->setHidden(true);
	
    // 最后一列全部扩展
    table->horizontalHeader()->setStretchLastSection(true);
    
    // 表头根据内容自由间距
    table->horizontalHeader()->setSectionResizeMode(QHeaderView::ResizeToContents);
	// 禁止编辑
    table->setEditTriggers(QAbstractItemView::NoEditTriggers);

}
```

##### 2 一次写入所有数据

```cpp
void CBIRBCEmulatorForm::loadPerTableWithData(QTableWidget* table, std::vector<SKglConfig>vec)
{
    int index = 0;
    table->setRowCount(vec.size());
	
    // 按行填入
    for (auto &data : vec)
    {
        QStringList str;
        str << QString::number(index + 1) << QString::fromLocal8Bit(data.strKglName.c_str()) << QString::number(data.kglOrder) << QString::number(data.dkglOrder);
        
		for (int col = 0; col < str.size() && col < table->columnCount(); ++col)
		{
			QTableWidgetItem* item = new QTableWidgetItem(str[col]);
			table->setItem(index, col, item);
		}
		index++;
    }
}
```

##### 3 动态末尾追加写入

```cpp
// 添加一行
static void addOneRowInTable(QTableWidget *table, QStringList vals) 
{
	int count = table->rowCount();
	table->insertRow(count);

	QTableWidgetItem* item;
	for (int col = 0; col < table->columnCount() && col < vals.size(); col++)
	{
		item = new QTableWidgetItem(vals[col]);
		table->setItem(count, col, item);

	}
}
// 添加多行
void addRowsAndSetValues(int n) {
    int rowCount = tableWidget->rowCount();  // 获取当前行数

    // 添加n行
    for (int i = 0; i < n; ++i) {
        tableWidget->insertRow(rowCount + i);  // 在末尾添加新行
    }

    // 赋值给新添加的行
    for (int i = rowCount; i < rowCount + n; ++i) {
        for (int j = 0; j < tableWidget->columnCount(); ++j) {
            tableWidget->setItem(i, j, new QTableWidgetItem(QString("New Item %1,%2").arg(i + 1).arg(j + 1)));
        }
    }
}

void VOBCEmulatorForm::loadData()
{
	QTableWidget* table = ui->tableWidget_ztl;

	auto config = m_param->GetData().vecTrainStateConfig;
	QStringList vals;
	static int index = 1;
	for (auto& data : config)
	{
		vals << QString::number(index++) << QString::fromLocal8Bit(data.name.c_str()) << QString::number(0) << QString::number(0);
		addOneRowInTable(table, vals);
		vals.clear();
	}
}
```



##### 4 选中行加深色

```cpp
// 多行
void highLightRows(std::vector<int> vecRow)
{
    if (vecRow.size() == 0) return;
    
    QTableWidget* table = ui->tableWidget_kglzt;
    table->clearSelection();
    for (int row : vecRow) {
        for (int column = 0; column < table->columnCount(); ++column) {
            QTableWidgetItem* item = table->item(row, column);
            if (item) item->setSelected(true);
        }
    }

    table->scrollToItem(table->item(vecRow.front(), 0));    
    return;
}

// 单击选中一行
ui->tableWidget_bjxx->setSelectionBehavior(QAbstractItemView::SelectRows);
```

##### 5 双击单元格触发

```cpp
connect(table, &QTableWidget::cellDoubleClicked, this, &JZEmulatorForm::on_CellDoubleClicked);

private slots:
	void on_CellClicked(int row, int column);
void JZEmulatorForm::on_CellDoubleClicked(int row, int column)
{
    // 获取当前调用函数的表格
	QTableWidget* table = qobject_cast<QTableWidget*>(sender());
	if (column == 3) {
		QTableWidgetItem* item = table->item(row, column);
        // 根据不同表格进行不同的操作
		if (table == ui->tableWidget_jzqd)
		{
			if (item->text() == QString::fromLocal8Bit("空闲")) {
				item->setText(QString::fromLocal8Bit("占用"));
			}
			else if (item->text() == QString::fromLocal8Bit("占用")) {
				item->setText(QString::fromLocal8Bit("空闲"));
			}
		}
		else if(table == ui->tableWidget_txyc || table == ui->tableWidget_swsbgz || table == ui->tableWidget_snsbgz)
		{
			if (item->text() == QString::fromLocal8Bit("正常")) {
				item->setText(QString::fromLocal8Bit("故障"));
			}
			else if (item->text() == QString::fromLocal8Bit("故障")) {
				item->setText(QString::fromLocal8Bit("正常"));
			}
		}
		else if (table == ui->tableWidget_snbkbsd)
		{
			if (item->text() == QString::fromLocal8Bit("灯灭")) {
				item->setText(QString::fromLocal8Bit("灯亮"));
			}
			else if (item->text() == QString::fromLocal8Bit("灯亮")) {
				item->setText(QString::fromLocal8Bit("灯灭"));
			}
		}
	
		
	}
}
```

##### 6 修改单元格触发

```cpp
// 指定操作不触发单元格
// 阻断信号
table->blockSignals(true);
xxx
table->blockSignals(false);
```

```cpp
connect(ui->tableWidget_mnl, &QTableWidget::cellChanged, this, &VOBCEmulatorForm::on_CellChanged);

private slots:
	void on_CellChanged(int row, int column);

void VOBCEmulatorForm::on_CellChanged(int row, int column)
{
	auto mnl = m_map[curTrain].analog;
	QTableWidget* table = qobject_cast<QTableWidget*>(sender());
	if (column == 2)
	{
		QTableWidgetItem* item = table->item(row, column);
		int value = item->text().toInt();
		if (row == 0) mnl.lcdqsd = value;
		else if (row == 1) mnl.lczdsd = value;
	}	
}
```



##### 6 清除表格数据





### 5.3 stacked Widget

* 根据按钮点击，显示不同的widget

堆叠窗口（Stacked Widget）是Qt框架中常用的一种容器控件，用于管理多个子窗口（小部件），但同时只显示其中一个子窗口。它的常用用法包括：

```cpp
// 创建堆叠窗口对象(可以ui直接创建)
QStackedWidget *stackedWidget = new QStackedWidget;

// 创建子窗口（页面）并添加到堆叠窗口中
QWidget *page1 = new QWidget;
QWidget *page2 = new QWidget;
QWidget *page3 = new QWidget;

stackedWidget->addWidget(page1);
stackedWidget->addWidget(page2);
stackedWidget->addWidget(page3);

// 切换显示不同的子窗口
stackedWidget->setCurrentIndex(0); // 显示第一个页面
stackedWidget->setCurrentWidget(page2); // 通过指定页面对象显示第二个页面

// 或者使用信号和槽机制来触发页面切换
connect(button1, &QPushButton::clicked, stackedWidget, [=](){
    stackedWidget->setCurrentIndex(0);
});

connect(button2, &QPushButton::clicked, stackedWidget, [=](){
    stackedWidget->setCurrentWidget(page2);
});

// 将堆叠窗口添加到布局中
layout->addWidget(stackedWidget);

```

#### 5.3.1 应用

* 根据name和widget自动添加到stack widget中，点击button，切换页面

```cpp
Coroutine<void> MainWindow::init()
{
    // 获取子页面信息
    auto &emulators = EmulatorManager::getInstance()->emulators();
    for (auto &emulator : emulators)
    {
        // 子页面名称
        auto btn = new QPushButton(QString::fromLocal8Bit(emulator->name()));
        // 子页面窗口
        auto widget = emulator->widget();
		
        // 添加
        // verticalLayoutMainPage：垂直layout
        ui->verticalLayoutMainPage->addWidget(btn);
        
        // stackedWidgetMainPage： stack widget
        ui->stackedWidgetMainPage->addWidget(widget);
        // 设置子窗口可以使用主窗口大小
        widget->setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding);

        // 点击切换页面
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







### 5.4 QTabWidget

*  自带切换选项，展现窗口

```cpp
// 设置选项卡字体大小
QTabBar* tabBar = ui->tabWidget->tabBar();
tabBar->setFont(QFont("Arial", 8));

// 设置窗口内字体大小
QFont tabFont = tabWidget->font();
tabFont.setPointSize(12); 
```

`QTabWidget` 是 Qt 中用于管理和显示多个标签页的控件。它允许在一个窗口中显示多个页面，每个页面都有一个关联的标签。以下是 `QTabWidget` 的常用接口，整理成表格：

| 方法/属性                        | 描述                                                         |
| -------------------------------- | ------------------------------------------------------------ |
| **添加和移除标签页**             |                                                              |
| `addTab(widget, text)`           | 向 `QTabWidget` 添加一个新的标签页，参数是要添加的 `widget` 和 `text`（标签页的标题）。 |
| `insertTab(index, widget, text)` | 在指定的 `index` 位置插入一个新的标签页。参数是插入位置 `index`，标签页 `widget` 和 `text`（标题）。 |
| `removeTab(index)`               | 移除指定位置的标签页。参数 `index` 是标签页的索引。          |
| **访问和操作标签页**             |                                                              |
| `widget(index)`                  | 获取指定位置的标签页（`QWidget`）。参数 `index` 是标签页的索引。 |
| `indexOf(widget)`                | 返回指定 `widget` 在 `QTabWidget` 中的索引。                 |
| `count()`                        | 返回当前 `QTabWidget` 中标签页的数量。                       |
| `currentIndex()`                 | 返回当前显示的标签页的索引。                                 |
| `setCurrentIndex(index)`         | 设置当前显示的标签页，参数 `index` 是要显示的标签页索引。    |
| **标签和图标设置**               |                                                              |
| `setTabText(index, text)`        | 设置指定标签页的标题。参数 `index` 是标签页索引，`text` 是新的标题。 |
| `tabText(index)`                 | 获取指定标签页的标题。参数 `index` 是标签页索引。            |
| `setTabIcon(index, icon)`        | 设置指定标签页的图标。参数 `index` 是标签页索引，`icon` 是 `QIcon` 对象。 |
| `tabIcon(index)`                 | 获取指定标签页的图标。参数 `index` 是标签页索引。            |
| **标签工具提示**                 |                                                              |
| `setTabToolTip(index, text)`     | 设置指定标签页的工具提示文本。参数 `index` 是标签页索引，`text` 是工具提示文本。 |
| `tabToolTip(index)`              | 获取指定标签页的工具提示文本。参数 `index` 是标签页索引。    |
| **标签可见性和状态**             |                                                              |
| `setTabEnabled(index, bool)`     | 设置指定标签页是否可用。参数 `index` 是标签页索引，`bool` 表示是否可用。 |
| `isTabEnabled(index)`            | 检查指定标签页是否可用。参数 `index` 是标签页索引。          |
| `setTabVisible(index, bool)`     | 设置指定标签页是否可见。参数 `index` 是标签页索引，`bool` 表示是否可见。 |
| `isTabVisible(index)`            | 检查指定标签页是否可见。参数 `index` 是标签页索引。          |
| **选项和行为**                   |                                                              |
| `setTabsClosable(bool)`          | 设置标签页是否可以被关闭。参数 `bool` 表示是否允许关闭。     |
| `tabsClosable()`                 | 检查标签页是否可以被关闭。返回一个布尔值。                   |
| `setMovable(bool)`               | 设置标签页是否可以拖动以重新排序。参数 `bool` 表示是否允许拖动。 |
| `isMovable()`                    | 检查标签页是否可以拖动。返回一个布尔值。                     |
| `setTabPosition(TabPosition)`    | 设置标签的位置。参数是 `QTabWidget::TabPosition` 枚举值，指定标签位置（如顶部、底部等）。 |
| `tabPosition()`                  | 获取当前标签的位置。返回一个 `QTabWidget::TabPosition` 枚举值。 |
| **信号和事件**                   |                                                              |
| `currentChanged(index)`          | 一个信号，当当前标签页改变时触发。参数 `index` 是新标签页的索引。 |
| `tabBarClicked(index)`           | 一个信号，当用户点击标签栏时触发。参数 `index` 是被点击的标签页索引。 |
| `tabBarDoubleClicked(index)`     | 一个信号，当用户双击标签栏时触发。参数 `index` 是被双击的标签页索引。 |
| `tabCloseRequested(index)`       | 一个信号，当用户点击标签页的关闭按钮时触发。参数 `index` 是请求关闭的标签页索引。 |

**添加和移除标签页**

- `addTab(widget, text)`:
  向 `QTabWidget` 添加一个新的标签页。
  ```cpp
  QTabWidget *tabWidget = new QTabWidget;
  QWidget *page1 = new QWidget;
  tabWidget->addTab(page1, "Page 1");
  ```

- `insertTab(index, widget, text)`:
  在指定的位置插入一个新的标签页。
  ```cpp
  QWidget *page2 = new QWidget;
  tabWidget->insertTab(1, page2, "Page 2"); // 在第二个位置插入
  ```

- `removeTab(index)`:
  移除指定位置的标签页。
  ```cpp
  tabWidget->removeTab(1); // 移除第二个标签页
  ```

- **访问和操作标签页**
  - `widget(index)`:
    获取指定位置的标签页。
    ```cpp
    QWidget *page = tabWidget->widget(0); // 获取第一个标签页
    ```

  - `indexOf(widget)`:
    返回指定 `widget` 在 `QTabWidget` 中的索引。
    ```cpp
    int index = tabWidget->indexOf(page1); // 获取 page1 的索引
    ```

  - `count()`:
    返回当前 `QTabWidget` 中标签页的数量。
    ```cpp
    int numberOfTabs = tabWidget->count();
    ```

  - `currentIndex()`:
    返回当前显示的标签页的索引。
    ```cpp
    int currentTabIndex = tabWidget->currentIndex();
    ```

  - `setCurrentIndex(index)`:
    设置当前显示的标签页。
    ```cpp
    tabWidget->setCurrentIndex(1); // 显示第二个标签页
    ```

- **标签和图标设置**
  - `setTabText(index, text)`:
    设置指定标签页的标题。
    ```cpp
    tabWidget->setTabText(0, "New Page 1 Title");
    ```

  - `tabText(index)`:
    获取指定标签页的标题。
    ```cpp
    QString title = tabWidget->tabText(0);
    ```

  - `setTabIcon(index, icon)`:
    设置指定标签页的图标。
    ```cpp
    QIcon icon(":/path/to/icon.png");
    tabWidget->setTabIcon(0, icon);
    ```

  - `tabIcon(index)`:
    获取指定标签页的图标。
    ```cpp
    QIcon icon = tabWidget->tabIcon(0);
    ```

- **标签工具提示**
  - `setTabToolTip(index, text)`:
    设置指定标签页的工具提示文本。
    ```cpp
    tabWidget->setTabToolTip(0, "This is Page 1");
    ```

  - `tabToolTip(index)`:
    获取指定标签页的工具提示文本。
    ```cpp
    QString toolTip = tabWidget->tabToolTip(0);
    ```

- **标签可见性和状态**
  - `setTabEnabled(index, bool)`:
    设置指定标签页是否可用。
    ```cpp
    tabWidget->setTabEnabled(0, false); // 禁用第一个标签页
    ```

  - `isTabEnabled(index)`:
    检查指定标签页是否可用。
    ```cpp
    bool isEnabled = tabWidget->isTabEnabled(0);
    ```

  - `setTabVisible(index, bool)`:
    设置指定标签页是否可见。
    ```cpp
    tabWidget->setTabVisible(0, false); // 隐藏第一个标签页
    ```

  - `isTabVisible(index)`:
    检查指定标签页是否可见。
    ```cpp
    bool isVisible = tabWidget->isTabVisible(0);
    ```

- **选项和行为**
  - `setTabsClosable(bool)`:
    设置标签页是否可以被关闭。
    ```cpp
    tabWidget->setTabsClosable(true);
    ```

  - `tabsClosable()`:
    检查标签页是否可以被关闭。
    ```cpp
    bool closable = tabWidget->tabsClosable();
    ```

  - `setMovable(bool)`:
    设置标签页是否可以拖动以重新排序。
    ```cpp

### 5.5 label

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202405161643521.png" alt="image-20240516164321249" style="zoom:50%;" />

| 属性      | 功能                  |
| --------- | --------------------- |
| alignment | 设置label文字水平居中 |

### 5.6 QCheckBox

在Qt中，`QCheckBox`是一个常见的复选框控件。它允许用户选择或取消选择某个选项。以下是`QCheckBox`类的一些常用接口，整理成表格：

| 方法/属性                      | 描述                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| `isChecked()`                  | 检查复选框是否被选中，返回一个布尔值 `True`（选中）或 `False`（未选中）。 |
| `setChecked(bool)`             | 设置复选框的选中状态。如果参数为 `True`，复选框被选中；如果为 `False`，复选框未选中。 |
| `toggle()`                     | 切换复选框的状态。如果复选框被选中，它会变为未选中；如果未选中，则变为选中。 |
| `setText(str)`                 | 设置复选框旁边显示的文本。                                   |
| `text()`                       | 获取复选框当前显示的文本。                                   |
| `isTristate()`                 | 检查复选框是否支持三态（未选中、部分选中、选中）。返回 `True` 表示支持，`False` 表示不支持。 |
| `setTristate(bool)`            | 设置复选框是否支持三态模式。如果参数为 `True`，复选框可以有三种状态；否则只有两种状态。 |
| `checkState()`                 | 返回当前的选中状态。可能的值有：`Qt::Unchecked`（未选中）、`Qt::PartiallyChecked`（部分选中）、`Qt::Checked`（选中）。 |
| `setCheckState(Qt.CheckState)` | 设置复选框的选中状态，参数可以是 `Qt::Unchecked`、`Qt::PartiallyChecked` 或 `Qt::Checked`。 |
| `stateChanged(int)`            | 一个信号，当复选框的状态发生变化时被触发。传递的参数是新的状态（0 - 未选中，1 - 部分选中，2 - 选中）。 |

- **isChecked()**: 
  检查复选框是否被选中。
  ```python
  if checkbox.isChecked():
      print("Checkbox is checked")
  ```

- **setChecked(bool)**: 
  设置复选框的选中状态。
  
  ```python
  checkbox.setChecked(True)  # 选中复选框
  checkbox.setChecked(False) # 取消选中复选框
  ```
  
- **toggle()**: 
  切换复选框的状态。
  ```python
  checkbox.toggle()  # 如果当前选中，则取消选中；反之亦然
  ```

- **setText(str)**: 
  设置复选框旁边的文本。
  ```python
  checkbox.setText("I agree to the terms and conditions")
  ```

- **text()**: 
  获取当前显示的文本。
  ```python
  current_text = checkbox.text()
  print(current_text)
  ```

- **isTristate()**: 
  检查复选框是否支持三态。
  ```python
  if checkbox.isTristate():
      print("Checkbox supports tristate")
  ```

- **setTristate(bool)**: 
  设置复选框是否支持三态。
  ```python
  checkbox.setTristate(True)  # 允许复选框有三个状态
  ```

- **checkState()**: 
  获取当前的选中状态。
  ```python
  state = checkbox.checkState()
  if state == Qt.Checked:
      print("Checkbox is checked")
  elif state == Qt.PartiallyChecked:
      print("Checkbox is partially checked")
  else:
      print("Checkbox is unchecked")
  ```

- **setCheckState(Qt.CheckState)**: 
  设置复选框的选中状态。
  ```python
  checkbox.setCheckState(Qt.Checked)            # 设置为选中
  checkbox.setCheckState(Qt.PartiallyChecked)   # 设置为部分选中
  checkbox.setCheckState(Qt.Unchecked)          # 设置为未选中
  ```

- **stateChanged(int)**: 
  信号，在复选框的状态改变时触发。
  ```python
  def on_state_changed(state):
      if state == 0:
          print("Unchecked")
      elif state == 1:
          print("Partially checked")
      elif state == 2:
          print("Checked")
  
  checkbox.stateChanged.connect(on_state_changed)
  ```

这些接口在开发`Qt`应用程序时非常有用，允许你根据需要对复选框的行为和外观进行细粒度的控制。

### 5.7 RadioButton

```cpp
#include <QApplication>
#include <QWidget>
#include <QRadioButton>

class MyWindow : public QWidget {
public:
    MyWindow() {
        // 创建单选按钮
        QRadioButton *radioButton1 = new QRadioButton("选项 1");
        QRadioButton *radioButton2 = new QRadioButton("选项 2");
        QRadioButton *radioButton3 = new QRadioButton("选项 3");

        // 创建确认按钮
        QPushButton *button = new QPushButton("确认选择");
        
        // 设置默认勾选第一个单选按钮
        radioButton1->setChecked(true);
		
        
};

```

```cpp
// 单选按钮分组
#include <QRadioButton>
#include <QButtonGroup>

class MyWindow : public QWidget {
public:
    MyWindow() {
        // 创建单选按钮
        QRadioButton *radioButton1 = new QRadioButton("选项 1");
        QRadioButton *radioButton2 = new QRadioButton("选项 2");
        QRadioButton *radioButton3 = new QRadioButton("选项 3");

        // 创建确认按钮
        QPushButton *button = new QPushButton("确认选择");
        
        // 设置默认勾选第一个单选按钮
        radioButton1->setChecked(true);

        // 分组。每组可以单选一个
        QButtonGroup *group1 = new QButtonGroup(this);
        group1->addButton(radioButton1);
        group1->addButton(radioButton2);

        QButtonGroup *group2 = new QButtonGroup(this);
        group2->addButton(radioButton3);
        group2->addButton(radioButton4);
        
        // 绑定槽函数
        // qt6绑定方式
		connect(group2, &QButtonGroup::buttonClicked, this, &QJKEmulatorForm::onGroup2ButtonClicked);
        
        // qt5 绑定方式
		connect(group1, SIGNAL(buttonClicked(QAbstractButton*)), this, SLOT(onGroup1ButtonClicked(QAbstractButton*)));
        
private:
        void onGroup1ButtonClicked(QAbstractButton *button) {
        	QMessageBox::information(this, "组 1 选择", "您选择了: " + button->text());
    	}

};
```



## 6 layout

### 6.1 全局函数

| 函数                     | 功能               |
| ------------------------ | ------------------ |
| `widget.showMaximized()` | 显示时，窗口最大化 |
| ``                       |                    |
| ``                       |                    |
| ``                       |                    |
| ``                       |                    |



### 6.2 QVBoxLayout

| 函数           | 功能                                                         |
| -------------- | ------------------------------------------------------------ |
| `addStretch()` | 添加一个可伸缩的空间,在窗口大小改变时控件保持在布局的顶部不动 |
| ``             |                                                              |
| ``             |                                                              |
| ``             |                                                              |

### 6.3 UI控件

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202405161341094.png" alt="image-20240516134128034" style="zoom: 50%;" />

| 属性    | 作用                     |
| ------- | ------------------------ |
| Margin  | 布局边距大小             |
| spacing | 布局内各个部件间距       |
| stretch | 布局内各个部件的所占比例 |



## 7 全局app设置

### 7.1 设置全局字体

``` cpp
// mainwindow.cpp
setWindowTitle(QString::fromLocal8Bit("中心仿真平台"));
QFont font("Arial", 10);
qApp->setFont(font);
```



## 8 添加资源文件

1. <img src="C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230720124303130.png" alt="image-20230720124303130" style="zoom: 50%;" />
2. 

<img src="C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230720124346409.png" alt="image-20230720124346409" style="zoom: 50%;" />

3. 

<img src="C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230720124433998.png" alt="image-20230720124433998" style="zoom:50%;" />

* 起名res，生成res.qrc文件，双击打不开，右键open in edit

4. 

<img src="C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230720124649734.png" alt="image-20230720124649734" style="zoom:50%;" />

* 添加前缀 /
* 添加文件
* 编译，添加完成

5. 使用：

```cpp
":前缀+资源名"
Qicon(":/source/up.png")
```

## 6 UI控件属性

### 6.1 弹簧、label

1. 设置图标

   ```cpp
   ui->actionnew->setIcon(QIcon(":/source/Luffy.png"));
   ```

2. Spacers弹簧

   ![image-20230721144057883](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230721144057883.png)

![image-20230721144042661](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230721144042661.png)

* 1、控制控件之间的距离，使其不随着窗口大小而改变
* 2、用于一个容器内部的控件间距调整
* 2、打破布局，可以让弹簧的作用消失



3. 容器

* 用来存放多个组件，内部可以用弹簧控制组件之间的距离
* 可以在layout设置边距为0
* 可以调整控件的显示位置：水平、垂直、栅格
* 在sizePolicy中，设置策略为Fixed，显示出在某一方向上的真是距离



4. 显示组件Display Widgets

* 常用Label展示文字、图片

```cpp
QLabel *label = new QLabel(this);
label->setParent(this);

// 字体
QFont font;
font.setFamily("华文新魏");
font.setPointSize(20);
label->setFont(font);

// 文字内容
// 1
label->setText(QString::number(i+1));
// 2
QString str1 = QString("Level: %1").arg(this->levelNum_);
label->setText(str1);


// 设置文字水平和竖直居中
label->setAlignment(Qt::AlignHCenter | Qt::AlignVCenter);

// 标签大小、位置
// 1
label->setFixedSize(levelBt->size());
label->move(25+(i%4)*120,150+(i/4)*120);
// 2
label->setGeometry(50,this->height()-150,120,100);
```



* label使用在按钮上时，会覆盖遮住按钮的点击事件

```cpp
// 设置标签穿透
label->setAttribute(Qt::WA_TransparentForMouseEvents);
```

* 设置图片

```cpp
QLabel *label2 = new QLabel;
label2->setParent(this);

// label的大小
label2->setGeometry(0,0,50,50);
label2->setPixmap(QPixmap(":/res/BoardNode.png"));

label2->move(57+ i*50,200+j*50);
```









5. 输入框

* 常用line Edit
* 在QLineEdit中，可以设置为输入内容不可见

### 6.2 按钮

![image-20230724134923115](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230724134923115.png)

#### 6.2.1 PushButten

* 一般用文字表示

#### 6.2.2 Tool Butten

* 一般用图标表示
* ![image-20230721165905757](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230721165905757.png)
* ![image-20230721165806768](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230721165806768.png)

1. 设置文字、图标
2. 设置尺寸，显示方式，透明度

#### 6.2.3 RadioButten

* 单选框，配合GroupBox使用

* ```cpp
  // 点击触发槽函数
  connect(ui->manbt,&QRadioButton::clicked,[=]{
      qDebug()<< "点击男生";
  });
  
  ```

* 设置默认选项

  ```cpp
  ui->manbt->setChecked(true);
  ```

  

#### 6.2.4 Check Box

* 多选框，配合GroupBox使用

* 点击触发槽函数

```cpp
connect(ui->motherbt,&QCheckBox::clicked,[=]{
    qDebug()<< "老板娘啊老板娘！";

});
```

* 获取变化state

```cpp
connect(ui->motherbt,&QCheckBox::stateChanged,[=](int state){
    qDebug()<< state;
});
// 0:取消
// 1：未全选，选择该选项
// 2：全选，选择该选项
```



### 6.3 结构

#### 6.3.1 list Widget

* 以列表的形式存放数据

```cpp
1、ui创建列表
2、cpp文件代码添加元素
// 添加单个元素
QListWidgetItem * it = new QListWidgetItem("锄禾日当午");
ui->listWidget->addItem(it);

// 添加多个元素
QStringList *its = new QStringList({"汗滴禾下土","谁知盘中餐","粒粒皆辛苦"});
QStringList its2({"汗滴禾下土","谁知盘中餐","粒粒皆辛苦"});
// its->append("汗滴禾下土","谁知盘中餐","粒粒皆辛苦");
ui->listWidget->addItems(*its);
ui->listWidget->addItems(*its2);


```



#### 6.3.2 tree Widget

* 以大纲级别的形式存储数据

![image-20230724135201558](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230724135201558.png)

```cpp
1、ui创建树
2、添加元素
// 设置标签
    ui->treeWidget->setHeaderLabels(QStringList()<<"英雄"<<"介绍");

// 设置一级内容
QTreeWidgetItem * li = new QTreeWidgetItem(QStringList()<<"力量");
QTreeWidgetItem * jing = new QTreeWidgetItem(QStringList()<<"精力");

// 加入到容器
ui->treeWidget->addTopLevelItem(li);
ui->treeWidget->addTopLevelItem(jing);

// 添加子节点（二级内容）
QStringList hero1;
hero1<<"伽罗"<<"射手，靠平a普攻";
QTreeWidgetItem * jialuo = new QTreeWidgetItem(hero1);
li->addChild(jialuo);

//三级内容
QStringList win;
win<<"必胜"<<"选了就一定赢";
QTreeWidgetItem * mywin = new QTreeWidgetItem(win);
jialuo->addChild(mywin);
    
   
```

#### 6.3.3 table Widget

* 表格形式存储

![image-20230724143409744](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230724143409744.png)

```cpp
QStringList name = {"张飞","关羽","刘备"};
QStringList sex = {"男","男","男"};
// 列数
ui->tableWidget->setColumnCount(3);
// 列名
ui->tableWidget->setHorizontalHeaderLabels(QStringList()<<"姓名"<<"性别"<<"年龄");
// 行数
ui->tableWidget->setRowCount(3);
// 正文// 传入数据为QString类型
for(int i = 0;i<3;i++){
    int j = 0 ;
    ui->tableWidget->setItem(i,j++,new QTableWidgetItem(name[i]));
    ui->tableWidget->setItem(i,j++,new QTableWidgetItem(sex[i]));
    ui->tableWidget->setItem(i,j++,new QTableWidgetItem(QString::number(i+18)));

    }
```

### 6.4 输入

#### 6.4.1 下拉框

![image-20230724160753092](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230724160753092.png)

* 设置选项

```cpp
// 下拉框
ui->comboBox->addItem("清华");
ui->comboBox->addItem("北大");
ui->comboBox->addItem("复旦");

```



* 设置默认

```cpp
// 设置指定选项
ui->comboBox->setCurrentText("北大");
```





#### 6.4.2 Spin Box

![image-20230724174040596](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230724174040596.png)

帮助手册：QSpinBox

* 信号

```cpp
// 函数重载，使用函数指针指明
void valueChanged(int i)
void valueChanged(const QString &text)
```



* 槽函数

```cpp
// 设置数值
QSpinBox::setValue
    
```

* 操作

```cpp
// 设置数值
spinBox->setValue(20);
// 得到当前值
spinBox->Value();
```



  

#### 6.4.3  拖拉条

* Horizontal Slider
* 信号

```cpp
QSlider::valueChanged
```



* 槽函数

```cpp
// 设置数值
QSlider::setValue(int num)
```



### 6.5 自定义控件

1. 新建自定义ui

<img src="C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230724161125661.png" alt="image-20230724161125661" style="zoom: 33%;" />

2. 制作自定义控件

<img src="C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230724161453101.png" alt="image-20230724161453101" style="zoom:50%;" />

3. 主ui内创建存放自定义控件的容器（eg：Widget）

<img src="C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230724161620476.png" alt="image-20230724161620476" style="zoom:50%;" />



4. 提升为所创建的控件类型，添加

<img src="C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230724161838900.png" alt="image-20230724161838900" style="zoom: 50%;" />

5. 容器类型变为自定义控件类型，使用成功

<img src="C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230724162050965.png" alt="image-20230724162050965" style="zoom:50%;" />

6. 关联两个组件

```cpp
ui->setupUi(this);
void (QSpinBox::* ptr)(int) = &QSpinBox::valueChanged;
// spinBox改变，滑动条移动
connect(ui->spinBox,ptr,ui->horizontalSlider,&QSlider::setValue);
// 滑动条移动，spinBox改变
connect(ui->horizontalSlider,&QSlider::valueChanged,ui->spinBox,&QSpinBox::setValue);

```



## 7 对话框

点击功能键，弹出对话框，进行提示或选择

### 7.1 自定义对话框

#### 7.1.1 模态对话框 

* 不可以对其他窗口操作，阻塞
* 采用栈保存

```cpp
connect(ui->actionOpen,&QAction::triggered,[=](){
        QDialog dlg;
        dlg.resize(500,400);
        dlg.exec();
        qDebug()<<"模式对话框已经弹出！";
    });
```



#### 7.1.2 非模态对话框

* 采用堆保存

```cpp
connect(ui->actionnew,&QAction::triggered,[=](){
        QDialog *dlg2 = new QDialog(this);
        dlg2->resize(500,400);
        dlg2->show();
        dlg2->setAttribute(Qt::WA_DeleteOnClose); // 设置打开上限，防止内存泄露
        qDebug()<<"非模态对话框已经弹出！";

    });
```



### 7.2 标准对话框

#### 7.2.1 消息对话框

| 类型     | 函数                                                         |
| -------- | ------------------------------------------------------------ |
| 显示消息 | `QMessageBox::information(this, "Title", "This is an information message.");` |
| 警告     | `QMessageBox::warning(this, "Title", "This is a warning message.");` |
| 错误     | `QMessageBox::critical(this, "Title", "This is an error message.");` |
| 询问选择 | `reply = QMessageBox::question(this, "Title", "Do you want to continue?", QMessageBox::Yes |QMessageBox::No);` |
| 自定义   | 自定义无图标显示框                                           |

```cpp
// 无图标
void CBIEmulatorForm::showMessage(QString text, QString title)
{
    QMessageBox msgBox;
    msgBox.setWindowTitle(title);
    msgBox.setText(text);
    msgBox.setIcon(QMessageBox::NoIcon); // 设置图标为 NoIcon
    msgBox.setStandardButtons(QMessageBox::Ok);
    msgBox.exec();
}
```



```cpp
#include <QMessageBox>

class MyWidget : public QWidget {
    Q_OBJECT

public:
    MyWidget(QWidget *parent = nullptr) : QWidget(parent) {
        QPushButton *infoButton = new QPushButton("Show Information", this);
        infoButton->setGeometry(10, 10, 150, 30);
        connect(infoButton, &QPushButton::clicked, this, &MyWidget::showInformation);

        QPushButton *warnButton = new QPushButton("Show Warning", this);
        warnButton->setGeometry(10, 50, 150, 30);
        connect(warnButton, &QPushButton::clicked, this, &MyWidget::showWarning);

        QPushButton *errorButton = new QPushButton("Show Error", this);
        errorButton->setGeometry(10, 90, 150, 30);
        connect(errorButton, &QPushButton::clicked, this, &MyWidget::showError);

        QPushButton *questionButton = new QPushButton("Ask Question", this);
        questionButton->setGeometry(10, 130, 150, 30);
        connect(questionButton, &QPushButton::clicked, this, &MyWidget::askQuestion);
    }

private slots:
    void showInformation() {
        QMessageBox::information(this, "Information", "This is an information message.");
    }

    void showWarning() {
        QMessageBox::warning(this, "Warning", "This is a warning message.");
    }

    void showError() {
        QMessageBox::critical(this, "Error", "This is an error message.");
    }

    void askQuestion() {
        QMessageBox::StandardButton reply;
        reply = QMessageBox::question(this, "Question", "Do you want to continue?",
                                      QMessageBox::Yes | QMessageBox::No);
        if (reply == QMessageBox::Yes) {
            QMessageBox::information(this, "Answer", "You chose Yes.");
        } else {
            QMessageBox::information(this, "Answer", "You chose No.");
        }
    }
};

```





#### 7.2.2 颜色对话框

```cpp
connect(ui->actioncolor,&QAction::triggered,[=]{
        QColor color = QColorDialog::getColor(QColor(255,0,0));
        qDebug()<<"红"<< color.red()<<"黄"<<color.yellow() << "蓝"<<color.blue();
    });

```

#### 7.3.3 文件对话框

 以下是 `QFileDialog` 常用方法的表格，包含每个方法的返回值信息：

| 方法                   | 功能描述                                                     | 返回值类型    | 返回值描述                                             |
| ---------------------- | ------------------------------------------------------------ | ------------- | ------------------------------------------------------ |
| `getOpenFileName`      | 显示一个文件选择对话框，用于选择一个文件。                   | `QString`     | 返回所选文件的路径。如果取消选择，则返回空字符串。     |
| `getOpenFileNames`     | 显示一个文件选择对话框，用于选择多个文件。                   | `QStringList` | 返回所选文件的路径列表。如果取消选择，则返回空列表。   |
| `getSaveFileName`      | 显示一个文件保存对话框，用于选择保存文件的位置和名称。       | `QString`     | 返回选择的保存文件路径。如果取消选择，则返回空字符串。 |
| `getExistingDirectory` | 显示一个目录选择对话框，用于选择一个现有的目录。             | `QString`     | 返回所选目录的路径。如果取消选择，则返回空字符串。     |
| `setNameFilter`        | 设置文件类型过滤器，例如 "*.txt;*.cpp"。                     | `void`        | 无返回值。                                             |
| `setDirectory`         | 设置对话框的初始目录。                                       | `void`        | 无返回值。                                             |
| `setFileMode`          | 设置文件选择对话框的模式，例如选择单个文件、多个文件或目录。 | `void`        | 无返回值。                                             |
| `setViewMode`          | 设置对话框的视图模式，例如详细视图或列表视图。               | `void`        | 无返回值。                                             |

```cpp
#include <QApplication>
#include <QFileDialog>
#include <QDebug>

int main(int argc, char *argv[])
{
    QApplication app(argc, argv);

    // 单个文件选择
    QString fileName = QFileDialog::getOpenFileName(nullptr, "选择文件", QDir::homePath(), "Images (*.png *.xpm *.jpg);;Text files (*.txt);;XML files (*.xml)");
    if (!fileName.isEmpty()) {
        qDebug() << "Selected file:" << fileName;
    } else {
        qDebug() << "No file selected.";
    }

    // 多个文件选择
    QStringList fileNames = QFileDialog::getOpenFileNames(nullptr, "选择多个文件", QDir::homePath(), "Images (*.png *.xpm *.jpg);;Text files (*.txt);;XML files (*.xml)");
    if (!fileNames.isEmpty()) {
        qDebug() << "Selected files:" << fileNames;
    } else {
        qDebug() << "No files selected.";
    }

    // 文件保存
    QString saveFileName = QFileDialog::getSaveFileName(nullptr, "保存文件", QDir::homePath(), "Text files (*.txt);;XML files (*.xml)");
    if (!saveFileName.isEmpty()) {
        qDebug() << "File to save:" << saveFileName;
    } else {
        qDebug() << "No file chosen for saving.";
    }

    // 选择目录
	auto path = QFileDialog::getExistingDirectory(nullptr, QString::fromLocal8Bit("打开车站路径!"), "."); // 设置默认打开目录  （.）
    if (path.isEmpty())
    {
        co_return;
    }

    return 0;
}
```

### 代码说明

- **单个文件选择**：
  - `getOpenFileName` 显示一个文件选择对话框，返回所选文件的路径，如果用户取消选择则返回空字符串。

- **多个文件选择**：
  - `getOpenFileNames` 显示一个文件选择对话框，返回所选文件的路径列表，如果用户取消选择则返回空列表。

- **文件保存**：
  - `getSaveFileName` 显示一个文件保存对话框，返回选择的保存文件路径，如果用户取消选择则返回空字符串。

- **选择目录**：
  - `getExistingDirectory` 显示一个目录选择对话框，返回所选目录的路径，如果用户取消选择则返回空字符串。

这些方法提供了灵活的文件和目录选择功能，可以满足大多数应用程序的需求。通过适当的参数配置和返回值处理，可以大大提高用户体验和操作效率。

#### 7.3.4 字体对话框

```cpp
connect(ui->actionfront,&QAction::triggered,[=]{
        bool flag;
        QFont font = QFontDialog::getFont(&flag,QFont("微软雅黑"，36));
        qDebug()<<"字体"<<font.family().toUtf8().data()<<"字号"<<font.pointSize()<<"是否加粗"<<font.bold();

    });

```

## 8 事件

在Qt中，`QEvent` 是一个表示各种事件的基类。Qt提供了许多派生自 `QEvent` 的事件类，用于处理不同类型的事件。

事件的本质：==重写定义好的事件函数==

* 父类 -> 子类

`QMouseEvent * ev = dynamic_cast<QMouseEvent *>(qEvent)`

| 派类                                              | 作用                                               |
| ------------------------------------------------- | -------------------------------------------------- |
| QMouseEvent                                       | 鼠标事件，用于处理鼠标的按下、释放、移动等         |
| QWheelEvent                                       | 鼠标滚轮事件，用于处理鼠标滚轮滚动                 |
| QFocusEvent                                       | 焦点事件，用于处理控件的获取焦点和失去焦点         |
| QResizeEvent                                      | 调整大小事件，当控件的大小发生改变时触发           |
| QMoveEvent                                        | 移动事件，当控件的位置发生改变时触发               |
| QCloseEvent                                       | 关闭事件，用于处理窗口关闭事件                     |
| QPaintEvent                                       | 绘制事件，当控件需要进行绘制时触发                 |
| `QDragEnterEvent`、`QDragMoveEvent`、`QDropEvent` | 拖放事件，用于处理拖放操作                         |
| QContextMenuEvent                                 | 上下文菜单事件，用于处理上下文菜单（右键菜单）触发 |
| QHoverEvent                                       | 鼠标悬停事件，用于处理鼠标悬停在控件上的情况       |
| QInputMethodEvent                                 | 输入法事件，用于处理输入法相关的事件               |
| QKeyEvent                                         | 键盘事件，用于处理键盘按键的按下和释放             |

### 8.1 事件分发器 & 事件过滤器

![image-20230726162030368](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230726162030368.png)

1. 过滤器

* 在分发器之前，作用于控件本身

```cpp
bool eentFilter(QObject *, Qvent *);

// 安装过滤器
ui->lable->installEventFilter(this);
// 重写过滤器
bool eentFilter(QObject * obj, Qvent * ev){
    if(obj == ui->label){ // 选择执行过滤操作的控件
        if(ev->type == QEvent::MouseButtonPress){ // 选择阻塞的事件
            ...
        }
        
    }  
}
```



2. 分发器

* 作用于过滤器下

* 事件的触发经过分发器下放，根据自定义的方法处理
* 可以在分发器中拦截

```cpp
bool myLabel::event(QEvent *ev){
    if(ev->type() == QEvent::MouseButtonPress){
        // 父类转子类
        QMouseEvent *ev1 = dynamic_cast<QMouseEvent *>(ev);
        QString str = QString("拦截点击行为,x = %1, y = %2, globax = %3, globay = %4")
                .arg(ev1->x()).arg(ev1->y()).arg(ev1->globalX()).arg(ev1->globalY());

        qDebug()<<str;
        return true;

    }
    // 其余事件交给父类处理
    return QLabel::event(ev);
}
```



### 8.2 QMouseEvent

#### 8.2.1 鼠标进出区域

```cpp
void myLabel::enterEvent(QEvent *event){
    qDebug()<<"鼠标进来";
}

void myLabel::leaveEvent(QEvent *event){
    qDebug()<<"鼠标退出";

}
```

#### 8.2.2 鼠标按压、释放

* 手册 QLabel -> Reimplemented Protected Functions

```cpp
void myLabel::mousePressEvent(QMouseEvent *ev){
    qDebug()<<"按压";
    // 显示鼠标位置 
    QString str = QString("x = %1, y = %2").arg(ev->x()).arg(ev->y());
    qDebug()<<str;  
}

void myLabel::mouseReleaseEvent(QMouseEvent *ev){
    qDebug()<<"释放";
}
```





#### 8.2.3 鼠标在区域内移动

```cpp
// 1、默认点击移动
void myLabel::mouseMoveEvent(QMouseEvent *ev){
    qDebug()<<"鼠标点击移动";

}
// 2、无点击运动
// 控件构造函数中设置 鼠标追踪
myLabel::myLabel(QWidget *parent) : QLabel (parent)
{
    setMouseTracking(true);
}
```

#### 8.2.4 左右鼠标

```cpp
// 1、点击
void myLabel::mousePressEvent(QMouseEvent *ev){
    if(ev->button() == Qt::LeftButton){
        qDebug()<<"左键按压";
    }
    if(ev->button() == Qt::RightButton){
        qDebug()<<"右键按压";
    }
    if(ev->button() == Qt::MidButton){
        qDebug()<<"滚轮按压";
    }
}

// 2、释放
void myLabel::mouseReleaseEvent(QMouseEvent *ev){

    if(ev->button() == Qt::LeftButton){
        qDebug()<<"左键释放";
    }
    if(ev->button() == Qt::RightButton){
        qDebug()<<"右键释放";
    }
    if(ev->button() == Qt::MidButton){
        qDebug()<<"滚轮释放";
    }
}

// 3、移动
void myLabel::mouseMoveEvent(QMouseEvent *ev){
    if(ev->buttons() & Qt::LeftButton){
        qDebug()<<"左键移动";
    }
    if(ev->buttons() & Qt::RightButton){
        qDebug()<<"右键移动";
    }
    if(ev->buttons() & Qt::MidButton){
        qDebug()<<"滚轮移动";
    }

}
```



#### 8.2.5 追踪鼠标位置

```cpp
QString str = QString("x = %1, y = %2, globax = %3, globay = %4")
            .arg(ev->x()).arg(ev->y()).arg(ev->globalX()).arg(ev->globalY());
qDebug()<< str;

```

### 8.3 QPaintEvent

#### 8.3.1 基础使用

* 所有的绘图操作，均放在paintEvent函数内

* 通过update重新执行paintEvent事件

```cpp
void Widget::paintEvent(QPaintEvent *event){

    // 1 实例画家，指定绘图设备，this指定的是当前widget
    QPainter painter(this);

    // 2 选择画笔
    QPen pen(QColor(255,0,0));
    // 宽度
    pen.setWidth(3);
    // 风格
    pen.setStyle(Qt::DotLine);
    // 使用笔刷，最后设置
    painter.setPen(pen);

    // 3 选择画刷
    QBrush brush(Qt::cyan);
    // 风格
    brush.setStyle(Qt::Dense7Pattern);
    // 使用
    painter.setBrush(brush);

    // 画线
    painter.drawLine(QPoint(0,0),QPoint(150,150));

    // 画圆、椭圆
    painter.drawEllipse(QPoint(150,150),50,50);

    // 画矩形
    painter.drawRect(QRect(100,100,100,50));

    // 画文字
    painter.drawText(QRect(100,100,100,50),"好好学习，天天向上");
    
    

}
```

```cpp
// painter高级设置
// 1、画图抗锯齿
painter.serRenderHint(QPainter::Antialiasing);

// 2、保存/恢复 画笔位置
painter.save();
painter.translate(100,0);
painter.restore();  
    
```

#### 8.3.2 导入资源图片

```cpp
QPainter painter(this);

painter.drawPixmap(x,y,QPixmap(":/image"));

```

* 通过按钮调节图片位置

```cpp
// 构造函数内
connect(ui->move,&QPushButton::clicked,[=]{
    move_x += 10;
    update();
});

// event事件函数内
if(move_x > this->width()){
    move_x = 0;
}
painter.drawPixmap(move_x,20,QPixmap(":/source/Luffy.png"));
```



* 通过定时器调节图片位置

```cpp
// 构造函数内
QTimer *timer = new QTimer(this);
connect(timer,&QTimer::timeout,[=]{
    move_x ++;
    update();
});
timer->start(10);

// event事件函数内
if(move_x > this->width()){
    move_x = 0;
}
painter.drawPixmap(move_x,20,QPixmap(":/source/Luffy.png"));
```

#### 8.3.3 绘图设备

* 即可以在设备上直接画画

| 设备     | 写位置 | 区别                                 |
| :------- | ------ | ------------------------------------ |
| QWidget  | 窗口   | 装在其余设备的图片（Pixmap、Imange） |
| QPixmap  | 磁盘   | 对平台多优化                         |
| QImage   | 磁盘   | 操作像素点                           |
| QPicture | 磁盘   | 保存和重现绘图指令                   |



1. QPixmap

```cpp
1、画图
// 声明设备
QPixmap pix(300,300);
// 调整背景
pix.fill(Qt::white)
// 声明画家,指定设备
QPainter painter(&pix);
// 画图
painter.drawLine(10，10,20 ,20);
// 保存
mix.save("C:\\Users\\zhang\\Desktop\\line.png");
```

_______

```cpp
2、加载图片到widget中
QPainter painter(this);
// 法1
painter.drawPixmap(x,y,QPixmap(":/image"));

// 法2
QPixmap mix;
mix.load(":/source/Luffy.png");
// 缩小尺寸
pix.scaled(pix.width()*0.5,pix.height()*0.5);
painter.drawPixmap(20,20,mix);

```



2. QImage

```cpp
1、画图
// 声明设备
QImage img(300,300,QImage::Format_RGB32);
// 调整背景
img.fill(Qt::white)
// 声明画家,指定设备
QPainter painter(&img);
// 画图
painter.drawLine(10，10);
// 保存
img.save("c:\\pix.png");
```

_______

```cpp
2、放入wiget
// 加载到Widget中
QPainter painter(this);
// 法1
painter.drawImage(x,y,QImage("C:\\Users\\zhang\\Desktop\\line2.png"));

// 法2
QImage img;
img.load(":/source/Luffy.png");
painter.drawImage(20,20,img);
```

_______

```cpp
3、 修改像素点
QPainter painter(this);
QImage img;
img.load(":/source/Luffy.png");

// 修改像素点
for(int i = 50;i<150;i++){
    for(int j = 50; j<150;j++){
        QRgb value = qRgb(255,0,0);
        img.setPixel(i,j,value);
    }
}

painter.drawImage(20,20,img);
```



3. QPicture

* 可以设置自己的后缀名
* 不可以直接查看，用来重现画图的指令

```cpp
QPicture pic;
QPainter painter;
// 开始画画
painter.begin(&pic);
painter.drawEllipse(QPoint(150,150),50,50);
painter.end();

pic.save("C:\\Users\\zhang\\Desktop\\line3.zyq");

// 重现指令
QPicture pic2;
pic2.load("C:\\Users\\zhang\\Desktop\\line3.zyq");
painter.begin(this);
painter.drawPicture(0,0,pic2);
painter.end();
```

## 9 文件

### 9.1 读写文件

```cpp
// QByteArray 相当于 char *

QByteArray byteArray; // 创建一个空的字节数组
QByteArray byteArray1("Hello"); // 使用字符串构造字节数组
QByteArray byteArray2 = "World"; // 使用字符串赋值构造字节数组


int size = byteArray.size(); // 获取字节数组的大小（字节数）
const char* data = byteArray.data(); // 获取字节数组的指针（const char* 类型）

```



```cpp
// 打开文件
QFile file(path);
file.open(QIODevice::ReadOnly); // writeOnly   Append
file.close();

// 读取内容
// 全部读取
QByteArray data = file.readAll();

// 按行读取
QByteArray array;
while(!file.atEnd()){
    array += file.readLine();
}

// 追加内容
file.open(QIODevice::Append);
file.write("\n我不是李白");
file.close();
```

### 9.2 文件信息

```cpp
QFileInfo info(path);
qDebug()
    <<"文件大小："<< info.size() 
    << "后缀名："<<info.suffix() 
    << "文件名："<<info.fileName()
    << "创建日期："<<info.birthTime().toString("yyyy/MM/dd hh:mm:ss") // 包含头文件
    <<"最后修改日期"<<info.lastModified().toString("yyyy/MM/dd hh:mm:ss");
```

## 10 动画

* 结合定时器播放图片

  

```cpp
// 1.点击旋转按钮
tm1 = new QTimer(this);

connect(tm1,&QTimer::timeout,[=]{
    QString str = QString(":/res/Coin000%1.png").arg(this->min++);

    this->initButten(str);
    
    qDebug()<<this->flag<<" "<< min;
    if(min>max) {
        tm1->stop();
        this->min = 1;
        this->flag = 0;
        mutex++;
    }

});

void CoinButten::chageFlag(){
        // 上锁
        this->mutex--;
    // 旋转(启动定时器)
        tm1->start(500);
    }

// 重写点击事件
void CoinButten::mousePressEvent(QMouseEvent *e){
    // 锁被占用，本次点击失效
    if(!this->mutex){
        return;
    }else{
        // 锁可用，执行点击事件
        QPushButton::mousePressEvent(e);
    }
}
```

## 11 定时器

### 11.1 功能

* 需要堆创建

注意： 定时器作用于一个 窗口 或者 控件

1. 窗口：在widget的构造函数中定义定时器，对该窗口内的 变量进行控制
2. 控件：在自定义的控件的构造函数中实例定时器

#### 法1

* 创建定时器

```cpp
int id = startTimer(1000);  // ms为单位
```



* 所有的定时器全部封装在timerEvent函数内
* 通过ev->timerID分辨是哪个定时器

```cpp
void Widget::timerEvent(QTimerEvent *ev){
    if(ev->timerId() == id1){
        static int num =1;

        ui->timelb->setText(QString::number(num++));
    }
    if(ev->timerId() == id2){
        static int num2 =10;

        ui->timelb2->setText(QString::number(num2++));
    }

}
```

#### 法2

```cpp
#include <QTimer>

// 创建定时器、关联控件
QTimer *ti = new QTimer(this);
connect(ti,&QTimer::timeout,[=,&num3]{
    static int num3 = 1;
    ui->lb3->setText(QString::number(num3++));
});

tm.start(500);  // 启动
tm.stop(); // 结束

```

### 11.2 静态函数



1. `QTimer::singleShot(int msec, const QObject *receiver, const char *member)`：在指定的时间间隔后触发一个槽函数或全局函数，仅触发一次。

2. `QTimer::singleShot(int msec, Qt::TimerType timerType, const QObject *receiver, const char *member)`：与上述函数类似，但可以指定定时器类型，可选值为`PreciseTimer`和`CoarseTimer`。`PreciseTimer`提供更高精度的定时器，而`CoarseTimer`提供更高效的定时器。

3. `QTimer::timerId()`：返回当前定时器的唯一标识符。通常用于配合`QObject::killTimer`来取消定时器。

这些静态函数在特定情况下非常有用，可以根据需求选择适合的函数来管理定时器。请注意，`QTimer::singleShot`和`QTimer::timerId`是静态函数，您无需创建`QTimer`对象即可使用它们。而普通的定时器操作（例如定时器的启动和停止）通常通过`QTimer`对象的实例进行管理。

```cpp
 QTimer::singleShot(200,this,[=]{
            // 主窗口隐藏
            this->hide();
            // 选择窗口出现
            chooseWindow->show();
        });
```

## 12 QT类

### 12.1 QSetting



| 方法                                                         | 功能描述                                      |
| ------------------------------------------------------------ | --------------------------------------------- |
| `QSettings(organization, application)`                       | 创建一个基于组织和应用名称的 QSettings 对象。 |
| `QSettings(fileName, format)`                                | 创建一个基于文件名和格式的 QSettings 对象。   |
| `void setValue(const QString &key, const QVariant &value)`   | 设置一个键值对。如果键已经存在，则更新其值。  |
| `QVariant value(const QString &key, const QVariant &defaultValue = QVariant()) const` | 获取键对应的值，如果键不存在则返回默认值。    |
| `bool contains(const QString &key) const`                    | 检查设置中是否包含某个键。                    |
| `void remove(const QString &key)`                            | 删除指定的键及其值。                          |
| `QStringList allKeys() const`                                | 返回所有键的列表。                            |
| `void clear()`                                               | 清空所有设置。                                |
| `void sync()`                                                | 将更改写入永久存储。                          |
| `void beginGroup(const QString &prefix)`                     | 开始一个设置组，所有键将在该组中。            |
| `void endGroup()`                                            | 结束一个设置组。                              |
| `int beginReadArray(const QString &prefix)`                  | 开始读取一个数组，并返回数组的大小。          |
| `void endArray()`                                            | 结束读取一个数组。                            |
| `void setArrayIndex(int i)`                                  | 设置当前数组索引。                            |

```cpp
#include <QCoreApplication>
#include <QSettings>
#include <QDebug>

int main(int argc, char *argv[])
{
    QCoreApplication app(argc, argv);

    // 创建一个基于组织和应用名称的 QSettings 对象
    QSettings settings("MyCompany", "MyApp");

    // 设置一些键值对
    settings.setValue("username", "john_doe");
    settings.setValue("window/width", 800);
    settings.setValue("window/height", 600);

    // 读取这些值
    QString username = settings.value("username", "default_user").toString();
    int width = settings.value("window/width", 1024).toInt();
    int height = settings.value("window/height", 768).toInt();

    qDebug() << "Username:" << username;
    qDebug() << "Window width:" << width;
    qDebug() << "Window height:" << height;

    // 检查某个键是否存在
    if (settings.contains("username")) {
        qDebug() << "Username is set.";
    }

    // 删除一个键
    settings.remove("username");

    // 开始一个设置组
    settings.beginGroup("network");
    settings.setValue("proxy", "proxy.example.com");
    settings.setValue("port", 8080);
    settings.endGroup();

    // 读取设置组内的值
    settings.beginGroup("network");
    QString proxy = settings.value("proxy", "default_proxy").toString();
    int port = settings.value("port", 80).toInt();
    settings.endGroup();

    qDebug() << "Proxy:" << proxy;
    qDebug() << "Port:" << port;

    // 开始读取一个数组
    settings.beginWriteArray("recentFiles");
    for (int i = 0; i < 5; ++i) {
        settings.setArrayIndex(i);
        settings.setValue("file", QString("file%1.txt").arg(i + 1));
    }
    settings.endArray();

    // 读取数组中的值
    int size = settings.beginReadArray("recentFiles");
    for (int i = 0; i < size; ++i) {
        settings.setArrayIndex(i);
        QString file = settings.value("file").toString();
        qDebug() << "Recent file:" << file;
    }
    settings.endArray();

    // 获取所有键
    QStringList keys = settings.allKeys();
    qDebug() << "All keys:" << keys;

    // 清空所有设置
    settings.clear();

    return 0;
}
```

### 12.2 QVariant

在 Qt 中，`QSettings::value` 方法返回的是一个 `QVariant` 对象。`QVariant` 是一个可以存储多种类型数据的类，因此需要将它转换成实际需要的类型。在你的示例中，`settings.value("proxy", "default_proxy")` 返回的是一个 `QVariant` 对象，但你需要一个 `QString` 类型的值，所以需要调用 `toString()` 方法来进行转换。

```cpp
#include <QCoreApplication>
#include <QSettings>
#include <QVariant>
#include <QDebug>

int main(int argc, char *argv[])
{
    QCoreApplication app(argc, argv);

    // 创建一个基于组织和应用名称的 QSettings 对象
    QSettings settings("MyCompany", "MyApp");

    // 设置一些键值对
    settings.setValue("username", "john_doe");
    settings.setValue("window/width", 800);
    settings.setValue("window/height", 600);
    settings.setValue("isMaximized", true);

    // 获取这些值并转换为相应的类型
    QString username = settings.value("username").toString();
    int width = settings.value("window/width").toInt();
    int height = settings.value("window/height").toInt();
    bool isMaximized = settings.value("isMaximized").toBool();

    qDebug() << "Username:" << username;
    qDebug() << "Window width:" << width;
    qDebug() << "Window height:" << height;
    qDebug() << "Is Maximized:" << isMaximized;

    return 0;
}
```

### 12.3 QString

* c字符串 <-> QString

  ```cpp
  const char* str;
  QString strq = QString::fromLocal8Bit(str);
  
  QString str;
  const char* strch = str.toLocal8Bit();
  ```

* std::string  <->  QString

  ```cpp
  std::string str;
  QString strq = QString::fromLocal8Bit(str.c_str()); // 先转为c字符串 
  
  QString strst;
  std::sting str = std::string(strst.toLocal8Bit());  // 先转为c字符串
  ```

* 常量字符串 == c字符串

  ```cpp
  QString strq = QString::fromLocal8Bit("我的爱人！"); // 先转为c字符串 
  ```

* string <-> int <-> QString

```cpp
int a = 2;
std::string b = std::to_string(a);
Qstring s = QString::number(a);

int c = std::stoi(b);
int d = s.toInt();
```



* 模板字符串

  ```cpp
  QString jkPath = QString("%1/jk/%2%3.ini").arg(path).arg(QString::fromLocal8Bit(name.c_str())).arg(i);
  ```

  | 类型       | 由QString 转换方法                  | 转换为 QString 方法                      |
  | ---------- | ----------------------------------- | ---------------------------------------- |
  | int        | `str.toInt()`                       | `QString::number(intValue)`              |
  | double     | `str.toDouble()`                    | `QString::number(doubleValue)`           |
  | QByteArray | `str.toUtf8()`                      | `QString::fromUtf8(byteArray)`           |
  | QDateTime  | `str.fromString()`                  | `toString()`                             |
  | uint8_t    | `static_cast<uint8_t>(str.toInt())` | `QString::number(static_case<int>(val))` |

  

### 12.4 QDir

目录操作类

| 方法名           | 功能描述                             | 返回值类型      | 返回值描述                                                |
| ---------------- | ------------------------------------ | --------------- | --------------------------------------------------------- |
| `exists`         | 检查目录是否存在。                   | `bool`          | 如果目录存在则返回 `true`，否则返回 `false`。             |
| `absolutePath`   | 返回目录的绝对路径。                 | `QString`       | 返回目录的绝对路径。                                      |
| `canonicalPath`  | 返回目录的规范路径。                 | `QString`       | 返回目录的规范路径，如果无法访问目录则返回空字符串。      |
| `cd`             | 更改当前目录。                       | `bool`          | 如果成功更改目录则返回 `true`，否则返回 `false`。         |
| `cdUp`           | 更改到上一级目录。                   | `bool`          | 如果成功更改到上一级目录则返回 `true`，否则返回 `false`。 |
| `currentPath`    | 返回当前工作目录的路径。             | `QString`       | 返回当前工作目录的路径。                                  |
| `entryList`      | 返回目录中所有条目的名称列表。       | `QStringList`   | 返回目录中所有条目的名称列表。                            |
| `entryInfoList`  | 返回目录中所有条目的信息列表。       | `QFileInfoList` | 返回目录中所有条目的信息列表。                            |
| `filePath`       | 返回目录中指定文件的完整路径。       | `QString`       | 返回目录中指定文件的完整路径。                            |
| `isReadable`     | 检查目录是否可读。                   | `bool`          | 如果目录可读则返回 `true`，否则返回 `false`。             |
| `mkdir`          | 创建一个子目录。                     | `bool`          | 如果成功创建子目录则返回 `true`，否则返回 `false`。       |
| `mkpath`         | 创建一个路径，包括所有必需的子目录。 | `bool`          | 如果成功创建路径则返回 `true`，否则返回 `false`。         |
| `nameFilters`    | 返回当前目录使用的名称过滤器。       | `QStringList`   | 返回名称过滤器列表。                                      |
| `remove`         | 删除目录中的文件或子目录。           | `bool`          | 如果成功删除则返回 `true`，否则返回 `false`。             |
| `rename`         | 重命名目录中的文件或子目录。         | `bool`          | 如果成功重命名则返回 `true`，否则返回 `false`。           |
| `rmdir`          | 删除子目录。                         | `bool`          | 如果成功删除子目录则返回 `true`，否则返回 `false`。       |
| `setCurrent`     | 设置当前工作目录。                   | `bool`          | 如果成功设置当前工作目录则返回 `true`，否则返回 `false`。 |
| `setNameFilters` | 设置名称过滤器。                     | `void`          | 无返回值。                                                |
| `dirName`        | 返回目录的名称（路径的最后一部分）。 | `QString`       | 返回目录名称。                                            |

```cpp
#include <QApplication>
#include <QDir>
#include <QDebug>

int main(int argc, char *argv[])
{
    QApplication app(argc, argv);

    // 创建一个 QDir 对象，指向某个路径
    QDir dir("/home/user/Documents");

    // 检查目录是否存在
    if (dir.exists()) {
        qDebug() << "Directory exists:" << dir.absolutePath();
    } else {
        qDebug() << "Directory does not exist.";
    }

    // 获取目录名
    auto zm = dir.dirName();
    qDebug() << "Directory name:" << zm;

    // 更改当前目录
    if (dir.cd("..")) {
        qDebug() << "Changed to directory:" << dir.absolutePath();
    } else {
        qDebug() << "Failed to change directory.";
    }

    // 返回目录中所有条目的名称列表
    QStringList entryList = dir.entryList();
    qDebug() << "Directory entries:" << entryList;

    // 创建一个子目录
    if (dir.mkdir("NewFolder")) {
        qDebug() << "Created NewFolder.";
    } else {
        qDebug() << "Failed to create NewFolder.";
    }

    // 删除一个子目录
    if (dir.rmdir("NewFolder")) {
        qDebug() << "Removed NewFolder.";
    } else {
        qDebug() << "Failed to remove NewFolder.";
    }

    // 设置名称过滤器
    dir.setNameFilters(QStringList() << "*.txt" << "*.cpp");
    qDebug() << "Filtered entries:" << dir.entryList();

    return 0;
}
```

### 12.5 QDateTime

```cpp
// 获取年月日时分秒
#include <QCoreApplication>
#include <QDateTime>
#include <QDebug>

int main(int argc, char *argv[])
{
    QCoreApplication a(argc, argv);

    // 获取当前日期和时间
    QDateTime current = QDateTime::currentDateTime();

    // 获取年月日时分秒
    uint8_t year = current.date().year() - 2000;  // 假设年份范围为2000-2099
    uint8_t month = current.date().month();
    uint8_t day = current.date().day();
    uint8_t hour = current.time().hour();
    uint8_t minute = current.time().minute();
    uint8_t second = current.time().second();

    // 打印结果
    qDebug() << "Year:" << year;
    qDebug() << "Month:" << month;
    qDebug() << "Day:" << day;
    qDebug() << "Hour:" << hour;
    qDebug() << "Minute:" << minute;
    qDebug() << "Second:" << second;

    return a.exec();
}

```





## 13 布局设计

#### gemotry几何形

| 函数     | 描述                        |
| -------- | --------------------------- |
| left()   | 返回矩形的左边界的 x 坐标。 |
| top()    | 返回矩形的上边界的 y 坐标。 |
| right()  | 返回矩形的右边界的 x 坐标。 |
| bottom() | 返回矩形的下边界的 y 坐标。 |
| width()  | 返回矩形的宽度。            |
| height() | 返回矩形的高度。            |
| center() | 返回矩形的中心点坐标。      |

## 设计

### 1 设计自定义按键

* 内部实现
  1. 根据图片作为按钮
  2. 根据需求，鼠标点击触发按键动画、点击释放事件等

### 2 打开新窗口

```
// 新建窗口类

// 主窗口中connect函数中
this.hide

// 设置下个窗口出现位置和原窗口一致
other.setGeometry(this.setGeometry)
other.show()
```

### 3 打包程序

1. 环境变量加入：D:\QT\QT5.11.1\5.11.1\mingw53_32\bin
2. 添加软件图标

* 把图标添加到工程文件，在pro文件添加`RC_ICONS=xxxx.ico`
* 注意图标文件以ico文件结尾

3. 将qt切换release，编译后，创建新文件中，将.exe文件拷贝到空文件

1. 文件中右键+shift打开命令行

2. 输入打包命令

   ```
    windeployqt 11_CoinFilp.exe
   ```

3. 生成文件夹，内的.exe可以直接打开

4. 安装向导：hm nis edit



## 12 通信

### 1. 串口

```cmake
cmake_minimum_required(VERSION 3.14)

# 设置项目名称和 Qt 版本
project(SerialPortExample LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 查找 Qt 包，包括 SerialPort 模块
find_package(Qt6 REQUIRED COMPONENTS Core SerialPort)

# 如果使用的是 Qt5，请用以下方式：
# find_package(Qt5 REQUIRED COMPONENTS Core SerialPort)

# 添加可执行文件
add_executable(SerialPortExample main.cpp)

# 链接 Qt 库
target_link_libraries(SerialPortExample PRIVATE Qt6::Core Qt6::SerialPort)

# 如果使用的是 Qt5，请用以下方式：
# target_link_libraries(SerialPortExample PRIVATE Qt5::Core Qt5::SerialPort)

```

```cpp
#include <QSerialPort>
#include <QDebug>
// ======1 创建
QSerialPort serialPort;

// ======2 设置属性
serialPort.setPortName("COM1");  // 设置串口名称
serialPort.setBaudRate(QSerialPort::Baud9600);  // 设置波特率
serialPort.setDataBits(QSerialPort::Data8);  // 设置数据位
serialPort.setParity(QSerialPort::NoParity);  // 设置无校验位
serialPort.setStopBits(QSerialPort::OneStop);  // 设置停止位
serialPort.setFlowControl(QSerialPort::NoFlowControl);  // 设置无流控制

// ======3 连接异步读，收到数据立刻调用槽函数处理
connect(m_serialPort, &QSerialPort::readyRead, this, &ZndsNCEmulatorForm::handleReadyRead);

// ======4 打开串口
if (serialPort.open(QIODevice::ReadWrite)) {
    
    // 方式1：发送的字节数组
    QByteArray dataToSend = "Hello, SerialPort!";
    // 方式2：发送vector<uint8_t>
    QByteArray dataToSend(reinterpret_cast<const char*>(m_protocolPacket.data()), m_protocolPacket.size());
    
    // ======= 5发送数据
    qint64 bytesWritten = serialPort.write(dataToSend);
    
    if (bytesWritten == -1) {
        qDebug() << "Failed to write data to serial port";
    } else {
        qDebug() << "Sent" << bytesWritten << "bytes";
    }
} else {
    qDebug() << "Failed to open serial port:" << serialPort.errorString();
}

// ========6 读取数据--槽函数
void ZndsNCEmulatorForm::handleReadyRead()
{
	QByteArray data = m_serialPort->readAll(); 
    // 转为vector<uint8_t> 存储
	std::vector<uint8_t> dataVector(reinterpret_cast<const uint8_t*>(data.constData()),
		reinterpret_cast<const uint8_t*>(data.constData()) + data.size());
	
	// 处理数据 ...
}
// ========7关闭串口
serialPort.close();

```

### 2. UDP

```cmake
# 查找 Qt 包，包括 网络 模块
find_package(Qt5 COMPONENTS Widgets Network REQUIRED)

# 链接 Qt 库
target_link_libraries(SerialPortExample PRIVATE Qt5::Widgets Qt5::Network)
```

```cpp
#include <QUdpSocket>
#include <QHostAddress>
#include <QCoreApplication>
#include <QDebug>

class MyUdpApp : public QObject {
    Q_OBJECT

public:
    MyUdpApp() {
        udpSocket = new QUdpSocket(this);
        
        // 绑定到本地端口
        udpSocket->bind(QHostAddress::Any, port);
        
        // 连接信号
        connect(udpSocket, &QUdpSocket::readyRead, this, &MyUdpApp::onReadyRead);
    }

private slots:
    // 异步读
    void onReadyRead();
    void sendDatagram(const QByteArray &data, const QHostAddress &address, quint16 port);

private:
    QUdpSocket *udpSocket;
    const quint16 port = 1234; // 使用你需要的端口
};
// 读
void MyUdpApp::onReadyRead() {
    while (udpSocket->hasPendingDatagrams()) {
        QByteArray datagram;
        datagram.resize(udpSocket->pendingDatagramSize());
        QHostAddress sender;
        quint16 senderPort;

        udpSocket->readDatagram(datagram.data(), datagram.size(), &sender, &senderPort);
        qDebug() << "Received:" << datagram << "from" << sender.toString() << ":" << senderPort;
    }
}
// 发送
void MyUdpApp::sendDatagram(const QByteArray &data, const QHostAddress &address, quint16 port) {
    udpSocket->writeDatagram(data, address, port);
}

```

```cpp
int main(int argc, char *argv[]) {
    QCoreApplication a(argc, argv);

    MyUdpApp udpApp;

    // 发送数据示例
    QByteArray data("Hello, UDP!");
    udpApp.sendDatagram(data, QHostAddress::Broadcast, udpApp.port);

    return a.exec();
}
```



## 13 时间类

### 1 DataTime

* 获取当前时间的年月日时分秒

```cpp
#include <QCoreApplication>
#include <QDateTime>
#include <QDebug>

int main(int argc, char *argv[])
{
    QCoreApplication a(argc, argv);

    QDateTime now = QDateTime::currentDateTime();

    int year = now.date().year();
    int month = now.date().month();
    int day = now.date().day();

    int hour = now.time().hour();
    int minute = now.time().minute();
    int second = now.time().second();

    qDebug() << "Year:" << year;
    qDebug() << "Month:" << month;
    qDebug() << "Day:" << day;
    qDebug() << "Hour:" << hour;
    qDebug() << "Minute:" << minute;
    qDebug() << "Second:" << second;

    return a.exec();
}

```





# 调用第三方库

## 0.3 QT调用ffmepg库

* 将`D:\videoTools\ffmpeg\build`的 `ffmepg-4.2`导入工程目录
* 工程文件`.pro`中加入

```shell
INCLUDEPATH += \
    $$PWD/ffmepg-4.2/include
LIBS += $$PWD/ffmepg-4.2/bin/avformat.lib \
    $$PWD/ffmepg-4.2/bin/avcodec.lib \
    $$PWD/ffmepg-4.2/bin/avdevice.lib \
    $$PWD/ffmepg-4.2/bin/avfilter.lib \
    $$PWD/ffmepg-4.2/bin/avutil.lib \
    $$PWD/ffmepg-4.2/bin/swresample.lib \
    $$PWD/ffmepg-4.2/bin/swscale.lib

```

* 执行，产生build-xxxxx-debug文件
* 将ffmepg-4.2的bin目录下的`.ddl`文件，拷贝到build-xx-debug文件中，与debug、release文件并列
* 若编译错误，删除debug和release文件，重新执行

```c
#include <stdio.h>

#include "libavutil/avutil.h"

int main()
{
    printf("Hello FFMPEG, version is %s\n", av_version_info());
    return 0;
 }

```

```cpp
#include <iostream>
extern "C" {
    #include "libavutil/avutil.h"
}

using namespace std;

int main()
{
    cout << "Hello ffmpeg is" << av_version_info() << endl;
    return 0;
}

```

# qt、vs安装

## 下载qt5.15.2

[安装说明](https://github.com/ZhangYuQiao326/internship/blob/main/file/QT/qt5.15.2%E5%AE%89%E8%A3%85.html)

[安装包](百度网盘/me/计算机/qt/5.15.2安装)

账号密码zhangyuqiao26@outlook.com Zyq0326.

## 打开Visual Studio 2022

选择菜单栏的【扩展】->【管理扩展】

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202405151612379.png" alt="image-20240515161241007" style="zoom: 33%;" />

## 下载QT插件

输入Qt搜索，然后下载【Qt Visual Studio Tools】，等待下载完成

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202405151613212.png" alt="image-20240515161321728" style="zoom:33%;" />

下载【Qt Vs Cmake Tools】,可以右键新建qt项

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202407021603615.png" alt="image-20240702160335253" style="zoom:67%;" />

## 安装QT插件

等待自动安装完成后，会弹出如下界面，点击【Install】

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202405151614967.png" alt="image-20240515161401616" style="zoom:33%;" />

如果弹出以下弹窗，点击【End Tasks】，这里是因为未关闭VS软件，点击后自动关闭

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202405151614253.png" alt="image-20240515161422903" style="zoom:33%;" />

关闭VS后，等待安装完成

## 设置QT插件

再次打开Vs，【扩展】->【Qt VS Tools】->【Options】

![image-20240515161501737](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202405151615819.png)

进入【Options】界面后，选择【Qt】->【Versions】->【add new Qt Versions】

![image-20240515161526437](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202405151615522.png)

打开【add new Qt Versions】后，点击文件夹，在Qt目录下找到【msvc2019_64/bin/qmake.exe】，这里根据自己的版本选择，点击【确定】

![image-20240515161539609](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202405151615700.png)

## 设置默认打开ui文件界面

【ui文件】右键打开方式

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202405151617579.png" alt="image-20240515161734520" style="zoom: 50%;" />

【添加】选择qt目录下的【msvc2019_64/bin/designer.exe】，设为【默认】打开

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202405151619075.png" alt="image-20240515161933727" style="zoom:50%;" />

![image-20240515164012980](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202405151640041.png)

## 下载qt插件2

--该插件用于右键创建qt文件

**qt vs cmake tools**

![image-20241008113436191](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20241008113436191.png)

# 错误

==问题1: **qt 在ui界面添加控件后在cpp文件中无法调用解决方法**==
解决方法： 点击项目，将[shadow](https://so.csdn.net/so/search?q=shadow&spm=1001.2101.3001.7020) build里的✔取消；此方法是改变项目构建（build）的位置，取消勾选后会在项目内部构建
结果：成功解决问题

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202404281724230.png" alt="image-20240428172412623" style="zoom:50%;" />

**解决**：vs中，添加完毕，组件爆红，先ctrlB编译项目，再ctrl左键点击组件，进入ui类当中，存在组件，则说明添加成功



==问题2：**在exe可执行文件目录添加qt依赖的动态库**==

* 清楚qt程序是通过msvc编译 还是 minGW编译，采用对应的powershell

使用`windeployqt`非常简单，它是一个在Qt安装目录的bin文件夹中的可执行文件。以下是使用`windeployqt`的基本步骤：

1. **打开命令提示符或者PowerShell**：

   打开`qt5.15.2（msvs 64-bit）`

   进入`cd bin`目录

2. **导入可执行文件所在的目录**：
   直接拖动exe文件进入powershell

3. **运行`windeployqt`命令**：
   `windeployqt.exe`在路径后面加上

   ```shell
   windeployqt.exe D:\software\Perfessional\QT5.15.2\5.15.2\mingw81_64\bin>D:\Work\22\Debug\站机仿真平台.exe 
   ```

4. **等待`windeployqt`执行完成**：
   `windeployqt`将会分析你的可执行文件，并将所需的Qt动态链接库复制到相同目录下。执行完成后，你应该能在该目录中看到新复制的Qt库文件。

5. **运行你的应用程序**：
   确保所有的Qt库文件都已经被复制到了正确的位置，然后尝试运行你的应用程序。

==问题3： **qt工程没有pro文件**==

build选择qmake

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202405211643847.png" alt="image-20240521164313422" style="zoom:50%;" />

==问题4：无法自动生成ui_xx_xx.h头文件==

QT:

先对项目进行清除（删除已经生成的ui文件），重新构建（build）

如果不行，则使用uic.exe手动生成

1. 打开qt5.15.2powershell
2. 进入demo.ui的目录
3. 使用命令 `uic demo.ui > ui_demo.h `生成到当前文件
4. 可以移动到自动生成ui文件的目录，方便管理，默认在：`D:\software\Perfessional\qt5.14\myProject\CSM\build\Desktop_Qt_5_15_2_MSVC2019_64bit-Debug\CSM_autogen\include`

VS:



==问题5：QString与std::string转换的乱码问题==

```cpp
std::string cstr;
QString qstring;
//从std::string 到QString
qstring = QString(QString::fromLocal8Bit(cstr.c_str()));
//从QString 到 std::string
cstr = string((const char *)qstring.toLocal8Bit());
```

==问题6： 1104无法打开动态库dll、exe==

exe: 进程未关闭，找到任务管理器关闭线程

dll：后台关闭进程，清理缓存，重新生成



# qtcreater操作

## 1 快捷键

| 快捷键         | 功能            |
| -------------- | --------------- |
| ctrl + alt + m | 打开/关闭菜单栏 |

## 2 项目管理

### 2.1 创建子目录

工程文件夹下创建目录 -->  creater中创建新文件 --> 设置文件存放的位置为新目录中 --> 自动识别cmake

--> 注意添加cmakelist的`include_directories`识别头文件路径





