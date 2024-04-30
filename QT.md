学习资料 [爱编程的大丙](https://subingwen.cn/)



QT下载网址：[Index of /new_archive/qt](https://download.qt.io/new_archive/qt/)

百度网盘：嵌入式->qt->第二章

qt账号 zhangyuqiao26@gmail.com   Vw3G7@K,zZYjq7g

zhangyuqaio26@outlook.com Zyq0326.

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

    // 进入消息阻塞，即窗口不关闭，等到点击叉号，窗口关闭
    return a.exec();
}
```

![image-20230718142235686](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230718142235686.png)

## 1.1 pro文件介绍

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



* 菜单栏

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

### QComboBox

* 下拉菜单

| 方法                                                         | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `addItem(const QString &text, const QVariant &userData = QVariant())` | 向 ComboBox 中添加一个文本项，并可选择关联一个自定义数据。   |
| `insertItem(int index, const QString &text, const QVariant &userData = QVariant())` | 在指定位置插入一个文本项，并可选择关联一个自定义数据。       |
| `removeItem(int index)`                                      | 移除指定索引处的项。                                         |
| `clear()`                                                    | 清空 ComboBox 中的所有项。                                   |
| `setCurrentIndex(int index)`                                 | 将当前选中项设置为指定索引处的项。                           |
| `currentIndex()`                                             | 返回当前选中项的索引。                                       |
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
QComboBox comboBox;
comboBox.addItem("Option 1", QVariant(1));
```

### tableWidget

* 创建新的表格

  ```cpp
  QTableWidget *table=new QTableWidget();
  ```

* 设置列数,超过的列数无法显示

  ```cpp
   table->setColumnCount(3);//设置3列
  ```

* 设置行数

  ```cpp
  table->setRowCount(5);//设置5行
  ```

* 设置表头(先设置表格行列数，在设置表头)

  ```cpp
  QStringList header;  //QString类型的List容器
  header<<"学号"<<"姓名"<<"性别";//设置内容是学号、姓名、性别
  table->setHorizontalHeaderLabels(header);//设置表头内容
  ```

* 插入一行空数据

  ```cpp
  // 序号从0开始
  int row = tableWidget.rowCount();
  tableWidget.insertRow(row);
  ```

* 每个单元格设置内容

  ```cpp
  QTableWidgetItem *item0 = new QTableWidgetItem("Item 1");
  QTableWidgetItem *item1 = new QTableWidgetItem("Item 2");
  QTableWidgetItem *item2 = new QTableWidgetItem("Item 3");
  tableWidget.setItem(row, 0, item0);
  tableWidget.setItem(row, 1, item1);
  tableWidget.setItem(row, 2, item2);
  ```

* 内容不可编辑

  ```cpp
   table->setEditTriggers(QAbstractItemView::NoEditTriggers); //设置表格内容不可编辑
  ```

  

* 显示表格

  ```cpp
  table.show()
  ```

* 设置表头字体属性

  ```cpp
  QFont font ;//定义一个字体变量
  font.setBold(true);  //设置粗体
  table->horizontalHeader()->setFont(font);//把字体变量属性加进表头中
  ```

* 设置表头的内容充满整个表格宽度

  ```cpp
  table->horizontalHeader()->setStretchLastSection(true); //设置表头充满表格的宽度
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

  

## 5 添加资源文件

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

## 6 UI控件

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

![image-20230720145353137](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230720145353137.png)

#### 7.2.1 消息对话框

* 错误对话框

![image-20230720145932970](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230720145932970.png)

```cpp
#include<QMessageBox>

connect(ui->actionwrong,&QAction::triggered,[=]{
        QMessageBox::critical(this,"critical","错误！");
    });
```

* 信息对话框

![image-20230720150629588](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230720150629588.png)

```cpp
connect(ui->actioninfo,&QAction::triggered,[=]{
        QMessageBox::information(this,"info"," 提示！");
    });
```



* 提问对话框

![image-20230720150640111](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230720150640111.png)

```cpp
connect(ui->actionchoose,&QAction::triggered,[=]{
    QMessageBox::question(this,      // 显示在当前窗口
                          "ques",    // 对话框名
                          "做出选择！", // 显示信息
                          QMessageBox::Save |QMessageBox::Cancel, // 选项名字
                          QMessageBox::Cancel); // 默认关联回车键
    });
```

第四个参数：

<img src="C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230720150434053.png" alt="image-20230720150434053" style="zoom: 80%;" />

```cpp
// 提问对话框 最后 返回的是 做出的选项
// 使用
connect(ui->actionchoose,&QAction::triggered,[=]{
        if(QMessageBox::Save ==  QMessageBox::question(this,"ques","做出选择！",QMessageBox::Save | QMessageBox::Cancel,QMessageBox::Cancel))
        {
           qDebug()<<"保存完毕！";
        }else{
           qDebug()<<"取消成功！";
        }
    });
```

#### 7.2.2 颜色对话框

```cpp
connect(ui->actioncolor,&QAction::triggered,[=]{
        QColor color = QColorDialog::getColor(QColor(255,0,0));
        qDebug()<<"红"<< color.red()<<"黄"<<color.yellow() << "蓝"<<color.blue();
    });

```

<img src="C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230720170345210.png" alt="image-20230720170345210" style="zoom:67%;" />

#### 7.3.3 文件对话框

```cpp
 QString file = QFileDialog::getOpenFileName(this,"打开文件","C:\\Users\\zhang\\Desktop"
```



```cpp
connect(ui->actionOpen,&QAction::triggered,[=](){
        QFileDialog::getOpenFileName(this,"打开文件","C:\\Users\\zhang\\Desktop","(*.txt)");
});
```



<img src="C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230720171010454.png" alt="image-20230720171010454" style="zoom:67%;" />

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

## 布局设计

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



## 12 网络编程

```
Header:
#include <QTcpServer> 
qmake:
QT += network

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

# 错误

问题: **qt 在ui界面添加控件后在cpp文件中无法调用解决方法**
解决方法： 点击项目，将[shadow](https://so.csdn.net/so/search?q=shadow&spm=1001.2101.3001.7020) build里的✔取消；此方法是改变项目构建（build）的位置，取消勾选后会在项目内部构建
结果：成功解决问题

![image-20240428172412623](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202404281724230.png)





