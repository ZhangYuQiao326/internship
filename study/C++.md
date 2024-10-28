#   项目

1、cjson网址：https://sourceforge.net/projects/cjson/

教程：[从零开始的 JSON 库教程 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/json-tutorial)

2、MyTinySTL网址：https://github.com/Alinshans/MyTinySTL
3、oatpp网址：https://github.com/oatpp/oatpp
4、Tinyhttpd网址：https://github.com/EZLippi/Tinyhttpd/blob/master/httpd.c
5、nginx网址：http://nginx.org/
6、Redis网址：https://redis.io/download

# 一 入门基础

## 1 初识

### 1.1 注释

```cpp
// 单行   ctrl+/
```

### 1.2 变量

```cpp
int a = 10;
```



### 1.3 常量

```cpp
// 1 宏常量,放在文件的上方
#define week = 7; 

// 2 修饰变量，也作为常量
const int a = 14; 
```



### 1.4 关键字

![image-20230317191627581](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230317191627581.png)

### 1.5 标识符命名

## 2 数据类型

### 2.1 整型



![image-20230317191841799](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230426120954438.png)

### 2.2 sizeof（）

```cpp
// 统计数据类型的大小
int a = 2;
sizeof(a);
```



### 2.3 浮点型

![image-20230317193148590](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230317193148590.png)

```cpp
float a = 3.13f;  // 默认显示6位数
double b = 2.313;
```

```cpp
// 科学计数法
float a = 3e2; // 3*10^2
float b =4e-2; // 4*0.1^2 
```

### 2.4 字符型

```cpp
char a = 'b'; // 1个zi'jie
```

### 2.5 转义字符

```cpp
\n
\t
\\
```

### 2.6 字符串型

```cpp
// 法1
char a[] = "hello";
// 法2 
string b = "hello"
```



## 3 运算符



## 4 流程结构

### 4.1 条件判断

```cpp
#include <iostream>
using namespace std;

int main()
{
    double a = 0;
    double b = 0;
    double c = 0;
    cout << "请输入a的体重:" << endl;
    cin >> a;
    cout << "请输入b的体重:" << endl;
    cin >> b;
    cout << "请输入c的体重:" << endl;
    cin >> c;
    if (a >= b)
    {
        if (a >= c)
        {
            cout << "最重的小猪是a" << endl;
        }
    }
    else if (b >= c)
    {
        cout << "最重的小猪是b" << endl;
    }
    else
    {
        cout << "最重的小猪是c" << endl;
    }
    system("pause");
    return 0;
}

```

### 4.2 选择结构

```cpp
#include <iostream>
using namespace std;

int main()
{
    int score = 0;
    cout << "请输入你的打分！" << endl;
    cin >> score;
    switch (score)
    {
    case 1:
        cout << "1" << endl;
        break;
    case 2:
        cout << "2" << endl;
        break;
    case 3:
        cout << "3" << endl;
        break;
    case 4:
        cout << "4" << endl;
        break;
    default:
        cout << "nothing" << endl;
        break;
    }
    system("pause");
    return 0;
}
```

### 4.3 if 和 switch区别

```cpp
suitch: 只能判别整型or字符型，可以是区间
优点： 结构清晰，执行效率搞
```

### 4.4 while循环

```cpp
#include <iostream>
#include <ctime>
using namespace std;

int main()
{
    // 添加随机数种子
    srand((unsigned int)time(NULL));
    // 生成0~99随机数，+1后为1~100，%后为随机数取值范围
    int num = rand() % 100 + 1;
    int sco = 0;

    while (1)
    {
        cout << "请输入你猜的数字:" << endl;
        cin >> sco;
        if (sco > num)
        {
            cout << "大了！" << endl;
            continue;
        }
        else if (sco < num)
        {
            cout << "过小！" << endl;
            continue;
        }
        else
        {
            cout << "恭喜猜对~" << endl;
            break;
        }
    }

    system("pause");
    return 0;
}
```

```cpp
// 获取个位数
#include <iostream>
using namespace std;

int main()
{
    int num = 100;
    int a;
    int b;
    int c;
    while (num < 1000)
    {
        a = num % 10;
        b = num / 10 % 10;
        c = num / 100;
        if (a * a * a + b * b * b + c * c * c == num)
        {
            cout << num << endl;
        }
        num++;
    }
    system("pause");
    return 0;
}
```

### 4.5 for循环

```cpp
#include <iostream>
using namespace std;

int main()
{
    for (int i = 1; i < 101; i++)
    {
        int a = i % 10;
        int b = i / 10;
        if (a == 7 || b == 7 || i % 7 == 0)
        {
            cout << "拍桌子！" << endl;
        }
        else
        {
            cout << i << endl;
        }
    }
    system("pause");
    return 0;
}

// 嵌套循环,打印星号
#include <iostream>
using namespace std;

int main()
{
    for (int i = 0; i < 10; i++)
    {
        for (int i = 0; i < 10; i++)
        {
            cout << "* ";
        }
        cout << endl;
    }

    system("pause");
    return 0;
}

// 嵌套循环，打印乘法表
#include <iostream>
using namespace std;

int main()
{
    for (int i = 1; i < 10; i++)
    {
        for (int j = 1; j < i + 1; j++)
        {
            cout << j << " * " << i << "\t";
        }
        cout << endl;
    }

    system("pause");
    return 0;
}
```

### 4.6 跳转语句

* break

* continue

* goto

  ```cpp
  #include <iostream>
  using namespace std;
  
  int main()
  {
      cout << "1" << endl;
      cout << "2" << endl;
      goto flag;
      cout << "3" << endl;
      cout << "4" << endl;
      cout << "5" << endl;
  flag:
      cout << "6" << endl;
  
      system("pause");
      return 0;
  }
  ```

  

## 5 数组

### 5.1 初始化

```cpp
int list[10];
int list[4] = {1,2,3,4}
int list[] = {1,2,3}

int main()
{
    int arr[6] = {1, 2, 3, 4, 5, 6};
    for (int i = 0; i < 6; i++)
    {
        // 查看每个元素
        cout << arr[i] << endl;
    }
    // 查看数组地址, 注意返回的是地址！！not 内容
    cout << arr << endl;
    // 查看某个元素地址
    cout << &arr[2] << endl;
    // 数组长度
    cout << sizeof(arr) / sizeof(arr[1]) << endl;
}
```

### 5.2 逆置

```cpp
#include <iostream>
using namespace std;

int main()
{
    int arr[7] = {1, 2, 3, 4, 5, 6, 7};
    int mid;
    int length = sizeof(arr) / sizeof(arr[1]);

    for (int i = 0; i < length / 2; i++)
    {
        mid = arr[i];
        arr[i] = arr[length - i - 1];
        arr[length - i - 1] = mid;
    }

    for (int i = 0; i < 7; i++)
    {
        cout << arr[i] << endl;
    }

    system("pause");
    return 0;
}
```

### 5.3 数组作为参数传入函数

```cpp
// 将数组作为参数传递
int arr[3];

// 值传递
void swap(int Arr[]){}
swap(arr); // 传入首地址相当于传入数组；

// 地址传递->指针传入
void swap(int *arr){}
swap(arr)//arr为数组首地址
```



### 5.4 冒泡排序

![image-20230320204155781](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230320204155781.png)



```cpp
#include <iostream>
using namespace std;

int main()
{
    int arr[9] = {2, 4, 0, 5, 7, 1, 3, 8, 9};
    cout << "初始的数组为:";
    for (int i = 0; i < 9; i++)
    {
        cout << arr[i];
    }
    cout << endl;
    // 冒泡排序
    for (int i = 0; i < 9 - 1; i++)
    {
        for (int j = 0; j < 9 - i - 1; j++)
        {
            if (arr[j] > arr[j + 1])
            {
                int tmp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = tmp;
            }
        }
    }
    // 排序完成
    cout << "排序后的的数组为:";
    for (int i = 0; i < 9; i++)
    {
        cout << arr[i];
    }
    cout << endl;

    system("pause");
    return 0;
}
```

### 5.5 二维数组

```cpp
// 初始化
// 二维数组定义方式
	// 1. 数据类型  数组名[行数][列数];
	// 2. 数据类型  数组名[行数][列数] = { {数据1，数据2 } ，{数据3，数据4 } };
	// 3. 数据类型  数组名[行数][列数] = { 数据1，数据2，数据3，数据4 };
	// 4. 数据类型  数组名[][列数] = { 数据1，数据2，数据3，数据4 };
int arr[2][3];

int arr[2][3] = {
    {1,2,3};
    {3,2,1}
}

int arr[2][3] = {1,2,3,4,5,6}

int arr [][3] = {1,2,3,4,5,6}; // 正确，第二个参数必须定义，且省略行时，必须赋值

int arr[][3]; // 错误，没有赋值，无法推到行数

int arr[3][]; // 不合法，行可以省略，列不可以省略


// 打印值
#include <iostream>
using namespace std;

int main()
{
    int arr[][3] = {1, 2, 3, 4, 5, 6};
    for (int i = 0; i < 2; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            cout << arr[i][j] << " ";
        }
        cout << endl;
    }

    system("pause");
    return 0;
}

// 所占空间
sizeof(arr)
// 每行  
sizeof(arr[0])
// 第一个
sizeof(arr[0[0]])
    
```

### 5.6 常用函数

```cpp
// 打印数组
void printArr(int *arr, int len)
{

    cout << "[";
    for (int i = 0; i < len; i++)
    {
        if (i == len - 1)
        {
            break;
        }
        cout << arr[i] << ",";
    }
    cout << arr[len - 1] << "]" << endl;
}

// 冒泡排序
void bubbleSort(int *arr, int len)
{
    for (int i = 0; i < len - 1; i++)
    {
        for (int j = 0; j < len - i - 1; j++)
        {
            if (arr[j] > arr[j + 1])
            {
                int tmp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = tmp;
            }
        }
    }
}
```

### 5.7 数组类型

* 数组

  ```cpp
  int a[3];
  ```

* 指针数组

  ```cpp
  // 存放指针的数组
  int* a[3] = {p1,p2,p3}
  ```

* 指向指针数组的指针

  ```cpp
   int* *p= new int* a[3];
  // int* 为数组类型，指针类型
  ```

  

* 数组指针

  ```cpp
  // 指向数组的指针
  int a[3] = {1,2,3}
  int (*p)[3] = &a;
  ```





  

## 6 函数

### 6.1 定义

* main函数只能返回int型
* 不用def

```cpp
// 定义，要写在main函数前
// 1、无返回无参数
void aaa(){
    cout<<"hello"<<endl;
}

// 2、无返回有参数
void aaa(int a){
    cout<< a <<endl;
}

// 3、有返回有参数
int aaa(int a){
    cout<< a <<endl;
    return 10;
}

// 4、有返回无参数
int aaa(){
    return 10;
}
```

### 6.2 声明

```cpp
// 声明
// 如果没有在main函数前定义函数，用声明
int aaa(int a);

// 声明可以有多次，定义只能有一次
```

### 6.3 参数传递

* 值传递

  ```cpp
  // 变量
  void swap(int num1, int num2){};
  swap(a,b);
  
  // 数组
  void swap(int Arr[],int len){}
  swap(arr,len); // 传入首地址相当于传入数组；
  
      
  // 结构体
  void print(Stunt stu){};
  print(stu);
  
  // 结构体数组
  void print(Stunt stu[], int len){};
  print(stu, len);
  
  ```

  

  地址传递

  ```cpp
  // 变量
  void swap(int *num1, int *num2){};
  swap(&a,&b);
      
  // 数组
  void Sort(int *p){};
  Sort(arr);
  
  // 结构体
  void print(Stunt *stu){};
  print(&stu);
  ```

* 与python对比

```cpp
//1.函数传参过程中，对于一些基本数据类型，如int（整型），float（浮点型），str（字符串）等，是值传递，函数内部对以上数据类型的数据进行修改时并不会改变原值。

//2.对于list（列表）、dict（字典）、tuple（元组）则是地址传递，函数内部对以上数据类型操作时会改变原数据值。
```

### 6.4 创建新函数

步骤：

1、 确定参数类型-----是否改变原变量值

* 值传递： 拷贝副本进行函数操作   `void fun(int a){};`     `fun(a);`

* 地址传递： 对源变量进行改变操作 `void fun(int *p){};`    `fun(&a);`
* 引用传递： 相当于地址传递 `void fun(int &a);`  `fun(a)`

2、 确定函数返回值类型-----返回值是否存放于原内存空间

* 普通函数：将执行结果存放在一个新的内存空间  `void fun(){};`

* 引用类型函数： 将执行结果写到原本的内存空间

  `Person &addPerson (Person p) {this->age += p.age};` `p1.addPerson(p2).addPerson(p2)`

### 6.5 常用函数

```cpp
// 随机函数
rand()%(b-a+1)+a  // 生成随机a~b的整数
```

## 7 输出函数

### 7.1 格式化输出 snprintf

```cpp
snprintf 接受多个参数，下面是各参数的说明：

str：指向要写入的目标字符串的指针。
size：目标字符串的大小（包括结尾的空字符）。
format：格式化字符串，指定了要输出的数据的格式。
...：可变数量的参数，根据 format 字符串中的占位符进行格式化。int snprintf(char* str, size_t size, const char* format, ...);
```

`snprintf` 接受多个参数，下面是各参数的说明：

- `str`：指向要写入的目标字符串的指针。

- `size`：目标字符串的大小（包括结尾的空字符）。

- `format`：格式化字符串，指定了要输出的数据的格式。

- `...`：可变数量的参数，根据 `format` 字符串中的占位符进行格式化。

- ```c
  char fileName[LOG_NAME_LEN] = {0};
  snprintf(fileName, LOG_NAME_LEN - 1, "%s/%04d_%02d_%02d%s",
           path_, t.tm_year + 1900, t.tm_mon + 1, t.tm_mday, suffix_);
  // ./log/2023_06_01.log
  ```

- 成功：返回写入的字符数，不包括空字符

  失败:-1



## 8  指针

### 7.1 定义

```cpp
// 指针内为地址
int a =10;
int *p = &a;
int **pp = &p
// 调用
*p = 20
```

### 7.2 指针常量

* 指针常量和常量指针，本质均为指针
* 只是使用后的作用不同

```cpp
int * const p = &a;
// p不能再指向别的位置 p = &b ×
// *p可以修改当前位置的值 *p = 2 √
```



### 7.3 常量指针

```cpp
const int *p = &a;
// *p不能修改值 *p = 12 ×
// p可以指向别的位置 p = &b √
```

### 7.4 数组指针

```cpp
int arr[] = {1,2,3};
// arr是第一个元素的地址
int *p = arr;
// 调用，通过指针自增访问元素
 for (int i = 0; i < 3; i++)
    {
        cout << *p << endl;
        p++;
    }
```

### 7.5 函数指针

* 详见高级编程
格式为 返回类型 `(*指针变量名)(参数列表)`
```cpp
int (*funcPtr)(int, int);
void (*callback)(LoopAsync *async);
```

### 分辨

```cpp
int *p[10]
int (*p)[10]
int *p(int)
int (*p)(int)

```

- int *p[10]表示指针数组，强调数组概念，是一个数组变量，数组大小为10，数组内每个元素都是指向int类型的指针变量。
- int (*p)[10]表示数组指针，强调是指针，只有一个变量，是指针类型，不过指向的是一个int类型的数组，这个数组大小是10。
- int *p(int)是函数声明，函数名是p，参数是int类型的，返回值是int *类型的。
- int (*p)(int)是函数指针，强调是指针，该指针指向的函数具有int类型参数，并且返回值是int类型的。

### 7.6 包装冒泡排序

```cpp
#include <iostream>
using namespace std;

// 打印数组
void printArr(int *arr, int len)
{

    cout << "[";
    for (int i = 0; i < len; i++)
    {
        if (i == len - 1)
        {
            break;
        }
        cout << arr[i] << ",";
    }
    cout << arr[len - 1] << "]" << endl;
}
// 冒泡排序
void bubbleSort(int *arr, int len)
{
    for (int i = 0; i < len - 1; i++)
    {
        for (int j = 0; j < len - i - 1; j++)
        {
            if (arr[j] > arr[j + 1])
            {
                int tmp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = tmp;
            }
        }
    }
}

int main()
{
    int arr[10] = {4, 5, 7, 9, 2, 6, 8, 3, 1, 10};
    int len = sizeof(arr) / sizeof(arr[0]);
    print(arr, 10);
    bubbleSort(arr, 10);
    printArr(arr, 10);

    system("pause");
    return 0;
}
```



## 9 结构体

### 8.1 定义

```cpp
#include <iostream>
using namespace std;

struct Student
{
    string name;
    int age;
    string country = "中华人民共和国"; // 常量写在后面
}; // 注意冒号


int main()
{
    // 初始化
    struct Student zhangsan;（不适用）
    Pool* pool = new Pool();（法1）
	Pool* pool = static_cast<Pool*>(std::malloc(sizeof(Pool)));
    
    // 通过 . 调用属性
    zhangsan.name = "张三";
    zhangsan.age = 23;
    
    cout << "名字：" << zhangsan.name << " 年龄：" << zhangsan.age << " 国籍：" << zhangsan.country << endl;
    system("pause");
    return 0;
}
```

### 8.2 结构体数组

```cpp
// 用数组形式，一次性实例化多个对象
int main()
{
    struct Student stuArr[3] = {
        {"李四", 22},
        {"王五", 18},
        {"陈六", 7}};

    cout << stuArr[1].age << stuArr[2].name << stuArr[0].country << endl;

    system("pause");
    return 0;
}
```

### 8.3 结构体指针

```cpp
int main(){
	Student s = {"狗子", 3};
    Student *q = &s;
    // 1 用箭头访问
    cout << q->country << endl;
    // 2 *p== s ,用 . 访问
    cout << (*q).age << endl;
}
```

### 8.4 结构体嵌套

```cpp
#include <iostream>
using namespace std;
// 注意嵌套的小结构体要定义在大结构体前面
struct Student
{
    string name;
    int age;
};
// 老师
struct Teacher
{
    string name;
    int age;
    int id;
    // 结构体类型+变量名
    struct Student stu;
};

int main()
{	
    // 赋值用{}嵌套赋值
    Teacher t = {"小时", 12, 001, {"小孩子", 4}};
	
    // 访问，多个 . 依次
    cout << t.age << t.stu.name << endl;

    system("pause");
    return 0;
}
```

### 8.5 结构体作为函数参数

```cpp
#include <iostream>
using namespace std;

struct Student
{
    string name;
    int age;
};

// 值传递
void printStu(Student stu)
{
    stu.age = 1;
    stu.name = "李四";
    cout << "函数内部值传递 " << stu.age << stu.name << endl;
};

// 地址传递
void printStu_add(Student *p)
{
    p->age = 2;
    p->name = "王五";
    cout << "函数内部地址传递 " << p->age << p->name << endl;
};

int main()
{
    Student stu1;
    stu1.age = 12;
    stu1.name = "张三";
    cout << "main函数内:" << stu1.age << stu1.name << endl;
    printStu(stu1);
    cout << "main函数-值传递:" << stu1.age << stu1.name << endl;
    printStu_add(&stu1);
    cout << "main函数-地址传递:" << stu1.age << stu1.name << endl;

    system("pause");
    return 0;
}
```

![image-20230321205618122](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230321205618122.png)



### 8.6 结构体数组作为函数参数

```cpp
// 类型+虚拟数组名，[]内不带有数组长度，长度外部赋值；
void print(struct Teacher Arr[], int len){};
// 调用
Teacher Arr[5];
int len = sizeof(Arr)/sizeof(Arr[0]);
// 传入结构体数组名
print(Arr,len)
```



### 8.6 const 修饰

```cpp
// 背景
// 因为值传递，是复制一份原数据，会造成内存的浪费
// 地址传递可以有效缓解内存，却会改变源数据
// const修饰后，地址传递将不会改变元数据
void printStu_add(const Student *p)
{
    p->age = 2;
    p->name = "王五";
    cout << "函数内部地址传递 " << p->age << p->name << endl;
};
int main(){
   printStu_add(stu) 
};
```

### 8.7 老师带学生

```cpp
#include <iostream>
using namespace std;

struct Student
{
    string name;
    int scords;
};

struct Teacher
{
    string name;
    struct Student sArr[5];
};
// 赋值函数
void getinfo(struct Teacher Arr[], int len, string name)
{
    for (int i = 0; i < len; i++)
    {
        Arr[i].name = name[i];
        for (int j = 0; j < 5; j++)
        {
            Arr[i].sArr[j].name = name[j];
            Arr[i].sArr[j].scords = 60;
        }
    }
};
// 输出函数
void print(struct Teacher Arr[], int len)
{
    for (int i = 0; i < len; i++)
    {
        cout << "老师:" << Arr[i].name << endl;
        for (int j = 0; j < 5; j++)
        {
            cout << "学生:" << Arr[i].sArr[j].name;
            cout << "分数" << Arr[i].sArr[j].scords << endl;
        }
    }
};

int main()
{
    Teacher tArr[3];
    int len_tea = sizeof(tArr) / sizeof(tArr[0]);
    string name = "ABCDE";
    getinfo(tArr, len_tea, name);
    print(tArr, len_tea);

    system("pause");
    return 0;
}
```

## 10 分文件编写

```cpp
// 相当于导包导包
// 1. .h头文件
// 包括其他头文件以及全局函数声明、类中方法声明
// 2. .cpp原文件
// 来写自定义函数，方法注明作用域，并用#include "xx.h" 导入自定义头文件
```

### 9.1 类

* 不分开编写

```cpp
#include <iostream>
using namespace std;

class Circle
{
    // 1、权限
public:
    // 2、属性
    const double PI = 3.14;
    double m_r;
    // 3、行为/方法
    double zc()
    {
        return 2 * PI * m_r;
    };
    void setR(double r)
    {
        m_r = r;
    };
};

int main()
{
    Circle a1;
    a1.setR(3.1);
    cout << "a1的半径为: " << a1.m_r << endl;
    cout << "a1的周长为: " << a1.zc() << endl;

    system("pause");
    return 0;
}

```



* 文件编写

```cpp
// .h头文件

# include<iostream>
using namespace std;

class Circle
{
    // 1、权限
public:
    // 2、属性
    const double PI = 3.14;
    double m_r;
    // 3、行为/方法
    // 只保留声明
    double zc();
    void setR(double r);
};
```

```cpp
// .cpp类源文件

# include<iostream>
# include "Circle"
using namespace std;

// 对类中的方法进行实现
// 注明作用域为Circle类中的成员函数
double Circle::zc()
{
    return 2 * PI * m_r;
};
void Circle::setR(double r)
{
    m_r = r;
};

```

```cpp
// 主函数源文件

# include<iostream>
# include "Circle"
using namespace std;

int main()
{
    Circle a1;
    a1.setR(3.1);
    cout << "a1的半径为: " << a1.m_r << endl;
    cout << "a1的周长为: " << a1.zc() << endl;

    system("pause");
    return 0;
}
```







# 二 核心

## 1 内存模型

代码执行前

* 代码段区
* 全局区（静态区）

代码执行后

* 堆
* 栈

### 1.1 代码段

```cpp
// 存放程序体的二进制代码。比如我们写的函数，都是在代码区的。
// 宏定义是直接替换，不会分配内存，存储于程序的代码段中；
// const常量需要进行内存分配，存储于程序的数据段中
```

### 1.2 全局区

![image-20230323094555178](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230323094555178.png)

```cpp
//全局区：
// 全局变量：定义在main函数外边的变量

int a = 10; // 全局变量
const int a = 10;  // 全局常量
int main(){
    int b = 10; // 局部变量（非全局）
    const int b =10;  // 局部常量（非全局）
    string a = "abcde"; // 字符串常量
    static int c = 10; // 静态变量
}
```

### 1.3 栈

```cpp
// 存放
// 局部变量、函数形参

// 由编译器自动释分配释放，不要返回局部变量的值
return (int)&a;  // 不能返回，内存已经释放
```

### 1.4 堆

```cpp
// 自己讲数据开辟到堆区，new返回的是地址,用指针接收
int *p = new int(13);
delete p; // 删除地址

int *arr = new int[10];
for(int i = 0; i<10; i++){
    arr[i] = 100+i;
}
delete[] arr; //删除数组地址

```



## 2 引用

### 2.1 定义

* reference
* 给变量起别名，操作同一块内存

引用在C++中的本质是一个别名（alias），它允许你为一个已存在的对象创建一个别名，从而可以通过这个别名来访问原始对象。引用的主要目的是提供一种更直观、更容易理解和使用的方式来操作数据，同时避免了不必要的数据复制。

引用的存在有以下主要原因：

1. **避免数据的复制**：当你传递一个对象给函数或在函数中返回一个对象时，C++通常会复制整个对象，这可能会导致性能开销。引用允许你通过引用原始对象来传递和操作数据，而不需要复制整个对象。

2. **提高代码的可读性**：引用可以用来创建别名，使代码更具可读性。通过引用，你可以更清晰地表达你的意图，以及你正在操作的是原始对象。

3. **支持操作符重载**：引用是操作符重载的基础之一，它允许你创建类似于内置类型的自定义类型。例如，引用使得自定义类能够像内置类型一样使用赋值运算符、下标运算符等。

4. **支持函数返回左值**：引用允许函数返回一个左值，这对于连续赋值和函数链式调用非常有用。如果函数返回的是一个引用，那么可以通过连续调用函数来修改相同的对象。

引用的一个典型应用是函数参数传递，尤其是按引用传递（传递引用而不是复制对象）。这可以避免不必要的数据复制，提高程序的性能。例如：

```cpp
void modifyValue(int& value) {
    value = 42; // 修改原始对象的值
}

int main() {
    int x = 10;
    modifyValue(x); // 传递 x 的引用，允许在函数中修改 x 的值
    // 现在 x 的值为 42
    return 0;
}
```

总之，引用是C++中的一种强大的工具，它提供了一种更灵活、更高效的方式来处理数据，同时提高了代码的可读性和可维护性。引用的本质是为了提供一种更接近原始数据的访问方式，而不需要进行不必要的数据复制。

![image-20231205100101300](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20231205100101300.png)



### 2.2 引用做函数参数

```cpp
// 引用传递
// 形参改变实参
void swap(int &a, int &b){
    int temp = a;
    a = b;
    b = temp;
}
void main(){
    int a = 1;
    int b =2;
    swap(a,b);
}
```



### 2.3 引用做函数返回值

![image-20231205102924391](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20231205102924391.png)

[static具体用法](#static1)

```cpp
// 传引用返回
// 即将返回的数据存放在原本的内存空间中，最终函数返回为内存空间的地址
int& fun(){
    int a = 10;
    return a; // ❌ a存放在栈内，函数执行完毕，内存空间释放，无法存放a，所以不能返回
    static int b = 1; // 在数据段开辟内存空间，生命周期为main函数
    return b; // 静态变量内存不释放，可以返回，返回值为b的引用，即b的地址, int &tmp = b;
}
void main(){
    int& w = fun(); // w为tmp的引用，tmp为b的引用
    fun() =  20; // 法1：引用赋值
    w = 10； //法2：引用赋值
       
}
```

```cpp
// 传值返回
int fun(){
    int a = 10;
    return a;    // 返回临时变量tmp，具有常性，即 const int tmp = a;
}
void main(){
    
    int v = fun();  // 赋值
    
    int &w = fun(); // ❌,返回的是const tmp， 不能权限放大
    const int &w = fun();
    fun() =  20; // 法1：引用赋值
    w = 10； //法2：引用赋值
       
}
```

```cpp
// 关于接收
// 1 引用 接收 传引用返回
int &a = int& fun();
const int &a = int& fun();

// 2 值 接收传值返回
int a = int func();

// 3 常量引用接收值返回
const int &a = int func();
```



### 2.4 指针和引用的转换

```cpp
int x = 42;
int* ptr = &x;
int& ref = *ptr; // 将指针 ptr 转换为引用 ref

```

```cpp
int y = 10;
int& r = y;
int* ptr2 = &r; // 将引用 r 转换为指针 ptr2

```





## 3 函数提高

### 3.1 默认参数

* 默认参数放在后边

```cpp
int func(int a, int b = 10, int c =20){};
```

* 声明和函数定义只能有一个有默认参数

```cpp
int fun(int a = 10, int b = 1);

int fun(int a, int b){};
```

```cpp
int fun(int a, int );

int fun(int a = 10, int b = 1){};
```

### 3.2 占位参数

* 调用函数时候，需要给占位参数传值

```cpp
int fun(int a, int){};

fun(10,2);
```

* 占位参数可以有默认值

```cpp
int fun(int a, int = 2){};

fun(10);
```

### 3.3 函数重载

* 可以让函数名相同，提高复用性

* 条件：1、同一个作用域

  ​            2、函数名相同

  ​            3、确保参数类型 or 参数个数 or 参数顺序不同

```cpp
int fun(int a){};
int fun(int a, int a){};
int fun (float a){};
```

* 注意：

```cpp
// 引用作为参数
void fun(int &a){};
void fun(const int &a){};

int a =10;
fun(a); // void fun(int &a){};
fun(10); //void fun(const int &a){};
```

## 4 类和对象

下面具体展开



# 五 文件操作

## 5.1 文本文件

* 五步操作
* 文件打开方式
* ![image-20230404223629526](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230404223629526.png)

```cpp
#include <iostream>
// 1、头文件
#include <fstream>
using namespace std;

void writer()
{
    // 2、实例化文件流
    ofstream ofs;
    // 3、打开文件（位置，打开方式）
    ofs.open("person.txt", ios::out);
    // 4、写入
    ofs << "姓名:张宇乔" << endl;
    ofs << "年龄:23" << endl;
    ofs << "性别：男 " << endl;
    // 5、关闭文件
    ofs.close();
    cout << "success!" << endl;
}

void reader()
{	
    // 2、实例化文件流
    ifstream ifs;
    // 3、打开文件
    ifs.open("person.txt", ios::in);

    if (!ifs.is_open())
    {
        cout << "文件打开失败！" << endl;
        return;
    }
    else
    {
        // 4、按行读文件到控制台
        string line;
        while (getline(ifs, line)) //从ifs读到line里，控制台打印
        {
            cout << line << endl;
        }
    }
    // 5、关闭文件
    ifs.close();
}

int main()
{
    // writer();
    reader();
    system("pause");
    return 0;
}
```

```cpp
// 写入对象
class Person{
    int age;
    stirng name;
    int id;
}

ofstream ofs;
ofs.open(txt,ios::out);
int age;
stirng name;
int id;
while(ofs<<age && ofs<<name && ofs<<id){
    cout<<"success"<<endl;
}


// 读
ifstream ifs;
ifs.open(txt,ios::in);
Person p;
ifs>>p.age;
ifs>>p.name;
ifs>>p.id
```

* 读文件内容，将其分开

```cpp
#include <sstream>
#include <ifstream>

static ShaderCodeRes getCode(const std::string &filepath) {
    // 从指定文件中获取着色器逻辑代码
    std::ifstream file(filepath);

    enum class ShaderType {
        NONE = -1, VERTEX = 0, FRAGMENT = 1
    };
    ShaderType type = ShaderType::NONE;

    std::string line;
    std::stringstream ss[2];
    while (getline(file, line))
    {
        // 分割不同的着色器
        if (line.find("#shader") != std::string::npos) {
            if (line.find("vertex") != std::string::npos) {
                // vertex shader
                type = ShaderType::VERTEX;
            }
            else if (line.find("fragment") != std::string::npos) {
                // fragment shader
                type = ShaderType::FRAGMENT;
            }
        }
        else {
            // 不分隔
            ss[(int)type] << line << '\n';

        }
    }
    
    // 将sstream内容返回为字符串类型
    return { ss[0].str(), ss[1].str()};
}
```



## 5.2 二进制文件

1、二进制方式写文件主要利用流对象调用成员函数write

2、函数原型 ：`ostream& write(const char * buffer,int len);`

3、参数解释：字符指针buffer指向内存中一段存储空间。len是读写的字节数

```cpp
#include <fstream>
#include <string>

class Person
{
public:
	char m_Name[64];
	int m_Age;
};

//二进制文件 写文件
void writer()
{
	//1、包含头文件

	//2、创建输出流对象  // 声明二进制方式写入
	ofstream ofs("person.txt", ios::out | ios::binary);
	
	//3、打开文件
	//ofs.open("person.txt", ios::out | ios::binary);

	Person person = {"张三"  , 18};

	//4、写文件   //person的地址开始，写入他的长度   // 地址注意转化为const char*
	ofs.write((const char *)&person, sizeof(person));

	//5、关闭文件
	ofs.close();
}

// 二进制 读文件
void reader(){
    
    ifstream ifs("person.txt", ios::in | ios::binary)
    if(!ifs.is_open){
        cout<< "打开失败！"<<endl;
        return;
    }else{
        ////person的地址开始，写入他的长度   // 地址注意转化为char*
        ifs.read((char *)&person, sizeof(person));
        cout<<"姓名"<<person.name<<endl;
    }
    ifs.close();
}
int main() {

	writer();
    reader();

	system("pause");

	return 0;
}
```

## 5.3 C中的操作文件函数

```c
# include<stdio>

FILE *fp;  // fp指向FILE文件结构体，（句柄）用来操作文件

fp = fopen("hello.txt","w")；  //"r" 为只读模式，"w" 为写入模式，"a" 为追加模式等
if(fp == nullptr){
	return 1;
}

fprintf(fp,"my name is\n");  // 写入数据
fputs(buff.begin(), fp); //法2

fclose(fp);   // 关闭文件

// 读方式打开
fp = fopen("hello.txt","r");
if(fp == nullptr){
	return 1;
}

char buff[1024];
while(fgets(buff,sizeof(buff),fp) != NULL){   // 读取一行
	printf("%s",buff) 
}

// 追加方式打开
fp_ = fopen(fileName, "a");
if (fp_ == nullptr)
{
    mkdir(path_, 0777);  // 0777权限创建目录
    fp_ = fopen(fileName, "a");
}
```

* 若是多线程访问文件，需要用互斥锁

  







# 四 面向对象

* 具有相同属性的对象统称为类

## 4.1 封装

### 4.1.1 封装

```cpp
#include <iostream>
using namespace std;

class Circle
{
    // 1、权限
public:
    // 2、属性
    const double PI = 3.14;
    double m_r;
    // 3、行为/方法
    double zc()
    {
        return 2 * PI * m_r;
    };
    void setR(double r)
    {
        m_r = r; // 方法中调用属性，直接使用即可，不用self. 
    };
};

int main()
{
    Circle a1;
    a1.setR(3.1);
    cout << "a1的半径为: " << a1.m_r << endl;
    cout << "a1的周长为: " << a1.zc() << endl;

    system("pause");
    return 0;
}
```

### 4.1.2 访问权限

* 公共权限 public            类内可访问，类外可访问
* 保护权限 protected      类内可访问，类外不可访问，儿子可访问
* 私有权限 private           类内可访问，类外不可访问。儿子不可访问

```cpp
class Per{
public：
    string m_Name;
protected:
    int age;
private:
    m_Id;
    m_Password;

public:
    void setName(string name){
        m_Name = name;
    }
}
```

### 4.1.3 静态属性、方法类外定义

* 静态成员变量、成员函数可类外定义
* 成员变量不可类外定义

```cpp
#include <iostream>
using namespace std;

class Person
{
public:
    static int a;
    int b;
    Person(int b);
    void func(int a);
};
int Person::a = 1;
void Person::func(int a)
{
    this->a = a;
}

Person::Person(int b)
{
    this->b = b;
}

int main()
{
    Person p(2);
    cout << p.a << endl;
    cout << p.b << endl;
    p.func(3);
    cout << p.a << endl;

    system("pause");
    return 0;
}
```



### 4.1.4 struct和class区别

* 访问权限不同

  struct默认公有

  class默认私有，需要转为public才能被使用

### 4.1.5 成员属性私有化

* 设置外部接口用来访问（set/show）

* ```cpp
  class Stu{
  private:
      int m_Age;
      int m_Id;
  
  public:
      void setId(int id){
          m_Id = id;
      };
      int showId(){
          return m_Id;
  }
  }
  ```

  

## 4.2 多态

多态分为两类

* 静态多态: 函数重载 和 运算符重载属于静态多态，复用函数名
* 动态多态: 派生类和虚函数实现运行时多态



静态多态和动态多态区别：

* 静态多态的函数地址早绑定  -  编译阶段确定函数地址
* 动态多态的函数地址晚绑定  -  运行阶段确定函数地址

### 4.2.1 动态多态

```cpp
// 使用条件

  1、 有继承关系

  2、子类重写父类的虚函数

  3、父类的指针或引用指向子类的对象，即定义父类引用，调用时传参子类对象，执行子类的重写后函数

//使用场景

  1、通过一个全局函数，调用不同子类对象的同一个函数，一个函数执行不同的操作
  2、为了接口的最大程度复用
// 使用方式
  1、子类的对象实例化方式不同(通过指针or引用实现)
      普通 Son son1；
      多态1 Parent *son2 = new SOn;
	  多态2 Parent & son3 = son1;
```

```cpp
class Animal
{
public:
	//Speak函数就是虚函数
	//函数前面加上virtual关键字，变成虚函数，那么编译器在编译的时候就不能确定函数调用了。
	virtual void speak()
	{
		cout << "动物在说话" << endl;
	}
};

class Cat :public Animal
{
public:
	void speak()
	{
		cout << "小猫在说话" << endl;
	}
};

class Dog :public Animal
{
public:

	void speak()
	{
		cout << "小狗在说话" << endl;
	}

};
//我们希望传入什么对象，那么就调用什么对象的函数
//如果函数地址在编译阶段就能确定，那么静态联编
//如果函数地址在运行阶段才能确定，就是动态联编

// 全局函数，传入父类的指针或引用
void DoSpeak(Animal & animal)
{
	animal.speak();
}

void test01()
{
	Cat cat;
    //父类指针或引用指向子类对象
	DoSpeak(cat);


	Dog dog;
    //父类指针或引用指向子类对象
	DoSpeak(dog);
}


int main() {

	test01();

	system("pause");

	return 0;
}
```

### 4.2.2 动态继承原理

```
动态多态的实现关键在于虚函数，基类通过virtual关键字声明和实现虚函数，此时基类会拥有一张虚函数表，虚函数表会记录其对应的函数指针。
当子类继承基类时，子类也会获得一张虚函数表，注意，是复制父类的表，不是与父类共用一张表，不同之处在于，子类如果重写了某个虚函数，其在虚函数表上的函数指针会被替换为子类的虚函数指针。
```



![image-20230404123555238](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230404123555238.png)



### 4.2.3 案例1--计算器

```cpp
# include<iostream>;
using namespace std;
// 基类
class BaseCaculator {
public:
	int num1;
	int num2;
	virtual int getResult()
	{
		return 0;
	}
};
// 加法
class Add :public BaseCaculator {
public:
	Add(int a, int b) {
		this->num1 = a;
		this->num2 = b;
	}
	int getResult() {
		return num1 + num2;
	}
};

// 乘法
class Mul :public BaseCaculator {
public:
	Mul(int a, int b) {
		this->num1 = a;
		this->num2 = b;
	}
	int getResult() {
		return num1 * num2;
	}
};

// 指针实现多态-法1(推荐)
void test1() {
	BaseCaculator* bc = new Add(1, 2);
	cout << bc->getResult() << endl;
	delete bc;
}
// 指针实现多态-法2
int act(BaseCaculator *p){
    return p->getResult();
    delete p;
}
void test2(){
    act(new Add(1,2))
    
}
// 引用实现多态-法1
void test2() {
	Mul mul(2, 3);
	BaseCaculator& bb = mul;
	cout << bb.getResult() << endl;
}
// 引用实现多态-法2  
int act(BaseCaculator &bc) {
	 return bc.getResult();
}
void test3() {
	Mul mul(3, 4);
	cout<<act(mul)<<endl;
}

int main() {
	test1();
	test2();
	test3();

	system("pause");
	return 0;

}
```

### 4.2.5 纯虚函数和抽象类

* 虚函数：一个类中只有几个函数是各自特性，有数据是共享的
* 纯虚函数：整个父类全是模板，均需要子类重写

```cpp
// 虚函数等号后为0，则纯虚函数
// 有一个纯虚函数，则类为抽象类
// 抽象类特点：
// 1、 无法实例化
// 2、 抽象类的子类，必须要重写父类
class Base{
public:
    virtual void func() = 0;
}
```



### 4.2.5 案例2--泡饮料

```cpp
//抽象制作饮品
class AbstractDrinking {
public:
	//烧水
	virtual void Boil() = 0;
	//冲泡
	virtual void Brew() = 0;
	//倒入杯中
	virtual void PourInCup() = 0;
	//加入辅料
	virtual void PutSomething() = 0;
	//规定流程
	void MakeDrink() {
		Boil();
		Brew();
		PourInCup();
		PutSomething();
	}
};

//制作咖啡
class Coffee : public AbstractDrinking {
public:
	//烧水
	virtual void Boil() {
		cout << "煮农夫山泉!" << endl;
	}
	//冲泡
	virtual void Brew() {
		cout << "冲泡咖啡!" << endl;
	}
	//倒入杯中
	virtual void PourInCup() {
		cout << "将咖啡倒入杯中!" << endl;
	}
	//加入辅料
	virtual void PutSomething() {
		cout << "加入牛奶!" << endl;
	}
};

//制作茶水
class Tea : public AbstractDrinking {
public:
	//烧水
	virtual void Boil() {
		cout << "煮自来水!" << endl;
	}
	//冲泡
	virtual void Brew() {
		cout << "冲泡茶叶!" << endl;
	}
	//倒入杯中
	virtual void PourInCup() {
		cout << "将茶水倒入杯中!" << endl;
	}
	//加入辅料
	virtual void PutSomething() {
		cout << "加入枸杞!" << endl;
	}
};

//业务函数
void DoWork(AbstractDrinking* drink) {
	drink->MakeDrink();
	delete drink;
}

void test01() {
	DoWork(new Coffee);
	cout << "--------------" << endl;
	DoWork(new Tea);
}


int main() {

	test01();

	system("pause");

	return 0;
}
```

### 4.2.6 虚析构和纯虚析构

总结：

​	1. 虚析构或纯虚析构就是用来解决通过父类指针释放子类对象

​	2. 如果子类中没有堆区数据，可以不写为虚析构或纯虚析构

​	3. 拥有纯虚析构函数的类也属于抽象类

 ```cpp
 class Animal {
 public:
 
 	Animal()
 	{
 		cout << "Animal 构造函数调用！" << endl;
 	}
 	virtual void Speak() = 0;
 
 	//虚析构函数
 	virtual ~Animal()
 	{
 		cout << "Animal虚析构函数调用！" << endl;
 	}
 
 	//纯虚构函数，类外定义
 	virtual ~Animal() = 0;
 };
 
 Animal::~Animal()
 {
 	cout << "Animal 纯虚析构函数调用！" << endl;
 }
 
 
 
 class Cat : public Animal {
 public:
     string *m_Name;
 	Cat(string name)
 	{
 		cout << "Cat构造函数调用！" << endl;
         // 通过堆开辟内存1
 		m_Name = new string(name);
 	}
 	virtual void Speak()
 	{
 		cout << *m_Name <<  "小猫在说话!" << endl;
 	}
 	~Cat()
 	{
 		cout << "Cat析构函数调用!" << endl;
         // 手动释放堆内存1
 		if (this->m_Name != NULL) {
 			delete m_Name;
 			m_Name = NULL;
 		}
 	}
 
 };
 
 void test01()
 {
     // 再次开辟堆内存2
 	Animal *animal = new Cat("Tom");
 	animal->Speak();
 
 	//通过父类指针去释放内存2，会导致子类对象可能清理不干净，造成内存泄漏
 	//怎么解决？给基类增加一个虚析构函数
 	//虚析构函数就是用来解决通过父类指针释放子类对象
 	delete animal;
 }
 
 int main() {
 
 	test01();
 
 	system("pause");
 
 	return 0;
 }
 ```

### 4.2.7 案例3--组装电脑

```cpp
#include<iostream>
using namespace std;

//抽象CPU类
class CPU
{
public:
	//抽象的计算函数
	virtual void calculate() = 0;
};

//抽象显卡类
class VideoCard
{
public:
	//抽象的显示函数
	virtual void display() = 0;
};

//抽象内存条类
class Memory
{
public:
	//抽象的存储函数
	virtual void storage() = 0;
};

//电脑类
class Computer
{
public:
	Computer(CPU * cpu, VideoCard * vc, Memory * mem)
	{
		m_cpu = cpu;
		m_vc = vc;
		m_mem = mem;
	}

	//提供工作的函数
	void work()
	{
		//让零件工作起来，调用接口
		m_cpu->calculate();

		m_vc->display();

		m_mem->storage();
	}

	//提供析构函数 释放3个电脑零件
	~Computer()
	{

		//释放CPU零件
		if (m_cpu != NULL)
		{
			delete m_cpu;
			m_cpu = NULL;
		}

		//释放显卡零件
		if (m_vc != NULL)
		{
			delete m_vc;
			m_vc = NULL;
		}

		//释放内存条零件
		if (m_mem != NULL)
		{
			delete m_mem;
			m_mem = NULL;
		}
	}

private:

	CPU * m_cpu; //CPU的零件指针
	VideoCard * m_vc; //显卡零件指针
	Memory * m_mem; //内存条零件指针
};

//具体厂商
//Intel厂商
class IntelCPU :public CPU
{
public:
	virtual void calculate()
	{
		cout << "Intel的CPU开始计算了！" << endl;
	}
};

class IntelVideoCard :public VideoCard
{
public:
	virtual void display()
	{
		cout << "Intel的显卡开始显示了！" << endl;
	}
};

class IntelMemory :public Memory
{
public:
	virtual void storage()
	{
		cout << "Intel的内存条开始存储了！" << endl;
	}
};

//Lenovo厂商
class LenovoCPU :public CPU
{
public:
	virtual void calculate()
	{
		cout << "Lenovo的CPU开始计算了！" << endl;
	}
};

class LenovoVideoCard :public VideoCard
{
public:
	virtual void display()
	{
		cout << "Lenovo的显卡开始显示了！" << endl;
	}
};

class LenovoMemory :public Memory
{
public:
	virtual void storage()
	{
		cout << "Lenovo的内存条开始存储了！" << endl;
	}
};


void test01()
{
	//第一台电脑零件
	CPU * intelCpu = new IntelCPU;
	VideoCard * intelCard = new IntelVideoCard;
	Memory * intelMem = new IntelMemory;

	cout << "第一台电脑开始工作：" << endl;
	//创建第一台电脑
	Computer * computer1 = new Computer(intelCpu, intelCard, intelMem);
	computer1->work();
	delete computer1;

	cout << "-----------------------" << endl;
	cout << "第二台电脑开始工作：" << endl;
	//第二台电脑组装
	Computer * computer2 = new Computer(new LenovoCPU, new LenovoVideoCard, new LenovoMemory);;
	computer2->work();
	delete computer2;

	cout << "-----------------------" << endl;
	cout << "第三台电脑开始工作：" << endl;
	//第三台电脑组装
	Computer * computer3 = new Computer(new LenovoCPU, new IntelVideoCard, new LenovoMemory);;
	computer3->work();
	delete computer3;

}
```





### 4.2.4 模板

```cpp
// 基类
class Parent{
private:
    int a;
public:
    virtrue void func(){};
};
// 编写接口1--引用
void operator(Parent &p){
    p.func()
};
// 编写接口2--指针
void operator(Parent *p){
    p->func();
    delete p;
}

//子类
class SOn:public Parent{
    void func(){
        // 重写
    }
};

// 调用1
void test1(){
    Son son;
    operator(son); // 接口调用
    Son tea;
    operator(tea);
        
}
// 调用2
void test2(){
    operator(new Son);
}

```

```cpp
// 基类
class Parent{
public:
    virtual void func() = 0
}
// 继承
class Son:public Parnt{
public:
    void fun(){
        //改写
    }
}
// 调用1
void test1(){
    // 实例化对象son1
    parent * son1 = new Son;
    // 调用函数
    son1.func();
    // 释放内存
    delete son1;
}

// 调用2
void test2(){
    Son son2;
    Parent &son3 = son2;
}
```





## 4.3 继承

* 减少重复性代码

```cpp
class Base{
    // 公共代码
}
class python: public Base{
    void py(){
        // 个性化代码
    }
}
class cpp: public Base{
    void cpp(){
        // 个性化代码
    }
}
```



### 4.3.1 继承方式

![image-20230404100647142](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230404100647142.png)

* 注意：对于父类的私有变量，子类全部继承，只是隐藏起来不可访问

* 继承中，先调用父类构造函数，再调用子类构造函数，析构顺序与构造相反

* ```cpp
  // 构造方法用来初始化类的对象，与父类的其它成员不同，它不能被子类继承
  // 子类可以继承父类所有的成员变量和成员方法，但不继承父类的构造方法
  // 如果子类没有定义构造方法，则调用父类的无参数的构造方法。
  ```

* 

* 

### 4.3.2 父类成员变量、函数的调用

* 访问子类同名成员   直接访问即可
* 访问父类同名成员   需要加作用域

```cpp
class Base {
public:
	Base()
	{
		m_A = 100;
	}

	void func()
	{
		cout << "Base - func()调用" << endl;
	}

	void func(int a)
	{
		cout << "Base - func(int a)调用" << endl;
	}

public:
	int m_A;
};

// 继承
class Son : public Base {
public:
	Son()
	{
		m_A = 200;
	}

	//当子类与父类拥有同名的成员函数，子类会隐藏父类中所有版本的同名成员函数
	//如果想访问父类中被隐藏的同名成员函数，需要加父类的作用域
	void func()
	{
		cout << "Son - func()调用" << endl;
	}
public:
	int m_A;
};

// 测试
void test01()
{
	Son s;

	cout << "Son下的m_A = " << s.m_A << endl;
	cout << "Base下的m_A = " << s.Base::m_A << endl;
	
	s.func();
	s.Base::func();
	s.Base::func(10);

}
int main() {

	test01();

	system("pause");
	return EXIT_SUCCESS;
}
```

### 4.3.3 父类静态成员变量、函数的调用

* 父类中有静态变量A，子类继承后，又新增一个静态变量A

```cpp
class Base {
public:
	static void func();
	static void func(int a);
	static int m_A;
};

int Base::m_A = 100;

class Son : public Base {
public:
	static void func();
	static int m_A;
};

int Son::m_A = 200;

//同名成员属性
void test01()
{
	//通过对象访问
	cout << "通过对象访问： " << endl;
	Son s;
	cout << "Son  下 m_A = " << s.m_A << endl;
	cout << "Base 下 m_A = " << s.Base::m_A << endl;

	//通过类名访问
	cout << "通过类名访问： " << endl;
	cout << "Son  下 m_A = " << Son::m_A << endl;
	cout << "Base 下 m_A = " << Son::Base::m_A << endl;
}

//同名成员函数
void test02()
{
	//通过对象访问
	cout << "通过对象访问： " << endl;
	Son s;
	s.func();
	s.Base::func();

	cout << "通过类名访问： " << endl;
	Son::func();
	Son::Base::func();
	//出现同名，子类会隐藏掉父类中所有同名成员函数，需要加作作用域访问
	Son::Base::func(100);
}
int main() {

	//test01();
	test02();

	system("pause");

	return 0;
}
```

### 4.3.4 多继承语法

* 一个子类继承多个父类

```cpp
class Base1 {
public:
	Base1()
	{
		m_A = 100;
	}
public:
	int m_A;
};

class Base2 {
public:
	Base2()
	{
		m_A = 200;  //开始是m_B 不会出问题，但是改为mA就会出现不明确
	}
public:
	int m_A;
};

//语法：class 子类：继承方式 父类1 ，继承方式 父类2 
class Son : public Base2, public Base1 
{
public:
	Son()
	{
		m_C = 300;
		m_D = 400;
	}
public:
	int m_C;
	int m_D;
};


//多继承容易产生成员同名的情况
//通过使用类名作用域可以区分调用哪一个基类的成员
void test01()
{
	Son s;
	cout << "sizeof Son = " << sizeof(s) << endl;
	cout << s.Base1::m_A << endl;
	cout << s.Base2::m_A << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

### 4.3.5 菱形继承

![image-20230404111427114](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230404111427114.png)

1.     羊继承了动物的数据，驼同样继承了动物的数据，当草泥马使用数据时，就会产生二义性。
2.     草泥马继承自动物的数据继承了两份，其实我们应该清楚，这份数据我们只需要一份就可以。

```cpp
class Animal
{
public:
	int m_Age;
};

class Sheep : public Animal {};
class Tuo   : public Animal {};
class SheepTuo : public Sheep, public Tuo {};

void test01()
{
	SheepTuo st;
    // 添加作用域访问同名变量
	st.Sheep::m_Age = 100;
	st.Tuo::m_Age = 200;
}


int main() {

	test01();

	system("pause");

	return 0;
}
```

1.     菱形继承带来的主要问题是==子类继承两份相同的数据==，导致资源浪费以及毫无意义
2.     利用虚继承可以解决菱形继承问题

```cpp
class Animal
{
public:
	int m_Age;
};

//继承前加virtual关键字后，变为虚继承
//此时公共的父类Animal称为虚基类
class Sheep : virtual public Animal {};
class Tuo   : virtual public Animal {};
class SheepTuo : public Sheep, public Tuo {};

void test01()
{
	SheepTuo st;
	st.Sheep::m_Age = 100;
	st.Tuo::m_Age = 200;

	cout << "st.Sheep::m_Age = " << st.Sheep::m_Age << endl;
	cout << "st.Tuo::m_Age = " <<  st.Tuo::m_Age << endl;
	cout << "st.m_Age = " << st.m_Age << endl;
}


int main() {

	test01();

	system("pause");

	return 0;
}
```

虚继承：继承的是一个虚拟基类指针vbptr，通过偏移量访问虚拟基类表，表内存放虚拟基类的成员变量，只有一份，修改sheep.age 或 tuo.age 都会改变这个值，最终sheeptuo继承的是这个唯一的age。

![image-20230404111312059](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230404111312059.png)







## 4.4 对象的初始化和清理

### 4.4.1 构造函数和析构函数

* 编译器会默认构造空函数

```cpp
#include <iostream>
using namespace std;

class Person
{
public:
    // 1、构造函数名与类名相同
    // 2、可以有参数，可以函数重载
    Person()
    {
        cout << "初始化" << endl;
    }
    // 1、析构函数名与类名相同
    // 2、无参数，对象释放时自动执行
    ~Person()
    {
        cout << "释放对象" << endl;
    }
};

void test()
{
    // 函数执行后被释放，所以p自动执行析构
    Person p;
}

int main()
{
    test();   // 析构
    Person q; // 整个main函数结束后，才会析构
    system("pause");
    return 0;
}
```

### 4.4.2 构造函数的分类和调用

* 无参构造(默认构造函数)

```cpp
Person()
{
    cout << "初始化" << endl;
}
c++11中设置默认方式
Person() = default;
```



* 有参构造 (专属写法)

```cpp
Person(int a)
{
    age = a;
}

//
Person(int a) : a_(a);
```



* 拷贝构造

```cpp
// 按照b的属性进行a的初始化
// 保持b的属性不变
Person(const Person &b)
{
    age = b.age;
}
```

* 移动构造

接受同类型对象的右值引用作为参数的构造函数，用于高效地将临时对象或者资源所有权转移给新对象。

```cpp
// 设置默认
Person(Person &&) = default;
```



* 构造函数调用

```cpp
void test(){
    // 1、括号法
    Person p1; // 无参初始化，不可以写Person p1();
    Person p2(10); // 有参初始化
    Person p3(p2); // 拷贝初始化
    
    // 2、显示法
    Person p1; 
    Person p1(12);
    Person p2 = Person(10); // Person(10):匿名函数，执行完毕后立即释放空间
    Person p2 = Person(p2);
    
    
    // 3、隐式转换法
    Person p1; 
    Person p2 = 10;
    Person p3 = p2;
    
}
```

* 移动构造函数



### 4.4.3 explicit关键字

`explicit` 是 C++ 中的一个关键字，用于修饰类的构造函数。当一个构造函数声明为 `explicit` 时，它将被标记为显式构造函数，禁止隐式类型转换和复制初始化。

通常情况下，当构造函数只有一个参数时，编译器会自动执行隐式类型转换，将参数类型转换为类的对象类型。然而，如果构造函数被声明为 `explicit`，则不允许进行隐式类型转换，而要求在创建对象时明确调用该构造函数。

以下是使用 `explicit` 关键字的示例：

```cpp
class MyClass {
public:
    explicit MyClass(int value) : data(value) {}
    int GetData() const { return data; }

private:
    int data;
};

int main() {
    MyClass obj1(10);          // 正确，显式调用构造函数
    MyClass obj2 = 20;         // 错误，禁止隐式类型转换
    MyClass obj3 = MyClass(30); // 正确，显式调用构造函数

    int value = obj1.GetData(); // 正确，访问对象的成员函数

    return 0;
}

```



### 4.4.3 拷贝构造函数的调用时机

* 1、利用存在的对象创建新的对象

* 2 、值传递的方式给函数参数传参

  ```cpp
  class Person{
      Person(const Person &p);
  }
  void work(Person p){}
  
  void test(){
      Person p1;
      work(p1);  // 拷贝p1的属性给参数p，修改p不会改变p1的只
  }
  ```

* 3、值方式返回局部对象

  ```cpp
  Person show(){
      Person p1;
      return p1; // 返回p1的拷贝
  }
  void test(){
      Person p = show(); // 用p接收p1的拷贝
  }
  ```

  

### 4.4.4 深拷贝与浅拷贝

对于构造函数为用户自己开辟的空间的对象来讲：

成员属性存放在开辟的堆区，释放时候重复释放造成问题

```cpp
class Person 
{
public:
    int m_age;
    int* m_height; // 指针
public:
    //无参（默认）构造函数
    Person() {
    cout << "无参构造函数!" << endl;
    }
    
    //有参构造函数
    Person(int age ,int height) {
    cout << "有参构造函数!" << endl;
    m_age = age;
    m_height = new int(height); //申请空间，此时m_height为指针
    }
}
```



浅拷贝： 编译器默认的拷贝方式，简单的赋值拷贝操作

```cpp
// 系统默认的拷贝函数
Person(const Person& p) {
    cout << "拷贝构造函数!" << endl;
    m_age = p.m_age;
    m_height = p.m_height;// 两块指针指向同一块堆区
}
// 浅拷贝问题：堆区的重复释放
```

![image-20230401203117007](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230401203117007.png)

深拷贝，用户自定义拷贝函数，指向新的堆区，分开释放堆区

<a name = "深拷贝">跳转</a>

```cpp

Person(const Person& p) {
    cout << "拷贝构造函数!" << endl;
    m_age = p.m_age;
    m_height = new int(*p.m_height);// 深拷贝，m_heigt为指针
}
//自定义析构函数
~Person() {
    cout << "析构函数!" << endl;
    if (m_height != NULL)
    {
        delete m_height;
    }
}
// 总结：如果属性有在堆区开辟的，一定要自己提供拷贝构造函数，防止浅拷贝带来的问题
```

![image-20230401202532714](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230401202532714.png)

  

### 4.4.5 初始化列表

* 快速构造函数

```cpp
class Person{
private:
    int m_a;
    int m_b;
    int m_c;
public:
    Person(int a, int b, int c):m_a(a), m_b(b), m_c(c){};
};

int main(){
    Person p(1,2,3);
}
```

### 4.4.6 对象成员

* 类嵌套

```cpp
//当类中成员是其他类对象时，我们称该成员为 对象成员
//构造的顺序是 ：先调用对象成员的构造，再调用本类构造
//析构顺序与构造相反

class Person{
public:
    string m_name;
    Phone m_phone;
    // 对象嵌套，法1
    Person(String name, string pName){
        m_name = name;
        m_phone = pName; // 对象的是隐式转换调用构造函数=====m_phone(pName) 初始化手机名
    }
    //法2
    Person(string name, string pname):m_name(name), m_phone(pname){};
}
```

```cpp
// 法1
#include <iostream>
using namespace std;

class Phone
{
public:
    string m_name;
    int m_id;
    Phone(string name, int id) : m_name(name), m_id(id) {}
};

class Person
{
public:
    string m_name;
    Phone m_phone;
    // ----------初始化，传入一个Phone类型
    Person(string name, Phone myphone) : m_name(name), m_phone(myphone){};
};

int main()
{
    // -----------定义Phone
    Phone myPhone("huawei", 1);
    cout << "我的手机是: " << myPhone.m_name << " "
         << "序列号为: " << myPhone.m_id << endl;
    
    // ---------传入初始化Person
    Person myself("张宇乔", myPhone);
    cout << "我是" << myself.m_name << "我的手机是: " << myself.m_phone.m_name << " "
         << "序列号为: " << myself.m_phone.m_id << endl;

    system("pause");
    return 0;
}
```

```cpp
// 法2
#include <iostream>
using namespace std;

class Phone
{
public:
    string m_name;
    int m_id;
    Phone(string name, int id) : m_name(name), m_id(id) {}
};

class Person
{
public:
    string m_name;
    Phone m_phone;
    // -----------直接传入Phone所需要的初始化数据
    Person(string name, string pname, int id) : m_name(name), m_phone(pname, id){};
};

int main()
{
    Phone myPhone("huawei", 1);
    cout << "我的手机是: " << myPhone.m_name << " "
         << "序列号为: " << myPhone.m_id << endl;
    // ------------直接初始化Person + Phone
    Person myself("张宇乔", "iphone", 2);
    cout << "我是" << myself.m_name << "我的手机是: " << myself.m_phone.m_name << " "
         << "序列号为: " << myself.m_phone.m_id << endl;

    system("pause");
    return 0;
}
```

### 4.4.7 静态成员变量

* 所有对象共享一个类属性
* 类内声明，类外定义
* 有访问权限

```cpp
#include <iostream>
using namespace std;

class Person
{
public:
    string name;
    // 类内声明静态成员变量     // 不能直接赋值，需要类外定义
    static string home;

private:
    int age;
};

// 类外定义Person类内的静态成员变量；
string Person::home = "中国";

int main()
{
    // p1与p2共同访问home静态变量，p2修改则p1也修改
    Person p1;
    cout << p1.home << endl;

    Person p2;
    p2.home = "美国";
    cout << p1.home << endl;

    system("pause");
    return 0;
};

》》中国
》》美国
```

```cpp
// 访问方式1---类名访问
Person.home
    
// 方式2-----通过对象问访问
Person p1;
p1.home;
    
```



### 4.4.8 静态成员函数

* 所有对象共享一个方法
* 静态成员函数没有this指针，只能访问静态成员变量
* 有访问权限

```cpp
class Person
{
public:
    string name;
    static string home;
    // 静态成员函数
    static void func()
    {
        // 访问静态成员变量
        home = "泰国";
        // 报错，不能访问非静态，当多个对象调用静态函数时候，无法区分修改是哪个对象的name
        name = "zz"
    }
};

string Person::home = "中国";

int main()
{
    Person p1;
    cout << p1.home << endl;
    p1.func();
    cout << p1.home << endl;

    system("pause");
    return 0;
};
》》 中国
》》 泰国
```

```cpp
// 访问方式1 ---类名访问
Person.func();

// 方式2 ---对象访问
Person p1；
p1.func();
```







## 4.5 C++对象模型和this指针

### 4.5.1 成员变量和成员函数是分开存储的

```cpp
class Person{
           // 空类实例化后，p1占1个字节
    int a; // 非静态变量，占4个字节，属于类的对象上
    int b; // 所占内存累加 4+4 = 8
    string c; // 4 +4 +32 = 40;
    
    static int b;
    void func(){}
    static void func(){}  // 均不属于类的对象
}
```



### 4.5.2 this指针

![image-20230402135455639](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230402135455639.png)

![image-20230402135715246](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230402135715246.png)

```cpp
// 每个成员函数都有默认的this指针
// this指针本质是== 指针常量 == Person *const this
```



* 用途

```cpp
// 重点思考
class Person
{
public:
    Person(int age)
    {
    //1、当形参和成员变量同名时，可用this指针来区分
    this->age = age;
    }
    
    Person& PersonAddPerson(Person p)
    {
     // 原内存空间上的age发生变动
    this->age += p.age;
    //返回对象本身，存到原位置上
    return *this;
    }
int age;
};
void test01()
{
Person p1(10);
cout << "p1.age = " << p1.age << endl;
Person p2(10);
// 链式编程
p2.PersonAddPerson(p1).PersonAddPerson(p1).PersonAddPerson(p1);
cout << "p2.age = " << p2.age << endl;
}
int main() {
test01();
system("pause");![image-20230402201717807](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230402201717807.png)
return 0;
}
```

![image-20230402201731425](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230402201731425.png)



### 4.5.3 const常函数

```cpp
// 成员函数后加const后我们称为这个函数为常函数 void ShowPerson() const {}
// 常函数内不可以修改成员属性,可以访问
// 成员属性声明时加关键字mutable后，在常函数中依然可以修改
```

```cpp
class Person {
public:
    Person() {
    m_A = 0;
    mutable m_B = 0;
    }
    //this指针的本质是一个指针常量，指针的指向不可修改 == Person *const this

    //如果想让指针指向的值也不可以修改，需要声明常函数 == const Person *const this
    void ShowPerson() const {
       
    this->mA = 100; // ❌ 不可修改
    this->m_B = 100; // 可以修改
    }
}  
```

### 4.5.4 const常对象

```cpp
// 实例化对象前加const为常对象 const Person p1;
// 常对象不可以修改其属性
// 成员属性声明时加关键字mutable后，在常对象中依然可以修改
// 常对象只能调用常函数
```

```cpp
void test01() {
    const Person p; //常量对象
    p.m_A =1 // ❌ 不可修改
    cout << person.m_A << endl; //可以访问
    
    person.m_B = 100; //但是常对象可以修改mutable修饰成员变量

    person.MyFunc(); //常对象只能调用常函数
}
```

## 4.6 友元

在程序里，有些私有属性 也想让类外特殊的一些函数或者类进行访问，就需要用到友元的技术



友元的目的就是让一个函数或者类 访问另一个类中私有成员



友元的关键字为  ==friend==



友元的三种实现

* 全局函数做友元
* 类做友元
* 成员函数做友元

### 4.6.1 全局函数作友元

```cpp
#include <iostream>
using namespace std;

class Home
{
    // 添加友元：friend+全局函数声明
    friend void boy(Home home);

public:
    string sittingRoom;

private:
    string bedRoom;
};

// 1、全局函数作友元
void boy(Home home)
{

    cout << "boy参观客厅:" << home.sittingRoom << endl;
    // 添加友元后可访问
    cout << "boy参观卧室:" << home.bedRoom << endl;
}

int main()
{
    Home home;
    boy(home);

    system("pause");
    return 0;
}
```

### 4.6.2 类作友元

* 一类的实例化对象都可访问其私有变量

```cpp
#include <iostream>
using namespace std;

class Home
{
    // 添加友元：friend+全局函数声明
    friend void boy(Home home);
    // 添加友元：friend+类声明
    friend class Friends;

public:
    string sittingRoom = "我的客厅";

private:
    string bedRoom = "我的卧室";
};

// 1、全局函数作友元
void boy(Home home)
{

    cout << "boy参观客厅:" << home.sittingRoom << endl;
    // 添加友元后可访问
    cout << "boy参观卧室:" << home.bedRoom << endl;
}

// 2、类作友元
class Friends
{

public:
    Home home;
    Friends(Home home)
    {
        this->home = home;
    }
    void test()
    {
        cout << "类中的一个朋友参观客厅:" << home.sittingRoom << endl;
        // 添加友元后可访问
        cout << "类中的一个朋友参观卧室:" << home.bedRoom << endl;
    }
};

int main()
{
    Home home;
    // 1、全局函数友元
    boy(home);
    // 2、类友元
    Friends girl(home);
    girl.test();

    system("pause");
    return 0;
}
```

### 4.6.3 相同class的各个object互为友元

![image-20230422123740987](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230422123740987.png)

* 相同class下的对象a,b,c
* a可以访问c的私有变量

### 4.6.4 类中成员函数友元

```cpp
class Building;
class goodGay
{
public:

	goodGay();
	void visit(); //只让visit函数作为Building的好朋友，可以发访问Building中私有内容
	void visit2(); 

private:
	Building *building;
};


class Building
{
	//告诉编译器  goodGay类中的visit成员函数 是Building好朋友，可以访问私有内容
	friend void goodGay::visit();

public:
	Building();

public:
	string m_SittingRoom; //客厅
private:
	string m_BedRoom;//卧室
};

Building::Building()
{
	this->m_SittingRoom = "客厅";
	this->m_BedRoom = "卧室";
}

goodGay::goodGay()
{
	building = new Building;
}

void goodGay::visit()
{
	cout << "好基友正在访问" << building->m_SittingRoom << endl;
	cout << "好基友正在访问" << building->m_BedRoom << endl;
}

void goodGay::visit2()
{
	cout << "好基友正在访问" << building->m_SittingRoom << endl;
	//cout << "好基友正在访问" << building->m_BedRoom << endl;
}

void test01()
{
	goodGay  gg;
	gg.visit();

}

int main(){
    
	test01();

	system("pause");
	return 0;
}
```



## 4.7 运算符重载

* 自定义运算符的运算方式

### 4.7.1 加号重载

```cpp
class Person {
public:
	Person() {};
	Person(int a, int b)
	{
		this->m_A = a;
		this->m_B = b;
	}
	//成员函数实现 + 号运算符重载 Person p3 = p1.operator+(p2)
	Person operator+(const Person& p) {
		Person temp;
		temp.m_A = this->m_A + p.m_A;
		temp.m_B = this->m_B + p.m_B;
		return temp;
	}


public:
	int m_A;
	int m_B;
};

//全局函数实现 + 号运算符重载 Person p3 = operator(p1,p2)
Person operator+(const Person& p1, const Person& p2) {
	Person temp(0, 0);
	temp.m_A = p1.m_A + p2.m_A;
	temp.m_B = p1.m_B + p2.m_B;
	return temp;
	}

//运算符重载 可以发生函数重载 (person + int)
Person operator+(const Person& p2, int val)  
{
	Person temp;
	temp.m_A = p2.m_A + val;
	temp.m_B = p2.m_B + val;
	return temp;
}

void test() {

	Person p1(10, 10);
	Person p2(20, 20);

	//成员函数方式
	Person p3 = p2 + p1;  //相当于 p2.operaor+(p1)
	cout << "mA:" << p3.m_A << " mB:" << p3.m_B << endl;


	Person p4 = p3 + 10; //相当于 operator+(p3,10)
	cout << "mA:" << p4.m_A << " mB:" << p4.m_B << endl;

}

int main() {

	test();

	system("pause");

	return 0;
}
```

### 4.7.2 左移运算符重载

* 输出自定义格式

```cpp
class Person {
    // 友元访问私有变量
	friend ostream& operator<<(ostream& out, Person& p);

public:

	Person(int a, int b)
	{
		this->m_A = a;
		this->m_B = b;
	}

	//成员函数 实现不了  p << cout 不是我们想要的效果
	//void operator<<(Person& p){
	//}

private:
	int m_A;
	int m_B;
};

//全局函数实现左移重载
//ostream对象只能有一个
// 返回ostream类型

ostream& operator<<(ostream& cout, Person& p) { //简写：cout<<p
	cout << "a:" << p.m_A << " b:" << p.m_B;
	return out;
}

void test() {

	Person p1(10, 20);

    //链式编程，保证cout << p1 的返回为ostream类型
	cout << p1 << "hello world" << endl; 
}

int main() {

	test();

	system("pause");

	return 0;
}
```

### 4.7.3 递增运算符重载

* 实现自增

```cpp
class MyInteger {
	// 友元
	friend ostream& operator<<(ostream& out, MyInteger myint);

public:
	MyInteger() {
		m_Num = 0;
	}
	//前置++，返回引用，无占位符
	MyInteger& operator++() {
		//先++
		m_Num++;
		//再返回
		return *this;
	}

	//后置++，返回值，有int占位符区分
    // 不返回引用是因为i++后，返回的还是i，无法进行(i++)++操作
	MyInteger operator++(int) {
		//先返回
		MyInteger temp = *this; //记录当前本身的值，然后让本身的值加1，但是返回的是以前的值，达到先返回后++；
		m_Num++;
		return temp;
	}

private:
	int m_Num;
};


ostream& operator<<(ostream& out, MyInteger myint) {
	out << myint.m_Num;
	return out;
}


//前置++ 先++ 再返回
void test01() {
	MyInteger myInt;
	cout << ++myInt << endl;
	cout << myInt << endl;
}

//后置++ 先返回 再++
void test02() {

	MyInteger myInt;
	cout << myInt++ << endl;
	cout << myInt << endl;
}

int main() {

	test01(); 1 1
	test02(); 0 1

	system("pause");

	return 0;
}
```

### 4.7.4 赋值运算符重载

+ 在类里面，需要Person p1 = p2， 解决浅拷贝问题，用深拷贝解决

```cpp
class Person
{
public:

	Person(int age)
	{
		//将年龄数据开辟到堆区
		m_Age = new int(age);
	}

	//重载赋值运算符 
	Person& operator=(Person &p)
	{
		if (m_Age != NULL)
		{
			delete m_Age;
			m_Age = NULL;
		}
		//编译器提供的代码是浅拷贝
		//m_Age = p.m_Age;

		//提供深拷贝 解决浅拷贝的问题，重载就是改掉这个代码
		m_Age = new int(*p.m_Age);

		//返回自身
		return *this;
	}


	~Person()
	{
		if (m_Age != NULL)
		{
			delete m_Age;
			m_Age = NULL;
		}
	}

	//年龄的指针
	int *m_Age;

};


void test01()
{
	Person p1(18);

	Person p2(20);

	Person p3(30);

	p3 = p2 = p1; //链式赋值操作

	cout << "p1的年龄为：" << *p1.m_Age << endl;

	cout << "p2的年龄为：" << *p2.m_Age << endl;

	cout << "p3的年龄为：" << *p3.m_Age << endl;
}

int main() {

	test01();

	//int a = 10;
	//int b = 20;
	//int c = 30;

	//c = b = a;
	//cout << "a = " << a << endl;
	//cout << "b = " << b << endl;
	//cout << "c = " << c << endl;

	system("pause");

	return 0;
}
```

### 4.7.5 关系运算符重载

```cpp
class Person
{
public:
	Person(string name, int age)
	{
		this->m_Name = name;
		this->m_Age = age;
	};

	bool operator==(Person & p)
	{
		if (this->m_Name == p.m_Name && this->m_Age == p.m_Age)
		{
			return true;
		}
		else
		{
			return false;
		}
	}

	bool operator!=(Person & p)
	{
		if (this->m_Name == p.m_Name && this->m_Age == p.m_Age)
		{
			return false;
		}
		else
		{
			return true;
		}
	}

	string m_Name;
	int m_Age;
};

void test01()
{
	//int a = 0;
	//int b = 0;

	Person a("孙悟空", 18);
	Person b("孙悟空", 18);

	if (a == b)
	{
		cout << "a和b相等" << endl;
	}
	else
	{
		cout << "a和b不相等" << endl;
	}

	if (a != b)
	{
		cout << "a和b不相等" << endl;
	}
	else
	{
		cout << "a和b相等" << endl;
	}
}


int main() {

	test01();

	system("pause");

	return 0;
}
```

### 4.7.6 函数调用运算符重载

```cpp
class MyPrint
{
public:
	void operator()(string text)
	{
		cout << text << endl;
	}

};
void test01()
{
	//重载的（）操作符 也称为仿函数
	MyPrint myFunc;
	myFunc("hello world");
}


class MyAdd
{
public:
	int operator()(int v1, int v2)
	{
		return v1 + v2;
	}
};

void test02()
{
	MyAdd add;
	int ret = add(10, 10);
	cout << "ret = " << ret << endl;

	//匿名对象调用  
	cout << "MyAdd()(100,100) = " << MyAdd()(100, 100) << endl;
}

int main() {

	test01();
	test02();

	system("pause");

	return 0;
}
```















#### 1.2.5 普通函数与函数模板的调用规则



调用规则如下：

1. 如果函数模板和普通函数都可以实现，优先调用普通函数
2. 可以通过空模板参数列表来强制调用函数模板
3. 函数模板也可以发生重载
4. 如果函数模板可以产生更好的匹配,优先调用函数模板





**示例：**

```C++
//普通函数与函数模板调用规则
void myPrint(int a, int b)
{
	cout << "调用的普通函数" << endl;
}

template<typename T>
void myPrint(T a, T b) 
{ 
	cout << "调用的模板" << endl;
}

template<typename T>
void myPrint(T a, T b, T c) 
{ 
	cout << "调用重载的模板" << endl; 
}

void test01()
{
	//1、如果函数模板和普通函数都可以实现，优先调用普通函数
	// 注意 如果告诉编译器  普通函数是有的，但只是声明没有实现，或者不在当前文件内实现，就会报错找不到
	int a = 10;
	int b = 20;
	myPrint(a, b); //调用普通函数

	//2、可以通过空模板参数列表来强制调用函数模板
	myPrint<>(a, b); //调用函数模板

	//3、函数模板也可以发生重载
	int c = 30;
	myPrint(a, b, c); //调用重载的函数模板

	//4、 如果函数模板可以产生更好的匹配,优先调用函数模板
	char c1 = 'a';
	char c2 = 'b';
	myPrint(c1, c2); //调用函数模板
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

总结：既然提供了函数模板，最好就不要提供普通函数，否则容易出现二义性











#### 1.2.6 模板的局限性

**局限性：**

* 模板的通用性并不是万能的



**例如：**

```C++
	template<class T>
	void f(T a, T b)
	{ 
    	a = b;
    }
```

在上述代码中提供的赋值操作，如果传入的a和b是一个数组，就无法实现了



再例如：

```C++
	template<class T>
	void f(T a, T b)
	{ 
    	if(a > b) { ... }
    }
```

在上述代码中，如果T的数据类型传入的是像Person这样的自定义数据类型，也无法正常运行



因此C++为了解决这种问题，提供模板的重载，可以为这些**特定的类型**提供**具体化的模板**



**示例：**

```C++
#include<iostream>
using namespace std;

#include <string>

class Person
{
public:
	Person(string name, int age)
	{
		this->m_Name = name;
		this->m_Age = age;
	}
	string m_Name;
	int m_Age;
};

//普通函数模板
template<class T>
bool myCompare(T& a, T& b)
{
	if (a == b)
	{
		return true;
	}
	else
	{
		return false;
	}
}


//具体化，显示具体化的原型和定意思以template<>开头，并通过名称来指出类型
//具体化优先于常规模板
template<> bool myCompare(Person &p1, Person &p2)
{
	if ( p1.m_Name  == p2.m_Name && p1.m_Age == p2.m_Age)
	{
		return true;
	}
	else
	{
		return false;
	}
}

void test01()
{
	int a = 10;
	int b = 20;
	//内置数据类型可以直接使用通用的函数模板
	bool ret = myCompare(a, b);
	if (ret)
	{
		cout << "a == b " << endl;
	}
	else
	{
		cout << "a != b " << endl;
	}
}

void test02()
{
	Person p1("Tom", 10);
	Person p2("Tom", 10);
	//自定义数据类型，不会调用普通的函数模板
	//可以创建具体化的Person数据类型的模板，用于特殊处理这个类型
	bool ret = myCompare(p1, p2);
	if (ret)
	{
		cout << "p1 == p2 " << endl;
	}
	else
	{
		cout << "p1 != p2 " << endl;
	}
}

int main() {

	test01();

	test02();

	system("pause");

	return 0;
}
```

总结：

* 利用具体化的模板，可以解决自定义类型的通用化
* 学习模板并不是为了写模板，而是在STL能够运用系统提供的模板







# 五 模板

### 1.2 类模板

#### 1.3.1 类模板语法

类模板作用：

* 建立一个通用类，类中的成员 数据类型可以不具体制定，用一个**虚拟的类型**来代表。

==类模板是用来创建一个类==，无法自动推导其类型

**语法：** 

```c++
template<typename T>
类
```

**解释：**

template  ---  声明创建模板

typename  --- 表面其后面的符号是一种数据类型，可以用class代替

T    ---   通用的数据类型，名称可以替换，通常为大写字母



**示例：**

```C++
#include <string>
//类模板
template<class NameType, class AgeType> 
class Person
{
public:
	Person(NameType name, AgeType age)
	{
		this->mName = name;
		this->mAge = age;
	}
	void showPerson()
	{
		cout << "name: " << this->mName << " age: " << this->mAge << endl;
	}
public:
	NameType mName;
	AgeType mAge;
};

void test01()
{
	// 指定NameType 为string类型，AgeType 为 int类型
	Person<string, int>P1("孙悟空", 999);
	P1.showPerson();
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

总结：类模板和函数模板语法相似，在声明模板template后面加类，此类称为类模板











#### 1.3.2 类模板与函数模板区别



类模板与函数模板区别主要有两点：

1. ==类模板==没有自动类型推导的使用方式
2. 类模板在模板参数列表中可以有默认参数




**示例：**

```C++
#include <string>
//类模板
template<class NameType, class AgeType = int> 
class Person
{
public:
	Person(NameType name, AgeType age)
	{
		this->mName = name;
		this->mAge = age;
	}
	void showPerson()
	{
		cout << "name: " << this->mName << " age: " << this->mAge << endl;
	}
public:
	NameType mName;
	AgeType mAge;
};

//1、类模板没有自动类型推导的使用方式
void test01()
{
	// Person p("孙悟空", 1000); // 错误 类模板使用时候，不可以用自动类型推导
	Person <string ,int>p("孙悟空", 1000); //必须使用显示指定类型的方式，使用类模板
	p.showPerson();
}

//2、类模板在模板参数列表中可以有默认参数
void test02()
{
	Person <string> p("猪八戒", 999); //类模板中的模板参数列表 可以指定默认参数
	p.showPerson();
}

int main() {

	test01();

	test02();

	system("pause");

	return 0;
}
```

总结：

* 类模板使用只能用显示指定类型方式
* 类模板中的模板参数列表可以有默认参数











#### 1.3.3 类模板中成员函数创建时机



类模板中成员函数和普通类中成员函数创建时机是有区别的：

* 普通类中的成员函数一开始就可以创建
* 类模板中的成员函数在调用时才创建





**示例：**

```C++
class Person1
{
public:
	void showPerson1()
	{
		cout << "Person1 show" << endl;
	}
};

class Person2
{
public:
	void showPerson2()
	{
		cout << "Person2 show" << endl;
	}
};

template<class T>
class MyClass
{
public:
	T obj;

	//类模板中的成员函数，并不是一开始就创建的，而是在模板调用时再生成

	void fun1() { obj.showPerson1(); }
	void fun2() { obj.showPerson2(); }

};

void test01()
{
	MyClass<Person1> m;
	
	m.fun1();

	//m.fun2();//编译会出错，说明函数调用才会去创建成员函数
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

总结：类模板中的成员函数并不是一开始就创建的，在调用时才去创建









#### 1.3.4 类模板对象做函数参数

学习目标：

* 类模板实例化出的对象，向函数传参的方式



一共有三种传入方式：

1. 指定传入的类型   --- 直接显示对象的数据类型
2. 参数模板化           --- 将对象中的参数变为模板进行传递
3. 整个类模板化       --- 将这个对象类型 模板化进行传递





**示例：**

```C++
#include <string>
//类模板
template<class NameType, class AgeType = int> 
class Person
{
public:
	Person(NameType name, AgeType age)
	{
		this->mName = name;
		this->mAge = age;
	}
	void showPerson()
	{
		cout << "name: " << this->mName << " age: " << this->mAge << endl;
	}
public:
	NameType mName;
	AgeType mAge;
};

//1、指定传入的类型
void printPerson1(Person<string, int> &p) 
{
	p.showPerson();
}
void test01()
{
	Person <string, int >p("孙悟空", 100);
	printPerson1(p);
}

//2、参数模板化
template <class T1, class T2>
void printPerson2(Person<T1, T2>&p)
{
	p.showPerson();
	cout << "T1的类型为： " << typeid(T1).name() << endl;
	cout << "T2的类型为： " << typeid(T2).name() << endl;
}
void test02()
{
	Person <string, int >p("猪八戒", 90);
	printPerson2(p);
}

//3、整个类模板化
template<class T>
void printPerson3(T & p)
{
	cout << "T的类型为： " << typeid(T).name() << endl;
	p.showPerson();

}
void test03()
{
	Person <string, int >p("唐僧", 30);
	printPerson3(p);
}

int main() {

	test01();
	test02();
	test03();

	system("pause");

	return 0;
}
```

总结：

* 通过类模板创建的对象，可以有三种方式向函数中进行传参
* 使用比较广泛是第一种：指定传入的类型









#### 1.3.5 类模板与继承



当类模板碰到继承时，需要注意一下几点：

* 当子类继承的父类是一个类模板时，子类在声明的时候，要指定出父类中T的类型
* 如果不指定，编译器无法给子类分配内存
* 如果想灵活指定出父类中T的类型，子类也需变为类模板




**示例：**

```C++
template<class T>
class Base
{
	T m;
};

//class Son:public Base  //错误，c++编译需要给子类分配内存，必须知道父类中T的类型才可以向下继承
class Son :public Base<int> //必须指定一个类型
{
};
void test01()
{
	Son c;
}

//类模板继承类模板 ,可以用T2指定父类中的T类型
template<class T1, class T2>
class Son2 :public Base<T2>
{
public:
	Son2()
	{
		cout << typeid(T1).name() << endl;
		cout << typeid(T2).name() << endl;
	}
};

void test02()
{
	Son2<int, char> child1;
}


int main() {

	test01();

	test02();

	system("pause");

	return 0;
}
```

总结：如果父类是类模板，子类需要指定出父类中T的数据类型









#### 1.3.6 类模板成员函数类外实现



学习目标：能够掌握类模板中的成员函数类外实现



**示例：**

```C++
#include <string>

//类模板中成员函数类外实现
template<class T1, class T2>
class Person {
public:
	//成员函数类内声明
	Person(T1 name, T2 age);
	void showPerson();

public:
	T1 m_Name;
	T2 m_Age;
};

//构造函数 类外实现
template<class T1, class T2>
Person<T1, T2>::Person(T1 name, T2 age) {
	this->m_Name = name;
	this->m_Age = age;
}

//成员函数 类外实现
template<class T1, class T2>
void Person<T1, T2>::showPerson() {
	cout << "姓名: " << this->m_Name << " 年龄:" << this->m_Age << endl;
}

void test01()
{
	Person<string, int> p("Tom", 20);
	p.showPerson();
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

总结：类模板中成员函数类外实现时，需要加上模板参数列表









#### 1.3.7 类模板分文件编写

学习目标：

* 掌握类模板成员函数分文件编写产生的问题以及解决方式



问题：

* 类模板中成员函数创建时机是在调用阶段，导致分文件编写时链接不到


解决：

* 解决方式1：直接包含.cpp源文件
* 解决方式2：将声明和实现写到同一个文件中，并更改后缀名为.hpp，hpp是约定的名称，并不是强制




**示例：**

person.hpp中代码：

```C++
#pragma once
#include <iostream>
using namespace std;
#include <string>

template<class T1, class T2>
class Person {
public:
	Person(T1 name, T2 age);
	void showPerson();
public:
	T1 m_Name;
	T2 m_Age;
};

//构造函数 类外实现
template<class T1, class T2>
Person<T1, T2>::Person(T1 name, T2 age) {
	this->m_Name = name;
	this->m_Age = age;
}

//成员函数 类外实现
template<class T1, class T2>
void Person<T1, T2>::showPerson() {
	cout << "姓名: " << this->m_Name << " 年龄:" << this->m_Age << endl;
}
```



类模板分文件编写.cpp中代码

```C++
#include<iostream>
using namespace std;

//#include "person.h"
#include "person.cpp" //解决方式1，包含cpp源文件

//解决方式2，将声明和实现写到一起，文件后缀名改为.hpp
#include "person.hpp"
void test01()
{
	Person<string, int> p("Tom", 10);
	p.showPerson();
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

总结：主流的解决方式是第二种，将类模板成员函数写到一起，并将后缀名改为.hpp









#### 1.3.8 类模板与友元



学习目标：

* 掌握类模板配合友元函数的类内和类外实现



全局函数类内实现 - 直接在类内声明友元即可

全局函数类外实现 - 需要提前让编译器知道全局函数的存在



**示例：**

```C++
#include <string>

//2、全局函数配合友元  类外实现 - 先做函数模板声明，下方在做函数模板定义，在做友元
template<class T1, class T2> class Person;

//如果声明了函数模板，可以将实现写到后面，否则需要将实现体写到类的前面让编译器提前看到
//template<class T1, class T2> void printPerson2(Person<T1, T2> & p); 

template<class T1, class T2>
void printPerson2(Person<T1, T2> & p)
{
	cout << "类外实现 ---- 姓名： " << p.m_Name << " 年龄：" << p.m_Age << endl;
}

template<class T1, class T2>
class Person
{
	//1、全局函数配合友元   类内实现
	friend void printPerson(Person<T1, T2> & p)
	{
		cout << "姓名： " << p.m_Name << " 年龄：" << p.m_Age << endl;
	}


	//全局函数配合友元  类外实现
	friend void printPerson2<>(Person<T1, T2> & p);

public:

	Person(T1 name, T2 age)
	{
		this->m_Name = name;
		this->m_Age = age;
	}


private:
	T1 m_Name;
	T2 m_Age;

};

//1、全局函数在类内实现
void test01()
{
	Person <string, int >p("Tom", 20);
	printPerson(p);
}


//2、全局函数在类外实现
void test02()
{
	Person <string, int >p("Jerry", 30);
	printPerson2(p);
}

int main() {

	//test01();

	test02();

	system("pause");

	return 0;
}
```

总结：建议全局函数做类内实现，用法简单，而且编译器可以直接识别











#### 1.3.9 类模板案例

案例描述:  实现一个通用的数组类，要求如下：



* 可以对内置数据类型以及自定义数据类型的数据进行存储
* 将数组中的数据存储到堆区
* 构造函数中可以传入数组的容量
* 提供对应的拷贝构造函数以及operator=防止浅拷贝问题
* 提供尾插法和尾删法对数组中的数据进行增加和删除
* 可以通过下标的方式访问数组中的元素
* 可以获取数组中当前元素个数和数组的容量

**示例：**

myArray.hpp中代码

```C++
#pragma once
#include <iostream>
using namespace std;

template<class T>
class MyArray
{
public:
    
	//构造函数
	MyArray(int capacity)
	{
		this->m_Capacity = capacity;
		this->m_Size = 0;
		pAddress = new T[this->m_Capacity];
	}

	//拷贝构造
	MyArray(const MyArray & arr)
	{
		this->m_Capacity = arr.m_Capacity;
		this->m_Size = arr.m_Size;
		this->pAddress = new T[this->m_Capacity];
		for (int i = 0; i < this->m_Size; i++)
		{
			//如果T为对象，而且还包含指针，必须需要重载 = 操作符，因为这个等号不是 构造 而是赋值，
			// 普通类型可以直接= 但是指针类型需要深拷贝
			this->pAddress[i] = arr.pAddress[i];
		}
	}

	//重载= 操作符  防止浅拷贝问题
	MyArray& operator=(const MyArray& myarray) {

		if (this->pAddress != NULL) {
			delete[] this->pAddress;
			this->m_Capacity = 0;
			this->m_Size = 0;
		}

		this->m_Capacity = myarray.m_Capacity;
		this->m_Size = myarray.m_Size;
		this->pAddress = new T[this->m_Capacity];
		for (int i = 0; i < this->m_Size; i++) {
			this->pAddress[i] = myarray[i];
		}
		return *this;
	}

	//重载[] 操作符  arr[0]
	T& operator [](int index)
	{
		return this->pAddress[index]; //不考虑越界，用户自己去处理
	}

	//尾插法
	void Push_back(const T & val)
	{
		if (this->m_Capacity == this->m_Size)
		{
			return;
		}
		this->pAddress[this->m_Size] = val;
		this->m_Size++;
	}

	//尾删法
	void Pop_back()
	{
		if (this->m_Size == 0)
		{
			return;
		}
		this->m_Size--;
	}

	//获取数组容量
	int getCapacity()
	{
		return this->m_Capacity;
	}

	//获取数组大小
	int	getSize()
	{
		return this->m_Size;
	}


	//析构
	~MyArray()
	{
		if (this->pAddress != NULL)
		{
			delete[] this->pAddress;
			this->pAddress = NULL;
			this->m_Capacity = 0;
			this->m_Size = 0;
		}
	}

private:
	T * pAddress;  //指向一个堆空间，这个空间存储真正的数据
	int m_Capacity; //容量
	int m_Size;   // 大小
};
```



类模板案例—数组类封装.cpp中

```C++
#include "myArray.hpp"
#include <string>

void printIntArray(MyArray<int>& arr) {
	for (int i = 0; i < arr.getSize(); i++) {
		cout << arr[i] << " ";
	}
	cout << endl;
}

//测试内置数据类型
void test01()
{
	MyArray<int> array1(10);
	for (int i = 0; i < 10; i++)
	{
		array1.Push_back(i);
	}
	cout << "array1打印输出：" << endl;
	printIntArray(array1);
	cout << "array1的大小：" << array1.getSize() << endl;
	cout << "array1的容量：" << array1.getCapacity() << endl;

	cout << "--------------------------" << endl;

	MyArray<int> array2(array1);
	array2.Pop_back();
	cout << "array2打印输出：" << endl;
	printIntArray(array2);
	cout << "array2的大小：" << array2.getSize() << endl;
	cout << "array2的容量：" << array2.getCapacity() << endl;
}

//测试自定义数据类型
class Person {
public:
	Person() {} 
		Person(string name, int age) {
		this->m_Name = name;
		this->m_Age = age;
	}
public:
	string m_Name;
	int m_Age;
};

void printPersonArray(MyArray<Person>& personArr)
{
	for (int i = 0; i < personArr.getSize(); i++) {
		cout << "姓名：" << personArr[i].m_Name << " 年龄： " << personArr[i].m_Age << endl;
	}

}

void test02()
{
	//创建数组
	MyArray<Person> pArray(10);
	Person p1("孙悟空", 30);
	Person p2("韩信", 20);
	Person p3("妲己", 18);
	Person p4("王昭君", 15);
	Person p5("赵云", 24);

	//插入数据
	pArray.Push_back(p1);
	pArray.Push_back(p2);
	pArray.Push_back(p3);
	pArray.Push_back(p4);
	pArray.Push_back(p5);

	printPersonArray(pArray);

	cout << "pArray的大小：" << pArray.getSize() << endl;
	cout << "pArray的容量：" << pArray.getCapacity() << endl;

}

int main() {

	//test01();

	test02();

	system("pause");

	return 0;
}
```

总结：

能够利用所学知识点实现通用的数组

### 1.3全特化

```cpp
template<typename T>
void mySwap(T& a, T& b)
{
	T temp = a;
	a = b;
	b = temp;
}

// 特化
template<>
void mySuap<int>(int& a, int& b)
{
	int temp = a;
	a = b;
	b = temp;
}
```

### 1.4 偏特化

```cpp
// 个数偏特化
template<class T, class Alloc = alloc>
class vector{}

template <class Alloc>
class vector<bool,Alloc>{}   // 接收两个参数，当第一个参数类型确定为bool

// 范围偏特化
template<class A>
struct iteractor{}

temlate<class T>
struct iteractor<T*>{}   // 当A为指针时候，执行特化，但是具体的指针类型T泛化
```































#### 5.1.1 for_each

**功能描述：**

* 实现遍历容器

**函数原型：**

* `for_each(iterator beg, iterator end, _func);  `

  // 遍历算法 遍历容器元素

  // beg 开始迭代器

  // end 结束迭代器

  // _func 函数或者函数对象



**示例：**

```C++
#include <algorithm>
#include <vector>

//普通函数
void print01(int val) 
{
	cout << val << " ";
}
//函数对象
class print02 
{
 public:
	void operator()(int val) 
	{
		cout << val << " ";
	}
};

//for_each算法基本用法
void test01() {

	vector<int> v;
	for (int i = 0; i < 10; i++) 
	{
		v.push_back(i);
	}

	//遍历算法
	for_each(v.begin(), v.end(), print01);
	cout << endl;

	for_each(v.begin(), v.end(), print02());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**for_each在实际开发中是最常用遍历算法，需要熟练掌握









#### 5.1.2 transform

**功能描述：**

* 搬运容器到另一个容器中

**函数原型：**

* `transform(iterator beg1, iterator end1, iterator beg2, _func);`

//beg1 源容器开始迭代器

//end1 源容器结束迭代器

//beg2 目标容器开始迭代器

//_func 函数或者函数对象



**示例：**

```C++
#include<vector>
#include<algorithm>

//常用遍历算法  搬运 transform

class TransForm
{
public:
	int operator()(int val)
	{
		return val;
	}

};

class MyPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

void test01()
{
	vector<int>v;
	for (int i = 0; i < 10; i++)
	{
		v.push_back(i);
	}

	vector<int>vTarget; //目标容器

	vTarget.resize(v.size()); // 目标容器需要提前开辟空间

	transform(v.begin(), v.end(), vTarget.begin(), TransForm());

	for_each(vTarget.begin(), vTarget.end(), MyPrint());
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：** 搬运的目标容器必须要提前开辟空间，否则无法正常搬运





# 六 STL算法

### 5.2 常用查找算法

学习目标：

- 掌握常用的查找算法





**算法简介：**

- `find`                     //查找元素
- `find_if`               //按条件查找元素
- `adjacent_find`    //查找相邻重复元素
- `binary_search`    //二分查找法
- `count`                   //统计元素个数
- `count_if`             //按条件统计元素个数




#### 5.2.1 find

**功能描述：**

* 查找指定元素，找到返回指定元素的迭代器，找不到返回结束迭代器end()



**函数原型：**

- `find(iterator beg, iterator end, value);  `

  // 按值查找元素，找到返回指定位置迭代器，找不到返回结束迭代器位置

  // beg 开始迭代器

  // end 结束迭代器

  // value 查找的元素





**示例：**

```C++
#include <algorithm>
#include <vector>
#include <string>
void test01() {

	vector<int> v;
	for (int i = 0; i < 10; i++) {
		v.push_back(i + 1);
	}
	//查找容器中是否有 5 这个元素
	vector<int>::iterator it = find(v.begin(), v.end(), 5);
	if (it == v.end()) 
	{
		cout << "没有找到!" << endl;
	}
	else 
	{
		cout << "找到:" << *it << endl;
	}
}

class Person {
public:
	Person(string name, int age) 
	{
		this->m_Name = name;
		this->m_Age = age;
	}
	//重载==
	bool operator==(const Person& p) 
	{
		if (this->m_Name == p.m_Name && this->m_Age == p.m_Age) 
		{
			return true;
		}
		return false;
	}

public:
	string m_Name;
	int m_Age;
};

void test02() {

	vector<Person> v;

	//创建数据
	Person p1("aaa", 10);
	Person p2("bbb", 20);
	Person p3("ccc", 30);
	Person p4("ddd", 40);

	v.push_back(p1);
	v.push_back(p2);
	v.push_back(p3);
	v.push_back(p4);

	vector<Person>::iterator it = find(v.begin(), v.end(), p2);
	if (it == v.end()) 
	{
		cout << "没有找到!" << endl;
	}
	else 
	{
		cout << "找到姓名:" << it->m_Name << " 年龄: " << it->m_Age << endl;
	}
}
```

总结： 利用find可以在容器中找指定的元素，返回值是**迭代器**













#### 5.2.2 find_if

**功能描述：**

* 按条件查找元素

**函数原型：**

- `find_if(iterator beg, iterator end, _Pred);  `

  // 按值查找元素，找到返回指定位置迭代器，找不到返回结束迭代器位置

  // beg 开始迭代器

  // end 结束迭代器

  // _Pred 函数或者谓词（返回bool类型的仿函数）



**示例：**

```C++
#include <algorithm>
#include <vector>
#include <string>

//内置数据类型
class GreaterFive
{
public:
	bool operator()(int val)
	{
		return val > 5;
	}
};

void test01() {

	vector<int> v;
	for (int i = 0; i < 10; i++) {
		v.push_back(i + 1);
	}

	vector<int>::iterator it = find_if(v.begin(), v.end(), GreaterFive());
	if (it == v.end()) {
		cout << "没有找到!" << endl;
	}
	else {
		cout << "找到大于5的数字:" << *it << endl;
	}
}

//自定义数据类型
class Person {
public:
	Person(string name, int age)
	{
		this->m_Name = name;
		this->m_Age = age;
	}
public:
	string m_Name;
	int m_Age;
};

class Greater20
{
public:
	bool operator()(Person &p)
	{
		return p.m_Age > 20;
	}

};

void test02() {

	vector<Person> v;

	//创建数据
	Person p1("aaa", 10);
	Person p2("bbb", 20);
	Person p3("ccc", 30);
	Person p4("ddd", 40);

	v.push_back(p1);
	v.push_back(p2);
	v.push_back(p3);
	v.push_back(p4);

	vector<Person>::iterator it = find_if(v.begin(), v.end(), Greater20());
	if (it == v.end())
	{
		cout << "没有找到!" << endl;
	}
	else
	{
		cout << "找到姓名:" << it->m_Name << " 年龄: " << it->m_Age << endl;
	}
}

int main() {

	//test01();

	test02();

	system("pause");

	return 0;
}
```

总结：find_if按条件查找使查找更加灵活，提供的仿函数可以改变不同的策略















#### 5.2.3 adjacent_find

**功能描述：**

* 查找相邻重复元素



**函数原型：**

- `adjacent_find(iterator beg, iterator end);  `

  // 查找相邻重复元素,返回相邻元素的第一个位置的迭代器

  // beg 开始迭代器

  // end 结束迭代器

  



**示例：**

```C++
#include <algorithm>
#include <vector>

void test01()
{
	vector<int> v;
	v.push_back(1);
	v.push_back(2);
	v.push_back(5);
	v.push_back(2);
	v.push_back(4);
	v.push_back(4);
	v.push_back(3);

	//查找相邻重复元素
	vector<int>::iterator it = adjacent_find(v.begin(), v.end());
	if (it == v.end()) {
		cout << "找不到!" << endl;
	}
	else {
		cout << "找到相邻重复元素为:" << *it << endl;
	}
}
```

总结：面试题中如果出现查找相邻重复元素，记得用STL中的adjacent_find算法









#### 5.2.4 binary_search

**功能描述：**

* 查找指定元素是否存在



**函数原型：**

- `bool binary_search(iterator beg, iterator end, value);  `

  // 查找指定的元素，查到 返回true  否则false

  // 注意: 在**无序序列中不可用**

  // beg 开始迭代器

  // end 结束迭代器

  // value 查找的元素





**示例：**

```C++
#include <algorithm>
#include <vector>

void test01()
{
	vector<int>v;

	for (int i = 0; i < 10; i++)
	{
		v.push_back(i);
	}
	//二分查找
	bool ret = binary_search(v.begin(), v.end(),2);
	if (ret)
	{
		cout << "找到了" << endl;
	}
	else
	{
		cout << "未找到" << endl;
	}
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**二分查找法查找效率很高，值得注意的是查找的容器中元素必须的有序序列









#### 5.2.5 count

**功能描述：**

* 统计元素个数



**函数原型：**

- `count(iterator beg, iterator end, value);  `

  // 统计元素出现次数

  // beg 开始迭代器

  // end 结束迭代器

  // value 统计的元素





**示例：**

```C++
#include <algorithm>
#include <vector>

//内置数据类型
void test01()
{
	vector<int> v;
	v.push_back(1);
	v.push_back(2);
	v.push_back(4);
	v.push_back(5);
	v.push_back(3);
	v.push_back(4);
	v.push_back(4);

	int num = count(v.begin(), v.end(), 4);

	cout << "4的个数为： " << num << endl;
}

//自定义数据类型
class Person
{
public:
	Person(string name, int age)
	{
		this->m_Name = name;
		this->m_Age = age;
	}
	bool operator==(const Person & p)
	{
		if (this->m_Age == p.m_Age)
		{
			return true;
		}
		else
		{
			return false;
		}
	}
	string m_Name;
	int m_Age;
};

void test02()
{
	vector<Person> v;

	Person p1("刘备", 35);
	Person p2("关羽", 35);
	Person p3("张飞", 35);
	Person p4("赵云", 30);
	Person p5("曹操", 25);

	v.push_back(p1);
	v.push_back(p2);
	v.push_back(p3);
	v.push_back(p4);
	v.push_back(p5);
    
    Person p("诸葛亮",35);

	int num = count(v.begin(), v.end(), p);
	cout << "num = " << num << endl;
}
int main() {

	//test01();

	test02();

	system("pause");

	return 0;
}
```

**总结：** 统计自定义数据类型时候，需要配合重载 `operator==`

















#### 5.2.6 count_if

**功能描述：**

* 按条件统计元素个数

**函数原型：**

- `count_if(iterator beg, iterator end, _Pred);  `

  // 按条件统计元素出现次数

  // beg 开始迭代器

  // end 结束迭代器

  // _Pred 谓词

  

**示例：**

```C++
#include <algorithm>
#include <vector>

class Greater4
{
public:
	bool operator()(int val)
	{
		return val >= 4;
	}
};

//内置数据类型
void test01()
{
	vector<int> v;
	v.push_back(1);
	v.push_back(2);
	v.push_back(4);
	v.push_back(5);
	v.push_back(3);
	v.push_back(4);
	v.push_back(4);

	int num = count_if(v.begin(), v.end(), Greater4());

	cout << "大于4的个数为： " << num << endl;
}

//自定义数据类型
class Person
{
public:
	Person(string name, int age)
	{
		this->m_Name = name;
		this->m_Age = age;
	}

	string m_Name;
	int m_Age;
};

class AgeLess35
{
public:
	bool operator()(const Person &p)
	{
		return p.m_Age < 35;
	}
};
void test02()
{
	vector<Person> v;

	Person p1("刘备", 35);
	Person p2("关羽", 35);
	Person p3("张飞", 35);
	Person p4("赵云", 30);
	Person p5("曹操", 25);

	v.push_back(p1);
	v.push_back(p2);
	v.push_back(p3);
	v.push_back(p4);
	v.push_back(p5);

	int num = count_if(v.begin(), v.end(), AgeLess35());
	cout << "小于35岁的个数：" << num << endl;
}


int main() {

	//test01();

	test02();

	system("pause");

	return 0;
}
```

**总结：**按值统计用count，按条件统计用count_if













### 5.3 常用排序算法

**学习目标：**

- 掌握常用的排序算法

**算法简介：**

- `sort`             //对容器内元素进行排序
- `random_shuffle`   //洗牌   指定范围内的元素随机调整次序
- `merge `           // 容器元素合并，并存储到另一容器中
- `reverse`       // 反转指定范围的元素





#### 5.3.1 sort

**功能描述：**

* 对容器内元素进行排序





**函数原型：**

- `sort(iterator beg, iterator end, _Pred);  `

  // 按值查找元素，找到返回指定位置迭代器，找不到返回结束迭代器位置

  //  beg    开始迭代器

  //  end    结束迭代器

  // _Pred  谓词





**示例：**

```c++
#include <algorithm>
#include <vector>

void myPrint(int val)
{
	cout << val << " ";
}

void test01() {
	vector<int> v;
	v.push_back(10);
	v.push_back(30);
	v.push_back(50);
	v.push_back(20);
	v.push_back(40);

	//sort默认从小到大排序
	sort(v.begin(), v.end());
	for_each(v.begin(), v.end(), myPrint);
	cout << endl;

	//从大到小排序
	sort(v.begin(), v.end(), greater<int>());
	for_each(v.begin(), v.end(), myPrint);
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**sort属于开发中最常用的算法之一，需熟练掌握













#### 5.3.2 random_shuffle

**功能描述：**

* 洗牌   指定范围内的元素随机调整次序



**函数原型：**

- `random_shuffle(iterator beg, iterator end);  `

  // 指定范围内的元素随机调整次序

  // beg 开始迭代器

  // end 结束迭代器

  

**示例：**

```c++
#include <algorithm>
#include <vector>
#include <ctime>

class myPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

void test01()
{
	srand((unsigned int)time(NULL));
	vector<int> v;
	for(int i = 0 ; i < 10;i++)
	{
		v.push_back(i);
	}
	for_each(v.begin(), v.end(), myPrint());
	cout << endl;

	//打乱顺序
	random_shuffle(v.begin(), v.end());
	for_each(v.begin(), v.end(), myPrint());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**random_shuffle洗牌算法比较实用，使用时记得加随机数种子















#### 5.3.3 merge

**功能描述：**

* 两个容器元素合并，并存储到另一容器中



**函数原型：**

- `merge(iterator beg1, iterator end1, iterator beg2, iterator end2, iterator dest);  `

  // 容器元素合并，并存储到另一容器中

  // 注意: 两个容器必须是**有序的**

  // beg1   容器1开始迭代器
  // end1   容器1结束迭代器
  // beg2   容器2开始迭代器
  // end2   容器2结束迭代器
  // dest    目标容器开始迭代器

  

**示例：**

```c++
#include <algorithm>
#include <vector>

class myPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

void test01()
{
	vector<int> v1;
	vector<int> v2;
	for (int i = 0; i < 10 ; i++) 
    {
		v1.push_back(i);
		v2.push_back(i + 1);
	}

	vector<int> vtarget;
	//目标容器需要提前开辟空间
	vtarget.resize(v1.size() + v2.size());
	//合并  需要两个有序序列
	merge(v1.begin(), v1.end(), v2.begin(), v2.end(), vtarget.begin());
	for_each(vtarget.begin(), vtarget.end(), myPrint());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**merge合并的两个容器必须的有序序列











#### 5.3.4 reverse

**功能描述：**

* 将容器内元素进行反转



**函数原型：**

- `reverse(iterator beg, iterator end);  `

  // 反转指定范围的元素

  // beg 开始迭代器

  // end 结束迭代器

  

**示例：**

```c++
#include <algorithm>
#include <vector>

class myPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

void test01()
{
	vector<int> v;
	v.push_back(10);
	v.push_back(30);
	v.push_back(50);
	v.push_back(20);
	v.push_back(40);

	cout << "反转前： " << endl;
	for_each(v.begin(), v.end(), myPrint());
	cout << endl;

	cout << "反转后： " << endl;

	reverse(v.begin(), v.end());
	for_each(v.begin(), v.end(), myPrint());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**reverse反转区间内元素，面试题可能涉及到









### 5.4 常用拷贝和替换算法

**学习目标：**

- 掌握常用的拷贝和替换算法

**算法简介：**

- `copy`                      // 容器内指定范围的元素拷贝到另一容器中
- `replace`                // 将容器内指定范围的旧元素修改为新元素
- `replace_if `          // 容器内指定范围满足条件的元素替换为新元素
- `swap`                     // 互换两个容器的元素




#### 5.4.1 copy

**功能描述：**

* 容器内指定范围的元素拷贝到另一容器中



**函数原型：**

- `copy(iterator beg, iterator end, iterator dest);  `

  // 按值查找元素，找到返回指定位置迭代器，找不到返回结束迭代器位置

  // beg  开始迭代器

  // end  结束迭代器

  // dest 目标起始迭代器



**示例：**

```c++
#include <algorithm>
#include <vector>

class myPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

void test01()
{
	vector<int> v1;
	for (int i = 0; i < 10; i++) {
		v1.push_back(i + 1);
	}
	vector<int> v2;
	v2.resize(v1.size());
	copy(v1.begin(), v1.end(), v2.begin());

	for_each(v2.begin(), v2.end(), myPrint());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**利用copy算法在拷贝时，目标容器记得提前开辟空间















#### 5.4.2 replace

**功能描述：**

* 将容器内指定范围的旧元素修改为新元素



**函数原型：**

- `replace(iterator beg, iterator end, oldvalue, newvalue);  `

  // 将区间内旧元素 替换成 新元素

  // beg 开始迭代器

  // end 结束迭代器

  // oldvalue 旧元素

  // newvalue 新元素



**示例：**

```c++
#include <algorithm>
#include <vector>

class myPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

void test01()
{
	vector<int> v;
	v.push_back(20);
	v.push_back(30);
	v.push_back(20);
	v.push_back(40);
	v.push_back(50);
	v.push_back(10);
	v.push_back(20);

	cout << "替换前：" << endl;
	for_each(v.begin(), v.end(), myPrint());
	cout << endl;

	//将容器中的20 替换成 2000
	cout << "替换后：" << endl;
	replace(v.begin(), v.end(), 20,2000);
	for_each(v.begin(), v.end(), myPrint());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**replace会替换区间内满足条件的元素













#### 5.4.3 replace_if

**功能描述:**  

* 将区间内满足条件的元素，替换成指定元素



**函数原型：**

- `replace_if(iterator beg, iterator end, _pred, newvalue);  `

  // 按条件替换元素，满足条件的替换成指定元素

  // beg 开始迭代器

  // end 结束迭代器

  // _pred 谓词

  // newvalue 替换的新元素



**示例：**

```c++
#include <algorithm>
#include <vector>

class myPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

class ReplaceGreater30
{
public:
	bool operator()(int val)
	{
		return val >= 30;
	}

};

void test01()
{
	vector<int> v;
	v.push_back(20);
	v.push_back(30);
	v.push_back(20);
	v.push_back(40);
	v.push_back(50);
	v.push_back(10);
	v.push_back(20);

	cout << "替换前：" << endl;
	for_each(v.begin(), v.end(), myPrint());
	cout << endl;

	//将容器中大于等于的30 替换成 3000
	cout << "替换后：" << endl;
	replace_if(v.begin(), v.end(), ReplaceGreater30(), 3000);
	for_each(v.begin(), v.end(), myPrint());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**replace_if按条件查找，可以利用仿函数灵活筛选满足的条件







#### 5.4.4 swap

**功能描述：**

* 互换两个容器的元素



**函数原型：**

- `swap(container c1, container c2);  `

  // 互换两个容器的元素

  // c1容器1

  // c2容器2

  

**示例：**

```c++
#include <algorithm>
#include <vector>

class myPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

void test01()
{
	vector<int> v1;
	vector<int> v2;
	for (int i = 0; i < 10; i++) {
		v1.push_back(i);
		v2.push_back(i+100);
	}

	cout << "交换前： " << endl;
	for_each(v1.begin(), v1.end(), myPrint());
	cout << endl;
	for_each(v2.begin(), v2.end(), myPrint());
	cout << endl;

	cout << "交换后： " << endl;
	swap(v1, v2);
	for_each(v1.begin(), v1.end(), myPrint());
	cout << endl;
	for_each(v2.begin(), v2.end(), myPrint());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**swap交换容器时，注意交换的容器要同种类型













### 5.5 常用算术生成算法

**学习目标：**

- 掌握常用的算术生成算法



**注意：**

* 算术生成算法属于小型算法，使用时包含的头文件为 `#include <numeric>`



**算法简介：**

- `accumulate`      // 计算容器元素累计总和

- `fill`                 // 向容器中添加元素

  

#### 5.5.1 accumulate

**功能描述：**

*  计算区间内 容器元素累计总和



**函数原型：**

- `accumulate(iterator beg, iterator end, value);  `

  // 计算容器元素累计总和

  // beg 开始迭代器

  // end 结束迭代器

  // value 起始值



**示例：**

```c++
#include <numeric>
#include <vector>
void test01()
{
	vector<int> v;
	for (int i = 0; i <= 100; i++) {
		v.push_back(i);
	}

	int total = accumulate(v.begin(), v.end(), 0);

	cout << "total = " << total << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**accumulate使用时头文件注意是 numeric，这个算法很实用



#### 5.5.2 fill

**功能描述：**

* 向容器中填充指定的元素



**函数原型：**

- `fill(iterator beg, iterator end, value);  `

  // 向容器中填充元素

  // beg 开始迭代器

  // end 结束迭代器

  // value 填充的值



**示例：**

```c++
#include <numeric>
#include <vector>
#include <algorithm>

class myPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

void test01()
{

	vector<int> v;
	v.resize(10);
	//填充
	fill(v.begin(), v.end(), 100);

	for_each(v.begin(), v.end(), myPrint());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**利用fill可以将容器区间内元素填充为 指定的值





### 5.6 常用集合算法

**学习目标：**

- 掌握常用的集合算法



**算法简介：**

- `set_intersection`          // 求两个容器的交集

- `set_union`                       // 求两个容器的并集

- `set_difference `              // 求两个容器的差集

  



#### 5.6.1 set_intersection

**功能描述：**

* 求两个容器的交集



**函数原型：**

- `set_intersection(iterator beg1, iterator end1, iterator beg2, iterator end2, iterator dest);  `

  // 求两个集合的交集

  // **注意:两个集合必须是有序序列**

  // beg1 容器1开始迭代器
  // end1 容器1结束迭代器
  // beg2 容器2开始迭代器
  // end2 容器2结束迭代器
  // dest 目标容器开始迭代器



**示例：**

```C++
#include <vector>
#include <algorithm>

class myPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

void test01()
{
	vector<int> v1;
	vector<int> v2;
	for (int i = 0; i < 10; i++)
    {
		v1.push_back(i);
		v2.push_back(i+5);
	}

	vector<int> vTarget;
	//取两个里面较小的值给目标容器开辟空间
	vTarget.resize(min(v1.size(), v2.size()));

	//返回目标容器的最后一个元素的迭代器地址
	vector<int>::iterator itEnd = 
        set_intersection(v1.begin(), v1.end(), v2.begin(), v2.end(), vTarget.begin());

	for_each(vTarget.begin(), itEnd, myPrint());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：** 

* 求交集的两个集合必须的有序序列
* 目标容器开辟空间需要从**两个容器中取小值**
* set_intersection返回值既是交集中最后一个元素的位置













#### 5.6.2 set_union

**功能描述：**

* 求两个集合的并集



**函数原型：**

- `set_union(iterator beg1, iterator end1, iterator beg2, iterator end2, iterator dest);  `

  // 求两个集合的并集

  // **注意:两个集合必须是有序序列**

  // beg1 容器1开始迭代器
  // end1 容器1结束迭代器
  // beg2 容器2开始迭代器
  // end2 容器2结束迭代器
  // dest 目标容器开始迭代器

  

**示例：**

```C++
#include <vector>
#include <algorithm>

class myPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

void test01()
{
	vector<int> v1;
	vector<int> v2;
	for (int i = 0; i < 10; i++) {
		v1.push_back(i);
		v2.push_back(i+5);
	}

	vector<int> vTarget;
	//取两个容器的和给目标容器开辟空间
	vTarget.resize(v1.size() + v2.size());

	//返回目标容器的最后一个元素的迭代器地址
	vector<int>::iterator itEnd = 
        set_union(v1.begin(), v1.end(), v2.begin(), v2.end(), vTarget.begin());

	for_each(vTarget.begin(), itEnd, myPrint());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：** 

- 求并集的两个集合必须的有序序列
- 目标容器开辟空间需要**两个容器相加**
- set_union返回值既是并集中最后一个元素的位置








#### 5.6.3  set_difference

**功能描述：**

* 求两个集合的差集



**函数原型：**

- `set_difference(iterator beg1, iterator end1, iterator beg2, iterator end2, iterator dest);  `

  // 求两个集合的差集

  // **注意:两个集合必须是有序序列**

  // beg1 容器1开始迭代器
  // end1 容器1结束迭代器
  // beg2 容器2开始迭代器
  // end2 容器2结束迭代器
  // dest 目标容器开始迭代器

  

**示例：**

```C++
#include <vector>
#include <algorithm>

class myPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

void test01()
{
	vector<int> v1;
	vector<int> v2;
	for (int i = 0; i < 10; i++) {
		v1.push_back(i);
		v2.push_back(i+5);
	}

	vector<int> vTarget;
	//取两个里面较大的值给目标容器开辟空间
	vTarget.resize( max(v1.size() , v2.size()));

	//返回目标容器的最后一个元素的迭代器地址
	cout << "v1与v2的差集为： " << endl;
	vector<int>::iterator itEnd = 
        set_difference(v1.begin(), v1.end(), v2.begin(), v2.end(), vTarget.begin());
	for_each(vTarget.begin(), itEnd, myPrint());
	cout << endl;


	cout << "v2与v1的差集为： " << endl;
	itEnd = set_difference(v2.begin(), v2.end(), v1.begin(), v1.end(), vTarget.begin());
	for_each(vTarget.begin(), itEnd, myPrint());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：** 

- 求差集的两个集合必须的有序序列
- 目标容器开辟空间需要从**两个容器取较大值**
- set_difference返回值既是差集中最后一个元素的位置

# 七 数据库管理系统

## 1 主函数

```cpp
// 写分支函数，调用manger的API
int main() {
	while (true) { // 只有0才能退出死循环
		showMenu();
		int choice;
		cin >> choice;
		switch (choice)
		{
		case 1:
			break;
		case 2:
			break;
		case 3:
			break;
		case 0:
            cout << "欢迎下次使用~" << endl;
			system("pause");
			return 0;
			break;
		default:
			cout << "输入错误！" << endl;
			system("pause");
			system("cls");

			break;
		}
	}
	system("pause");
	return 0;
}
```



### 1.2 Manger

```cpp
// manger.h
```

```cpp
// manger.cpp
初始化：
    file内容-> vector-> 后续操作
```



### 1.3 文件

```cpp
// 属性
bool file_exit;
vector<>//map<>  // 用于初始化或读取时存放数据
    
// 保存
void SpeechManger::save() {
	ofstream ofs("result.csv", ios::out | ios::app); // 追加
	for (vector<int> ::iterator it = this->top3.begin();it != this->top3.end();it++) {
		ofs << *it
			<< ","
			<< this->id_Sperker[*it].scord[1]
			<< ",";
	}
	ofs<< endl;
	ofs.close();
	this->file_exit = true;
	cout << "记录已保存！" << endl;
}
```

```cpp
// 读取
// 读取一般在初始化中执行
void SpeechManger::loadRecord() {
	ifstream ifs("result.csv", ios::in);
	if (!ifs.is_open()) {
		cout << "文件不存在！" << endl;
		this->file_exit = false;
		ifs.close();
		return;
	}
	char ch;
	ifs >> ch;
	if (ifs.eof()) {
		cout << "文件为空！" << endl;
		this->file_exit = false;
		ifs.close();
		return;
	}
	// 文件不为空
	this->file_exit = true;
	ifs.putback(ch); // 将尾符放回
	string data;
	
	int index = 1;
	while (ifs >> data) {
		int start = 0;
		vector<string> v;
		int pos = -1;
		// 读完一行
		while (true) {
			pos = data.find(",", start);
			if (pos == -1) {
				break;
			}
			else {
				string s1 = data.substr(start, pos - start); // 得到逗号切割后的字符串
				v.push_back(s1); // 放入容器中
				start = pos + 1;
			}
		}
		// 数据全部读完后，放入map<int, vector<string>> record
		this->record.insert(make_pair(index, v));
		index += 1;
	}
	ifs.close();
	cout << "加载完成！" << endl;
}
```

```cpp
// 清空
void SpeechManger::clearInfo() {
	cout << "是否确认清空？" << endl;
	cout << "1、确认" << endl;
	cout << "2、取消" << endl;
	int choice;
	cin >> choice;
	if (choice == 1) {
		if (!this->file_exit)
		{
			cout << "文件为空或者文件不存在" << endl;
			system("pause");
			system("cls");
			return;
		}
		// 打开并清空
		ofstream ofs("result.csv", ios::trunc);
		ofs.close();
		this->file_exit = false;
		cout << "清空成功！" << endl;
		system("pause");
		system("cls");
	}
	else if (choice == 2) {
		system("cls");
		return;
	}
	else{
		cout << "输入错误" << endl;
		system("pause");
		system("cls");
		return;
		}	
	
}
```

### 1.4 其他头文件

```cpp
// 一个类为一个头文件 和 cpp文件
```

### 1.5 return 和 break

```
return ： 退出当前执行的void函数，继续执行调用该函数的父函数
return 0： 退出当前执行的int函数，继续执行调用该函数的父函数
break  :  结束当前循环，for  or  while，继续执行该循环下边的语句
exit(0):  系统执行，程序正常退出，即结束整个程序(正常结束进程)
exit(-1): 系统执行，程序非正常退出，即结束整个程序（异常结束进程）
=======return0和 exit（0）  都可以结束while（true）的循环函数
```

* while

```cpp
while(true){
    xxxx;
    xxxxx;
    break;
}
```

* while+if

```cpp
while(true){
	if(){
        xxx
    }else{
        xxx
        break;
    }
}
```

* while+switch

```cpp
bool a = true;
while(bool){
switch(){
        case:
        break;
        case:
        a = false;           
}
}
    
```

### 1.6 用户选择输入

```cpp
// 选择输入放在while循环里
while(true){
    cout<<"请输入id"<<endl;
    int id;
    cin>> id;
    if(id>0&&id<10){
        cout<<"输入成功"<<endl;
        break; // 终止循环，进行下一步
	}else{
        cout<<"输入错误"<<endl; 
        
        // 不写下面就是重新输入，写了下面是退出函数
        system("pause");
        system("cls");
        return; // 退出当前函数
    }
}
```













## 1 通讯录管理系统

```cpp
#include <iostream>
using namespace std;

// 显示页面
void showMenu()
{
    cout << "***************************" << endl;
    cout << "*****  1、添加联系人  *****" << endl;
    cout << "*****  2、显示联系人  *****" << endl;
    cout << "*****  3、删除联系人  *****" << endl;
    cout << "*****  4、查找联系人  *****" << endl;
    cout << "*****  5、修改联系人  *****" << endl;
    cout << "*****  6、清空联系人  *****" << endl;
    cout << "*****  7、退出通讯录  *****" << endl;
    cout << "***************************" << endl;
};
// 联系人
struct Person
{
    string name;
    string sex;
    int age;
    string phone;
    string addr;
};
// 通讯录
struct addressBook
{
    Person people[1000];
    int size = 0;
};

// 1、添加联系人
void addPerson(addressBook *p)
{
    // 名字
    cout << "请输入名字：" << endl;
    string name;
    cin >> name;
    p->people[p->size].name = name;
    // 性别
    cout << "请输入性别：" << endl;
    cout << "1--男" << endl;
    cout << "2--女" << endl;
    while (true)
    {
        int sex;
        cin >> sex;
        if (sex == 1)
        {
            p->people[p->size].sex = "男";
            break;
        }
        else if (sex == 2)
        {
            p->people[p->size].sex = "女";
            break;
        }
        else
        {
            cout << "请重新输入:" << endl;
        }
    };

    // 年龄
    cout << "请输入年龄：" << endl;
    int age;
    cin >> age;
    p->people[p->size].age = age;
    // 电话
    cout << "请输入电话：" << endl;
    string num;
    cin >> num;
    p->people[p->size].phone = num;
    // 地址
    cout << "请输入地址：" << endl;
    string adr;
    cin >> adr;
    p->people[p->size].addr = adr;
    p->size += 1;
    system("cls");
};

// 2、显示联系人
void showPerson(addressBook *p)
{
    if (p->size == 0)
    {
        cout << "暂无联系人" << endl;
    }
    else
    {
        for (int i = 0; i < p->size; i++)
        {
            cout << "[" << i << "]"
                 << " ";
            cout << "姓名：" << p->people[i].name << "\t";
            cout << "性别：" << p->people[i].sex << "\t";
            cout << "年龄：" << p->people[i].age << "\t";
            cout << "电话：" << p->people[i].phone << "\t";
            cout << "地址：" << p->people[i].addr << endl;
        }
    }
    system("pause");
    system("cls");
};
// 3、删除联系人
void delPerson(addressBook *p)
{
    int del_num;
    string name;
    // 查找联系人
    cout << "请输入需要查找的联系人姓名：" << endl;
    cin >> name;
    for (int i = 0; i < p->size; i++)
    {
        if (p->people[i].name == name)
        {
            del_num = i;
            break;
        }
        else
        {
            del_num = -1;
        }
    }
    // 执行删除操作，后面数据往前移动
    if (del_num == -1)
    {
        cout << "查无此人！" << endl;
    }
    else
    {
        for (int i = del_num; i < p->size; i++)
        {
            p->people[i] = p->people[i + 1];
        }
        cout << "删除成功！" << endl;
        p->size--;
    }
    system("pause");
    system("cls");
};
// 4、查找联系人
void serchPerson(addressBook *p)
{
    int del_num;
    string name;
    cout << "请输入需要查找的联系人姓名：" << endl;
    cin >> name;
    for (int i = 0; i < p->size; i++)
    {
        if (p->people[i].name == name)
        {
            del_num = 1;
            break;
        }
        else
        {
            del_num = -1;
        }
    }
    // 显示查找
    if (del_num == 1)
    {
        for (int i = 0; i < p->size; i++)
        {
            if (p->people[i].name == name)
            {
                cout << "[" << i << "]"
                     << " ";
                cout << "姓名：" << p->people[i].name << "\t";
                cout << "性别：" << p->people[i].sex << "\t";
                cout << "年龄：" << p->people[i].age << "\t";
                cout << "电话：" << p->people[i].phone << "\t";
                cout << "地址：" << p->people[i].addr << endl;
            }
        }
    }
    else
    {
        cout << "查无此人！" << endl;
    }
    system("pause");
    system("cls");
};

// 5、修改联系人
void changePerson(addressBook *p)
{
    // 查找此人
    int del_num;
    string name;
    cout << "请输入需要查找的联系人姓名：" << endl;
    cin >> name;
    for (int i = 0; i < p->size; i++)
    {
        if (p->people[i].name == name)
        {
            del_num = i;
            break;
        }
        else
        {
            del_num = -1;
        }
    }
    // 修改
    if (del_num == -1)
    {
        cout << "查无此人！" << endl;
    }
    else
    {
        // 名字
        cout << "请输入名字：" << endl;
        string name;
        cin >> name;
        p->people[del_num].name = name;
        // 性别
        cout << "请输入性别：" << endl;
        cout << "1--男" << endl;
        cout << "2--女" << endl;
        while (true)
        {
            int sex;
            cin >> sex;
            if (sex == 1)
            {
                p->people[del_num].sex = "男";
                break;
            }
            else if (sex == 2)
            {
                p->people[del_num].sex = "女";
                break;
            }
            else
            {
                cout << "请重新输入:" << endl;
            }
        };

        // 年龄
        cout << "请输入年龄：" << endl;
        int age;
        cin >> age;
        p->people[del_num].age = age;
        // 电话
        cout << "请输入电话：" << endl;
        string num;
        cin >> num;
        p->people[del_num].phone = num;
        // 地址
        cout << "请输入地址：" << endl;
        string adr;
        cin >> adr;
        p->people[del_num].addr = adr;
    }
    system("pause");
    system("cls");
}
// 6、清空联系人
void clearPerson(addressBook *p)
{
    p->size = 0;
    cout << "联系人已清空" << endl;
    system("pause");
    system("cls");
};

int main()
{
    int choose = 0;
    // 注意实例化位置在循环之前，若在内则数据被覆盖再次实例化
    addressBook adb;
    while (true)
    {
        showMenu();
        // 实例化通讯录

        cin >> choose;
        switch (choose)
        {
        case 1:
            addPerson(&adb);
            break;
        case 2:
            showPerson(&adb);
            break;
        case 3:
            delPerson(&adb);
            break;
        case 4:
            serchPerson(&adb);
            break;
        case 5:
            changePerson(&adb);
            break;
        case 6:
            clearPerson(&adb);
            break;
        case 0:
            cout << "欢迎下次使用~" << endl;
            system("pause");
            return 0;
            break;

        default:
            break;
        }
    };

    system("pause");
    return 0;
}
```

## 2 项目

![image-20230403153908225](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230403153908225.png)



 ![image-20230403153931615](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230403153931615.png)

![image-20230403153943416](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230403153943416.png)

![image-20230403154008973](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230403154008973.png)

![image-20230407180304687](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230407180304687.png)



# 八 侯捷 STL 泛型编程

![image-20230413205924700](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230413205924700.png)

## 1 泛型编程GP

* OOP面向对象编程：将数据（属性）和方法（函数）存在一起
* GP泛型编程： 将数据存储和操作函数分开，闭门造车
* ![image-20230420205512078](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230420205512078.png)

### 1.1 运算符重载

![image-20230420205719789](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230420205719789.png)

* 容器内重写运算符的含义
* 可以直接调用algorithm写好的函数

### 1.2 list内含有sort函数

```txt
为什么list中的sort不放在容器外，采用GP编程？
因为，algorithm中的sort算法采用了 随机访问迭代器指针（顺序表指针），而list中的迭代器不支持随机访问，所以无法使用全局sort
```

![image-20230420210257474](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230420210257474.png)

## 2 iterator 迭代器

 ![image-20230413220717251](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230413220717251.png)

* 泛化指针，用来调用算法处理容器值

* 所有容器的迭代器，均提供头尾函数，注意end()指针指向容器结尾的下一位,满足==前闭后开==

### 2.1 五大typedef

* 迭代器设计需要遵循原则

* 迭代器内声明五项内容，用来回答算法的提问

  1、iterator_category: 迭代器类型：class泛化指针 or  真正的指针

  ​										class迭代器在链表中存在，可以回答五个问题 (bidirectional_iteror_tag)

  ​										真正的指针在array、vector中存在，不能主动回答问题 (random_access_iterator_tag)

  2、value_type ：存放的数值类型

  3、difference_type：迭代器 begin() 和 end() 之间的距离

  4、pointer

  5、reference

![image-20230421170215590](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230421170215590.png)

### 2.2 iterator_traits

* 因为真正的指针不能回答问题，需要设置一个traits萃取机作为中间容器，代替其回答

![image-20230421171833266](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230421171833266.png)

* traits采用==偏特化==的技术，用于分辨class 和 non-class iterator

![image-20230421172023021](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230421172023021.png)

![image-20230421172158705](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230421172158705.png)

### 2.4 构成

* iterator由一堆typedef和一堆运算符重载构成

![image-20230421182804555](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230421182804555.png)

## 3 containers 容器

![image-20230413223446135](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230413223446135.png)

<img src="C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230421172825843.png" alt="image-20230421172825843" style="zoom: 150%;" />

### 3.1 array



![image-20230420183518614](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230420183518614.png)

* 不能扩充
* 只有三个typedf（value_tpye, pointer. iterator）

![image-20230421185718816](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230421185718816.png)

```cpp
array<int,10>a;
array<int.10>::iterator ite = a.begin();
auto ite = a.begin();
a.size();
a.front();
a.back();
a.data(); // 数组起始位置
```

### ___ arrary_iterator

* 不是class指针，在array中typedf定义
* 与算法交互时，将iterator传入traits中，获取5种属性值

### 3.2 vector

![image-20230420183537137](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230420183537137.png)

* 连续存储
* 空间的增长以2倍增长
* 单向扩充

```
元素   空间
1 1
2 2
3 4
4 4
5 8
6 8
7 8
8 8
9 16
```



![image-20230421174923722](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230421174923722.png)

```cpp
// vector 由三个指针控制：start、finsh、end_of_storage
// 只有四种typedf
// 1个vector的占12个字节
// 二倍扩增，将原内容重新拷贝
```

```cpp
std::<vector> v;
std::<vector> v = {1，2，3};
std::<vector> v (5,1); // 5个1
std::<vector> v (v2.first(),v2.end()); // 5个1
v.assign(5,2);
v.assign(v3.first(),v3.end());

v.reserver(int len) // 预先分配容器的内存大小，避免大量动态分配内存  
v.resize(); // 更改容器的大小
v.capacity(); // 查看申请的内存大小（个数）



v.begin(); //指针指向起始位置，给iterator初始值(iterator类型)
v.end(); // 指针指向结束位置，给oteratpr结束值(iterator类型)

v.size();  // 真正元素个数
v.capacity(); // 申请的空间总个数

v.push_back(); // 单个元素添加到vector
std::copy(str,str+len,v.begin())  // 将范围内的元素赋值到变量内
v.front(); // 首值
v.back(); // 尾值
v.data();n 
```



###  ___ vector_iterator

![image-20230421180916473](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230421180916473.png)

```cpp
// vector_iterator是一个指针
// 不是class指针，在array中typedf定义
// 与算法交互时，将iterator传入traits中，获取5种属性值
```

```cpp
vector<int> v;
v.push_back(10);
v.push_back(20);
v.push_back(30);
v.push_back(40);
```

```cpp
// 1、定义相同类型的iterator
vector<int>::iterator it = v.begin();
for (; it != v.end(); it++)
{
    cout << *it << endl;
}

// 2、根据赋值，自动推导iterator类型
for (auto it = v.begin(); it != v.end(); it++)
{
    cout << *it << endl;
}

// 3、11新特性     --用it依次取出容器中的值
for (auto it :v)
{
    cout << it << endl;    
}

for (auto &it :v)
{
    it*=3;    //取引用，操作后返回原内存 
}
```

### 3.3 deuqe

* 双向扩充
* 底层为map指针结构， 分段有序存储，宏观上为连续存储
* 每次扩充多少？？？？

![image-20230420183447375](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230420183447375.png)

```cpp
#include<deque>

deque<int> d;
d.push_back(10);
d.size();
d.front();
d,back();
d.max_size();
```



### 3.4 list

![image-20230420184208178](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230420184208178.png)

* 每次扩充1个节点
* 动态分配内存
* 有自己的sort

```cpp
l.size();
l.max_size(); // 最大可分配内存数
l.front();
l.back();
```

![image-20230421154030427](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230421154030427.png)

* 含有头节点node
* l.begin() 为头节点的next值，指向头节点下第一个节点
* l.end() 为头节点，即最后一个内容节点的下一个节点

* 一个list由一个头节点指针控制，占用4个字节

### ___ list_iterator

![image-20230421152831891](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230421152831891.png)





* node为迭代器，智能指针
* 迭代器自增下一位，会自动找寻`(*node).next`指针位置
* 满足迭代器前闭后开，即灰色节点不属于list

### 3.5 forward-list

<img src="C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230420184318454.png" alt="image-20230420184318454"  />

* 每次扩充1个节点
* 有自己的sort
* ![image-20230421190312771](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230421190312771.png)

### 3.6 mutiset

![image-20230420195204115](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230420195204115.png)

* key = value

```cpp
multiset<string> m;

```



### 3.7 multimap

![image-20230420191418652](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230420191418652.png)

* key 和 value分开存储

```cpp
multimap<long,string> m;
m.insert(make_pair(1,"aaa"));

m.size();

    
   
```

### 3.8 unordered_multiset

![image-20230420195413305](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230420195413305.png)

```cpp
unordered_multiset<string> c;

c.insert();
c.size();
c.max_size();
c.bucket_count();
c.load_factor();
c.max_load_factor();
c.max_bucket_count();
```

### 3.9 unordered_multimap

```cpp
template<
    class Key,
    class T,
    class Hash = std::hash<Key>,
    class KeyEqual = std::equal_to<Key>,
    class Allocator = std::allocator<std::pair<const Key, T>>
class unordered_map;

std::unordered_map<Key, T, Hash, KeyEqual, Allocator>

```

- `Key`：键的类型，用于唯一标识每个键值对。
- `T`：值的类型，存储在容器中与键相关联的值。
- `Hash`：哈希函数的类型，用于计算键的哈希值，默认情况下使用 `std::hash<Key>`，可以自定义哈希函数。
- `KeyEqual`：键比较函数的类型，用于比较两个键是否相等，默认情况下使用 `std::equal_to<Key>`，可以自定义键比较函数。
- `Allocator`：内存分配器的类型，用于分配和释放内存，默认情况下使用 `std::allocator<std::pair<const Key, T>>`，一般情况下不需要显式指定。

#### 3.9.1 自定义哈希函数

```cpp
// 法1  -- 结构体内定义
struct Hasher{
    int operator()(const vector<int> &arr) const{
        // 自定义哈希函数
        if(arr.size() == 0)
            return -1;
        int result = 0;
        for(const int &num : arr)
            result += num;
        return result;
    }
};
unordered_map<vector<int>, int, Hasher> m2i(0, Hasher());  
```

```cpp
// 法2  -- 直接定义哈希函数
int hasher(const vector<int> &arr){
    int hash_index = 0;
    for(const int &num : arr)
        hash_index = (hash_index << 1) ^ num;
    return hash_index;
}
 unordered_map<vector<int>, int, int (*)(const vector<int>&)> m2i(0, hasher) // 声明函数指针类型
```





### 3.10 string

`std::string` 是 C++ 标准库提供的字符串容器，提供了丰富的操作函数。下面是一些常用的 `std::string` 操作函数：

1. 构造函数和赋值操作：
   - `std::string str;`：默认构造函数，创建一个空字符串。
   - `std::string str("Hello");`：使用字符串字面值构造函数，创建一个包含指定内容的字符串。
   - `std::string str(str2);`：拷贝构造函数，使用另一个字符串进行初始化。
   - `std::string str = "Hello";`：赋值操作符，将一个字符串赋值给另一个字符串。
   - `str = str2;`：赋值操作符，将一个字符串赋值给另一个字符串。

2. 访问和修改：
   - `str[i]`：访问字符串中第 i 个字符。
   - `str.at(i)`：访问字符串中第 i 个字符，提供边界检查。
   - `str.front()`：访问字符串的第一个字符。
   - `str.back()`：访问字符串的最后一个字符。
   - `str.data()`：返回指向字符串数据的指针。
   - `str.size()` 或 `str.length()`：返回字符串的长度。
   - `str.empty()`：检查字符串是否为空。
   - `str.clear()`：清空字符串内容。
   - `str.resize(newSize)`：改变字符串的大小，可以增加或缩小字符串。====vector==也有
   - `str.reserve(newCapacity)`：预分配存储空间，以容纳至少 `newCapacity` 个字符。

3. 连接和拼接：
   - `str1 + str2`：字符串拼接操作符，将两个字符串连接为一个新的字符串。
   - `str1.append(str2)` 或 `str1 += str2`：将一个字符串追加到另一个字符串的末尾。
   - `str1.append(str2, pos, len)`：将另一个字符串的子串追加到当前字符串的末尾。
   - `str1.insert(pos, str2)`：在指定位置插入另一个字符串。

4. 查找和替换：
   - `str.find(subStr)`：查找子串 `subStr` 在字符串中的第一次出现的位置。
   - `str.find(subStr, pos)`：从指定位置开始查找子串 `subStr` 在字符串中的第一次出现的位置。
   - `str.replace(pos, len, newStr)`：替换字符串中从 `pos` 开始长度为 `len` 的子串为 `newStr`。

5. 子串操作：
   - `str.substr(pos)`：返回从指定位置开始到字符串末尾的子串。
   - `str.substr(pos, len)`：返回从指定位置开始指定长度的子串。

6. 字符串比较：
   - `str1 == str2`：比较两个字符串是否相等。
   - `str1 != str2`：比较两个字符串是否不相等。
   - `str1 < str2`、`str1 > str2`、`str

## 4 allocator 分配器

<img src="C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230420202531224.png" alt="image-20230420202531224"  />



![image-20230420202554298](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230420202554298.png)

* 不建议分配器单独使用

* new+delete  malloce+free推荐使用
### 4.1默认allocator

  ![image-20230421120032833](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230421120032833.png)

* 在构造容器时，第二个参数默认为allocator类型的分配器

![image-20230421120159686](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230421120159686.png)

* allocator类里面有两个重要的成员函数：allocate和deallocate
* 底层分别调用：operator new 和 operator delete
* 底层再次调用c中的 malloc 和 free

### 4.2 调用allocator

* allocator为定义的一个类，因此可以单独调用

```cpp
// 实例化模板类
allocator<int> myAllocator;
// 调用allocate函数分配内存
// 两个参数 1、申请的空间个数  2、任意类型字符来推算 申请空间的存放数值类型
int *p = myAllocator.allocate(512,(int*)0);  //512个int
myAllocator.deallocator(p,512) // 必须写出要释放的内存数目


//法2：不用具体实例化名字，用（）代表实例化
int *p = allocator<int>().allocate(512,(int*)0);
allocator<int>().deallocate(p,512);
```

### 4.3 malloc申请空间

![image-20230421122905135](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230421122905135.png)

* operator new  底层调用 malloc申请空间
* 申请的空间除了存放数据空间外，还有冗余空间用来放其余记录信息
* 整体空间一定，数据空间越大，冗余空间越小，反之亦然。普遍上都是冗余空间大，造成内存浪费

### 4.4 __pool_allocator扩展分配器

* 详细解释见：《内存管理》allocater

![image-20230421123250038](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230421123250038.png)

![image-20230421123227507](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230421123227507.png)



* 为了解决上述内存浪费，G2.9实现STL时，创造出一种新的分配器
* 用链表实现，#0挂在申请空间为8字节的内存空间，#1为16，依次为8的倍数，#15为128
* 通过这种办法省掉，malloc申请空间的前后记录内存空间大小的内存
* G4.9将这种分配器命为__pool_alloc

```cpp
// 使用默认
vector<int,allocator<int>> v1;

// 使用__pool_alloc
# include <ext\pool_allocator.h>
vector<int,__gnu_cxx::__pool_alloc<int>> v2;
```







## 5 algorithm 算法

### 5.1 std::copy

用于将一个范围内的元素复制到另一个范围中。

* 将指定的字符串放在vector中

  ```cpp
  vector<string> v;
  int *p = v.begin();
  
  char *str;  // 指向字符串组（字符串）的起始位置
  std::copy(str，str+len,p);// 将字符串起始长度len的字符放在p指向的位置
  ```

* 将源范围 `[str, str + len)` 中的元素复制到目标范围 `v` 开始的位置。这个目标范围可以是任何支持迭代器的容器或序列，包括 `std::vector`、`std::deque`、`std::list` 等。



# --------------------------

# 八 高级编程

## 8.1 标准构建类

### 8.1.1  规则

```
1、类声明与实现分开编写

2、成员变量名加name_

2、构造函数使用特定写法

3、函数参数传递使用引用传递，判断是否需要const
4、函数返回判断是否需要引用返回
```

### 8.1.2 头文件防卫式声明

- 使用 `#ifndef`，编译器每次看到 #include 这个文件都需要读入文件，解析代码，效率低.

  C/C++ 标准中的一部分，支持 C/C++ 的编译器都能使用，可移植性更高。

- 而使用 `#pragma once` 编译器根本不会重复打开文件， 大大提高效率。

  依赖于编译器，可移植性较差
  
- 防止头文件内的类重复定义

```cpp
// .h
# ifndef __HEADERNAME__
# define __HEADERNAME__
xxxxx
# endif
```

### 8.1.3  定义成员属性

1. bool类型变量

2. 智能指针类型，有参构造使用移动语义

3. STL容器

== 注意== 成员属性，必须在初始化列表中初始化

不要在成员函数中初始化， 函数中尽量只使用成员变量，可以构造const成员函数

```cpp
MyClass{
public:
    explicit MyClass(std::shared_ptr<int> intptr,std::map<key,value> map_): 
    intptr_(std::move(intptr)),map_(std::moce(map)){};
    
    std::shared_ptr<int> intptr_;
    std::map<key,value> map_;
}
```

### 8.1.4 定义成员函数

[const成员函数](#const成员函数)



<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230908110057812.png" alt="image-20230908110057812" style="zoom: 67%;" />

* 常量方法
* static关键字
* 常量引用参数

```cpp
class MyClass {
public:
    void printValue(const int& value) const;
};
```



### 8.1.5 缺省方式的构造函数

* 推荐 将 ==编译器默认的无参构造== 和 ==自定义有参构造== 结合起来，写为缺省函数
* 即声明时给出默认值；
* [构造函数分类](#构造函数)

```cpp
// 1，形参要赋值  2、采用构造函数特有写法(形参实参名相同不影响)
class Person{
public:
    int age_;
    string name_;
    
    Person() = default; // 编译器提供默认构造
    Person(int age = 0, string name = "zhang"):age(age_),name(name_) {}; //自定义有参构造
    Person(int age = 0, string name = "zhang"):age(age_),name(name_) {}; // 缺省
    
}
```

### 8.1.6 重载

* 赋值运算符重载（自定义深拷贝）

```cpp
mystring& operator= (const mystring& str) {
		// 确保非自身赋值
		if (this != &str) {
			delete[] _str;
			_str = new char[str.size() + 1];
			strcpy_s(_str, str.size() + 1, str.data());

			_size = str.size();
			_capacity = str.capacity();
			return *this;
		}
	}
```

* 输出运算符重载

```cpp
// 类外定义
ostream& operator<< (ostream& out, const mystring& str) {
	for (size_t i = 0; i < str.size(); ++i) {
		cout << str[i];
	}
	return out;
}
```

* 自增运算符重载

在C++中，当你重载自增 (`operator++`) 操作符时，有两种版本：前置自增和后置自增。这两种版本通过参数列表进行区分。

1. **前置自增 (`operator++()`)**
    - 当你不给 `operator++` 传递任何参数时，这意味着你正在定义和实现前置自增操作符。
    - 使用前置自增时，迭代器会先自增，然后返回递增后的值的引用。

2. **后置自增 (`operator++(int)`)**
    - 当你传递一个整数参数给 `operator++` 时（通常命名为 `int`，但其实名字可以是任何有效的标识符），这意味着你正在定义和实现后置自增操作符。
    - 使用后置自增时，迭代器首先返回其当前值的一个副本（这是为什么需要一个额外的参数：为了区分它与前置版本），然后才进行自增操作。

```cpp
__list_iterator& operator++ () {
    _node = _node->_next;
    return *this;
}

// it++
__list_iterator operator++ (int) {
    __list_iterator temp = *this;  
    _node = _node->_next;     
    return temp;                  
}
```



## 8.2 const用法

<a name="const成员函数">跳转</a>

==const放在最前面或最后面==

1. 变量

声明为一个常量，其值为100。一旦定义了常量，就不能再修改它的值。

```cpp
const int MAX_VALUE = 100;

// 对一个文件的引用，权限只能不变或者缩小 
int a = 10;   //可读可写
const int &b = a;  //正确，权限缩小， 只读

const int a = 10; //只读
int &b = a;    // 错误，可读可写
const int &c = a; //只读，权限不变，正确

// 赋值没权限限制
const int a = 10; // 只读
int b = a;  // b 可读可写，只是赋值， a的权限和b没有关系，正确
const int b = a; // 正确

// 类型转换时引用，要const
int a = 10;
float &b = a;  // 错误,在类型转换时，需要借助中间量，中间量的属性是const，因此本质是，b是 tmp的引用，需要const
const float &b = a; // 通过修改a,不能影响b，因为b是tmp的引用， a到tmp是赋值，与a的权限无关
```

2. 函数传参

`printValue`函数的参数 `value` 被声明为常量。这意味着在函数内部不能修改该参数的值。

注意：const一般和引用&一起适用，替代指针传参

```cpp
void printValue(const int & value)

```

3. 函数返回值 

`getValue`函数的返回值被声明为常量。这意味着函数返回的值不能被修改。

```cpp
int& func(int& a){};
// const 同时使用
const int& func(const int& a){return a + 1;}  // return中含有const变量，返回需要const
int& func(const int& a){int val = a + 1; return val;}// return没有const，则不需要返回const


```

4. 成员函数 （重要）

`printValue`函数被声明为一个`const`成员函数。这表示该函数在执行期间不会修改所调用的==成员变量==。

```cpp
class MyClass {
private:
    int id;
public:
    // 两种效果一样，一般采用第一个就可以
    void printValue1(int &id) const;		 // 函数为const，结果可以const也可以非const，函数（const） -> 结果（不限）
    const void printValue2(int &id) const;   // 函数返回值为const，函数本身必须为const；  结果（const） -> 函数（const）
};

```

==细节==

* 函数传参类型为const：const对象只能调用其内部的const成员函数，不能调用非const成员函数
* 传参类型为 非const ： 非const对象可以调用任意的函数

```cpp
class Student {
private:
    string name_;
    int id_;
public:
    // 1、成员变量在初始化列表中初始化
    Student() : name_("张三"), id_(0){};
    
    // 2、仅查看成员变量，设置const函数
    string getName() const{ return name_ };
    
    // 3、修改成员变量，不能设置const
    void modId(){ id_ = 1 };
}

// 上层类调用该类
class People {
public:
    // 调用 getName 函数
    void func1 (const Student &a) const { a.getName() }   // const & 传参， func1 为const函数
    
    // 调用 modId 函数
    void func2 ( Student &a ) { a.modId() }               // & 传参， func2 不能为const
    
    // 调用 getName 函数、getName 函数
    void func3 (const Student &a， const Student &b) const { a.getName(); b.getName(); } // const & 传参， func3 为const函数
    
    // 调用 getName 函数、modId 函数
    void func3 (const Student &a, Student &b) { a.getName(); b.modId(); } // a const & 传参,b & 传参， func3 不为const
    
}

// main函数调用该类
int main(){
    Student S;
    
    void fun1(const Student& S){
        S.getName();  // √ const对象只能调用其内部的const成员函数，不能调用非const成员函数
        S.modId(); // ×  const对象不能调用非const成员函数
    }
    
    void fun2(Student S){
        S.getName();  // √ 非const对象可以调用所有成员函数
        S.modId(); // √  
    }
}
```



5. 成员变量

   [初始化列表](#初始化列表)

​		const成员变量只能通过构造函数==初始化列表==进行初始化，并且必须有构造函数；

​		不同类对其const数据成员的值可以不同，所以不能在类中声明时初始化

6. static静态成员函数

* 静态成员函数==不能被const修饰==，const是限制函数过程中，不修改成员变量
* const是用于作用实例的函数，而static是作用于类



## 8.4 函数的参数与返回值类型

### 8.4.1 参数传递

* 参数传递全部用引用的方式传入
* 若不想改变实参值，则用const修饰

```cpp
void swap(int &a, int &b){}
void swap2(const int &a, const int &b){}
```

### 8.4.2 函数返回值

1. 引用函数类型

* 返回值需要覆盖原参数值，用引用返回
* 引用返回需要注意本体是否存在的问题

```cpp
// int引用类型
// 即将返回的数据存放在原本的内存空间中，最终函数返回为内存空间的地址
int& fun(){
    int a = 10;
    return a; // ❌ a存放在栈内，函数执行完毕，内存空间释放，无法存放a，所以不能返回
    static int b = 1;
    return b; // 静态变量内存不释放，可以返回，返回值为b的引用，即b的地址
}
```

2. 指针类型函数

   * 返回值为指针

   ```cpp
   int* add(int a, int b){return a + b;};
   ```



## 8.5 函数指针

* 本质为指针，一个指向函数的指针

### 8.5.1 声明

* 声明一个函数指针类型，接受 int 和 float 参数，返回 int

```cpp
// 法1
int (*funcPtr)(int, float);  

```

```cpp
// 法2
typedef int (*FuncPtrType)(int, float);
FuncPtrType funcPtr;

```

使用 `typedef` 将 `int (*)(int, float)` 这个函数指针==类型==定义为一个新的类型别名 `FuncPtrType`。现在，我们可以使用 `FuncPtrType` 来声明函数指针变量，而不需要每次都写出完整的函数指针类型。

```cpp
// 法3
using FuncPtrType = int (*)(int, float); 
FuncPtrType funcPtr;  

```

### 8.5.2 使用

```cpp
// 函数
int add(int a, int b);
// 定义函数指针
int (*funcPtr)(int, int) = add;
// 使用
int res = funPtr(1.2);

```

### 8.5.3 与指针函数类型区别

* 指针函数类型：函数

```cpp
int *fun1(int a, int b){};
```

* 函数指针类型： 指针

```cpp
int (*fun2)(int,int);
```





## 8.8 static

### 8.8.0

<a name = "static1">跳转</a>

> 静态变量在 == 数据区== 开辟内存空间，声明周期为main函数
>
> 静态变量的定义只会执行一次

```cpp
int & add1(int a, int b)
{
    static int c = a + b;
    return c;
}

int main(){
    int & A = add(1,2);  //执行一次定义 static int c = 1 + 2, A 是 c 的别名
    add(5, 5);  // 不会再执行 static int c = 5 + 5;  即c 永远是 1 + 2
}

int & add2(int a, int b)
{
    static int c = 1; // 执行1次定义
    c = a + b;
    return c;
}

int main(){
    // 直接跳过 static intc = 1，执行c = a + b
    int & A = add(1,2);  //执行一次 c = 1 + 2, A 是 c 的别名
    add(5, 5);  //  c = 5 + 5; 
    
}
```



### 8.8.1 静态成员变量

* 类内声明，类外初始化

公共静态成员变量可以通过类名或对象来访问。无论通过哪种方式访问，静态成员变量只有一份副本，与类的实例无关

私有静态成员变量不能通过main内访问，但必须在类外部初始化，访问调用其私有成员函数访问

```cpp
// 定义一个类
class MyClass {
public:
    static int staticVar; // 静态成员变量
};

int main() {
    // 1、通过类名访问静态成员变量
    MyClass::staticVar = 10;

    // 2、通过对象访问静态成员变量
    MyClass myObject;
    myObject.staticVar = 20;

    return 0;
}

```

```cpp
// 定义一个类
class MyClass {
private:
    static int staticVar; // 静态成员变量
public:
    static int getit(){
        return staticVar;
    }
};
static int staticVar = 10；
int main() {
    getit();

    return 0;
}

```

### 8.8.2 类外初始化和main内部初始化

```
静态成员变量需要在类外单独分配空间的原因是因为它们属于整个类，而不是类的实例。在类定义中声明的静态成员变量只是一种声明，用于描述该变量的类型和名称，并不会为其分配内存空间。

为了为静态成员变量分配内存空间，必须在类外部的全局范围内进行定义和初始化。这样做可以确保静态成员变量在程序启动时就分配了内存，并且可以在整个程序的生命周期内使用。

另外，静态成员变量的作用域是整个类，它们被所有类的实例共享。因此，在类外部分配空间可以确保所有实例共享同一个静态成员变量的内存空间，而不是每个实例都拥有自己的副本。

需要注意的是，静态成员变量的定义和初始化只能在类的实现文件中进行一次，以避免重复定义。通常，可以在类的头文件中声明静态成员变量，在实现文件中进行定义和初始化。
```



```cpp

类外初始化：静态成员变量的类外初始化是在类定义的外部进行的。这意味着在任何使用该类的地方，静态成员变量都已经初始化，并且可以直接使用。这样可以确保在程序的任何地方都能访问到已初始化的静态成员变量。

main 函数内初始化：在 main 函数内部对静态成员变量进行初始化是在程序执行到 main 函数时进行的。这意味着在 main 函数之前的代码中，静态成员变量可能尚未初始化，无法直接使用。只有在 main 函数开始执行之后，静态成员变量才被初始化并且可以使用。

初始化顺序：类外初始化的静态成员变量的初始化顺序是根据其定义的顺序决定的。而在 main 函数内初始化的静态成员变量的初始化顺序是根据它们在 main 函数内的出现顺序决定的。如果静态成员变量之间存在相互依赖关系，初始化顺序可能会影响程序的行为。

总结来说，类外初始化可以确保静态成员变量在任何使用类的地方都已经初始化，并且可以直接使用。而在 main 函数内初始化的静态成员变量则是在程序执行到 main 函数时才进行初始化，并且只能在 main 函数内部使用。选择何种方式初始化静态成员变量取决于具体的需求和设计。
```

### 8.8.3 私有静态成员变量



静态成员函数

在类中声明的静态成员函数不属于类的实例，而是属于类本身。静态成员函数没有 `this` 指针，无法访问非静态成员变量和非静态成员函数，只能调用其他静态成员函数或访问静态成员变量。

- 静态成员函数可以直接通过类名加作用域运算符调用，例如 `ClassName::staticFunction()`。
- 静态成员函数可以被类的实例调用，但实际上是通过隐式地将实例的指针传递给静态成员函数进行调用。

* 静态全局变量

  静态全局变量的作用域仅限于当前源文件，其他源文件无法直接访问

* 静态局部变量

​		在函数内部声明的静态局部变量只会在第一次调用时初始化，之后的函数调用会保留上一次调用结束时的值。静态局部变量的生命周		期与程序的运行周期相同，但作用域仅限于声明它的函数内部。

### 8.8.4 访问权限

![image-20230907173601180](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230907173601180.png)

* 所有对象均可访问静态成员变量，只有一个
* 所有对象均可访问静态成员函数，只有一个
* 静态成员函数只能访问静态成员变量，没有this
* 静态成员函数只能访问静态成员函数，没有this



### 8.8.5 使用静态成员函数

1. 成员函数只在类中使用，不调用成员变量，声明为static

   `节省内存：每个类的实例都包含一组成员变量，它们占用内存。然而，静态成员变量只有一个副本，存储在类的静态数据区，不需要每个对象都拥有一份副本，从而节省了内存。`

2. 访问静态成员变量，使用静态成员函数

   

### 8.8.6 汇总

在C++中，`static`关键字在不同的上下文中有不同的作用。根据面向过程和面向对象两种编程范式，`static`的使用和效果也有所不同。以下是对C++中`static`的作用和使用场景的详细解释：

#### 面向过程中的 `static`

1. **局部静态变量（Local Static Variables）**:
   - 定义在函数内部的静态变量在函数多次调用之间保持其值。也就是说，变量在函数的每次调用之间不会重新初始化。
   - 这种变量在程序的生命周期内只初始化一次，且在程序运行期间，始终驻留在内存中。
   - 使用场景：通常用于需要在函数调用之间保留状态的情况下，例如计数器、缓存机制等。

   ```cpp
   void counter() {
       static int count = 0; // 局部静态变量，只初始化一次
       count++;
       std::cout << count << std::endl;
   }
   
   int main() {
       counter(); // 输出 1
       counter(); // 输出 2
       counter(); // 输出 3
   }
   ```

   在上面的例子中，`count`变量在第一次调用`counter`函数时被初始化为0，并且在后续调用中保留其更新的值。

2. **全局静态变量和静态函数（Global Static Variables and Static Functions）**:
   - 在文件级别声明的静态变量和函数只在其声明的文件内部可见，不会被外部文件访问。这是实现文件内局部化（localization）的一种方法，避免全局命名空间污染。
   - 使用场景：常用于定义不需要被其他文件访问的辅助函数或变量。

   ```cpp
   // file1.cpp
   static int file_scope_variable = 42; // 只能在 file1.cpp 中访问
   
   static void helperFunction() { // 只能在 file1.cpp 中调用
       std::cout << "This is a helper function" << std::endl;
   }
   ```

   在`file1.cpp`中，`file_scope_variable`和`helperFunction`仅在`file1.cpp`中可见，其他文件无法访问或调用它们。

#### 面向对象中的 `static`

1. **静态成员变量（Static Member Variables）**:
   - 静态成员变量属于类，而不是类的某个具体对象。也就是说，所有该类的对象共享同一个静态成员变量。
   - 静态成员变量必须在类外部初始化。
   - 使用场景：用于表示所有类实例共享的属性，例如一个计数所有类实例数量的变量。

   ```cpp
   class MyClass {
   public:
       static int count;
       MyClass() { count++; }
   };
   
   int MyClass::count = 0; // 静态成员变量在类外初始化
   
   int main() {
       MyClass obj1;
       MyClass obj2;
       std::cout << MyClass::count << std::endl; // 输出 2
   }
   ```

   在上面的例子中，`count`是`MyClass`类的一个静态成员变量，所有`MyClass`对象共享同一个`count`，并且它记录了创建的`MyClass`对象的数量。

2. **静态成员函数（Static Member Functions）**:
   - 静态成员函数属于类，而不是类的某个具体对象。它们只能访问类的静态成员（变量或函数），而不能访问非静态成员，因为它们不具有`this`指针。
   - 使用场景：用于不依赖于类的具体对象的功能，例如工具函数或与类关联的全局行为。

   ```cpp
   class Utility {
   public:
       static void printMessage() {
           std::cout << "Hello from static member function!" << std::endl;
       }
   };
   
   int main() {
       Utility::printMessage(); // 可以直接通过类名调用
       Utility obj;
       obj.printMessage(); // 也可以通过对象调用
   }
   ```

   在上面的例子中，`printMessage`是`Utility`类的一个静态成员函数，可以直接通过类名调用，而无需创建类的实例。

#### 总结

- **面向过程**:
  - 局部静态变量：在函数内部，保留状态。
  - 全局静态变量和函数：在文件内可见，防止命名空间污染。

- **面向对象**:
  - 静态成员变量：属于类，所有对象共享。
  - 静态成员函数：属于类，不能访问非静态成员。

`static`关键字在C++中具有强大的功能，能够帮助我们管理变量的生命周期、作用域和可见性，并在面向对象编程中定义与对象无关的类级别的行为。

## 8.8 IO操作

* read

  系统调用，用于向fd打开的文件写入。【缓冲区<->fd打开的文件】

* print

  格式化字符串到标准输出【内容打印到控制台】

* snprintf

  格式化字符串到指定数组（起始位置由指针指定）【缓冲区<->格式化字符串】



文件操作：

linux：fd=open()、read、write

c: FILE * fp = fopen() 、fputs() 、fgets()



read printf puts

缓冲区类（fd打开文件，读入readv，写出write； 加入字符串append）

c++ 文件类 （file *fp, 读入fputs，写出fgets）  宏观上打开的文件

字符串（写到控制台，printf，写到数组（缓冲区）snprintf）



## 8.9 内存分配函数

* 堆分配

C语言中有几个常用的内存分配函数，它们允许您在运行时分配和管理内存。以下是一些主要的内存分配函数：

1. `malloc`（Memory Allocation）：
   - 函数签名：`void* malloc(size_t size);`
   - 作用：用于分配指定大小的堆内存，返回一个指向分配内存的指针。如果分配成功，返回一个合法的指针；如果分配失败，返回`NULL`。

2. `calloc`（Contiguous Allocation）：
   - 函数签名：`void* calloc(size_t num_elements, size_t element_size);`
   - 作用：用于分配指定数量和大小的连续块内存，返回一个指向分配内存的指针。所有分配的内存都被初始化为零。如果分配成功，返回一个合法的指针；如果分配失败，返回`NULL`。

3. `realloc`（Reallocate Memory）：
   - 函数签名：`void* realloc(void* ptr, size_t new_size);`
   - 作用：用于重新调整先前分配的内存块的大小。通常用于扩展或缩小内存块。它接受一个先前分配的内存块指针和新的大小作为参数，返回一个指向重新分配内存的指针。如果分配失败，返回`NULL`。如果`ptr`为`NULL`，则`realloc`的行为等同于`malloc`。

4. `free`：
   - 函数签名：`void free(void* ptr);`
   - 作用：用于释放通过`malloc`、`calloc`或`realloc`分配的内存。一旦调用`free`，相关内存块将被标记为可用，并可以被后续的内存分配函数重新分配。

这些内存分配函数通常用于动态内存管理，允许您在程序运行时根据需要分配和释放内存。需要注意的是，使用这些函数分配的内存必须显式释放，以避免内存泄漏问题。

* 栈分配

alloca` 是一个内存分配函数，但它并不属于标准C库（C标准库）。`alloca` 函数通常用于栈上分配内存，它的作用是在函数的栈帧中分配一块内存空间，用于临时存储数据。与 `malloc`、`calloc` 和 `realloc` 不同，`alloca` 不分配堆内存，而是分配在函数的栈帧上，这意味着分配的内存在函数返回时会自动释放，不需要显式调用 `free` 来释放它。

请注意，`alloca` 并不是标准C函数，而是一些编译器提供的扩展。因此，它的可移植性受限，不同的编译器可能有不同的实现方式或行为。如果要编写可移植的C代码，建议使用标准的内存分配函数 `malloc`、`calloc` 和 `realloc`，并记得在不再需要内存时使用 `free` 来释放它们。

`char *message = (char*)alloca(length * sizeof(char));`

## 8.10 内存处理函数

* `memset`

```cpp
// 按字节进行处理，初始化操作
// 只适用于初始化为0
int a[10];
memset(a,0, sizeof(int)*10);
    
memset(a,1, sizeof(int)*10);   // 发生错误  初始化为 000000001  00000001 00000001 00000001
```

* `memcpy`

[存在问题](#memcpy)

```cpp
// 按字节进行浅拷贝
// 如果对象中涉及到资源管理（拷贝指针）时，千万不能使用memcpy进行对象之间的拷贝，因为memcpy是浅拷贝，否则可能会引起内存泄漏甚至程序崩溃。
```



## 8.11 inline

[资料](E:\typora索引文件\c++\C++初阶课件\Lesson01---C++入门.pdf)



# 九 C++11新特性

[c++11新特性pdf](E:\typora索引文件\c++\C++进阶课件\Lesson06--C++11.pdf)

## 9.0 cast类型转换

**不用加std**

| 类型              | 使用                                                         |
| ----------------- | ------------------------------------------------------------ |
| `static_cast`     | 相同类型转换，数值转换、指针转换、父类指针指向子类（合法）   |
| `dynamic_cast`    | 必须有虚函数，子类指针指向父类（非法），根据==虚函数表==判断，若是子类的虚函数表，则转换成功，否则失败 |
| `reiterpret_cast` | 强转，常用于指针之间转换、指针与数值之间转换                 |
| `const_cast`      | 去除指向对象的指针或引用的const、valatile属性                |



### 8.7.1 static_cast

* 隐式转换（相似类型转换）

它可以将一种类型的值转换为另一种类型，前提是这两种类型之间存在明确定义的转换规则。 `static_cast` 是一种相对安全的类型转换，可以进行常见的类型转换，如数值类型之间的转换、指针类型之间的转换以及父子类之间的指针或引用转换。

语法如下：`static_cast<目标类型>(表达式)`

1、数值之间转换

```cpp
int x = 10;
double y = static_cast<double>(x);

```

2、指针类型之间转换

```cpp
int* ptr = new int(5);
void* voidPtr = static_cast<void*>(ptr);

```

3、父类指针指向子类对象

```cpp
class par {};
class son : public par {};
son * son = new son();
par* ptr = static_cast<son*>(son);
```

4、bool类型转换

如果值为零或空指针，则转换结果为 `false`。

如果值不为零或非空指针，则转换结果为 `true`

```cpp
int num = 10;
bool result = static_cast<bool>(num); true

int *a = NULL;
bool result = static_cast<bool>(a); false
```

### 8.7.2 reinterpret_cast

* 强制类型转换（不相近类型）
* 常用于不同类型指针或引用的转换、指针与整形之间的转换

```cpp
int *p = nullptr;
int i =1;
// p = (int *)i; c语言中强制类型转换
p = reinterpret_cast<int*> i;
```



### 8.7.3 dynamic_cast

`dynamic_cast` 主要用于多态类型的转换

1. 在多态类型中进行安全的向下转型：当基类指针或引用指向派生类对象时，可以使用 `dynamic_cast` 将其转换为派生类指针或引用。如果转换是有效的，即指针或引用指向的对象是目标类型的一个实例，那么转换将成功，==返回指向派生类的指针或引用==；否则，如果转换无效，即指针或引用指向的对象不是目标类型的实例，转换将==返回nullptr（==对于指针转换）或抛出 `std::bad_cast` 异常（对于引用转换）。
2. 进行类型的动态检查：可以使用 `dynamic_cast` 进行类型的动态检查，判断一个对象是否属于特定的类型。如果转换成功，即对象是目标类型的一个实例，转换将返回非空指针；否则，转换将返回空指针。

需要注意的是，`dynamic_cast` 只能用于具有虚函数的类类型之间的转换，并且转换涉及的类型必须存在继承关系。

1. 父类指针 接收 子类对象赋值， 天然可通过，发生切片
2. 子类指针 接收 父类对象赋值，分情况，若父类对象的指针实际指向父类对象，则失败、若实际指向子类对象，则成功
3. dynamic_cast用来判断，父类指针指向的具体对象，失败则nullptr

4. 使用dynamic_cast父类必须要有==虚函数==, 原理是通过虚表来判断具体指向哪一个对象

```cpp
class A {
public:
	virtual void fun() {};  //1 必须要有虚函数，即构成多态
protected:
	int _x;
};

class B : public A {
private:
	int _y;
};
int main() {
	A a1;
	B b1 ;
	A* pa = &a1;  // 父类指针指向父类对象
	// 切片
	A* pb = &b1; // 父类对象指向子类对象


	// B* pb2 = &a2; 报错：子类指针不能接收父类对象
	B* pa2 = dynamic_cast<B*> (pb);  // 父类必须为多态，即必须包含虚函数
	if (pa2 != nullptr) cout << "父类指针指向子类对象" << endl;
	else cout << "父类对象指向父类对象" << endl;

	return 0;
}
```



<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240304162243228.png" alt="image-20240304162243228" style="zoom:67%;" />



### 8.7.4 const_cast

* 移除指向对象的指针或引用的const属性，不能移除对象本身的const属性，会出现未定义的错误

```cpp
const int i = 1;
int p = const_cast<int>(i); // 错误

int j = 1;
const int* j1 = &j;
int *p = const_cast<int*>(j);
const int& j2 = j;
int &p = const_cast<int&>(j2);
```

【考点】

```cpp
const int i = 1;
int *p = const_cast<int*>(&i);
*p =2;
cout << *p <<endl; // 输出2
cout << i << endl; // 输出1， 但是此时内存中i的值已经被修改为2，但是输出的i是从寄存器中获取
// 设置volatile const int i = 1; 设置关键字防止编译器对const对象存取做优化，此时 cout <<i 为2
```

* volatile 用于防止编译器优化，确保每次访问变量时直接从内存读取，常用于多线程编程和访问硬件寄存器。

```cpp
volatile int a = 10;

int &b = const_cast<int&>(a); // 将a转化为引用，再取出volatile属性
```



## 9.1 智能指针

### 9.1.1 类型

| 类型         | 问题                              | 解决方案                       | 差异 |
| ------------ | --------------------------------- | ------------------------------ | ---- |
| 普通指针     | new后需要delete，忘记造成资源释放 | 智能指针                       |      |
| `auto_ptr`   | 拷贝构造释放了原ptr的指针         | unique_ptr，禁止左值拷贝       |      |
| `unique_ptr` | 禁止了拷贝构造和operator=         | shared_ptr, 开放拷贝，引用计数 |      |
| `shared_ptr` | 线程安全问题                      | 指针 和 计数器 在堆上开辟内存  |      |

* 智能指针原理
  1. RAII特性 ：利用对象的**生命周期**来控制**资源**，构造即初始化，析构则释放资源
  2. 实现指针的特性：即重载 *  和  ->

```cpp
#pragma once
#include <iostream>
#include <mutex>

namespace yu {

	template <class T>
	class auto_ptr {
	public:
		auto_ptr(T* ptr) : _ptr(ptr) {}

		// 转移所有权，导致资源指针为空
		auto_ptr(const auto_ptr<T>& p) : _ptr(p._ptr) {
			p._ptr = nullptr;
		}

		auto_ptr<T>& operator= (const auto_ptr<T>& p) {
			if (this->_ptr != p._ptr) {
				if (this->_ptr) delete _ptr;
				this->_ptr = p._ptr;
				p._ptr = nullptr;
			}
			return *this;
		}

		~auto_ptr() {
			if (_ptr) delete _ptr;
		}

		T& operator* () {
			return *_ptr;
		}

		T* operator-> () {
			return _ptr;
		}
	private:
		T* _ptr;

	};

	// auto_ptr导致问题： 拷贝会释放掉原智能指针的ptr，再次调用原ptr时候，会程序崩溃
    // 因此容器内也不能存放auto_ptr
    // 解决办法1:  scoped_ptr,delete掉拷贝构造和赋值运算符重在
    // 解决办法2： unique_ptr,delete拷贝构造和赋值运算符重载，开放右值引用的移动构造和右值运算符重载
    // 解决办法3： shared_ptr，添加引用计数

    
    // 用户显式调用资源转移
	template <class T>
	class unique_ptr {
	public:
		unique_ptr(T* ptr) : _ptr(ptr) {}
		unique_ptr(unique_ptr<T> p) = delete;
		unique_ptr& operator= (unique_ptr<T> p) = delete;

		~unique_ptr() {
			if (_ptr) delete(_ptr);
		}

		T& operator* () {
			return *_ptr;
		}

		T* operator-> () {
			return _ptr;
		}
	private:
		T* _ptr;
	};


	// 解决办法2 ： shared_ptr 通过引用计数，拷贝不释放原智能指针的_ptr
	// 注意线程安全
	// 引用计数要求： 1 多个对象可以访问同一个计数（static、指针、引用）  2 同时多个对象也可以访问不同的计数（指针），堆开辟空间

	template <class T>
	class shared_ptr {
	public:
		shared_ptr(T* p) : _ptr(p), _count(new int(1)), _mutex(new mutex) {};
		shared_ptr(const shared_ptr<T>& p) : _ptr(p._ptr), _count(p._count), _mutex(p._mutex) {
			addCount();
		}

		shared_ptr& operator= (const shared_ptr<int>& p) {
			if (_ptr != p._ptr) {
				release();
				_ptr = p._ptr;
				_count = p._count;
				_mutex = p._mutex;
				addCount();
			}
			return *this;
		}

		~shared_ptr() {
			release();
		}

		T& operator* () {
			return *_ptr;
		}

		T* operator-> () {
			return _ptr;
		}

		// 为线程安全，对于计数的加减操作，全部放在锁内
		void addCount() {
			_mutex->lock();
			++(*_count);
			_mutex->unlock();
		}

		// 释放自身的指针
		void release() {
			_mutex->lock();

			int flag = 1;
			if (--(*_count) == 0 && _ptr) {
				cout << "delete: " << _ptr << endl;
				delete _ptr;
				delete _count;
				// 锁内无法释放锁
				flag = 0;
			}
			if (flag == 0) delete _mutex;
			
		}

		T* get() {
			return _ptr;
		}
	private:
		T* _ptr;
		int* _count;  // 均在堆上开辟空间
		std::mutex* _mutex; // 在堆上开辟空间


	};

	// 3 shared_ptr存在交叉引用的问题，即两个shared_ptr指针相互指，导致无法释放
    // 解决： 定义对象时使用强智能指针，引用对象时使用若智能指针
    // 注意： 弱智能指针只是观察者角度，不修改引用计数，同样也不能使用资源
    // 要使用若智能指针的资源，要强转为强智能指针
    int maine{
        A{
            weak_ptr<B> b_;
        }
        B{
            weak_ptr<A> a_;   // 引用对象弱智能指针
            
            // 使用时候强转
            shared_ptr<A> ptr = a_.lock();
            if(ptr) {// 强转成功则使用，失败说明弱智能指针已经释放}
        }
        shared_ptr<A> a ; // 定义对象强智能指针
        shared_ptr<B> b ;
    }
}
```

### 9.1.2 初始化

1. 使用 `make_unique`/ `make_shared`，传入对象即可，内部自动调用new分配空间

```cpp
std::unique_ptr<int> ptr = std::make_unique<int>(10);  // 使用make_unique进行初始化
std::shared_ptr<int> ptr = std::make_shared<int>(10);  // 使用make_shared进行初始化

```

2. 使用指针初始化，传入new后的指针

```cpp
int *ptr = new int(10);
std::unique_ptr<int> uptr (ptr); // 后面直接跟括号,传入直接new出来的指针

// 简写
std::unique_ptr<int> uptr (new int(5));

```

new返回的是一个指针，智能指针是一个类对象，里面重载了函数和运算符，因此不能直接接收new的结果

 	错误：`std::unique_ptr<int> uptr = new int(5);`

### 9.1.3 作为参数或者使用

1. `std::shared_ptr<T>`：共享指针（Shared Pointer）

   - 作用：多个指针可以共享同一个对象，并在最后一个引用释放时自动销毁对象。
   - 注意交叉引用

   ```cpp
   std::shared_ptr<int> ptr1 = std::make_shared<int>(10);
   std::shared_ptr<int> ptr2 = ptr1;
   std::cout << *ptr1 << " " << *ptr2 << std::endl;  // 输出：10 10
   
   ```

  2、`std::unique_ptr<T>`：独占指针（Unique Pointer）

   - 作用：确保只有一个指针可以拥有对对象的独占权，并在该指针离开作用域时自动释放对象。
   - 注意：不能==左值传参==，需要转为右值后进行右值传参，因为禁止了左值拷贝 和 左值operator=

   ```cpp
std::unique_ptr<int> ptr = std::make_unique<int>(20);
1. vec.push_back(std::move(ptr)) // 值传参，开放右值拷贝

2. void func( unique_ptr<T>&& a){};
func(std::move(ptr));
   ```

  ```cpp
std::unique<int> ptr;
std::unique<int> newptr = make_unique<int>(5)

ptr = newptr; (❌) // 禁止了左值operator=
ptr = move(newptr);(√) // 开放右值operator=
  ```



3、`std::weak_ptr<T>`：弱引用指针（Weak Pointer）

   - 作用：用于解决共享指针可能导致的循环引用问题，并且不会增加引用计数，也不会使用强智能指针资源
   - 使用资源时候强转为强指针

   ```cpp
std::shared_ptr<int> sharedPtr = std::make_shared<int>(30);
std::weak_ptr<int> weakPtr = sharedPtr;
std::cout << *sharedPtr << " " << *weakPtr.lock() << std::endl;  // 输出：30 30

// 强转
std::shared_ptr<int> ptr = weakPtr.lock();
if(prt){// 强转成功则使用资源}
   ```

### 9.1.5 定制删除器

智能指针默认的删除器是直接delete ptr

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318110805454.png" alt="image-20240318110805454" style="zoom:67%;" />

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318110753422.png" alt="image-20240318110753422" style="zoom:67%;" />

传入一个实现删除的==仿函数==指针进去

智能指针，默认调用delete析构

当new数组、malloc等创建指针，不能通过delete析构，则定制删除器

## 9.2 nullptr

`nullptr` 是 C++11 引入的新关键字，用于表示空指针常量。它是一个特殊的字面值，可以隐式转换为任意类型的空指针。使用 `nullptr` 可以明确表示空指针，避免了空指针与整数类型的混淆。

```cpp
int* ptr = nullptr; // 使用 nullptr 初始化指针

```

`NULL` 是在 C 中使用的宏，它通常被定义为整数 0。在 C++ 中也可以使用 `NULL` 来表示空指针，但它的类型实际上是 `int`，因此在一些情况下可能会引发类型不匹配的问题。

```cpp
int* ptr = NULL; // 使用 NULL 初始化指针

```

## 9.3 函数返回值尾置

* 前置

  ```cpp
  int getValue()
  {
  	return 20;
  }
  ```

* 后置

  ```cpp
  auto getValue()->int 
  {
  	reurn 20;
  }
  ```
  
## 9.4 移动语义

* 移动语义主要适用于自定义的类型，其中移动操作可以显著减少资源的拷贝成本。

* 当需要将一个对象转移到一个新的智能指针或容器中时，可以使用移动语义来避免不必要的拷贝操作，提高性能和效率。

* 右值引用变量不再拥有原始资源的所有权。资源的所有权已经转移到其他对象（如移动赋值目标），因此在使用右值引用之后，我们应该小心避免对其进行访问，以免出现悬空引用或无效操作。

* 左值和右值是C++中非常重要的概念，理解它们有助于更好地理解语言的基本语义和编程模型。下面将详细解释左值和右值的用法，并提供示例来帮助你学习它们。

### 9.4.1 左值和右值

**左值（Lvalue）：**

  内存中有地址，可以修改的值

  1. **变量：** 变量是最常见的左值，因为它们具有名称，可以用于存储和修改值。
    
     ```cpp
     int x = 10; // x 是左值
     int y = 20;
     int c = x + y; // x+y为右值，c为左值
     ```
     
  2. **数组元素：** 数组元素也是左值，因为它们可以通过索引修改。
     ```cpp
     int arr[5] = {1, 2, 3, 4, 5};
     arr[0] = 42; // arr[0] 是左值
     ```

  3. **引用：** 引用也是左值，因为它们是变量的别名，可以用于修改原始变量的值。
    
     ```cpp
     int y = 20;
     int& ref = y; // ref 是左值，可以修改 y 的值
     int && ref2 = std::move(y) // ref2 是左值
     ref = 30; // 修改了 y 的值
     ```
     
  4. **函数返回的左值：** 如果函数返回的是一个具体的值（而不是临时对象或表达式的结果），那么它是左值。
    
     ```cpp
     int getValue() {
         return 100;
     }
     int result = getValue(); // result 是左值
     ```

  **右值（Rvalue）：**

* 没有内存地址，无法修改值

* 纯右值 ： 基本类型的常量或者临时对象
* 将亡值： 自定义类型的临时对象

  右值是临时的、不可修改的值，通常表示计算结果或临时对象。右值是可以放在赋值运算符的右边的值。右值通常用于初始化变量或作为函数参数。

  1. **字面常量：** 字面常量是右值，因为它们是固定的、不可修改的值。
    
     ```cpp
     int a = 42; // 42 是右值
     ```
     
  2. **函数的返回值（临时对象）：** 当创建临时对象时，它们通常是右值。
    
     ```cpp
     std::string getName() {
         return "Alice";
     }
     std::string greeting = "Hello, " + getName(); // "Hello, Alice" 是右值
     ```
     
  3. **表达式的返回值（临时对象）：** 复杂表达式的结果通常是右值，因为它们是计算的临时值。
    
     ```cpp
     int sum = 5 + 3; // (5 + 3) 是右值
     ```
     
  4. **`std::move` 返回的右值引用：** `std::move` 函数将左值转换为右值引用，返回的是右值引用。
     ```cpp
     int x = 42;
     int&& rvalueRef = std::move(x); // std::move(x) 是右值， rvalueRef是右值引用，但是本身为左值，可以修改x
     ```

  左值和右值在C++中的区分非常重要，因为它们在赋值、传递参数、函数返回值和移动语义等方面具有不同的语义。理解它们有助于编写更安全和高效的C++代码。

### 9.4.2 左值引用、右值引用

**左值引用**

```cpp
int a = 10;
int &b = a;
0035421F  lea         eax,[a]  // 将a的地址传给寄存器eax 
00354222  mov         dword ptr [b],eax // 将eax的值传给b
```

**为什么左值引用右值报错？**

```cpp
int &b = 10; //报错
```

因为立即数没有地址，无法传给eax寄存器

**解决**

* 使用const引用

```cpp
const int& b = 10;
// 创建临时变量tmp，含有地址，将地址传给b
010517C8  mov         dword ptr [ebp-14h],14h    《= ebp-14h就是内存栈上产生的临时量的内存地址
010517CF  lea         eax,[ebp-14h]   《= 取临时量的内存地址放入寄存器eax
010517D2  mov         dword ptr [b],eax  《= 再把eax寄存器的值（放的是临时量地址）存入b中

```









2. const左值引用可以引用右值（常量）

```cpp
const int &a = 10;
const int &b = x + y;
```

1. **右值引用**大部分引用右值

```cpp
int &&a = 10;
int &&b = x + y;
```

2. 通过move语义可以引用左值

```cpp
int &&c = move(a);
```

### 9.4.3 比较

| 类型                       | a                    | b    |
| -------------------------- | -------------------- | ---- |
| 左值引用                   |                      |      |
| 右值引用                   |                      |      |
| `void func(int a);`        | 传值拷贝             |      |
| `int func(){return val}`   | 传值返回             |      |
| `void func(const int& a);` | 传参过程中，减少拷贝 |      |
|                            |                      |      |

左值引用：

1. 做参数：减少传参时的拷贝
2. 做返回值：返回自身，减少拷贝

右值引用：

* 用来写类的**移动构造**和**移动赋值**，进而在类的使用过程中，减少拷贝次数

1. 做参数：减少传参时的拷贝，==右值引用传参时，不加const，允许对临时对象进行操作和转移资源==
2. **函数内：通过调用移动构造，减少拷贝次数**
3. 做返回值：返回自身，减少拷贝
4. 移动赋值、减少拷贝次数

![image-20240311173514030](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240311173514030.png)

### 9.4.4 右值引用的应用（2个）

1. **类的移动拷贝和移动赋值**

```cpp
class string
 {
 string(const char* str = "")
     :_size(strlen(str))
     , _capacity(_size)
     {
         //cout << "string(char* str)" << endl;
         _str = new char[_capacity + 1];
         strcpy(_str, str);
     }
 // s1.swap(s2)
 void swap(string& s)
 {
     ::swap(_str, s._str);
     ::swap(_size, s._size);
     ::swap(_capacity, s._capacity);
 }
 // 拷贝构造
 string(const string& s)
 	:_str(nullptr)
     {
         cout << "string(const string& s) -- 深拷贝" << endl;
         string tmp(s._str);
         swap(tmp);
     }
 // 赋值重载
 string& operator=(const string& s)
 {
     cout << "string& operator=(string s) -- 深拷贝" << endl;
     string tmp(s);
     swap(tmp);
     return *this;
 }
 // 移动构造
 string(string&& s)
     :_str(nullptr)
     ,_size(0)
     ,_capacity(0)
     {
         cout << "string(string&& s) -- 移动语义" << endl;
         swap(s);
     }
 // 移动赋值
 string& operator=(string&& s)
 {
     cout << "string& operator=(string&& s) -- 移动语义" << endl;
     swap(s);
     return *this;
 }

void push_back(T && val){
    allocator_.construct(vec_ + idx_, std::move(val));
    idex_++;
}
```

2. * 模板父函数通过万能引用和完美转发接收参数
   * 子函数函数重载 左值引用和右值引用

   ```cpp
   // 模板父函数
   template<class T>
   void PushBack(T&& x)
   {
       //Insert(_head, x);
       Insert(_head, std::forward<T>(x));
   }
    void PushFront(T&& x)
    {
        //Insert(_head->_next, x);
        Insert(_head->_next, std::forward<T>(x));
    }
   
   // 子函数重载
    void Insert(Node* pos, T&& x)
    {
        Node* prev = pos->_prev;
        Node* newnode = new Node;
        newnode->_data = std::forward<T>(x); // 关键位置
        // prev newnode pos
        prev->_next = newnode;
        newnode->_prev = prev;
        newnode->_next = pos;
        pos->_prev = newnode;
    }
    void Insert(Node* pos, const T& x)
    {
        Node* prev = pos->_prev;
        Node* newnode = new Node;
        newnode->_data = x; // 关键位置
        // prev newnode pos
        prev->_next = newnode;
             newnode->_prev = prev;
        newnode->_next = pos;
        pos->_prev = newnode;
    }
   
   
   ```

   

### 9.4.4 万能引用和完美转发

**问题**

```cpp
void foo(T &&val){ use val;};
// 当传参为右值时候，调用函数foo
// 函数体内部使用val时候，val为左值，因为val此时有变量名，有地址
// 所以内部需要保持val的右值属性
void foo(T &&val){ use std::move(val)};
```



| 传参引用类型                                 | 保证右值属性                     |
| -------------------------------------------- | -------------------------------- |
| 右值引用：`void foo(T &&)`                   | 移动语义：`std::move(val)`       |
| 万能引用：`template<class T> void foo(T &&)` | 完美转发：`std::forward<T>(val)` |



[完美转发参考pdf](E:\typora索引文件\c++\C++进阶课件\Lesson06--C++11.pdf)

**万能引用**是一种特殊类型的引用，它可以接受任意类型的值，包括左值和右值。

在C++中，万能引用通常使用`&&`符号来声明，就像右值引用一样。

万能引用通常与模板一起使用，例如：

```cpp
template<typename T>
void foo(T&& t) {
    // ...
}
```

在这个例子中，`T&&`就是一个万能引用。这个函数模板`foo`接受一个参数`t`，它可能是左值也可能是右值。在函数体内部，你可以根据`t`的具体类型来决定如何处理它。

万能引用通常与模板推导结合使用，这意味着编译器会根据传递给函数的实参类型来推导出`t`的类型。如果传递给`foo`的是左值，`T`会被推导为左值引用类型；如果传递给`foo`的是右值，`T`会被推导为非引用类型。

**完美转发**：右值引用在第二次传参的过程中，右值属性会消失，因此需要完美转发 `std::forward<T>(t)`来保持属性不变

```cpp
void Fun(int &x){ cout << "左值引用" << endl; }
void Fun(const int &x){ cout << "const 左值引用" << endl; }
void Fun(int &&x){ cout << "右值引用" << endl; }
void Fun(const int &&x){ cout << "const 右值引用" << endl; }

// 1 主函数，通过万能引用接收参数，自动推断为左右值引用
template<typename T>
void PerfectForward(T&& t)
{
    // 2 左值引用调用左值对应的函数，右值引用调用右值的函数，使用完美转发保持右值属性，否则属性失效，全部调用左值函数
 	Fun(std::forward<T>(t));
}
int main()
{
     PerfectForward(10);           // 右值
     int a;
     PerfectForward(a);            // 左值
     PerfectForward(std::move(a)); // 右值
     const int b = 8;
     PerfectForward(b);      // const 左值
     PerfectForward(std::move(b)); // const 右值
     return 0;
}

```

## 9.5 emplace

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318110833902.png" alt="image-20240318110833902" style="zoom:67%;" />

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318110845720.png" alt="image-20240318110845720" style="zoom:67%;" />

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318110858550.png" alt="image-20240318110858550" style="zoom:67%;" />

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318110911263.png" alt="image-20240318110911263" style="zoom:67%;" />

| 类型         | 相同                                           | 差异                                                         |
| ------------ | ---------------------------------------------- | ------------------------------------------------------------ |
| push_back    | 插入左值对象、右值对象 调用 拷贝构造和移动拷贝 |                                                              |
| em[lace_back | 插入左值对象、右值对象 调用 拷贝构造和移动拷贝 | 直接传入参数，调用默认构造在vector内部直接创建对象，减少了拷贝 |







## 9.5 枚举类型

* 在函数内部定义，作用域只存在函数内部
* 避免使用不同的整数值或字符串来表示着色器类型，提高了代码的可读性和维护性

```cpp
enum class ShaderType {
        NONE = -1, VERTEX = 0, FRAGMENT = 1
    };

// 需要通过枚举类型来访问
ShaderType type = ShaderType::NONE;
```

## 9.6 auto、范围for

【范围for原理】：

* 编译器将范围fot 替换为 迭代器
* 支持迭代器的容器即支持范围for

```cpp
int array[3] = {1, 2, 3 };
for(auto& e : array)
     e *= 2;

```

## 9.7 初始化列表

### 9.7.1 {}初始化

* 在C++98中，标准允许使用花括号{}对数组或者结构体元素进行统一的列表初始值设定

```cpp
int array1[] = { 1, 2, 3, 4, 5 };
Point p = { 1, 2 };

```

* C++11扩大了用大括号括起的列表(初始化列表)的使用范围，使其可用于所有的**内置类型**和**用户自定义**的类型，使用初始化列表时，可添加等号(=)，也可不添加。

```cpp
int array1[] = { 1, 2, 3, 4, 5 };
int array2[]{ 1, 2, 3, 4, 5 };
```

* 创建对象时也可以使用列表初始化方式调用构造函数初始化

```cpp
Date(int year, int month, int day)
 :_year(year)
 ,_month(month)
 ,_day(day)
 {}
```

### 9.7.2 initializer_list

* 该数据结构用来存储花括号内的值

```cpp
std::initializer_list ilt = { 10, 20, 30 }
```

【面试题】设计vector可以通过初始化列表初始化（通过花括号初始化）

1. 将花括号内的值通过initializer_list接收
2. 将initializer_list的值逐一赋给vector
3. 具体代码见vector章节

```cpp
template <class T>
myvector(std::initializer_list<T> il) 
: _start(new T[il.size()])
    , _finish(_start + il.size())
    , _end_of_storage(_start + il.size())
{
    iterator it = _start;
    for (auto& e : il) {
        *it++ = e;
    }
    
}
```

## 9.8 类型推导

* 获取变量类型

```cpp
vector<int > v1;
cout << typeid(v1).name() << endl;
```

* 定义同类型变量

```cpp
decltype(v1) v2;
```

## 9.9 类控制函数（default delete）

```cpp
class A{
    A() = default;  // 存在拷贝函数，则默认构造失效，通过显示指定
    A(const A& aa) = delete; // 通过关键字设置，不能拷贝该类对象
private:
    int _a;
}
```

## 9.10 绑定器

### 9.10.1 bind1st

函数对象 = 仿函数，即重载了operator()的对象

绑定器：bind，可以将二元函数对象变为一元函数对象

二元函数对象：仿函数内传入两个参数，比如greater仿函数

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318110911263.png" style="zoom:67%;" />

```cpp
// bind1st : 将二元参数函数的第一个形参变为固定值,
bind1st(greater<int>()，70);
// bind2nd : 将二元函数对象的第二个形参变为固定值
bind2nd(greater<int>()， 70);
```





---------

```cpp
// 需求：按顺序大小，在vector中插入70
// 解决：利用bind和仿函数
auto it = find_if(vec.beging(), vec.end(), bind1s(greater<int>(),70 ));
if(it != vec.end()) vec.insert(70);
```

### 9.10.2 bind

1. bind用于给函数传递参数,bind返回的是一个函数对象（仿函数）,通过调用ioerator()使用
2. 只能在语句中使用，语句完之后需要重新再写

```cpp
#include <functional>

void hello(std::string str) {
	std::cout << str << std::endl;

}
int msum(int x, int y) {
	return x + y;
}

class Test {
public:
	int msum(int x, int y) {
		return x + y;
	}
};
int main() {
	std::bind(hello, "hello boy")();
	std::cout << std::bind(msum, 10, 20)() << std::endl;
	// bind成员函数需要使用类对象，即Test（）一个对象
	std::cout << std::bind(&Test::msum, Test(), 10, 20)() << std::endl;
	return 0;
}
```

3. 通过function保存函数对象，重复调用

```cpp
std::function<void(std::string)> func1 = std::bind(hello, std::placeholders::_1);
func1("hha");
```

```cpp
std::function<返回值类型(参数类型)> func = std:: bind(函数，占位符1，占位符2);
func(参数1，参数2)
```

### 9.10.3 占位符

```cpp
 std::bind(msum, std::placeholders::_1, std::placeholders::_2)(10,20);
```

1. 绑定器最多可以绑定20个参数
2. 可使用`using namespace placeholders`代替命名空间





## 9.11 lambda匿名函数

* 也成为lambda函数
* 将函数定义和使用放在一起

### 9.11.1 定义

```
// 定义
auto result = []() -> 返回值类型 { };

// 使用
[](){} ();
```

* [] ： 捕获列表，标志lambda表达式的开始，不能省略

​                参数：=  表达式可以使用所在作用域内声明好的变量，值传递  （==常用==）    ==可读==、可修改静态变量

​						    &  表达式可以使用所在作用域内声明好的变量，引用传递    ==可修改==

​							a   表达式可以使用变量a,值传递

​							&a   表达式可以使用变量a,引用传递

* （）：参数列表，载入结构体所用参数，可以省略

### 9.11.2 使用

```cpp
// 只用到参数列表，[]不可省略
auto result = [] (int a, int b) { return a + b; }(3, 4);
```

```cpp
// 用到捕获列表，（）可以省略
[&pool]{}; // 引用传递
[pool]{}; // 值传递
[mypool = pool]{}; // 值传递

```

### 9.11.3 原理

![image-20240226115750005](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240226115750005.png)



## 9.12 线程库

### 12.1 成员函数

[线程池网页](https://cplusplus.com/reference/thread/thread/)

![image-20240228145051199](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240228145051199.png)

```cpp
// thread example
#include <iostream>       // std::cout
#include <thread>         // std::thread
 
void foo() 
{
  // do stuff...
}

void bar(int x)
{
  // do stuff...
}

int main() 
{
  std::thread first (foo);     // spawn new thread that calls foo()
  std::thread second (bar,0);  // spawn new thread that calls bar(0)

  std::cout << "main, foo and bar now execute concurrently...\n";

  // synchronize threads: 子线程关闭，主线程关闭
  first.join();                // pauses until first finishes
  second.join();               // pauses until second finishes

  std::cout << "foo and bar completed.\n";

  return 0;
}
```

### 12.2 启动多线程

```cpp
// m个线程对x自增n次
#include <iostream>
#include <vector>
#include <thread>
#include <atomic>
using namespace std;
int main() {
    int m, n;
    std::atomic<int> x = 0;
    cin >> m >> n ;
    std::vector<thread> v(m);
    for (int i = 0; i < m; ++i) {
        v[i] = thread([&x](int count) {
            for (int j = 0; j < count; ++j) {
                ++x;
            }
            }, n);
    }

    for (auto& t : v) {
        t.join();
        cout << t.get_id() << ".join()" << endl;
    }

    cout << x << endl;
    system("pause");
    return 0;
}
```

### 12.3 锁

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318111012823.png" alt="image-20240318111012823" style="zoom:67%;" />

```cpp
void f(){
	mutex mtx;
    mtx.lock();
    
    // ..  抛异常，直接退出，未解锁
    mtx.unlock();
}
int main(){
    try{
        f();
    }
    catch(exception& e){
        ...
    }
}
```

1. 抛异常导致死锁问题
2. 利用RAII思想解决：构造函数保存资源，析构函数自动释放

```cpp
template<class Lock>
class lock_guard{
    public:
    lock_guard(Lock& lk) : _lock(lk){
        _lock.lock();  // 自动上锁
    }
    ~lock_guard(){
        _lock.unlock(); // 自动解锁
    }
    private:
    Lock &_lock; // 锁不能拷贝，使用引用，即_lock是外部lk的别名
}
```

```cpp
#include <iostream>       // std::cout
#include <mutex>          // std::mutex, std::lock_guard

std::mutex mtx;
std::lock_guard<std::mutex> lck (mtx);

```

```cpp
//lock_guard  创建即上锁
// unique_lock 创建即上锁，也可以自己上锁解锁 
```

3. 通过局部作用域{}, 可以控制上锁和解锁的时机

### 9.12.4 条件变量

* wait的两种重载

```cpp
void wait (unique_lock<mutex>& lck);
// 当满足pred条件时候，解锁，一般传入一个返回bool的匿名函数
template <class Predicate>  void wait (unique_lock<mutex>& lck, Predicate pred);
```



```cpp
condtion_variable notFull;
// 自动上锁
std::unique_lock<std::mutex> lock(mtx_);
// 线程通信，队列不满时提交任务，否则wait
notFull_.wait(
    lock,
    [&]()->bool {return taskQue_.size() < taskQueMaxshreshHold_;}
);
```

* wait_for

```cpp
// 当时间超过时仍继续wait，则返回
if (!notFull_.wait_for(
		lock,
		std::chrono::seconds(1),
		[&]()->bool {return taskQue_.size() < taskQueMaxshreshHold_;}
	)) {
		std::cerr << "超时，task提交失败" << std::endl;
		return;
	}
```



## 9.13 异常

[参考学习文档](E:/typora索引文件/c++/C++进阶课件/Lesson07--异常.pdf)

## 9.14 using关键字

`using` 和 `typedef` 都可以用来创建类型别名，但它们之间有几个重要的区别：

1. **语法：**
   - `typedef` 是 C++ 的传统方式，它的语法相对较为复杂，容易引起误解。
   - `using` 是 C++11 引入的新特性，它的语法更加清晰、直观，更容易理解和使用。

2. **模板支持：**
   - `using` 支持模板，**可以创建模板别名**，使得代码更加灵活。
   - `typedef` 不能直接创建模板别名。

3. **范围：**
   - 在命名空间、类、结构体等范围内，`using` 更为灵活，可以定义局部别名，而 `typedef` 则不能在局部范围内使用。
   - `typedef` 只能在全局范围或者类内部使用。

4. **可读性和易用性：**
   - 由于语法的简洁和清晰，以及对模板的支持，`using` 更易读、易用，是更加现代化的选择。
   - `typedef` 的语法较为复杂，不够直观，可能会导致一些误解或错误的使用。

示例比较：

```cpp
// 使用 using
using MyInt = int;
using FuncPtr = void(*)(int);
using ThreadFunc  = std::functhion<void()>;
// 使用 typedef
typedef int MyInt;
typedef void(*FuncPtr)(int);
```

虽然在功能上它们是相同的，但是在 C++11 及以后的版本中，推荐使用 `using` 关键字来创建类型别名，因为它更加现代化、清晰和灵活。

## 9.15 packaged_task

* 用来包装一个任务函数，并允许在异步执行完函数后，获取返回结果
* jie'he

```cpp
#include <iostream>
#include <future>

int main() {
    // 创建一个 std::packaged_task，包装一个 Lambda 表达式
    std::packaged_task<int(int)> task([](int x) { return x * x; });

    // 获取与任务关联的 std::future 对象
    std::future<int> future = task.get_future();

    // 异步执行任务
    task(42);

    // 获取任务的结果
    int result = future.get();

    std::cout << "Result: " << result << std::endl;

    return 0;
}
```



# 十 设计模式

## 10.1 单例模式

单例模式是一种创建型设计模式，它确保一个类只有一个实例，并提供一个全局访问点以访问该实例。

在单例模式中，类的构造函数被限制为私有，这样外部代码就无法直接实例化该类。而通过提供一个静态方法或静态变量来访问类的实例，可以控制实例的创建和访问方式。

单例模式的主要目的是：

1. 保证类只有一个实例，节省系统资源。
2. 提供一个全局的访问点，方便其他对象获取该实例。
3. 控制实例化过程，确保所有对该类实例的访问都经过统一的接口。

常见的单例模式实现方式有两种：

1. 饿汉式单例：在类加载时就创建实例，并通过静态方法返回该实例。在多线程环境下，饿汉式单例可以保证线程安全，但可能会提前创建实例，造成资源浪费。
2. 懒汉式单例：在首次访问时才创建实例，并通过静态方法返回该实例。懒汉式单例在多线程环境下需要考虑线程安全的实现，常见的方式是使用双重检查锁或者静态内部类。
3. 线程安全：懒汉中，没有初始化静态指针，在调用时候，多个线程可能同时进行初始化
4. 解决方案：  加锁

单例模式适用于以下情况：

1. 需要保证一个类只有一个实例，并且该实例需要被全局访问。
2. 需要控制某个资源的共享访问，例如数据库连接池、线程池等。
3. 需要对实例化过程进行严格控制，确保所有的访问都经过同一个实例。

然而，单例模式也有一些缺点：

1. 可能会造成全局状态的问题，因为单例对象对于整个应用程序是全局可见的，任何地方都可以访问和修改它。
2. 单例对象的生命周期会比较长，可能会导致资源的长时间占用。
3. 单例对象的扩展和测试相对困难，因为它们的创建和使用过程被封装在单例类中。

因此，在使用单例模式时需要慎重考虑，并根据具体的场景和需求进行合理的设计和实现。

### 10.1.1 饿汉模式

在程序启动时就创建单例对象，并在需要使用时直接返回该对象。

```cpp
Sqlconpool{
public:
    static Sqlconpool *getInstance(){
        return ptr;
    }
}
private:
    // 私有构造函数，禁止外部创建对象
    Sqlconpool(){}
    static Sqlconpool *instance ;  // 静态成员变量指针，类唯一且共享，用来指向保存单例对象

//类外初始化
Sqlconpool ::instance = new Sqlconpool;
```

### 10.1.2 懒汉模式

* 在第一次使用时创建单例对象，可以延迟对象的创建。

* 注意线程安全问题

1. 构造函数全部私有，提供获取单例模式接口
2. 获取单例、释放单例注意线程安全
3. 提供GC类，实现程序结束后自动释放

```cpp
#include <mutex>

class Singleton{
public:
    // 唯一接口获取范例
    static Singleton* getSingle(){
        if(singlePtr == nullptr){   // 双重判断
            unique_lock<mutex> lock(mtx_);
            if(singlePtr ==nullptr){
                singlePtr = new Singleton();
            }
        }
        return singlePtr;
    }
    
    // 手动调用析构
    static void delInstance{
        unique_lock<mutex> lock (mtx_);
        if(singlePtr) delete singlePtr;
        singlePtr = nullptr;
    }
    
    // 程序结束后，使用类来析构
    class CGarnp{
    public:
        ~CGarnp(){
            Singleton::delInstance();
        }
    }
private:
    // 构造函数私有
    singleton(){};
    singleton(const singleton&) = delete;
    singleton& operator=(const singleton&)=delete;
    
    
    static Singleton* singlePtr_; // 单例对象指针
    static std::mutex mtx_;
    
}
Singleton* Singleton::singlePtr_ = nullptr;
std::mutex Singleton::mtx_;
static Singleton::CGarbo Garbo;
```





![image-20240304104911798](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240304104911798.png)



# 十一 优化操作

## 11.0 编译源代码

1.gcc是GNU Compiler Collection（就是GNU编译器套件），也可以简单认为是编译器，它可以编译很多种编程语言（括C、C++、Objective-C、Fortran、Java等等）。

2.当你的程序只有一个源文件时，直接就可以用gcc命令编译它。

3.但是当你的程序包含很多个源文件时，用gcc命令逐个去编译时，你就很容易混乱而且工作量大

4.所以出现了make工具
make工具可以看成是一个智能的批处理**工具**，它本身并没有编译和链接的功能，而是用类似于批处理的方式—通过调用makefile文件中用户指定的命令来进行编译和链接的。

5.makefile是什么？简单的说就像一首歌的**乐谱**，make工具就像**指挥家**，指挥家根据乐谱指挥整个乐团怎么样演奏，make工具就根据makefile中的命令进行编译和链接的。

6.makefile命令中就包含了调用gcc（也可以是别的编译器）去编译某个源文件的命令。

7.makefile在一些简单的工程完全可以人工手下，但是当工程非常大的时候，手写makefile也是非常麻烦的，如果换了个平台makefile又要重新修改。

8.这时候就出现了Cmake这个工具，**cmake就可以更加简单的生成makefile文件给上面那个make用**。当然cmake还有其他功能，就是可以跨平台生成对应平台能用的makefile，你不用再自己去修改了。

9.可是cmake根据什么生成makefile呢？它又要根据一个叫CMakeLists.txt文件（学名：组态档）去生成makefile。

10.到最后CMakeLists.txt文件谁写啊？亲，是你自己手写的。

11.当然如果你用IDE，类似VS这些一般它都能帮你弄好了，你只需要按一下那个三角形

12.cmake是make maker，生成各种可以直接控制编译过程的控制器的配置文件，比如makefile、各种IDE的配置文件。
13.make是一个简单的通过文件时间戳控制自动过程、处理依赖关系的软件，这个自动过程可以是编译一个项目

### 1 CMake

附件位置：`3.first_cmake`

```cpp
# 第一步：配置，-S 指定源码目录，-B 指定构建目录，在build目录下生成makefile文件及其配置文件
cmake -S . -B build 
```

![image-20231115113628228](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20231115113628228.png)

```
# 第二步：生成，--build 指定Makefile文件的位置，也可以直接使用make命令
cmake --build build
```



![image-20231115113736698](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20231115113736698.png)

```
# 运行
./build/first_cmake
```

### 2 linux编译动态库

```shell
g++ -fPIC -shared test.cpp -o libtest.so
```

- `g++`: 这是 GNU C++ 编译器的命令。
- `-fPIC`: 这个选项告诉编译器生成位置无关的代码，通常在生成共享库时需要使用。
- `-shared`: 这个选项告诉编译器生成一个共享库，而不是可执行文件。
- `test.cpp`: 这是你的源代码文件。
- `-o libtest.so`: 这个选项指定生成的共享库的输出文件名为 `libtest.so`。

这个命令将会编译 `test.cpp` 文件为一个名为 `libtest.so` 的共享库，你可以通过动态链接这个库到其他程序来使用其中的函数和功能

-------------

1. 主函数编译的时候，会从指定位置寻找所需要的头文件和库文件

2. 将编译好的动态库放入指定文件夹

3. ```shell
   mv libtest.so /usr/local/lib
   mv test.h /usr/local/include
   ```

---------

* 编译主文件 `-l`选项链接上库文件，库文件去掉`lib`开头和`.so`结尾

* 编译阶段从 `/usr/local/lib`寻找动态库

  ```shell
  g++ main.cpp -o main -ltest
  ```

* 执行阶段从`/etc/ld.so.conf.d`中，寻找动态库的路径`/usr/local/lib`，再根据路径寻找动态库

* 添加动态库路径：创建mylib.conf文件，在文件中添加动态库地址

  ```shell
  ./main
  ```

  

## 11.1 argc、argv

如果你的命令行有三个参数，你可以在`main`函数中使用`int`类型的三个参数来接收它们。以下是一个简单的例子：

```cpp
#include <iostream>

int main(int argc, char *argv[]) {
    // 确保有足够的参数
    if (argc != 4) {
        std::cerr << "Usage: " << argv[0] << " <arg1> <arg2> <arg3>" << std::endl;
        return 1;  // 返回非零值表示程序执行失败
    }

    // 将命令行参数转换为整数
    int arg1 = std::stoi(argv[1]);
    int arg2 = std::stoi(argv[2]);
    int arg3 = std::stoi(argv[3]);

    // 执行你的程序逻辑
    std::cout << "Sum of arguments: " << arg1 + arg2 + arg3 << std::endl;

    return 0;
}
```

在这个例子中，程序期望有三个命令行参数，并将它们转换为整数。如果参数数量不正确，程序会输出用法信息并返回一个非零值，表示程序执行失败。

例如，如果你运行程序 `./myprogram 1 2 3`，程序会输出：

```
Sum of arguments: 6
```

请注意，`std::stoi` 是一个用于将字符串转换为整数的标准库函数。如果你的参数不是整数，或者无法成功转换为整数，这个函数可能会抛出`std::invalid_argument`或`std::out_of_range`异常。在实际应用中，你可能需要添加适当的错误处理机制。



## 11. 2  #if 0 注释

`#if 0`, `#else`, 和 `#endif` 是C和C++中的预处理指令，用于条件编译（Conditional Compilation）。

1. **`#if 0`：**
   - 这是一个条件为假的预处理指令。任何位于 `#if 0` 和 `#endif` 之间的代码块都会被视为注释，不参与编译。这是一种暂时注释掉一块代码而不删除它的常见方法。

2. **`#else`：**
   - 如果 `#if` 后面的条件为假，则执行 `#else` 后面的代码块。这是用于在条件不满足时执行另一块代码的指令。

3. **`#endif`：**
   - 用于结束一个条件编译块。任何位于 `#if` 和 `#endif` 之间的代码，或者在 `#else` 和 `#endif` 之间的代码，都会在条件为真时编译，而在条件为假时被忽略。

这些条件编译指令通常用于在编译时选择性地包含或排除一些代码块，以便根据不同的编译配置生成不同的可执行文件。在你的提到的代码片段中，`#if 0` 之间的代码块是被注释掉的，而 `#else` 后面的代码块是生效的，这样就可以在不删除任何代码的情况下，选择性地启用或禁用不同的处理逻辑。

# --------------------------

#  八股

1 main函数的执行流程

在C++程序中，`main`函数是程序的入口点，是程序执行的起始函数。`main`函数的执行流程如下：

1. **Program Startup**: 当你运行一个C++程序时，操作系统会创建一个进程，并加载该程序的可执行文件。然后，操作系统会在该进程的虚拟地址空间中设置一些运行时环境和栈空间。

2. **调用main函数**: 接下来，程序执行会从`main`函数开始。`main`函数是C++程序的入口函数，程序会从`main`函数的第一条语句开始执行。

3. **局部变量和对象的初始化**: 

   在进入`main`函数之前，

   全局变量和静态变量会被初始化。

   全局对象初始化，即数据段

   未初始化部分的全局变量赋初值：数值型`short`，`int`，`long`等为`0`，`bool`为`FALSE`，指针为`NULL`等等，即`.bss`段的内容

   将main的参数argc argv传入main

   然后，`main`函数内部的局部变量和对象（如类的实例）也会被初始化。注意，局部变量的初始化是在运行时进行的。

​		执行main之后，全局对象析构函数

1. **执行main函数体**: `main`函数体中包含的语句会按照顺序依次执行，从第一条语句一直到函数的最后一条语句。程序将按照代码逻辑执行操作，包括控制流语句（如`if`、`while`、`for`等）和函数调用。
2. **返回值**: 如果在`main`函数中指定了返回值，程序执行到`return`语句时，将会返回相应的值。通常情况下，`main`函数的返回值为整数类型，表示程序的执行结果状态。
3. **Program Termination**: `main`函数执行结束后，程序会继续执行一些清理工作。它会关闭已打开的文件、释放动态分配的内存等资源。然后，操作系统会终止该进程，并将程序的退出状态返回给父进程或操作系统。

注意：`main`函数是C++程序的唯一入口，所有其他函数的调用都是通过`main`函数或其他函数间接调用的。当`main`函数返回时，程序的生命周期也就结束了。



2. 虚拟空间的构成

虚拟空间（Virtual Address Space）是操作系统为每个进程提供的抽象地址空间，它使得每个进程感觉自己拥有独立的地址空间，而不受其他进程的影响。虚拟空间的构成包括以下几个部分：

1. **代码段（Text Segment）**：也称为只读段，存放程序的机器代码（即编译后的可执行代码）。这个部分通常是只读的，以防止程序意外地修改自身的指令。

2. **数据段（Data Segment）**：存放已初始化的全局变量、静态变量和常量。在程序启动时，这些变量会被初始化为预定义的值。

3. **BSS段**：存放未初始化的全局变量和静态变量。在程序启动时，BSS段中的变量会被初始化为零或者空值。

4. **堆（Heap）**：用于动态分配内存。程序可以在堆上请求额外的内存，用于存储数据结构、对象或其他需要动态分配的数据。在C++中，使用`new`和`delete`关键字来管理堆上的内存。

5. **栈（Stack）**：用于存储函数调用时的局部变量、函数参数和函数返回地址等。栈是一种后进先出（LIFO）的数据结构，它会自动管理函数调用和返回过程中的内存分配和释放。

6. **共享库和动态链接库区域**：这部分用于存放共享库（Shared Libraries）或动态链接库（Dynamic Linking Libraries），以便多个进程可以共享这些库的代码和数据，节省内存空间。

7. **内核空间**：这是保留给操作系统内核使用的区域，用户程序无法直接访问这个区域。

虚拟空间的构成使得每个进程可以独立运行，且不会干扰其他进程的内存空间。实际的物理内存映射到虚拟地址空间是由操作系统的内存管理单元（Memory Management Unit，MMU）来完成的。MMU通过将虚拟地址转换为物理地址，实现了虚拟空间到物理内存的映射。

==1:两个int数相加实现，需要考虑什么？如何快速判断溢出？==

![image-20230814102714275](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20230814102714275.png)

==2.:值为-1的数据在断点调试时，显示的值是多少？在内存中是如何显示的？==

![image-20230814103523663](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20230814103523663.png)

== sizeof()的使用情况 ==

不完全正确。`sizeof`操作符不仅适用于在栈上创建的元素，它也适用于静态分配的元素和全局变量。但是，`sizeof`不适用于动态分配的堆上的元素，因为在堆上分配的内存块大小在编译时是未知的。

具体来说：

1. **栈上的元素**：您可以使用`sizeof`来获取在栈上分配的局部变量、参数和其他栈上的元素的大小。

   ```cpp
   int x;
   size_t size = sizeof(x); // 获取整数x的大小
   ```

2. **静态分配的元素**：全局变量和静态变量是在编译时分配内存的，因此您也可以使用`sizeof`来获取它们的大小。

   ```cpp
   static int y;
   size_t size = sizeof(y); // 获取静态整数y的大小
   ```

3. **动态分配的元素**：对于在堆上分配的内存块，`sizeof`操作符无法提供正确的大小信息，因为堆上的内存大小在运行时才确定。

   ```cpp
   int* ptr = new int[10];
   size_t size = sizeof(ptr); // 返回指针的大小，而不是堆上数组的大小
   ```

总之，`sizeof`可以用于获取在编译时已知大小的变量、数组和对象的大小。但是，对于动态分配的内存块，您需要跟踪分配的大小，通常使用`malloc`、`new`或其他分配函数的参数来记录它们的大小。





## 函数重载

### 1 什么是函数重载？

> c不支持重载，c++支持重载，函数名相同，参数不同，包括参数（类型、个数、顺序）不同，返回值可以相同

----------------------------

### 2 为什么c++支持函数重载，是怎么支持的？

<a name = "编译">跳转</a>

>  预处理  ---->   头文件展开、宏替换、条件编译（处理#if #endif）、去掉注释     test.i
>
>   编译  -------->  检查语法错误  生成汇编语言   test.s
>
>   汇编   -------->  生成机器代码  test.o
>
>   链接   -------->  多个源文件链接在一起，即不同文件的符号表装在一起，符号表内是该文件内定义的函数的地址
>
>   链接错误： 给了声明，汇编过了，但是链接时没找到函数定义
>
>   ==简单说，就是c++编译时候，使用函数名修饰规则，符号表内的函数名不同==
>
>   当调用一个函数的时候，编译阶段会call一个函数的地址，c中的文件符号表内，函数是通过  ==函数名表示，无法重载，而c++中，有函数名修饰规则==，即根据函数名和参数来命名，所以参数不同，名称相同的函数在符号表内的函数名不同，所以可以函数重载



![image-20231204102933313](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20231204102933313.png)

![image-20240318111130498](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318111130498.png)



`objdump -S`: 打印目标文件的链接信息

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318111142031.png" alt="image-20240318111142031" style="zoom:80%;" />



--------------------------

### 3 extern "C"

> 当 c++文件  和 c 文件 都想使用 C++ 编译出的库时候， 由于库是按照c++编译，符号表内的函数名命名规则不同， c++文件可以找到， c确找不到
>
> `extern "c" void *tpmalloc ()`
>
> 1  c++编译库时，按照c编译
>
> 2  c文件使用时，可以找到函数
>
> 3  c++看到extern "c" ，按照c的命名也能找到
>
> 总之， c 使用c++文件， c++使用c文件，都要用extern "c"

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318111156607.png" alt="image-20240318111156607" style="zoom:67%;" />

## 类

### 0 封装

> 将 属性 和 函数完美的结合起来，并加以权限。
>
> 封装允许类的成员函数访问==同类==的其他对象的==私有成员==

### 1 struct 和 class 区别

> C语言结构体中只能定义变量，在C++中，结构体内不仅可以定义变量，也可以定义函数。C++需要兼容C语言，所以C++中struct可以当成结构体使用。另外C++中struct还可以用来 定义类。和class定义类是一样的，区别是struct定义的类默认访问权限是public，class定义的类 默认访问权限是private。

------------

### 2 类的sizeof怎么计算？

> 类的实例化对象只存储==成员变量==，不存储成员方法
>
> 一个类可以实例化N个对象，每个对象可以存储不同的成员变量，但是调用的成员方法都是同一个，浪费空间，因此函数存储到公共的地方==代码区==。
>
> 没有成员变量的类的大小是1,不是为了存数据，而是为了占位，表示对象存在 ，具体大小根据编译器决定，vs中是1个字节
>
> 添加构造和析构函数，不计数，sizeof() 也是1
>
> 若析构函数为虚函数，则编译器添加一个指向虚函数表的指针，32位下4字节，64位下8字节



```cpp
// 内存对齐，sizeof(A) = 8
class A {
    int a;
    char *b
}

// 函数不占字节，sizeof(B) = 4;
class B{
    int a;
    void func();
}

// sizeof(C) = 1
class C{
    void func();
}

// sizeof(D) = 1
class D {
    
}
```

-------------

###  3 结构体内存对齐规则

>一、结构体对齐规则首先要看有没有用*#pragma pack宏*声明，这个宏可以改变对齐规则，有宏定义的情况下结构体的自身宽度就是宏上规定的数值大小，所有内存都按照这个宽度去布局（这样说其实不太严谨，后面会提到），#pragma pack 参数只能是 '1', '2', '4', '8', or '16'。
>
>二、在没有#pragma pack这个宏的声明下，遵循下面三个原则：
>
>1. 第一个成员地址为0。
>
>2. 其他成员变量首地址是 ==对齐数==的整数倍 
>
>​          注意：对齐数 = `min(自己的大小，默认编译器对齐大小)` ，编译器默认的一个对齐数 与 该成员大小的较小值。 VS中默认的对齐      数为8 
>
>3. 结构体总大小为：最大对齐数的整数倍。 
>
>4. 如果嵌套了结构体的情况，嵌套的结构体对齐到自己的最大对齐数的整数倍处，结构体的整 体大小就是所有最大对齐数（含嵌套结构体的对齐数）的整数倍。 
>
>```cpp
>struct test
>{
>  char a;  // 起始位置为0
>  int b;  // 对齐数为4，起始位置为0，4，8.... 本次为4
>  char c;  //对齐数2，起始位置0，2，4，8... 本次为8
>};
>
>// 总大小是最大对齐数的整数倍，即4的倍数，4，8，12， 本次为12
>```
>
><img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318111211124.png" alt="image-20240318111211124" style="zoom:67%;" />
>
>```cpp
>struct test
>{
>  char d[7]; // 7 0~6 
>  double a;// 8 8 ~15 
>  short  b; // 2 16~17 
>  char* c;// 4 20~23  
>};
>// 最大对齐数 8的倍数， 即sizeof=24
>```
>
>
>
>
>【面试题】 
>
>1. 结构体怎么对齐？为什么要进行内存对齐？ 
>
>2. 如何让结构体按照指定的对齐参数进行对齐？能否按照3、4、5即任意字节对齐？
>
>   设置 宏声明`#pragma pack(4)`等，即每个变量都是按照4的倍数对齐
>
>3. 什么是大小端？如何测试某台机器是大端还是小端，有没有遇到过要考虑大小端的场景？

### 4 this指针

>1. this指针的类型：类类型`A * const this`，即成员函数中，不能给this指针赋值。
>2. 只能在“成员函数”的内部使用
>3. this指针==本质上是“非静态成员函数”的形参==，当对象调用成员函数时，将对象地址作为实参传递给 this形参。所以对象中不存储this指针。 
>4. this指针是“非静态成员函数”第一个隐含的指针形参，linux存在==栈==中，vc下一般情况由编译器通过==ecx寄存器==自动传 递，不需要用户传递
>
><img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318111225381.png" alt="image-20240318111225381" style="zoom:67%;" />
>
>```cpp
>// 形参存于栈中，从后往前压入栈，读取时候从前往后
>// &d1，即对象d1的地址在linux也压入栈中，但是在vc处理中，将其传入ecx寄存器
>```
>
>

```cpp
class A {
private:
    int a_;
public:
    void print(){printf _a}; // void print(A *this){printf this->_a};
    void show(){}; // void show(A *this){};
}

int main(){
    A a;
    a.print(); // a.print(&a)   讲本对象的地址传给this指针， 通过this指针访问成员变量
}
```

【面试题】

> 1. this指针存于哪里？ linux在栈中，vc下在寄存器ecx中
>
> 2. this指针可以为空吗？
>
>    分情况，成员函数存放在代码段中，无需访问this，当调用成员函数时，函数需要访问成员变量时，需要访问this所指的地址，这个时候，this不能为空，否则崩溃。
>
>    当调用的成员函数无需访问成员变量时候，不需要访问this所指的地址，这个时候this可以为空
>
> ```cpp
> // 1.下面程序编译运行结果是？ A、编译报错 B、运行崩溃 C、正常运行
> class A
> {
> public:
>     void PrintA() {cout<<_a<<endl;}
>     void show(){};
> private:
> 	int _a;
> };
> int main()
> {
>     A* p = nullptr;
>     p->PrintA();  // p->printA(null) 传入this参数，即地址,继而访问null->_A,程序崩溃
>     p->show(); // p->show(null)，正常运行
>     return 0;
> }
> 
> ```
>
> 

### 5 6个默认的成员函数

<a name = "构造函数">跳转</a>

> 1 **默认构造函数**：（无参的构造函数都是默认构造）3种 编译器默认生成、自定义无参构造、==全缺省构造函数==（建议）
>
> ​								编译器 默认生成的构造函数（双标狗）：不对内置类型处理，调用自定义类型的构造函数
>
> <img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318111237904.png" alt="image-20240318111237904" style="zoom:67%;" />
>
> 2 **析构函数**: 调用自定义类型的析构函数
>
> 3 **拷贝构造**: 编译器默认给出浅拷贝（值拷贝）多次析构会产生问题，需要根据情况是否自定义深拷贝
>
> 4 **赋值运算符重载**：operator=，即 A1 = A2，本质还是浅拷贝构造
>
> 5 **普通对象 和 const对象取地址**

```cpp
// 赋值运算符重载
Data& operator= (const &Data d){
    if(this != &d){
        _year = d._year;
        _day = d._day;
    }
    return *this;  // this存放地址，*this表示对象本身，返回其引用别名，支持连等
}
```

> * 运算符重载
>
> * <img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318111249113.png" alt="image-20240318111249113" style="zoom:67%;" />
>
>   <img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318111300188.png" alt="image-20240318111300188" style="zoom:67%;" />



### 6 浅拷贝和深拷贝

[深拷贝实现](#深拷贝)

**深拷贝问题存在的地方**：总是与指针的拷贝有关

>1. 拷贝构造的传参
>2. 例如vector开辟新空间时，旧空间数据copy到新空间



![image-20231207102946913](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20231207102946913.png)

> st1._a 指向内存空间m1
>
> 浅拷贝是指讲st1的12字节数据 全被拷贝到 st2，数据完全一致，s2._a也指向m1
>
> st1析构时候释放m1，st2析构再次释放m1，程序崩溃，因为同一块内存空间不能释放两次
>
> 解决办法：深拷贝，st2开辟一块新内存m2，存储m1内的内容

![image-20231206145243781](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20231206145243781.png)

拷贝构造传值：无限调用  递归

拷贝构造传引用：使用 cosnt & 必须用引用 （使用）

```cpp
// 自定义深拷贝构造 (传统写法)
mystring(const mystring& str) :
_str(new char[str.size() + 1]), _size(str.size()), _capacity(str.capacity())
{
    strcpy_s(_str, str.size() + 1, str.data());
}

mystring& operator= (const mystring& str) {
    // 确保非自身赋值
    if (this != &str) {
        char* tmp = new char[str.size() + 1];
        memcpy(tmp, str.data(), str.size() + 1);
        delete[] _str;
        _str = tmp;

        _size = str.size();
        _capacity = str.capacity();
        return *this;
    }
}
```

```cpp
void swap(mystring& second) noexcept {
    std::swap(_str, second._str);
    std::swap(_size, second._size);
    std::swap(_capacity, second._capacity);
}

// 自定义深拷贝  (现代写法，狸猫换太子)
// mystring s1(s2)
mystring(const mystring& str) : _str(nullptr), _size(0), _capacity(0)
{
    mystring tmp(str.data()); //太子，开辟堆空间，新的mystring； 在堆空间开辟是在默认构造中定义的。
    this->swap(tmp); // 狸猫换太子，占据tmp的str，其余变量在函数结束后自动释放
}

// s1 = s2
mystring& operator= (mystring str) {  // 传值，调用拷贝构造，即str(s2)

    swap(str); // 狸猫换太子
    return *this;
}	

```



### 7 连续拷贝构造优化

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318111332480.png" alt="image-20240318111332480" style="zoom:67%;" />

值传递的过程都是拷贝构造

未优化：9次

优化后：7次

### 7 初始化列表

<a name="初始化列表"> 跳转 </a>

### 8  隐式类型转换

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318111348903.png" alt="image-20240318111348903" style="zoom:67%;" />

多个参数隐式类型转换

```cpp
Data d3 = {1,2,3}
```

### 9 静态成员函数

![image-20240318111405345](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318111405345.png)

```cpp
// 求1+2+...+n

class Sum{
pubilc:
    Sum(){
        sum_ += i_;
        i_ ++;
    }
    static int getSum_(){
        return sum_;
    }
    static void init(){
        i_ = 0;
        sum_ = 0;
    }
private:
    static int i_;
    static int sum_;
}
Sum::i_ = 1;
Sum::sum_ = 0;

class Solution{
pubilc:
    int solu(){
        Sum::init();  // oj平台测试多个样例，必须初始化，不然下次测试i_,sum_值是上次测试的结果
        Sum a[n];
        return Sum::getSum();
    }
    
}
```

### 10 友元

友元函数

友元类



### 11 匿名类

### 12 缺省函数

缺省参数是声明或定义函数时为函数的参数**指定一个缺省值**。在调用该函数时，如果没有指定实参则采用该形参的缺省值，否则使用指定的实参。

- 通俗点讲，就是在定义函数的时候可以给形参赋一个初始化的值，这个值就叫做缺省值，**缺省值可以有一个，也可以有多个**
- 半缺省参数必须从右往左**依次且连续**来给出，不能间隔着给【实参和形参同理】



### 13 继承

#### 1 赋值兼容规则

> 子类对象可以赋值给父类对象、父类指针、父类引用， 这个过程称为==切片==
>
> ![image-20231229104856702](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20231229104856702.png)

<a name="隐藏">跳转</a>

> 当派生类和父类有同名成员时，派生类会自动隐藏父类的成员，称作==隐藏==，或者==重定义==，有函数隐藏和变量隐藏
>
> 派生类和父类的析构函数也构成隐藏，因为最终析构函数会被转化为`destucter`
>
> 如何访问父类的成员？ 通过添加作用域
>
> 【面试题】重载：在同一作用域下，函数名相同，参数不同，返回值不同
>
> ​					重定义（隐藏）：父子类之间，函数名相同
>
> <img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318111426908.png" alt="image-20240318111426908" style="zoom:50%;" />

 

#### 2 派生类的默认成员函数

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318111440739.png" alt="image-20240318111440739" style="zoom:50%;" />

```cpp
// 父类
class Person
{
public :
     Person(const char* name = "peter"): _name(name ) {}

    
     Person(const Person& p): _name(p._name){}：
    
     Person& operator=(const Person& p )
     {
         if (this != &p) _name = p ._name;
        return *this ;
     }
    
	~Person(){};

protected :
 	string _name ; // 姓名
};
```

```cpp
// 派生类
class Student : public Person
{
public :
    // 1 派生类必须调用基类的构造函数去初始化基类的成员变量(name是基类成员，需要通过基类的构造函数进行初始化)
    // 如果基类没有默认的构造函数（有参构造），则必须在派生类构造函数的初始化列表阶段显示调用。
     Student(const char* name, int num) : Person(name), _num(num )	{};

    // 2 派生类的拷贝构造必须通过基类的拷贝构造初始化其基类的成员
     Student(const Student& s): Person(s), _num(s ._num) {};

    // 3 运算符重载，必须调基类的运算符重载初始化成员，注意作用域
     Student& operator = (const Student& s )
     {
        if (this != &s)
         {
            Person::operator =(s);
         	_num = s ._num;
        }
 		return *this ;
	 }

    // 4 派生类的析构函数会在被调用完成后自动调用基类的析构函数f清理基类成员
 	~Student(){}
protected :
 int _num ; //学号
};

```

【函数调用顺序】存放在栈中，先进后出

![image-20231229131428222](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20231229131428222.png)

#### 3 继承与友元

友元关系==不能继承==，也就是说基类友元不能访问子类私有和保护成员 

#### 4 继承与静态成员

基类定义了static静态成员，则整个继承体系里面==只有一个==这样的成员。无论派生出多少个子 类，都只有一个static成员实例 。



#### 5 菱形继承

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318111500619.png" alt="image-20240318111500619" style="zoom:50%;" />

![image-20231229145825131](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20231229145825131.png)

> 菱形继承所带来的两个问题：
>
> I 二义性
>
> ```cpp
> assistant a;
> a._name; // 无法判别是哪个_name
> 
> 解决：
>     // 需要显示指定访问哪个父类的成员可以解决二义性问题
>      a.Student::_name = "xxx";
>      a.Teacher::_name = "yyy";
> 
> ```
>
> II 数据冗余 
>
> ```cpp
> assistant中含有两个_name
>     
> 解决：虚拟继承同时解决解决数据冗余 和 二义性
> ```
>
> ```cpp
> class A
> {
> public:
>  	int _a;
> };
> 
> // class B : public A
> class B : virtual public A
> {
> public:
>  	int _b;
> };
> 
> // class C : public A
> class C : virtual public A
> {
> public:
>  	int _c;
> };
> 
> class D : public B, public C
> {
> public:
>  	int _d;
> };
> 
> ```
>

#### 6 虚继承

![image-20231229153650919](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20231229153650919.png)

> 虚拟继承底层： B，C各自拥有指针指向虚基表，虚拟表内存放继承A的成员的偏移量，通过偏移量找到继承的成员
>
> 指针称为：虚基表指针

#### 7 继承和组合

多继承是c++缺陷之一

```cpp
// 继承
class A {}
class B : public A {}

// 组合
class A {}
class C {
    A a;
}
```

* 继承允许你根据基类的实现来定义派生类的实现。这种通过生成派生类的复用通常被称 为白箱复用(white-box reuse)。术语“白箱”是相对可视性而言：在继承方式中，基类的 内部细节对子类可见 。继承一定程度破坏了基类的封装，基类的改变，对派生类有很 大的影响。
* 派生类和基类间的依赖关系很强，耦合度高。 对象组合是类继承之外的另一种复用选择。新的更复杂的功能可以通过组装或组合对象 来获得。对象组合要求被组合的对象具有良好定义的接口。这种复用风格被称为黑箱复 用(black-box reuse)，因为对象的内部细节是不可见的。对象只以“黑箱”的形式出现。 组合类之间没有很强的依赖关系，耦合度低。
* 优先使用对象组合有助于你保持每个类被 封装。 实际尽量多去用组合。组合的耦合度低，代码维护性好。不过继承也有用武之地的，有 些关系就适合继承那就用继承，另外要实现多态，也必须要继承。类之间的关系可以用 继承，可以用组合，就用组合。

#### 8 面试题

> 【什么是菱形继承？菱形继承的问题是什么？】
>
> 【什么是菱形虚拟继承？如何解决数据冗余和二义性的？】
>
> 【继承和组合的区别？什么时候用继承？什么时候用组合？】
>
> ![image-20240102191528276](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240102191528276.png)

### 8 多态

跟具体的实例化对象有关，不同的对象调用同一个函数会产生不同的操作

析构函数需要虚拟化

#### 1 构成多态的两个条件

1. 通过virtual关键字，实现虚函数（相同的函数名、参数、返回值，有例外）的==重现==
2. 通过==父类==对象的==指针或者引用==，去调用父类或者子类的虚函数

多态与实例化的对象有关，跟调用对象的类型无关，即子类和父类都是通过==父类==的指针/引用去调用虚函数

【两种调用方式】

【面试题1】

* 调用方式1：通过公共函数传入基类指针为参数，传入子类或者父类对象

```cpp
class Person {
public:
 	virtual void BuyTicket() { cout << "买票-全价" << endl; }
};

class Student : public Person {
public:
 	virtual void BuyTicket() { cout << "买票-半价" << endl; }
    void BuyTicket() { cout << "买票-半价" << endl; } 
};

void func(Person &st);  // √ 传入基类对象或者派生对象，通过基类指针调用函数接口，多态
void func(Person st); // ❌ 1 不构成多态，必须通过通过父类的指针/引用去调用虚函数
void func(Student st); // ❌ 2 不构成多态，必须通过通过父类，父亲不能复制给子类
```

【面试题2】

* 调用方式2：子类调用继承的父类的接口函数，来继续调用虚函数

```cpp
#include <iostream>
using namespace std;

class A
{
public:
    virtual void func(int val = 1) { std::cout << "A->" << val << std::endl; }
    virtual void test() { func(); }
};

class B : public A
{
public:
    void func(int val = 0) { std::cout << "B->" << val << std::endl; }
};

class C : public A
{
public:
    void func(int val = 3) { std::cout << "B->" << val << std::endl; }
    virtual void test() { func(); }
};

int main(int argc, char *argv[])
{
    B *p = new B;
    p->func();  // B->0   不构成多态，调用B重写的func
    p->test(); // B->1   多态，调用父类的test(A *this),向this传参p，即：
    			// 子类通过父类类型的指针调用子类重写的函数，构成多态
    			// 调用继承后重写的func，此时val是继承的1，重写的只是结构体

    C *q = new C;
    q->test();  // B->3  不构成多态，调用类本身的func和test
    return 0;
}
```



#### 2 虚函数重写的两个例外

* 协变(基类与派生类虚函数==返回值类型不同==) 

  派生类重写基类虚函数时，与基类虚函数返回值类型不同。

  即基类虚函数返回基类对象的指 针或者引用，派生类虚函数返回派生类对象的指针或者引用时，称为协变

```cpp
class A{};
class B : public A {};

class Person {
public:
 virtual A* f() {return new A;}
};
class Student : public Person {
public:
 virtual B* f() {return new B;}
};

```

* 析构函数的重写（==函数名不同==）

  如果基类的析构函数为虚函数，此时派生类析构函数只要定义，无论是否加virtual关键字， 都与基类的析构函数构成重写，虽然基类与派生类析构函数名字不同。虽然函数名不相同， 看起来违背了重写的规则，其实不然，这里可以理解为编译器对析构函数的名称做了特殊处 理，编译后析构函数的名称 统一处理成destructor。

```cpp
class Person {
public:
 	virtual ~Person() {cout << "~Person()" << endl;}
};
class Student : public Person {
public:
 	virtual ~Student() { cout << "~Student()" << endl; }
};

// 只有派生类Student的析构函数重写了Person的析构函数，下面的delete对象调用析构函
// 数，才能构成多态，才能保证p1和p2指向的对象正确的调用析构函数。
int main()
{
 	Person* p1 = new Person;
 	Person* p2 = new Student; // 不多态的话，析构调用~person()W
	delete p1;
 	delete p2;
 return 0;
}

```

#### 3 析构函数需要定义为虚函数

1. 基类析构没有virtual为虚函数：

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318111711438.png" alt="image-20240318111711438" style="zoom:50%;" />

2. 基类析构写为virtual为虚函数，构成多态

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318111724950.png" alt="image-20240318111724950" style="zoom:50%;" />

将基类的析构函数声明为虚函数是为了支持多态性，这在 C++ 中是实现多态行为的基础。在以下情况下，你通常会将基类的析构函数声明为虚函数：

1. **存在继承关系：** 如果你有一个基类，并且希望派生类能够通过基类指针进行动态绑定，那么基类的析构函数应该是虚函数。

2. **使用多态：** 如果你希望通过基类指针来销毁派生类对象，而希望调用派生类的析构函数，那么你需要将基类的析构函数声明为虚函数。

3. **资源释放：** 在面向对象编程中，通常使用析构函数来释放对象所占用的资源，如堆内存、文件句柄等。如果你有派生类，且派生类自己申请了资源，你需要确保在销毁派生类对象时能够正确释放这些资源，这就要求基类的析构函数是虚函数，以确保正确调用派生类的析构函数。

4. **避免内存泄漏：** 在使用多态时，如果基类的析构函数不是虚函数，那么当通过基类指针销毁派生类对象时，只会调用基类的析构函数，而不会调用派生类的析构函数。这可能导致派生类对象中申请的资源没有被正确释放，从而引发内存泄漏。

综上所述，当你希望通过基类指针销毁派生类对象时能够正确调用派生类的析构函数，或者当你的设计需要支持多态行为时，你应该将基类的析构函数声明为虚函数。

#### 4 重载 重写 重定义

![image-20240102124503578](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240102124503578.png)



#### 5 override  final

* final 修饰虚函数：该虚函数不能被改写
* final 修饰类： 该类不能被继承
* override：检查派生类是否重写了基类的某个虚函数，没有重写则编译错误

```cpp
class Car{
public:
	 virtual void Drive(){}
};
class Benz :public Car {
public:
 	virtual void Drive() override {cout << "Benz-舒适" << endl;}
};

```

#### 6 纯虚函数 抽象类

* 虚函数=0则为纯虚函数
* 包括纯虚函数的类为 抽象类
* 抽象类不能实例化
* 派生类继承抽象类，如果不重写纯虚函数，则派生类仍然为抽象类
* 强制重写虚函数，另外体现出接口继承的关系

```cpp
class Car
{
public:
	virtual void Drive() = 0;
};

```



#### 7 多态实现原理

![image-20240102154542850](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240102154542850.png)



【构成】

* 含有虚函数的类的构成：成员变量、虚函数表指针（vftptr）
* 子类的vftptr是拷贝基类的vftptr，虚函数表内存放虚函数的地址，以0结尾
* 子类不重写基类的虚函数，即将子类vftptr的仍指向父类的虚函数表
* 重写，创建新的虚函数表，修改子类的虚函数表指针

【sizeof计算】

* 普通函数和虚函数在代码段中，不计算大小
* 除了计算成员变量外，要计算虚函数表指针（32下4个字节）

【注意】

* 一个类的可以有多个虚地址表（==多重继承==）
* 每个类（含有虚函数）都有自己的虚函数表，虚函数表内存放的是指向函数的指针
* 虚地址表（vftptr值）在==编译==阶段生成，在运行时候填写具体的虚函数地址
* 同一个类的所有对象共享一张虚函数表

【存放位置】

* 代码段：虚函数、普通函数、虚函数表
* 栈： 虚函数表指针

```cpp
class A{
    int _a;
    void func1();
    virtual vfunc1();
    virtual vfunc2();
}
```

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318111755139.png" alt="image-20240318111755139" style="zoom:50%;" />

#### 8 多继承对象模型

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318111808118.png" alt="image-20240318111808118" style="zoom:50%;" />

* 子类继承父类的虚函数表，然后再其上进行覆盖
* 多继承时，继承多个父类的虚函数表
* 子类的虚函数写在第一个继承类的虚函数表上







####  9 面试题

[多态课件](E:\typora索引文件\c++\C++进阶课件\Lesson02--多态.pdf)

1 【内联函数不能为虚函数】

* 内联函数在调用的地方展开，没有地址，不能放入虚函数表

2 【static函数不能为虚函数】

* 静态成员函数没有this指针，无法访问虚函数表，所以静态成员函数无法放入虚函数表

3 【构造函数不能为虚函数】

* 虚函数的工作机制依赖于虚指针（`vptr`），而虚指针是在对象构造过程中被初始化

4 【析构函数可以是虚函数】

```cpp
// 特定场景要求为虚函数
class A{ ~A(){}}
class B : public A{ ~B(){}}

A *p = new B;  // 此时析构p，无多态，则调用 ~A(), B的资源得不到释放，可能造成内存泄漏

class A{ virtual ~A(){}}  // 析构声明为virtual，则析构时调用~B() 再调用~A()
```



## 内存管理

[资料](F:\学习视频\比特就业课c++\资料\课件\C++课件--2022修订\C++初阶课件\Lesson05---C&C++内存管理.pdf)

### 1 虚拟空间



![image-20231211104512980](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20231211104512980.png)  

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318111831844.png" alt="image-20240318111831844" style="zoom:67%;" />

--------------------

在 C 或 C++ 程序中，当你声明一个整数变量 `int a = 10;` 时，变量 `a` 和值 `10` 的存储位置取决于编译器、操作系统和具体的存储策略。

1. **a 存储在哪里？**
   - `a` 是一个局部变量，通常存储在 **栈** 上。当函数被调用时，为局部变量分配的内存会在函数返回时自动释放。

2. **10 存储在哪里？**
   - 值 `10` 在这个上下文中是一个立即数（literal），它不是一个变量，因此它并不存储在栈、堆、数据段或代码段中。相反，编译器通常会直接将这个值编码到机器代码指令中。

立即数（Immediate Value）是计算机科学和计算机工程中的一个术语，用于表示在机器代码指令中直接编码的常数值，而不是存储在寄存器或内存位置中的值。

当编译器生成机器代码时，某些操作可能需要使用常数值作为操作数。为了优化代码和提高执行效率，编译器可以选择将这些常数值作为立即数直接编码到生成的机器代码指令中，而不是首先将它们加载到寄存器或内存位置中。

例如，在 x86 架构的汇编语言中，你可能会看到像这样的指令：
```
MOV AX, 10
```
在这个指令中，`10` 是一个立即数，直接编码到 `MOV` 指令中，而不是从某个内存位置加载到 `AX` 寄存器中。

使用立即数可以节省额外的指令和内存访问，从而提高程序的执行效率。但是，过度使用立即数可能会增加代码的大小，因为每次使用都需要复制常数值到指令中，所以需要在代码大小和执行效率之间进行权衡。

-----------------

### 2 代码如何执行？

[编译过程](#编译)

![image-20240318111847454](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318111847454.png)

### 3 new 和 malloc的区别

![image-20231212173138574](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20231212173138574.png)

> 1 对于内置类型，均只开辟内存
>
> 2 new int(2) 可以初始化

```cpp

int *b = (int *)malloc(sizeof(int));
int *c = new int;
int *d = (int *)operator new(sizeof(int));
```

> 3 对于自定义类型，new会调用其构造函数，delete调用其析构函数

```cpp
class A{
public:
    A():a(20){};
    ~A(){};
private:
    int a;

};
int main()
{

    A a; // 调用构造函数，初始化a = 20;
    A *a1 = (A*)malloc(sizeof (A)); // 只申请内存
    A *a2 = new A; // 调用构造函数
    A *a3 = (A*)operator new(sizeof(A)); // 只申请内存

    cout << "Hello World!" << endl;
    return 0;
}
```

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318111916539.png" alt="image-20240318111916539" style="zoom:67%;" />

### 4 operator new 和 malloc 的区别 

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318111930100.png" alt="image-20240318111930100" style="zoom:67%;" />

### 5 malloc、operator new、new的关系

```cpp
// malloc  1、申请空间  2、失败return 0
// operator new ==>  malloc + 失败抛出异常
// new ===> operator new + 调用构造函数

// new 比 malloc  1、调用构造函数  2、失败抛异常
// delete 比 free  1、调用析构函数
// operator delete 和 free  没区别
```

### 6 定位new

* 又名replacement new

```cpp
int main(){
	// 模拟new
    // 分配内存
    A *p1 = (A*) operator new(sizeof(A));
    // 显式调用构造和析构(定位new)
    new(p1)A(10);
    
    // 模拟delete
    p1->~A();
    operator delete(p1);
}
```

### 7 内存泄漏

[资料](F:\学习视频\比特就业课c++\资料\课件\C++课件--2022修订\C++初阶课件\Lesson05---C&C++内存管理.pdf)

### 8 进程地址空间

进程地址空间本质：操作系统内核管理的数据结构，结构体表示 mm_struct

![image-20231220184507993](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20231220184507993.png)

![image-20231220184428855](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20231220184428855.png)

## STL

| 类型             | 成员变量                                           | 注意事项         | 遍历          |
| ---------------- | -------------------------------------------------- | ---------------- | ------------- |
| `string`         | `3个   _str、_size、_capacity`                     | 末尾的 \0        | 迭代器        |
| `vector`         | `3个   _start、 _finish、 _end_of_storage`         | 增容的问题       | 迭代器        |
| `list`           | `1个        _head`                                 | 迭代器分类封装   | 迭代器        |
| `deque`          | `解决vector和list的缺点，允许头插头删、空间开销小` | 迭代器访问效率低 | while(!empty) |
| `stack`          | `容器适配器`                                       |                  | while(!empty) |
| `queue`          | `容器适配器`                                       | 适配器           | while(!empty) |
| `priority_queue` | `优先级队列，大根堆,关注其输出的顺序`              | 仿函数           | \             |

* 重写默认构造，可以直接调用 `vector<int> vec;`

## 模板

### 1 非类型模板参数

```cpp
template<classs T, int N>
// T 为类型参数
// N 为非类型参数， double，自定义类型不能用于非类型参数， 常见的就是int short char long
class array
 {
 private:
 	T _array[N];
 	size_t _size;
 }；

```

### 2 模板偏特化

### 3 不能分离编译

> 【面试】 为什么模板函数、模板类不能分离编译？
>
> 【答案】会报链接错误，模板函数因为没有具体的类型，所以在func.cpp文件编译的时候，没有在符号表内生成模板函数的地址，因此在链接的时候，main函数找不到该函数，报链接错误
>
> ![image-20240318112005372](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318112005372.png)
>
> ![image-20240318112015088](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318112015088.png)
>
> 
>
> ![image-20231229095451690](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20231229095451690.png)

编译阶段，func头文件在test.cpp文件中展开，内含有 F1 和 模板函数F2 的声明, 编译通过（有承诺）

​					func头文件在func.cpp文件中展开，含有F1 和 F2的声明，编译通过，但是由于没有指定实例化类，所以符号表内中没有f2函数的地址

解决方案： 模板函数的定义和声明全部放在头文件中，然后在test的预处理阶段全部展开，在编译时候，根据test的实例对象，生成具体的函数地址



# -------------------------

# STL模拟汇总

| 容器     | 实现                                        | 注意                      |
| -------- | ------------------------------------------- | ------------------------- |
| `string` | `char* _str`                                | _str指向保存c字符串的数组 |
| `vector` | `iterator _start、_finish, _end_of_storage` | _start指向保存T对象的数组 |
| `list`   | `Node* _head` 带有头节点的双向链表          | 封装迭代器、重载运算符    |
| ``       | ``                                          |                           |

# 迭代器失效

| 容器类型             | 失效原因                     | 解决                                         |
| -------------------- | ---------------------------- | -------------------------------------------- |
| `vector deque`       | 增：开辟新空间、删：空间覆盖 | `intset、erase`返回迭代器                    |
| `list`               | 删：迭代器失效               | `erase(it++)`删除前迭代器先自增、`erase`返回 |
| `map、unordered_map` | 删：迭代器失效               | `erase(it++)`删除前迭代器先自增              |



## **一 序列容器：**

- 当容器调用`erase()`方法后，当前位置到容器末尾元素的所有迭代器全部失效。
- 当容器调用`insert()`方法后，当前位置到容器末尾元素的所有迭代器全部失效。
- 如果容器扩容，在其他地方重新又开辟了一块内存。原来容器底层的内存上所保存的迭代器全都失效了。

```c++
vector<int> q{ 1,2,3,4,5,6 };
// 在这里想把大于2的元素都删除
for (auto it = q.begin(); it != q.end(); it++) {
    if (*it > 2)
        q.erase(it); // 这里就会发生迭代器失效
}
```

使用 VS2019 运行什么也没打印就退出了进程。调试发现在 vector 源码内的`_Vector_const_iterator& operator++()`引发了异常：读取访问权限冲突，表明迭代器在执行`++`操作时报错，因为已经==失效的迭代器不能再进行自增运算==了。

迭代器失效的原因是：因为==vetor、deque 使用了连续分配的内存，`erase`操作删除一个元素导致后面所有的元素都会向前移动一个位置，这些元素的地址发生了变化，所以当前位置到容器末尾元素的所有迭代器全部失效==。

解决方法是利用`erase`方法可以返回下一个有效的 iterator，所以代码做如下修改即可：

```c++
// 在这里想把大于2的元素都删除
for(auto it=q.begin();it!=q.end();)
{
    if(*it>2)
    {
    	it=q.erase(it); // 这里会返回指向下一个元素的迭代器，因此不需要再自加了
    }
    else
    {
    	it++;
    }
}
```

## 二 链表式容器

对于链表式容器(如 list)，删除当前的 iterator，仅仅会使当前的 iterator 失效，这是因为 list 之类的容器，使用了链表来实现，插入、删除一个结点不会对其他结点造成影响。只要在 erase 时，==递增当前 iterator==即可，并且 erase 方法可以返回下一个有效的 iterator。

方式一：递增当前 iterator

```c++
list<int> l{ 1,2,3,4,5,6 };
for (auto it = l.begin(); it != l.end();) {
    if (*it > 2) l.erase(it++);
    else ++it;
}
```

方式二：通过 erase 获得下一个有效的 iterator

```c++
list<int> l{ 1,2,3,4,5,6 };
pli(l);
for (auto it = l.begin(); it != l.end();) {
    if (*it > 2) it = l.erase(it);
    else ++it;
}
```

## 三 关联式容器

对于关联容器(如 map, set,multimap,multiset)，删除当前的 iterator，仅仅会使当前的 iterator 失效，只要在 erase 时，递增当前 iterator 即可。这是因为 map 之类的容器，使用了红黑树来实现，插入、删除一个结点不会对其他结点造成影响。erase 迭代器只是被删元素的迭代器失效，但是返回值为 void，所以要采用`erase(iter++)`的方式删除迭代器。

```c++
for (iter = cont.begin(); it != cont.end();)
{
   (*iter)->doSomething();
   if (shouldDelete(*iter))
      cont.erase(iter++);
   else
      ++iter;
}

//测试错误的Map删除元素
void mapTest()
{
    map<int, string> dataMap;


    for (int i = 0; i < 100; i++)
    {
           string strValue = "Hello, World";

            stringstream ss;
            ss<<i;
            string tmpStrCount;
            ss>>tmpStrCount;
            strValue += tmpStrCount;
            dataMap.insert(make_pair(i, strValue));
    }

    cout<<"MAP元素内容为："<<endl;
     map<int, string>::iterator iter;
    for (iter = dataMap.begin(); iter != dataMap.end(); iter++)
    {
            int nKey = iter->first;
            string strValue = iter->second;
            cout<<strValue<<endl;
    }

    cout<<"内容开始删除："<<endl;
    //删除操作引发迭代器失效
    for (iter = dataMap.begin(); iter != dataMap.end();iter++)
    {
            int nKey = iter->first;
            string strValue = iter->second;

           if (nKey % 2 == 0)
           {
                dataMap.erase(iter);    //错误

           }
           /* cout<<iter->second<<endl;*/
    }
}
```

解析：`dataMap.erase(iter)`之后，iter 就已经失效了，所以 iter 无法自增，即`iter++`就会出bug。解决方案，就是在 iter 失效之前，先自增。

```go
void mapTest()
{
    map<int, string> dataMap;


    for (int i = 0; i < 100; i++)
    {
           string strValue = "Hello, World";

            stringstream ss;
            ss<<i;
            string tmpStrCount;
            ss>>tmpStrCount;
            strValue += tmpStrCount;
            dataMap.insert(make_pair(i, strValue));
    }

    cout<<"MAP元素内容为："<<endl;
    map<int, string>::iterator iter;
    for (iter = dataMap.begin(); iter != dataMap.end(); iter++)
    {
            int nKey = iter->first;
            string strValue = iter->second;
            cout<<strValue<<endl;
    }

    cout<<"内容开始删除："<<endl;
    for (iter = dataMap.begin(); iter != dataMap.end();)
    {
            int nKey = iter->first;
            string strValue = iter->second;

           if (nKey % 2 == 0)
           {
                dataMap.erase(iter++);
                auto a = iter;

           }
           else {
               iter ++;
           }
    }
}
```

解析：`dataMap.erase(iter++);`这句话分三步走，先把 iter 传值到 erase 里面，然后 iter 自增，然后执行 erase，所以 iter 在失效前已经自增了。

map 是关联容器，以红黑树或者平衡二叉树组织数据，虽然删除了一个元素，整棵树也会调整，以符合红黑树或者二叉树的规范，但是单个节点在内存中的地址没有变化，变化的是各节点之间的指向关系。

所以在 map 中为了防止迭代器失效，在有删除操作时，常用如下方法：

```c++
for (iter = dataMap.begin(); iter != dataMap.end(); )
{
         int nKey = iter->first;
         string strValue = iter->second;

         if (nKey % 2 == 0)
         {
               map<int, string>::iterator tmpIter = iter;
           iter++;
               dataMap.erase(tmpIter);
               //dataMap.erase(iter++) 这样也行

         }else
     {
          iter++;
         }
}
```

# --------------------------

# string

## 0 字符串操作函数

| 函数      | 描述                                                         |
| --------- | ------------------------------------------------------------ |
| `strlen`  | 计算字符串的长度（不包括终止的空字符）。                     |
| `strcpy`  | 将源字符串复制到目标字符串，==包括==终止的空字符。           |
| `strncpy` | 将源字符串的前 n 个字符复制到目标字符串，目标字符串不足时用空字符填充。 |
| `strcat`  | 将源字符串连接到目标字符串的末尾，==包括==终止的空字符。     |
| `strncat` | 将源字符串的前 n 个字符连接到目标字符串的末尾，添加终止的空字符。 |
| `strcmp`  | 比较两个字符串的大小，返回一个整数表示比较结果。             |
| `strncmp` | 比较两个字符串的前 n 个字符，返回一个整数表示比较结果。      |
| `strchr`  | 在字符串中查找第一次出现的指定字符，并返回指向该字符的指针。 |
| `strrchr` | 在字符串中查找最后一次出现的指定字符，并返回指向该字符的指针。 |
| `strstr`  | 在字符串中查找第一次出现的指定子字符串，并返回指向该子字符串的指针。 |
| `strtok`  | 分解字符串为一组令牌（token），通过指定的分隔符。            |
| `memcpy`  | 从源内存块复制指定字节数到目标内存块。                       |
| `memmove` | 将源内存块的指定字节数移动到目标内存块，允许源和目标重叠。   |
| `memset`  | 用指定的值填充内存块的前 n 个字节。                          |
| `memcmp`  | 比较两个内存块的前 n 个字节，返回一个整数表示比较结果。      |
| `strspn`  | 计算字符串前面连续包含在指定字符串中的字符数。               |
| `strcspn` | 计算字符串前面不包含在指定字符串中的字符数。                 |

```cpp
#include <iostream>
#include <cstring>

int main() {
    char str1[20] = "Hello";
    char str2[20] = "World";
    
    // strlen
    std::cout << "Length of str1: " << strlen(str1) << std::endl;
    
    // strcpy
    strcpy(str2, str1);
    std::cout << "str2 after strcpy: " << str2 << std::endl;
    
    // strncpy
    strncpy(str2, "C++ Programming", 5);
    str2[5] = '\0';  // 添加终止符
    std::cout << "str2 after strncpy: " << str2 << std::endl;
    
    // strcat
    strcat(str1, " World");
    std::cout << "str1 after strcat: " << str1 << std::endl;
    
    // strncat
    strncat(str1, "!!!", 2);
    std::cout << "str1 after strncat: " << str1 << std::endl;
    
    // strcmp
    std::cout << "strcmp result: " << strcmp(str1, str2) << std::endl;
    
    // strncmp
    std::cout << "strncmp result: " << strncmp(str1, "Hello", 5) << std::endl;
    
    // strchr
    char *p = strchr(str1, 'W');
    if (p) {
        std::cout << "Character W found at position: " << p - str1 << std::endl;
    }
    
    // strstr
    p = strstr(str1, "World");
    if (p) {
        std::cout << "Substring World found at position: " << p - str1 << std::endl;
    }
    
    // strtok
    char str3[] = "Hello,World,C++";
    char *token = strtok(str3, ",");
    while (token != NULL) {
        std::cout << "Token: " << token << std::endl;
        token = strtok(NULL, ",");
    }
    
    // memset
    memset(str2, 'A', 5);
    str2[5] = '\0';  // 添加终止符
    std::cout << "str2 after memset: " << str2 << std::endl;
    
    // memcpy
    char src[] = "Source";
    char dest[20];
    memcpy(dest, src, strlen(src) + 1);
    std::cout << "dest after memcpy: " << dest << std::endl;
    
    return 0;
}
```



###  0.1 无重叠时拷贝

`memcpy` 是 C/C++ 标准库中的一个函数，用于从一个源地址复制指定数量的字节到一个目标地址。其函数签名如下：

```cpp
void* memcpy(void* destination, const void* source, size_t num);
```

以下是 `memcpy` 函数的各个参数的解释：

1. **destination**: 这是指向目标数组或内存区域的指针。`memcpy` 会从 `source` 复制数据到 `destination`。

2. **source**: 这是指向源数组或内存区域的指针。`memcpy` 会从这里复制数据到 `destination`。

3. **num**: 这是要复制的字节数。`memcpy` 会从 `source` 复制 `num` 个字节到 `destination`。注意，这个参数的类型是 `size_t`，这是一个无符号整数类型，通常用于表示大小或字节数。

函数返回值：`memcpy` 函数没有返回值。它只是从 `source` 复制数据到 `destination`。

使用 `memcpy` 时，请确保目标和源区域不会重叠，因为这可能会导致不确定的行为。如果你需要处理可能重叠的区域，考虑使用 `memmove` 函数，它专门设计用于处理这种情况。

### 0.2 有重叠时拷贝

`memmove` 是一个 C 标准库函数，用于从一个内存区域复制指定数量的字节到另一个内存区域。其函数签名如下：

```c
void* memmove(void* destination, const void* source, size_t num);
```

以下是 `memmove` 函数的参数解释：

1. **destination**: 这是一个指针，指向目标内存区域，即要将数据复制到的位置。`memmove` 会将数据从 `source` 复制到这里。

2. **source**: 这也是一个指针，指向源内存区域，即数据的来源。`memmove` 会从这里复制数据到 `destination`。

3. **num**: 这是一个 `size_t` 类型的参数，表示要复制的字节数。`memmove` 会从 `source` 复制 `num` 个字节到 `destination`。

函数返回值：`memmove` 函数返回一个指向目标内存区域的指针，即 `destination`。这是为了方便在链式操作或其他情况下使用。

`memmove` 是设计用于处理可能重叠的内存区域，因此当源和目标内存区域重叠时，它能够确保正确地复制数据，而不会产生未定义的行为。

## 1 构造函数

### 1.1 默认、有参构造

* 采用缺省 + 初始化列表，实现默认 + 有参的构造函数
*  字符串常量初始化_str时候，即数组首地址指针 `_str`指向`str`常量字符串的首地址，该字符串位于代码段，因此无法进行修改操作; 
* 栈上开辟的内存不能扩容；在堆上开辟内存，将初始化的字符串常量拷贝过来

```cpp
mystring(const char* str = "\0") :
_str(new char[strlen(str) + 1]), 
_size(strlen(str)),
_capacity(strlen(str))
	{
		// 拷贝字符串常量的值
		memcpy(_str, str, strlen(str)+1);

	}
// 1、全缺省时候，const char* str = nullptr错误，strlen()函数遍历到'\0'结尾，设置为空指针就报错
// 2、const char* str = "\0"，可以优化为const char* str = ""
// 3、默认构造空字符串，即只有'\0'
```

### 1.2 深拷贝构造

```cpp
mystring(const mystring& str) : _str(new char[str.size() + 1]), 
_size(str.size()), 
_capacity(str.capacity())
	{
		memcpy(_str, str.data(), str.size() + 1);
	}
```

### 1.3 赋值运算符重载

```cpp
// 自定义深拷贝构造 (传统写法)
mystring(const mystring& str) :
_str(new char[str.size() + 1]), _size(str.size()), _capacity(str.capacity())
{
    strcpy_s(_str, str.size() + 1, str.data());
}

mystring& operator= (const mystring& str) {
    // 确保非自身赋值
    if (this != &str) {
        char* tmp = new char[str.size() + 1];
        memcpy(tmp, str.data(), str.size() + 1);
        delete[] _str;
        _str = tmp;

        _size = str.size();
        _capacity = str.capacity();
        return *this;
    }
}
```

```cpp
```



## 2 重载

### 2.1 输入运算符

```cpp
// getline即去掉空格
istream& operator>> (istream& in, mystring &str) {
	
	while (1) {
		char ch;
		// cin >> ch;
		ch = in.get();
		if (ch == ' ' || ch == '\n') {
			//空格或者换行，终止
			break;
		}
		str += ch;
	}
	return in;
}
```

### 2.2 输出运算符

```cpp
ostream& operator<< (ostream& out, const mystring& str) {
	for (size_t i = 0; i < str.size(); ++i) {
		cout << str[i];
	}
	return out;
}
```

## 3 迭代器

```cpp
typedef char* iterator;

iterator begin() const {
    return _str;
}

iterator end() const {
    return _str + _size;
}
```

三种遍历

```cpp
for (auto iter = str3.begin(); iter < str3.end(); ++iter) {
    cout << *iter;
}

// 编译器会转化为迭代器，所以类必须要定义 iterator、begin()、end()
for (auto& ch : str3) {
    cout << ch << "";
}

```

## 四 实现

[项目位置](D:\VisualStudio\Project\myString)

```cpp
#pragma once
#include <iostream>
#include <assert.h>
using namespace std;
class mystring
{
public:
	// ===================================一 迭代器==================================
	typedef char* iterator;
	iterator begin() const {
		return _str;
	}
	iterator end() const {
		return _str + _size;
	}

public:
	// ========================二 构造函数=================================
	//1 构造函数
	// ①采用缺省 + 初始化列表，实现默认 + 有参的构造函数
	// ②在堆上开辟内存存放_str; 栈上开辟的内存不能扩容；字符串常量初始化_str,指针指向代码段的常量，无法进行修改操作
		Mystring(const char* str = "\0")
		:_str(new char[strlen(str) + 1]),
		_size(strlen(str)),
		_capa(strlen(str))
	{
		strcpy(_str, str);
	}
	// 传统拷贝
	/*Mystring(const Mystring& str)
		:_str(new char[str.size() + 1]),
		_size(str.size()),
		_capa(str.capacity())
	{
		strcpy(_str, str.data());
	}*/
	// 现代拷贝
	Mystring(const Mystring& str)
		:_str(nullptr),
		_size(str.size()),
		_capa(str.capacity())
	{
		Mystring tmp(str.data());
		std::swap(_str, tmp._str);
	}
	Mystring& operator= ( Mystring str) // 利用拷贝构造，狸猫换太子
	{
		if (this != &str) // 判断非自己
		{
			std::swap(_str, str._str);
			_capa = str.capacity();
			_size = str.size();

		}
	}
	// 4 析构函数
	~mystring() {
		delete[] _str;  // 注意删除数组
		_capacity = _size = 0;
		_str = nullptr;

	}

	size_t size() const {
		return strlen(_str);
	}

	size_t capacity()const {
		return _capacity;
	}

	const char* data() const
	{
		return _str;
	}

	// ======================================= 三 重载 ==================================
	char& operator[] (size_t i) const {
		return _str[i];
	}
	
	bool operator<(const mystring& str) {};
	bool operator>(const mystring& str) {};
	bool operator==(const mystring& str) {};
	bool operator<=(const mystring& str) {};
	bool operator>=(const mystring& str) {};
	bool operator!=(const mystring& str) {};

	// ====================================== 四 测试 =========================================
	void printStr() const{
		for (size_t i = 0; i < strlen(_str); ++i) {
			cout << _str[i];
		}
		cout  << "  size: " << _size << "  capacity: " << _capacity << endl;
	}

	// ================================ 五 增    ==========================
	// 用来开辟空间和转移原数据
	void reserve(size_t n) {
		char* tmp = new char[n + 1];  // +1 是为了新的 \0 结尾，但是不算在capa里
		memcpy(tmp, _str, _size + 1 );  // 拷贝 \0
		delete[] _str;
		_str = tmp;
		_capacity = n;
	}
	void push_back(char ch) {
		// 如果当前大小已经等于容量，需要扩容
		if (_size == _capacity ) {  
			size_t newCap = (_capacity == 0) ? 2 : (_capacity * 2);
			reserve(newCap);
		}
		// 覆盖当前的 \0 末尾字符
		_str[_size] = ch;
		++_size;

		// 添加新的 \0 结尾
		_str[_size] = '\0';
	}

	void append(const char* str) {
		size_t len = strlen(str);
		if (_size + len > _capacity) {
			size_t newcap = (_capacity == 0) ? len : (_size + len);
			reserve(newcap);
		}
		memcpy(_str + _size, str, len + 1);
		_size += len;

	}

	mystring& operator+= (char ch) {
		this->push_back(ch);
		return *this;
	}

	mystring& operator+= (const char* str) {
		this->append(str);
		return *this;
	}

	mystring& insert(size_t pos, char ch) {
		// 插入位置合法(只插中间，不插末尾)
		assert(pos < _size);
		if (_size == _capacity) {
			size_t newcap = (_size == 0) ? 2 : (_capacity * 2);
			this->reserve(newcap);
		}
		size_t end = _size;
		while (end >= pos) {
			_str[end + 1] = _str[end]; // 从'\0'开始移动
			--end;
		}
		_str[pos] = ch;
		++_size;
		return *this;
	}

	mystring& insert(size_t pos, const char* str) {
		assert(pos < _size);
		size_t len = strlen(str);
		if (_size + len > _capacity) {
			reserve(_size + len);
		}
		size_t end = _size;
		while (end >= pos) {
			_str[end + len] = _str[end]; // 从'\0'开始移动
			--end;
		}
		memmove(_str + pos, str, len);
		_size += len;
		return *this;
	}

	// 调整_str的长度，用c填充，注意是调整_size的大小，不是_capacity
	void resize(size_t n, char c = '\0') {
		if (n < _size) {
			_str[n] = '\0';
			_size = n;
		}
		else if (n > _capacity) {
			reserve(n);

			// 空白用c填充
			for (size_t i = _size; i < _capacity; ++i) {
				_str[i] = c;
			}
			_size = n;
			_str[_capacity] = '\0';

		}
		else {
			for (size_t i = _size; i < n; ++i) {
				_str[i] = c;
			}
			_size = n;
			_str[_size ] = '\0';
		}
	}



	// ============================== 六 删 =============================================
	void erase(size_t pos, size_t len) {
		// pos位置删len长度
		assert(pos < _size);
		if (len >= _size - pos) {
			_str[pos] = '\0';
			_size = pos;
		}
		else {
			size_t cur = pos + len;
			while (cur < _size) {
				_str[cur - len] = _str[cur];
				++cur;
			}
			_size -= len;
			_str[_size] = '\0';
		}
	}
	
	// ==================================七 查 ==============================
	size_t find(char ch, size_t  pos = 0) {
		for (size_t i = pos; i < _size; ++i) {
			if (_str[i] == ch) return i;
		}
		return npos;
	}

	size_t find(const char* str, size_t  pos = 0) {
		char *p = strstr(_str, str);
		if (p == nullptr) return npos;
		else return p - _str; // 两个地址相减，得到下表
	}

	
private:
	// C类型的字符串，以\0结尾
	char* _str;

	// 容量相关
	size_t _capacity; // 可以存放的有效位数
	size_t _size;  // 有效位数
	static size_t npos;
};

// 类外定义静态变量
size_t mystring::npos = -1;

ostream& operator<< (ostream& out, const mystring& str) {
	for (size_t i = 0; i < str.size(); ++i) {
		cout << str[i];
	}
	return out;
}

// getline即去掉空格
istream& operator>> (istream& in, mystring &str) {
	
	while (1) {
		char ch;
		// cin >> ch;
		ch = in.get();
		if (ch == ' ' || ch == '\n') {
			//空格或者换行，终止
			break;
		}
		str += ch;
	}
	return in;
}


```

# vector

## 1 迭代器

### 1.1 迭代器类型

```cpp
// 1 iterator正向迭代器   12340
void test1(vector<int> &v) {
    v.push_back(0);
    vector<int>::iterator it = v.begin();
    while (it != v.end()) {
        cout << *it;
        ++it;
    }
    cout << endl;
}
// 2 const_iterator 12340
void test2(const vector<int>& v) {
    vector<int>::const_iterator it = v.begin();
    while (it != v.end()) {
        cout << *it;
        ++it;
    }
    cout << endl;
}
// 3 reverse_iterator 反向迭代器 04321
// 访问 rbegin()、rend()
void test3( vector<int>& v) {
    vector<int>::reverse_iterator it = v.rbegin();
    while (it != v.rend()) {
        cout << *it;
        ++it;
    }
    cout << endl;
}
// 4 const_reverse_iterator   04321

void test4(const vector<int>& v) {
    vector<int>::const_reverse_iterator it = v.rbegin();
    while (it != v.rend()) {
        cout << *it;
        ++it;
    }
    cout << endl;
}
```

### 1.2 迭代器失效

> 1.  push_back、insert、reserve、resize 能添加元素，可以导致新开辟内存，致使迭代器失效  ==解决== ：`开辟新内存后，重新设置pos位置`
> 2. erase 删除it所指元素，会vs下中断报错，g++下不报错，但是忽略it，失效 。  解决：`it = vec.erase(it)` 返回删除元素后的下一个的迭代器（还是该pos，只不过指向了下一个元素）

## 2 增容问题

* vector增容存在的问题（2个）

### 2.1  浅拷贝问题

<a name="memcpy">跳转</a>

> 1. 当开辟新空间时候，若就空间内存在指针，比如存放string，采用 memcpy() 则会导致浅拷贝问题

![image-20231224220759028](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20231224220759028.png)

【解决】通过赋值操作，调用string的 operator= 操作

```cpp
void reserve(size_t n) {
    if (n > capacity()) {
        size_t num = size();
        // 开辟空间，转移数据
        T* tmp = new T[n];
        // 浅拷贝问题
        //if (_start) memcpy(tmp, _start, sizeof(T) * num);
        if (_start) {
            for (size_t i = 0; i < num; ++i) {
                tmp[i] = _start[i];    // 本质调用string类的operator=深拷贝, 即 string s1 = s2;
            }
            delete[] _start;
        }

        _start = tmp;
        _finish = tmp + num;
        _end_of_storage = tmp + n;
    }

}
```

### 2.2 迭代器失效

1. 开辟新空间后，自身的迭代器失效

```cpp
// 重新设置自身迭代器
iterator = vector.begin();
```



1. 开辟新空间后，函数传参的迭代器失效

```cpp
// 重新设置
iterator insert(iterator pos, const T& x) {
    assert(pos <= _finish);
    if (_finish == _end_of_storage) {
        size_t num = size();
        size_t newcap = (capacity() == 0) ? 2 : capacity() * 2;
        reserve(newcap);
        // 更新pos位置
        pos = _start + num;
    }
    // 移动数据 (有数据的时候)
    if (_start != _finish) {
        iterator cur = _finish - 1;
        while (cur >= pos) {
            *(cur + 1) = *cur;
            --cur;
        }
    }
    // 插入 （无数据则直接插入）
    *pos = x;
    ++_finish;
    return pos;
}
```

## 3 模拟vector

```cpp
#include <iostream>
#include <assert.h>

template <class T>
class Myvector
{
public:
	typedef T* iterator;

	iterator begin() const {
		return _start;
	}

	iterator end() const
	{
		return _finish;
	}

	// construct
	Myvector() :
		_end_of_storage(nullptr),
		_start(nullptr),
		_finish(nullptr)
	{

	}


	template<class U = T>
	Myvector(int n, const T& val = T()) :
		_start(new T[n]),
		_finish(_start + n),
		_end_of_storage(_finish)
	{
		for (int i = 0; i < n; ++i)
		{
			_start[i] = val;
		}
	}

    // 为了防止 Myvector<int>(2,8); 走迭代器构造，必须设置判断
    // !std::is_integral<iter>::value  判断iter是否为整数，如 int double
    // std::enable_if<true>::type* = 0   如果内部位true，则等式成立，执行该模板。若false不成立，改模板不执行
	template<class iter>
	Myvector(iter begin, iter end, typename std::enable_if<!std::is_integral<iter>::value>::type* = 0) : _start(nullptr), _finish(nullptr), _end_of_storage(nullptr)
	{
		int len = end - begin;
		reserve(len);
		while (begin != end)
		{
			*_finish = *begin;
			begin++;
			_finish++;
		}
	}

	// copy
	Myvector(const Myvector& vec) : _start(nullptr), _finish(nullptr), _end_of_storage(nullptr)
	{
		Myvector tmp(vec.begin(), vec.end());
		std::swap(_start, tmp._start);
		std::swap(_finish, tmp._finish);
		std::swap(_end_of_storage, tmp._end_of_storage);

	}

	// =
	Myvector& operator= (Myvector vec)
	{
		_start = nullptr; _finish = nullptr; _end_of_storage = nullptr;
		std::swap(_start, vec._start);
		std::swap(_finish, vec._end);
		std::swap(_end_of_storage, vec._end_of_storage);
	}

	~Myvector()
	{
		delete[] _start;
		_start = _finish = _end_of_storage = nullptr;
	}

	int size() const
	{
		return _finish - _start;
	}

	int capacity() const
	{
		return _end_of_storage - _start;
	}

	// 内存扩充策略（以T的个数为准，不是以字节）
	int getNewCap()
	{
		if (capacity() == 0) {
			// return std::max(64 / sizeof(T), 1); 
			return 1;
		}
		// 容量小的策略
		if (capacity() < 30 && capacity() > 10000) {
			return capacity() * 2;
		}

		// 寻常的策略，+1目的：额外添加一个缓冲区
		return (capacity() * 3 + 1) / 2;
	}

	// 内存扩充实现
	void reserve(int cap)
	{
		if (cap > capacity())
		{
			// 开辟新空间
			T* tmp = new T[cap];
			// 空数据初始化指针，非空深拷贝数据
			if (size())
			{
				for (int i = 0; i < size(); ++i)
				{
					tmp[i] = _start[i];
				}

				int t_size = size();

				delete[] _start;
				_start = tmp;
				_finish = _start + t_size;
				_end_of_storage = _start + cap;

			}
			else
			{
				_start = _finish = tmp;
				_end_of_storage = _start + cap;
			}
		}
		else
		{
			// 删除多余空间
			if (size() > cap) _finish = _end_of_storage = _start + cap;
			else _end_of_storage = _start + cap;
		}
	}

	template<class T>
	iterator insert(iterator pos, const T& val)
	{
		assert(pos <= _finish);
		int midlen = pos - _start;
		if (_finish == _end_of_storage)
		{
			// 开空间
			int newcap = getNewCap();
			reserve(newcap);
			pos = _start + midlen;
		}
		else
		{
			if (_start != _finish)
			{
				// 移动数据
				int len = _finish - pos;
				for (auto it = _finish; it != pos; --it)
				{
					*it = *(it - 1);
				}
				_finish = _start + size();
			}
		}
		// 插入pos
		*pos = val;
		return pos;

	}

	template<class T>
	void push_back(const T& val)
	{
		insert(_finish, val);
	}

	iterator erase(iterator pos)
	{
		assert(pos < _finish);

		for (auto it = pos; it != _finish; it++)
		{
			*it = *(it + 1);
		}
		_finish--;
		return pos;
	}

	// []
	T& operator[](size_t pos) const
	{
		assert(pos < size());
		return _start[pos];
	}
	void print()
	{
		for (int i = 0; i < size(); ++i)
		{
			std::cout << _start[i];
		}
		std::cout <<"  ----size: " << size() << "  ----capa: " << capacity() << std::endl;
	}
private:
	iterator _start;
	iterator _finish;
	iterator _end_of_storage;


};

int main()
{
	Myvector<int> vec(5,10);
	vec.print();
	vec.insert(vec.begin() + 2, 77);
	vec.print();
	
	Myvector<int> vec2(vec);
	vec2.print();

	Myvector<int> vec3(vec2.begin()+2, vec2.begin()+5);
	vec3.print();

	Myvector<int> vec4(vec3);
	vec3.push_back(9);
	vec3.push_back(8);
	vec4.print();

	vec4.erase(vec4.begin() + 2);
	vec4.print();

	return 0;
}
```

## 4 扩容机制

> 1 vector是如何增容的？数据在扩容时如何处理，拷贝方式是什么，为什么？
>
> 1. vector是一个可动态增长的数组，插入、reserve、resize等操作都会面临增容问题
> 2. 最常见的情况是，vs下capacity是按1.5倍增长的，g++是按2倍增长的。但是具体增长多少，是按照需求定义的，比如我之前阅读过facebook内部使用的fbvecor，他的容量增加策略是：
>
> * 初始化的时候给64个字节，若装不下一个类型，就给他分配一个类型的空间大小
>
> * 增长策略是：当现有容量小于或者大于一个临界值时，按照二倍增长
> * 介于给定值中间时候，按照1.5倍增加，并额外给出0.5个空间作为缓冲区
>
> 3. 除此之外，扩容的过程中也会有很多问题，比如说
>
> * 迭代器失效，我们需要在扩容操作后，返回更新后的迭代器
> * 浅拷贝问题，在开辟新空间后赋值值，若采用内存处理函数memcpy进行拷贝，若vector存储有指针类型，则会导致浅拷贝，因此我们采用元素赋值的方法，调用元素的operator=进行深拷贝
>
> 4. 具体的拷贝策略
>
>    对于内置类型int等，`vector` 会使用**内存复制**（`memcpy`），效率快
>
>    对于自定义类型，由于浅拷贝问题，采用拷贝构造进行深拷贝
>
>    支持移动构造，优先采用移动构造

```cpp
size_type computePushBackCapacity() const {
    // 初始化策略，最小64bit，64bit能装多少个元素就装多少个，>=1， 如果装不下一个元素，就申请一个元素大小的空间
    if (capacity() == 0) {
        return std::max(64 / sizeof(T), size_type(1));
    }
    // 容量小的策略
    if (capacity() < folly::jemallocMinInPlaceExpandable / sizeof(T)) {
        return capacity() * 2;
    }
    // 容量大的策略
    if (capacity() > 4096 * 32 / sizeof(T)) {
        return capacity() * 2;
    }

    // 寻常的策略，+1目的：额外添加一个缓冲区
    return (capacity() * 3 + 1) / 2;
 }
```

# --------------------------

# list

## 1 迭代器类型

1 通过 传const参数调用  begin() const，得const_iterator

```cpp
void chage(const yu::list<int>& l) {
	auto it = l.begin(); // 调用const迭代器

void chage(yu::list<int>l) {
        auto it = l.begin(); // 调用普通迭代器  *it 会修改值
```

2 通过 cbegin() 获取常量迭代器

```cpp
cosnt_iterator it = list.begin();
cosnt_iterator it = list.cbegin();  // 定义了cbegin
```

3 范例

```cpp
// 迭代器类
// 两种类型的区别就在于，是否能修改it指向变量的值
// 区别在于  operator*  和  operator->,
// 定义两类迭代器，但是为了书写简约，通过 Ref, Ptr模板参数控制迭代器类型,
// iter<T, T&, T*> -> iterator
// iter<T, const T&, const T*> -> const_iterator
template <class T, class Ref, class Ptr>
struct __list_iterator 
    {
        // 1 指针
        typedef __list_node<T> Node;
        typedef __list_iterator<T, Ref, Ptr> Self;
        Node* _node;

        __list_iterator(Node* ptr) : _node(ptr) {}; // 构造迭代器

        // 2 重载
        // *it
        Ref operator* () {         //T& operator* () {}
            return _node->_data;
        }

        // 假设链表存储 Data(year,day),T 即为 Data类型
        // 原始：day = it._node->_data->day
        // 重载: day = it -> day
        Ptr operator-> () {           // T* operator-> () {
            return &_node->_data;
        }

        // ++it
        Self& operator++ () {
            _node = _node->_next;
            return *this;
        }

        // it++
        Self operator++ (int) {
            Self temp = *this;
            _node = _node->_next;     
            return temp;                  
        }

        // --it
        Self& operator-- () {
            _node = _node->_prev;
            return *this;
        }

        // it--
        Self operator-- (int) {
            Self temp = *this;
            _node = _node->_prev;
            return temp;
        }

        // it1 != it2
        bool operator!= (const Self& it) {
            return _node != it._node;
        }

        // it1 == it2
        bool operator== (const Self& it) {
            return _node == it._node;
        }


    };
```

## 2 模拟list

```cpp
#include <iostream>
using namespace std;

namespace yu {
	// 节点类
	template<class T>
	struct __list_node
	{
		// 默认构造（缺省）
		// 调用T类型的默认构造，int 即初始化为0
		__list_node(const T& val = T()) : _prev(nullptr), _next(nullptr), _data(val) {};
		__list_node<T>* _prev;
		__list_node<T>* _next;
		T _data;
	};

	// 迭代器类
	// 两种类型的区别就在于，是否能修改it指向变量的值
	// 区别在于  operator*  和  operator->,
	// 定义两类迭代器，但是为了书写简约，通过 Ref, Ptr模板参数控制迭代器类型,
	// iter<T, T&, T*> -> iterator
	// iter<T, const T&, const T*> -> const_iterator
	template <class T, class Ref, class Ptr>
	struct __list_iterator 
	{
		// 1 指针
		typedef __list_node<T> Node;
		typedef __list_iterator<T, Ref, Ptr> Self;
		Node* _node;  // 原始ptr

		__list_iterator(Node* ptr) : _node(ptr) {}; // 构造迭代器
		
		// 2 重载
		// *it
		Ref operator* () {         //T& operator* () {}
			return _node->_data;
		}

		// 假设链表存储 Data(year,day),T 即为 Data类型
		// 原始：day = it._node->_data->day
		// 重载: day = it -> day
		Ptr operator-> () {           // T* operator-> () {
			return &_node->_data;
		}
		
		// ++it
		Self& operator++ () {
			_node = _node->_next;
			return *this;
		}
		
		// it++
		Self operator++ (int) {
			Self temp = *this;
			_node = _node->_next;     
			return temp;                  
		}

		// --it
		Self& operator-- () {
			_node = _node->_prev;
			return *this;
		}

		// it--
		Self operator-- (int) {
			Self temp = *this;
			_node = _node->_prev;
			return temp;
		}

		// it1 != it2
		bool operator!= (const Self& it) {
			return _node != it._node;
		}

		// it1 == it2
		bool operator== (const Self& it) {
			return _node == it._node;
		}

		
	};

	// list
	// 带头节点，头节点不存值，begin()从下一位开始，end()为值节点下一位，即_head
	template<class T>
	class list {
		typedef __list_node<T> Node;
		typedef __list_iterator<T, T&, T*> iterator;
		typedef __list_iterator<T, const T&, const T*> const_iterator;
	public:
		// ================================================================= 构造函数
		//1 默认构造
		list() {
			_head = new Node;
			_head->_prev = _head;
			_head->_next = _head;
		}

		//2 拷贝构造
		list(const list<T>& l) {
			_head = new Node;
			_head->_prev = _head;
			_head->_next = _head;

			for (auto e : l) {
				push_back(e);
			}
		}
		//3 析构函数
		~list() {
			// 清除所有数据节点
			clear();
			// 删除头节点
			delete _head;
			_head = nullptr;
		}

		//4 赋值运算符重载
		list<T>& operator= (list<T> l) {
			swap(_head, l._head);
			return *this;
		}
		 

		// ================================================================ 迭代器
		iterator begin() {
			return iterator(_head->_next);
		}
		iterator end()  {
			return iterator(_head);
		}
		const_iterator begin() const { 
			return const_iterator(_head->_next);
		}
		const_iterator end() const {
			return const_iterator(_head);
		}


		// ========================增删改查
		// 在迭代器pos位置前插入
		iterator insert(iterator pos, const T& val) {
			Node* tmp = new Node(val);
			Node* cur = pos._node;

			tmp->_next = cur;
			tmp->_prev = cur->_prev;
			cur->_prev->_next = tmp;
			cur->_prev = tmp;
			return iterator(tmp);
		}

		void push_back(const T& val) {
			insert(end(), val);
		}

		void push_front(const T& val) {
			insert(begin(), val);
		}

		// 删除pos位置元素
		iterator erase(iterator pos)
		{
			// 找到待删除的节点
			Node* cur = pos._node;
			Node* pRet = cur->_next;

			// 将该节点从链表中拆下来并删除
			cur->_prev->_next = cur->_next;
			cur->_next->_prev = cur->_prev;
			delete cur;

			return iterator(pRet);
		}

		void pop_back() {
			erase(--end());
		}

		void pop_front() {

			erase(begin());
		}
		
#if 1
		void clear() {
			auto it = begin();
			while (it != end()) {
				erase(it++);
			}
		}
#elif 0
		void clear() {
			for (auto it = begin(); it != end(); ) {
				// 注意迭代器失效问题
				it = erase(it);
			}
		}
#endif
	private:
		Node* _head; // 包含头节点

	};
}
```

## 3 list和vector的使用场景

>  ==1 vector 和 list 的区别==
>
> 1 vector是可动态增长的数组，支持随机访问，二分查找，堆算法，头部或者中间的插入删除效率低，增容的代价大
>
> 2 list是带头节点的双向循环链表，通过迭代器顺序访问，不适合排序
>
> 3vector适合查询、排序，list适合增删
>
> 4 迭代器不同，vector的迭代器是原生指针，list迭代器是 原生指针+ 运算符重载，来模拟原生指针的操作
>
> 5 迭代器失效，vector的insert和erase会失效，list只有erase会失效

# --------------------------

# stack

## 后缀转中缀

[leetcode](https://leetcode.cn/problems/evaluate-reverse-polish-notation/submissions/)

根据后缀表达式，遇到数则入栈，遇到操作符，则出栈，先出的是右操作数，后出为左操作数，进行操作后将结果入栈，最后得到计算结果

```cpp
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<int> st;
        
        for(auto &str : tokens){
            if(str== "+"|| str== "-"|| str== "*" || str== "/"){
            //if(str[0]== '+'|| str[0]== '-'|| str[0]== '*' || str[0]== '/'){
                // 1 遇见操作符就出栈运算
                int right = st.top();
                st.pop();
                int left = st.top();
                st.pop();

                switch(str[0]){
                    case '+': 
                        st.push(left + right);
                        break;
                    case '-':
                        st.push(left - right);
                        break;
                    case '*':
                        st.push(left * right);
                        break;
                    case '/':
                        st.push(left / right);
                        break;
                }
            }else{
                // 2 遇见数就入栈
                st.push(stoi(str));
            }
        }
        return st.top();

    }
};
```



## 代码题

> 1 根据输入顺序，判断是否存在该输出顺序
>
> ```cpp
> // 模拟操作
> bool IsPopOrder(vector<int>& pushV, vector<int>& popV) {
>     stack<int> cur;
>     int i = 0, j = 0;
>     while(i <= pushV.size()){
>         if(cur.empty()) cur.push(pushV[i++]);
>         if(cur.top() != popV[j]) {
>             if(i == pushV.size()) break; // 无法再插入，break
>             cur.push(pushV[i++]);
>         }
>         else {
>             cur.pop();
>             if(cur.empty() && i == pushV.size()) break; // 栈空 且 输入完成，成功break
>             ++j;
>         }
> 
> 
>     }
>     if(cur.empty()) return true;
>     else return false;
> 
> }
> ```



> 后缀表达式（倪波尔表达式）的计算

# queue

## 1 容器适配器

在 C++ 中，容器适配器（Container Adapters）是一种特殊的容器，它们提供了一种特定的界面来操作底层容器。容器适配器不是实际的容器，而是使用现有容器（如 `std::vector`、`std::deque` 或 `std::list`）作为其内部实现，并提供了一个更简化的接口。

C++ 标准库提供了三种主要的容器适配器：

1. **std::stack**：
   - `std::stack` 是一个后进先出 (LIFO) 的数据结构，类似于堆栈。
   - 默认情况下，`std::stack` 使用 `std::deque` 作为其底层容器，但您也可以指定其他容器，如 `std::vector` 或 `std::list`。

2. **std::queue**：
   - `std::queue` 是一个先进先出 (FIFO) 的数据结构，类似于队列。
   - 默认情况下，`std::queue` 也使用 `std::deque` 作为其底层容器，但也可以更改为 `std::list`。

3. **std::priority_queue**：
   - `std::priority_queue` 是一个优先级队列，元素按照优先级从大到小排序（默认情况下）。
   - 它不直接使用一个现有的容器作为底层实现。相反，它使用一个特定的堆数据结构来维护元素的顺序。但是，您可以指定使用哪种容器作为其底层存储（例如 `std::vector`）。

使用容器适配器的好处是，它们提供了一个简单的接口来操作基础容器，同时隐藏了复杂性。例如，使用 `std::stack`，您可以轻松地进行堆栈操作，而不必直接操作 `std::deque`。这提高了代码的可读性和可维护性。

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318112102996.png" alt="image-20240318112102996" style="zoom:50%;" />

## 2 面试题

> ==1 为什么栈和队列不支持迭代器？==
>
> 为了维护他们的性质，即先进先出和先进后出，如果有迭代器，就可以随便访问了
>
> 

> 2 优缺点
>
> ![image-20231228092126289](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20231228092126289.png)
>
> vector: 头插头删效率低
>
> list：无法随机访问，占用了空间开销
>
> 解决方案： deque，开辟多个数组，通过中控控制，但是迭代器遍历，但是随机访问和迭代器访问效率低
>
> 测试过10w数据的排序，vector的效率是deque的4-5倍
>
> 但是作为queue和stack的底层适配器，需要关注的只是头插头删和尾插尾删



# priority_queue

* 优先级队列
* 默认为大根堆
* 对vector的适配器

## 1 仿函数

在C++中，仿函数（Functor）是一个==类或结构体==，其对象可以像函数那样被调用。换句话说，仿函数是一个重载了函数调用运算符`operator()`的对象。当你创建一个仿函数的对象并使用它时，你实际上是调用该对象的`operator()`方法。

1. **灵活性**: 通过仿函数，你可以将函数行为封装在一个对象中，这使得你可以将函数作为一个参数传递给其他函数，或者在算法中使用。
2. l**理解：**在一段代码的同一位置处，需要按照不同的逻辑处理
   * 常规：复制多个代码，同一位置修改不同的逻辑
   * 仿函数：在特定位置用仿函数处理，即没有规定好具体是哪个函数，通过模板传参来确定
3. **使用场景**： 在 ==函数==或者==算法==中，作为参数传入
   * 类中，传入模板类型
   * 函数中，传入模板对象

```cpp
template <class T>
struct less 
{
      bool operator()(const T& t1, const T& t2) {
          return t1 < t2;
      }
  };

template <class T>
struct greater
{
    bool operator()(const T& t1, const T& t2) {
        return t1 > t2;
    }
};

int main() {
    
    // 调用1
    greater<int> gt;
    gt(1,2);
    
    // 调用2
    sort(it.begin(), it.end(),gt);
    sort(it.begin(), it.end(), greater<int>());
    return 0;
}
```

## 2 模拟实现

```cpp
#include <iostream>
using namespace std;

#include <vector>

namespace yu {

	// 仿函数
	template <class T>
	struct less 
	{
		bool operator()(const T& t1, const T& t2) {
			return t1 < t2;
		}
	};

	template <class T>
	struct greater
	{
		bool operator()(const T& t1, const T& t2) {
			return t1 > t2;
		}
	};
    
	// 大根堆
	template<class T, class Container = vector<T>, class Compare = less<int>>
	class priority_queue {
	public:
		void push(const T& val) {
			_con.push_back(val);
			upAdjust(_con.size() - 1);
		};

		void pop() {
			swap(_con[0], _con[_con.size() - 1]);
			_con.pop_back();

			// 堆顶元素向下调整
			downAdjust(0);
		};

		T& top() {
			return _con[0];
		};

		size_t size() {
			return _con.size();
		};

		bool empty() {
			return _con.empty();
		};

		// ======================== 调整
		void upAdjust(size_t child)
		{
			size_t parent = ((child - 1) / 2);
			while (child > 0)
			{
				//if (_con[parent] < _con[child] )
				if(_pare(_con[parent], _con[child]))
				{
					swap(_con[child], _con[parent]);
					child = parent;
					parent = (child - 1) / 2;
				}
				else
				{
					break;
				}
			}
		}

		void downAdjust(size_t parent) {
			size_t child = parent * 2 + 1;
			while (child < _con.size()) {
				// 选出左右孩子中大的进行交换
				// if (child + 1 < _con.size() && _con[child] < _con[child + 1]) ++child;
				if (child + 1 < _con.size() && _pare(_con[child] , _con[child + 1])) ++child;
				// 比较
				if (_pare(_con[parent], _con[child])) {
					swap(_con[parent], _con[child]);
					parent = child; 
					child = parent * 2 + 1;
				}
				else {
					break;
				}
			}
		}
	
    private：
		Container _con;
		Compare _pare;
	};
}
```



## 1 代码题

> [数组中第k个最大的元素](https://leetcode.cn/problems/kth-largest-element-in-an-array/description/)

![image-20231228155550782](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20231228155550782.png)

```cpp
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        priority_queue<int, vector<int>, greater<int>> minheap;
        // 堆中先构造k个元素
        int i = 0;
        for(; i < k; ++i){
            minheap.push(nums[i]);  // 最小的元素在上边
        }
        
        // 将k后的元素与堆中最小值进行替换
        // 最后保证小根堆中是最大的k个元素，堆顶是第k大
        for(i; i < nums.size(); ++i){
            if(nums[i] > minheap.top()){
                minheap.pop();
                minheap.push(nums[i]);
            }
        }

        return minheap.top();
    }
};

// 时间复杂度 O(N * logK)
// 空间夫再度 O(K)
```

函数模板传对象， 类模板传类型

# -------------------------

# set map

## 1 set

> 1. 有自己的find
>
>    ```cpp
>     auto it = set.find(val);  // 查找效率O(longN)
>    
>    // 算法find
>       auto it = find(set.begin(), set.end(), val); // 查找效率O(N)
>    ```
>
> 2. 所有迭代器均为const
>
>    ```cpp
>     // 不能通过 *it 修改set值
>    ```
>
> 

## 2 map

> 1. 内部存放的是键值对pair
>
>    ```cpp
>    map<int, int> map;
>    map.insert(pair<int, int>(1,2));
>    
>    // 更喜欢用
>    map.insert(make_pair(1,2));
>    ```
>
> 2. insert的返回值
>
>    ```cpp
>    pair<iterator, bool> insert(pair);
>    1. 插入成功，iterator指向插入位置，bool为true
>    2. 插入key存在，iterator指向key位置，bool为false
>    ```
>
> 3. operator[] 原理
>
>    ```cpp
>    // 通过insert的返回值<iterator,bool>中的迭代器修改<key, value>中的value
>    mapped_type& operator[] (const key_type& k){
>        return (*((this->insert(make_pair(k,mapped_type()))).first)).second;
>    }
>          
>    1. map["苹果"] = 2;
>    2. key不存在，map[key] = val，即先插入<key, T()>, 在修改默认的val
>    3. key存在，直接修改val
>    4. 为什么不通过find实现找到插入位置？ 因为key不存在时，无法插入val
>    ```
>
>    <img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318112232434.png" alt="image-20240318112232434" style="zoom:67%;" />
>
>    4. 常用操作
>
>    ```cpp 
>    增： insert、operator[]
>    删： erase
>    改:  operator[]
>    查： map.find()
>    遍历： for(auto e : map)
>    ```
>
>    5. 排序仿函数，默认key从小到大排列、multi中key大小一致，则按insert顺序排列
>
>       [前k个高频单词](https://leetcode.cn/problems/top-k-frequent-words/)
>
>       ```cpp
>       class Solution {
>       public:
>           vector<string> topKFrequent(vector<string>& words, int k) {
>               map<string, int> m;
>               for(auto e : words){
>                   m[e] ++;
>               }
>                   
>               // kv呼唤，按照val排序
>               multimap<int,string,greater<int>> mmp;
>               for(const auto& pair : m){
>                   mmp.insert(make_pair(pair.second, pair.first));
>               }
>                   
>               auto it = mmp.begin();
>               vector<string> res;
>               for(int i = 0; i < k; ++i){
>                   res.push_back(it->second);
>                   ++it;
>                   
>               }
>               return res;
>           }
>       };
>       ```

4. map中括号和find查找区别？

   如果使用 `operator[]` 查找一个不存在的键，会自动插入一个具有该键的元素，并且该元素的值会被默认初始化

   如果查找的键不存在，`find()` 不会插入任何元素，它会返回一个指向 `end()` 的迭代器，表示没有找到对应的键。

# --------------------------

# 二叉搜索树

## 1 基础算法

### 1.1 概念

1. 二叉搜索树任何节点，左孩子<节点<有孩子
2. 通过中序遍历（左根右）得到的顺序是==从小到大==
3. 与一节点相邻的两个节点分别是：
   * 左子树最右的节点， ==一直遍历左子树上的右孩子，直到为nullptr==
   * 右子树最左的节点， ==一直遍历右子树上的左孩子，直到为nullptr==

### 1.2 找到相邻节点

```cpp
// 找到数值在cur相邻的节点
// 1 左子树最右的节点
Node* leftMax = cur -> left;
while(leftMax -> right ){
    leftMax = leftMax -> right;
}

// 1 右子树最左的节点
Node* rightMin = cur -> right;
while(rightMin -> left){
    rightMin = rightMin -> left;
}
```

### 1.3 递归遍历

* 四句话
  1. 根空就返回
  2. 进行根操作
  3. 有左子树，递归处理左子树（判断是否存在，根据具体是否省略）
  4. 有右子树，递归处理右子树（判断是否存在，根据具体是否省略）

```cpp
private:
void _preOrder(Node* root){
    if(root == nullptr) return;
    // 处理根操作
    cout << root -> val << endl;  // 根
    _preOrder(root -> left);  // 左
    _preOrder(root -> right); // 右
}

public:
void preOrder(){
    _preOrder(_root);
}
```

* 【面试题】

1 [根据二叉树创建字符串](https://leetcode.cn/problems/construct-string-from-binary-tree/)

```cpp
string tree2str(TreeNode* root) {
    string ans;

    if(root == nullptr) return ans;
    // 处理根操作
    ans += to_string(root->val);
    //有左子树，递归处理左子树
    if(root->left){
        ans += "(";
        ans+=tree2str(root->left);
        ans += ")";
    }
    if(!root->left && root->right){
        ans += "()";
    }
    // 有右子树，递归处理右子树
    if(root->right){
        ans += "(";
        ans+=tree2str(root->right);
        ans += ")";
    }
    return ans;
}
```

2 [二叉搜索树转为双向链表](https://www.nowcoder.com/practice/947f6eb80d944a84850b0538bf0ec3a5?tpId=13&&tqId=11179&rp=1&ru=/activity/oj&qru=/ta/coding-interviews/question-ranking)

```cpp
/*
struct TreeNode {
	int val;
	struct TreeNode *left;
	struct TreeNode *right;
	TreeNode(int x) :
			val(x), left(NULL), right(NULL) {
	}
};*/
class Solution {
public:
	// 递归要传prev的引用，递归函数内修改的prev，出了递归失效，所以传引用
	void convertList(TreeNode* pRootOfTree, TreeNode* &prev){
		// 通过中序遍历
		if(!pRootOfTree) return;
		convertList(pRootOfTree -> left, prev);
		// 处理根节点
		pRootOfTree -> left = prev; // 第一个位置prev为nullptr
		if(prev) prev -> right = pRootOfTree;
		prev = pRootOfTree;

		convertList(pRootOfTree -> right, prev);

	}
    TreeNode* Convert(TreeNode* pRootOfTree) {
        // 转换成链表
		TreeNode* prev = nullptr;
		convertList(pRootOfTree, prev);
		// 返回链表起始位置
		TreeNode* start = pRootOfTree;
		while(start && start -> left){
			start = start -> left;
		}
		return start;
    }
};

```

### 1.4 非递归遍历

* 用栈实现

* 一直遍历树的左孩子，直到null
* 访问完毕左孩子，访问有孩子，将右孩子全部转为左孩子，while继续访问
* <img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318112154237.png" alt="image-20240318112154237" style="zoom:67%;" />

```cpp
// 前序遍历
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
vector<int> preorderTraversal(TreeNode* root) {
    vector<int> res;
    stack<TreeNode*> st;

    TreeNode* cur = root;
    while(cur || !st.empty()){
        // 一直处理左子树
        while(cur){
            res.push_back(cur->val); // 根 左
            st.push(cur);
            cur = cur -> left;
        }
        // 左子树访问完，弹出，访问右子树，将右子树设置为根节点，递归处理
        // 右子树为空，继续弹出，访问上一个节点的右子树
        TreeNode* node = st.top();
        st.pop();

        cur = node -> right;

    }
    return res;
}
```

```cpp
// 中序

class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> v;
        TreeNode* cur = root;
        stack<TreeNode*> st;
        while(cur || !st.empty()){
            while(cur){
                st.push(cur);
                cur = cur -> left;
            }
            TreeNode* node = st.top();
            st.pop();
            v.push_back(node -> val);  // 调整插入位置
            
            cur = node -> right;

        }
        return v;

    }
};
```

* 都是访问过节点后再从栈中弹出
* 访问完左右孩子后，才访问根，根弹出栈
* 区分什么时候访问根： 1、无右孩子   2、右孩子已经访问过，用lastname记载
* 后序遍历，访问右孩子后，紧挨着就会访问根

```cpp
// 后序
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> v;
        TreeNode* cur = root;
        TreeNode* lastnode = nullptr;
        stack<TreeNode*> st;
        while(cur || !st.empty()){
            while(cur){
                st.push(cur);
                cur = cur -> left;
            }
            
            TreeNode* node = st.top();
            // 该节点无右孩子，或者右孩子已经访问，则访问该节点
            if(node -> right == nullptr || node->right == lastnode){
                lastnode = node;
                st.pop();
                v.push_back(node -> val);
            }else{
            // 访问右孩子
                cur = node -> right;
            }

        }
        return v;
    }
};
```



### 1.5 查找

* 基于中序遍历

```cpp
// 普通二叉树
private:
	bool _find(Node* root, const T& val) {
		if (!root) return false;
		return val == root->_data || _find(root->_left, val) || _find(root->_right, val);
	}
public:
	bool find(const T& val) {
		return _find(_root, val);
	}

// 搜索二叉树
bool _find2(Node* root, const T& val) {
    if (!root) return false;
    if (val > root->_data) {
        return _find2(root->_right, val);
    }else if (val < root->_data) {
        return _find2(root->_left, val);
    }
    else { return true; }
}
```



### 1.5 层次遍历

* 采用队列实现，出来一个节点，插入该节点的左右孩子
* 队列内保存的是Node* 类型节点

```cpp
// 打印
private:
void _levelOrder(Node* node) {
    queue<Node*> _queue;
    if (!node) return;
    _queue.push(node);
    while (!_deque.empty()) {
        Node* cur = _queue.front();
        cout << cur->_data;

        if (cur->_left) _queue.push(cur->_left);
        if (cur->_right) _queue.push(cur->_right);

        _queue.pop();
    }
}
public:
void levelOrder(){
    _levelOrder(_root);
}
```

【面试题】

[层次遍历自上而下放入vector](https://leetcode.cn/problems/binary-tree-level-order-traversal/)

* 当上一层全部出队，队中剩下的就是下一层的所有节点

```cpp
vector<vector<int>> levelOrder(TreeNode* root) {
    queue<TreeNode*> q;
    vector<vector<int>> vv;
    if(!root) return vv;
    q.push(root);

    while(!q.empty()){
        size_t lineSize = q.size();
        vector<int> v;
        for(size_t i = 0; i < lineSize; ++i){
            TreeNode* cur = q.front();
            v.push_back(cur-> val);


            if(cur->left) q.push(cur->left);
            if(cur->right) q.push(cur->right);

            q.pop();
        }
        vv.push_back(v);
    }
    return vv;
}
```

## 2 实现

| 操作         | 实现原理                                                     |
| ------------ | ------------------------------------------------------------ |
| `insert`     | 双指针，cur寻找插入位置，par记录cur的父节点                  |
| `erase`      | 分三种情况，删除节点有左右孩子，使用替换法处理               |
| `递归遍历`   | 递归算法                                                     |
| `非递归遍历` | 用栈处理，后续遍历需要用lastnode记录是否访问过根节点的右孩子 |
| `层次遍历`   | 用队列处理，出队一个父节点，入队其所有的子节点               |
|              |                                                              |



```cpp
#include <iostream>
using namespace std;
#include <deque>
#include <vector>
// 定义树节点
template <class T>
struct BSTNode {
	// 缺省默认构造
	BSTNode(const T& data = T()) : _left(nullptr), _right(nullptr), _data(data) {}
	T _data;
	BSTNode<T>* _left;
	BSTNode<T>* _right;
};

// 二叉搜索树
template <class T>
class BSTree {
	typedef BSTNode<T> Node;
public:
	// 默认构造
	BSTree() : _root(nullptr) {}

	// 析构 =============
	~BSTree() {
		delete _root;
		_root = nullptr;
	}

	// ======================插入
	bool insert(const T& val) {
		if (_root == nullptr) {
			_root = new Node(val);
			return true;
		}
		Node* cur = _root;
		Node* par = nullptr;
		while (cur) {
			par = cur;
			if (val > cur->_data) {
				cur = cur->_right;
			}
			else if (val < cur->_data) {
				cur = cur->_left;
			}
			else {
				// val已经存在
				return false;
			}
		}
		cur = new Node(val);
		if (val > par->_data) {
			par->_right = cur;
		}
		else {
			par->_left = cur;
		}
		return true;
	}

	// 中序遍历 =====================
private:
	void _midOrder( Node* node) {
		if (!node) return;
		if (node->_left) _midOrder(node->_left);
		cout << node->_data << " ";
		if (node->_right) _midOrder(node->_right);
	}

public:
	void midOrder() {
		_midOrder(_root);
		cout << endl;
	}

	// 层次遍历 =======================
private:
	void _dequeOrder(Node* node) {
		deque<Node*> _deque;

		if (!node) return;
		_deque.push_back(node);
		while (!_deque.empty()) {
			Node* cur = _deque.front();
			cout << cur->_data;
			
			if (cur->_left) _deque.push_back(cur->_left);
			if (cur->_right) _deque.push_back(cur->_right);

			_deque.pop_front();
		}
	}

	vector<vector<int>> _dequeOrder2(Node* node) {
		deque<Node*> _deque;
		vector<vector<int>> vv;
		if (!node) return vv;
		_deque.push_back(node);
		
		while (!_deque.empty()) {
			vector<int> v;
			size_t lineSize = _deque.size();
			// 遍历一层，一层全部输出后，下一层就已经全部放入
			for (size_t i = 0; i < lineSize; ++i) {
				
				Node* cur = _deque.front();
				v.push_back(cur->_data);
				_deque.pop_front();

				if (cur->_left) _deque.push_back(cur->_left);
				if (cur->_right) _deque.push_back(cur->_right);
			}
			vv.push_back(v);
			
		}
		return vv;
	}

	
public:
	void dequeOrder() {
		_dequeOrder(_root);
		cout << endl;
	}

	vector<vector<int>> dequeOrder2() {
		return _dequeOrder2(_root);
		
	}
	// 删除 =========================
	// 1. 删除节点的左孩子为空，父节点指向删除节点的右孩子
	// 2. 删除节点的右孩子为空，父节点指向删除节点的左孩子
	// 3. 删除节点的左右孩子都存在，采用替换法,选择删除节点的最大左孩子 或者 最小右孩子代替
	bool erase(const T& val) {
		// 树为空，删除失败
		if (_root == nullptr) return false;
		// 1 找到删除节点位置
		Node* par = _root;
		Node* cur = _root;
		while (cur) {
			
			if (val > cur->_data) {
				par = cur;
				cur = cur->_right;
			}
			else if (val < cur->_data) {
				par = cur;
				cur = cur->_left;
			}
			else {
				// 找到删除位置
				// 情况1
				if (cur->_left == nullptr) {
					if (cur == _root) {
						_root = cur->_right;
					}
					else {
						if (par->_left == cur) par->_left = cur->_right;
						else if (par->_right == cur) par->_right = cur->_right;
					}
					delete cur;
				}

				// 情况2
				else if (cur->_right == nullptr) {
					if (cur == _root) {
						_root = cur->_right;
					}
					else {
						if (par->_left == cur) par->_left = cur->_left;
						else if (par->_right == cur) par->_right = cur->_left;
					}
					delete cur;
				}

				// 情况3
				else {
					// 找到右子树最小节点
					Node* Rmin_par = cur;
					Node* Rmin = cur->_right;
					while (Rmin->_left) {
						Rmin_par = Rmin;
						Rmin = Rmin->_left;
					}

					// 代替
					cur->_data = Rmin->_data;

					// 删除Rmin，即父节点指向Rmin的右孩子
					if (Rmin_par->_left == Rmin) Rmin_par->_left = Rmin->_right;
					else if (Rmin_par->_right == Rmin) Rmin_par->_right = Rmin->_right;

					delete Rmin;
					
				}
				return true;
			
			}
			
		}
		return false;
	}


private:
	bool _find1(Node* root, const T& val) {
		if (!root) return false;
		return val == root->_data || _find(root->_left, val) || _find(root->_right, val);
	}

	bool _find2(Node* root, const T& val) {
		if (!root) return false;
		if (val > root->_data) {
			return _find2(root->_right, val);
		}else if (val < root->_data) {
			return _find2(root->_left, val);
		}
		else { return true; }


	}
public:
	bool find1(const T& val) {
		return _find(_root, val);
	}
	bool find2(const T& val) {
		return _find2(_root, val);
	}

	
private:
	Node* _root;
};


```



## 3 面试题

[二叉树最近公共祖先](https://leetcode.cn/problems/lowest-common-ancestor-of-a-binary-tree/)

<img src="C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20240104182941476.png" alt="image-20240104182941476" style="zoom:50%;" />

```cpp
class Solution {
public:
    bool find(TreeNode* tree, TreeNode* t){
        if(tree == nullptr) return NULL;
        
        return t == tree || find(tree->left,t) || find(tree -> right, t);

    }
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(p == root || q == root) return root;
        bool pinl, pinr, qinl, qinr;
        pinl = find(root -> left, p);
        pinr = !pinl;
        qinl = find(root -> left, q);
        qinr = !qinl;

        // pq不同侧，则root为祖先
        if((pinl && qinr) || (pinr && qinl)) return root;

        // pq同左侧
        if(pinl && qinl) return lowestCommonAncestor(root -> left, p, q);

        // pq同右侧
        if(pinr && qinr) return lowestCommonAncestor(root -> right, p, q);     

        return NULL;
    }
};
```

[根据中序和前序还原二叉树](https://leetcode.cn/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

思想： 依次根据前序的值，在中序种划分区域，确定左右孩子节点

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */

class Solution {
public:
    TreeNode* _build(vector<int>& preorder, vector<int>& inorder,int &prei, int start, int end ){
        if(start > end) return nullptr;
        // 非空，根据preorder则确定根节点
        TreeNode* root = new TreeNode(preorder[prei]);

        // 通过根节点在[start, end]分左右孩子区间
        int rooti = start;
        while(rooti <= end){
            if(preorder[prei] == inorder[rooti]) break;
            else ++rooti;
        }
        // 划分为[start, rooti-1] rooti [rooti+1, end]

        // 在左右子区间内递归
        if( start <= rooti -1) {
            root -> left = _build(preorder, inorder, ++prei,start, rooti-1);
        }else{
            root -> left = nullptr;
        }
        if(end >= rooti + 1) {
            root -> right = _build(preorder, inorder, ++prei, rooti+1, end);
        }else{
            root -> right = nullptr;
        }
        
        return root;


    }
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        int prei = 0;
        int instart = 0, inend = inorder.size() -1 ;

        return _build(preorder,inorder,prei,instart,inend);

    }
};
```



[中序和后序确定二叉树](https://leetcode.cn/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* _build(vector<int>& inorder, vector<int>& postorder,int &posti, int start, int end){
        if(start > end) return nullptr;

        // 不为空，确定根节点
        TreeNode* root = new TreeNode(postorder[posti]);

        // 划分空间
        int rooti = start;
        while(rooti <= end){
            if(inorder[rooti] == postorder[posti]) break;
            else ++rooti;
        }
        // [start, rooti - 1] rooti [rooti + 1]

        // 后序遍历从最后开始，左 右 根
        // 因此先确定有孩子，在确定左孩子
        if(rooti + 1 <= end) {
            root -> right = _build(inorder, postorder, --posti, rooti + 1, end);
        }else{
            root -> right = nullptr;
        }
        if(start <= rooti - 1){
            root -> left = _build(inorder, postorder, --posti, start, rooti - 1);
        }else{
            root -> left = nullptr;
        }
        

        return root;
    }
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        int posti = postorder.size() - 1;
        int instart = 0, inend = inorder.size() - 1;
        return _build(inorder, postorder, posti, instart, inend);

    }
};
```



### 问题

![image-20240104150009121](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240104150009121.png)



### 前缀查找树

```cpp
class Trie {
public:
    Trie() {
        isEnd = false;
        for(int i;i<28;i++){
            node[i] = NULL;
        }
        oper = NULL;

    }
    
    // 插入
    void insert(string word) {
        oper = this;
        for(int i;i<word.size();i++){
            int index = word[i] - 'a';
            if(oper->node[index]==NULL){
                Trie *new_node = new Trie();
                oper->node[index] = new_node;
                oper = new_node;   
            }
            oper = oper->node[index];
        }
        oper->isEnd = true;
    }
    
    // 查找word是否在前缀树中
    bool search(string word) {
        oper = this;
        for(int i;i<word.size();i++){
            int index = word[i] - 'a';
            if(oper->node[index] == NULL) return false;
            oper = oper->node[index];
        }
        return oper->isEnd;
    }
    
    // 查找prefix前缀是否在树中
    bool startsWith(string prefix) {
        oper = this;
        for(int i;i<prefix.size();i++){
            int index = prefix[i] - 'a';
            if(oper->node[index] == NULL) return false;
            oper = oper->node[index];
        }
        return true;

    }

    // 一个节点包含一个判断位和一个数组，用于指向孩子节点
    bool isEnd;
    Trie * node[28];
    // 操作指针
    Trie * oper;
};

```



```cpp
class Trie {
    bool isend;
    Trie* childen[28];
public:
    /** Initialize your data structure here. */
    Trie() {
        isend = false;
        for(int i = 0;i < 28;i++){
            childen[i] = NULL;
        }
    }
    
    /** Inserts a word into the trie. */
    void insert(string word) {
        Trie* node = this;
        for(int i = 0;i < word.size();i++){
            if(node->childen[word[i] - 'a'] == NULL){
                Trie* temp = new Trie();
                node->childen[word[i] - 'a'] = temp;
            }
            node = node->childen[word[i] - 'a'];
        }
        node->isend = true;
    }
    
    /** Returns if the word is in the trie. */
    bool search(string word) {
        Trie* node = this;
        for(int i = 0;i < word.size();i++){
            if(node->childen[word[i] - 'a'] == NULL) return false;
            node = node->childen[word[i] - 'a'];
        }
        return node->isend;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    bool startsWith(string prefix) {
        Trie* node = this;
        for(int i = 0;i < prefix.size();i++){
            if(node->childen[prefix[i] - 'a'] == NULL) return false;
            node = node->childen[prefix[i] - 'a'];
        }
        return true;
    }
};
```



# AVL

平衡搜索二叉树

1. 必须是搜索二叉树
2. 所有左右子树的高度差不超过1 

### 插入

```cpp
1. 根据搜索二叉树的插入操作进行插入
    找到插入位置
    新建节点插入
2. 调节平衡因子，根绝par和 cur的bf判断具体旋转策略
```

```cpp
bool insert(const pair<K, V>& kv) {
    if (_root == nullptr) {
        _root = new Node(kv);
        return true;
    }
    // 1 找到插入位置
    Node* cur = _root;
    Node* par = _root;

    while (cur) {
        if (kv.first >= cur->_kv.first) {
            par = cur;
            cur = cur->_right;
        }
        else if (kv.first < cur->_kv.first) {
            par = cur;
            cur = cur->_left;
        }
        else {
            return false;
        }
    }
    // 2 插入
    cur = new Node(kv);
    if (kv.first > par->_kv.first) {
        par->_right = cur;
        cur->_parent = par;

    }
    else {
        par->_left = cur;
        cur->_parent = par;
    }
    // 3 更新平衡因子，判断是否调整AVL
    while (par) {
        if (par->_right == cur) par->_bf++;
        else par->_bf--;

        // 3.1 不需要调整
        if (par->_bf == 0) break;
        // 3.2 循环判断父节点的平衡因子是否调整
        else if (par->_bf == 1 || par->_bf == -1) {
            cur = par;
            par = par->_parent;
        }
        // 3.3 需要旋转
        else if (par->_bf == 2) {
            // 左单旋
            if (cur->_bf == 1) {
                rotatelL(par);
            }
            else if (cur->_bf == -1) {
                // 右左双旋
                rotatelRL(par);
            }
            break;
        }
        else if (par->_bf == -2) {
            // 右单旋
            if (cur->_bf == -1) {
                rotatelR(par);
            }
            else if (cur->_bf == 1) {
                // 左右双旋
                rotatelLR(par);
            }
            break;
        }


    }
    return true;
}
```



### 旋转调整

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318112249849.png" alt="image-20240318112249849" style="zoom:25%;" />



1. 根据par的bf，确定是否旋转
2. 根据cur的bf，判断是单旋转or双旋
   * par 与 cur 同符号，单旋，最后设置两个节点，par 和 cur的bf 都为 0
   * par 与 cur 异符号，双旋，最后设置三个节点，参考下方
3. 若是双旋，根据curL or  curR 判断最后三个节点的修改后的bf
   * 若curL的bf为 -1， 则修改后的值为 1， 其余为0， 根据修改后的图示标注
   * 若curL的bf为 1， 则修改后的值为 -1， 其余为0

#### 1 左单旋

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318112307830.png" alt="image-20240318112307830" style="zoom:25%;" />

```cpp
void rotatelL(Node* par) {
    Node* cur = par->_right;

    // 分别处理三个节点(30 60 A)，共6个指针 和 平衡因子
    if (cur->_left) {
        par->_right = cur->_left;
        cur->_left->_parent = par;
    }
    else {
        par->_right = nullptr;
    }

    if (par == _root) {
        _root = cur;
        cur->_parent = nullptr;
    }
    else {
        cur->_parent = par->_parent;
        if (par->_parent->_left == par) par->_parent->_left = cur;
        else par->_parent->_right = cur; 

    }
    cur->_left = par;
    par->_parent = cur;
    par->_bf = cur->_bf = 0;
} 
```

#### 2 右单旋

```cpp
void rotatelR(Node* par) {
    Node* cur = par->_left;
    // cur的右子树
    if (cur->_right) {
        par->_left = cur->_right;
        cur->_right->_parent = par;
    }
    else {
        par->_left = nullptr;
    }

    // cur
    if (par == _root) {
        _root = cur;
        cur->_parent = nullptr;
    }
    else {
        cur->_parent = par->_parent;
        if (par->_parent->_left == par) par->_parent->_left = cur;
        else par->_parent->_right = cur;
    }

    // par
    cur->_right = par;
    par->_parent = cur;
    par->_bf = cur->_bf = 0;
}
```

#### 3 右左双旋

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240318112330144.png" alt="image-20240318112330144" style="zoom:25%;" />

* 先打掉右边突出（cur） --- 右单旋
* 再左单旋（par）---- 左单选

* 分情况，根据curL的修改平衡因子策略（1， -1， 0）

```cpp
1. 画出30， 90， 60三个节点， 经过调整后为 30  60  90
2. 若curL为-1，则修改bf相反为1，其余为0，1在右侧
3. 具体节点的bf根据图进行编码
```

```cpp
void rotatelRL(Node* par) {
    Node* cur = par->_right;
    Node* curL = cur->_left;
    int bf = curL->_bf;
    rotatelR(cur);
    rotatelL(par);
    if (bf == -1) {
        par->_bf = 0;
        cur->_bf = 1;
        curL->_bf = 0;
    }
    else if (bf == 1) {
        par->_bf = -1;
        cur->_bf = 0;
        curL->_bf = 0;
    }
    // 本身就是新增
    else if (bf == 0) {
        par->_bf = 0;
        cur->_bf = 0;
        curL->_bf = 0;
    }
}
```

#### 4 左右双旋

```cpp
策略一致，先画图，再根据bf确定修改后三个节点的bf
```

```cpp
void rotatelRL(Node* par) {
    Node* cur = par->_right;
    Node* curL = cur->_left;
    int bf = curL->_bf;
    rotatelR(cur);
    rotatelL(par);
    if (bf == -1) {
        par->_bf = 0;
        cur->_bf = 1;
        curL->_bf = 0;
    }
    else if (bf == 1) {
        par->_bf = -1;
        cur->_bf = 0;
        curL->_bf = 0;
    }
    // 本身就是新增
    else if (bf == 0) {
        par->_bf = 0;
        cur->_bf = 0;
        curL->_bf = 0;
    }
}
```

#### 是否平衡

```cpp
private:
	// 判断高度
	int _Height(Node* cur) {
		if (cur == nullptr) return 0;
		int lh = _Height(cur->_left);
		int rh = _Height(cur->_right);
		return  lh > rh ? lh + 1 : rh + 1;
	}

public:
	int Height() {
		return _Height(_root);
	}
private:
	// 是否平衡
	bool _isBlance(Node* cur) {
		if (!cur) return true;
		int lh = _Height(cur->_left);
		int rh = _Height(cur->_right);

		return abs(lh - rh) < 2 && _isBlance(cur->_left) && _isBlance(cur->_right);

	}
public:
	bool isBlance() {
		return _isBlance(_root);
	} 
```

# 红黑树

## 性质：

1. 根节点为黑
2.  任意节点若为红，则子节点为黑， 结论：没有连续的红节点
3. 任意节点的简单路径上，黑色节点的数量相同  
4. 结论：红黑树的最长路径不超过最短路径的2倍，最长：1红1黑  最短：全黑

## 插入

* 插入节点均为红色

  1. 若空树，则插入节点，变为黑，当根节点

  2. 若父节点为黑，则插入完成

  3. 若父节点为红，叔为红，则修改： 父 和 叔 均变黑， 爷变红； 继续拿爷当cur向上判断

     ![image-20240314120729274](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240314120729274.png)

  4. 若父节点为红，叔节点为空或为黑，则需  旋转 + 变色 ，插入结束

     * 右单旋 + 第二层变红，第一次变黑

       ![image-20240314121446300](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240314121446300.png)

     * 左单选 + 变色

     * 双旋 + 变色

       ![image-20240314122215511](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240314122215511.png)

       

​			

# 十三 特殊类的设计

[文档地址](E:\typora索引文件\c++\C++进阶课件\Lesson09--特殊类设计.pdf)

  # 十四 std库函数

## 14.1 find

在C++中，`std::find`和`std::find_if`函数都用于在容器中查找元素，但它们的使用方式和功能有所不同。

1. **`std::find`**:
   - `std::find`用于在容器中查找指定值的元素。
   - 它接受三个参数：容器的起始迭代器、容器的结束迭代器和要查找的值。
   - 它返回一个迭代器，指向找到的第一个匹配元素的位置。如果没有找到匹配元素，则返回容器的结束迭代器。
   - `std::find`适用于查找相等的元素。

示例用法：
```cpp
#include <algorithm>
#include <vector>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    auto it = std::find(vec.begin(), vec.end(), 3); // 在vec中查找值为3的元素
    if (it != vec.end()) {
        // 找到了元素
        // ...
    } else {
        // 未找到元素
        // ...
    }
    return 0;
}
```

2. **`std::find_if`**:
   - `std::find_if`用于在容器中按照指定条件查找元素。
   - 它接受三个参数：容器的起始迭代器、容器的结束迭代器和一个谓词（predicate）函数或者函数对象。
   - 它返回一个迭代器，指向第一个使谓词返回true的元素的位置。如果没有找到满足条件的元素，则返回容器的结束迭代器。
   - `std::find_if`适用于根据特定条件查找元素。

示例用法：
```cpp
#include <algorithm>
#include <vector>

bool isOdd(int n) {
    return n % 2 != 0;
}

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    auto it = std::find_if(vec.begin(), vec.end(), isOdd); // 在vec中查找第一个奇数元素
    if (it != vec.end()) {
        // 找到了元素
        // ...
    } else {
        // 未找到元素
        // ...
    }
    return 0;
}
```

总之，`std::find`用于查找相等的元素，而`std::find_if`用于根据条件查找元素。

## 14.2 sort

![image-20240313101401357](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\image-20240313101401357.png)

## 14.3 全排列算法

* next_permutation， 求出所有的排列组合
* 1 要求升序
* 2 调用do whille 因为至少有一种泽合，打印第一种后，自动打印所有

```cpp
#include <iostream>     // std::cout
#include <algorithm>    // std::next_permutation, std::sort

int main () {
  int myints[] = {1,2,3};

  std::sort (myints,myints+3);

  std::cout << "The 3! possible permutations with 3 elements:\n";
  do {
    std::cout << myints[0] << ' ' << myints[1] << ' ' << myints[2] << '\n';
  } while ( std::next_permutation(myints,myints+3) );
;

  return 0;
}
```



### 面试题

* 算法LRU
* tcp五层、osi七层
* c 和 c++ 区别
* 网络层和链路层作用
* 指针引用区别
* 栈和队列区别
* new malloc区别
* 智能指针区别
* url网页渲染过程
* 三握四挥 ，time_wait
* tcp udp区别 更安全or更可靠
* 虚函数和纯虚函数
