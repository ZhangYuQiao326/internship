# 一 c++17

## 1 std::optional

`std::optional`允许你表示一个可能有值也可能没有值的对象。

| 函数                      | 功能                      |
| ------------------------- | ------------------------- |
| `std::make_optional<T>()` | c++17引入，创建optional   |
| `std::nullopt`            | c++17引入，表示空optional |
| `has_value()`             | 判断是否为空              |
| `value()`                 | 不为空时获取元素          |
| `value_or()`              | 获取value或者默认值       |

## 2 std::apply

`std::apply` 是 C++17 中引入的一个函数模板，位于 `<tuple>` 头文件中。它的作用是将一个函数对象和一个元组中的参数进行绑定，并调用该函数对象

```cpp
#include <iostream>
#include <tuple>
#include <functional>

// 一个接受三个参数的函数对象
// 重载了operator()
struct Adder {
    int operator()(int a, int b, int c) const {
        return a + b + c;
    }
};

int main() {
    Adder adder; // 创建一个函数对象

    std::tuple<int, int, int> args(1, 2, 3); // 创建一个包含三个参数的元组

    // 使用 std::apply 将函数对象和参数元组绑定，并调用函数对象
    int result = std::apply(adder, args);

    std::cout << "Result: " << result << std::endl; // 输出结果：1 + 2 + 3 = 6

    return 0;
}
```

在这个例子中，`Adder` 是一个函数对象，它重载了圆括号运算符，接受三个整型参数并返回它们的和。在 `main` 函数中，首先创建了一个 `Adder` 对象 `adder`，然后创建了一个包含三个整型参数的 `std::tuple` 对象 `args`。

接着，通过 `std::apply(adder, args)` 将函数对象和参数元组绑定，并调用函数对象。`std::apply` 会将参数元组中的参数解包并传递给函数对象，最后返回函数对象的结果，这个结果被赋值给 `result`。

在这个例子中，`std::apply` 将参数元组 `(1, 2, 3)` 中的参数分别传递给函数对象 `adder`，得到的结果就是这三个参数的和，即 6。

### 1.1 创建对象

1. **直接赋值**：你可以直接将对象赋值给 `std::optional`。

```cpp
std::optional<int> optInt;
optInt = 42; // 直接赋值整数值
```

2. **使用 `emplace()` 方法**：你可以使用 `emplace()` 方法来在 `std::optional` 中构造对象。

```cpp
std::optional<Person> p;
p.emplace("Jim", 24); // 使用 emplace() 构造对象
```

3. **利用其他对象来构造**：你可以使用其他对象来构造 `std::optional` 中的对象，这将调用相应的构造函数。

```cpp
std::optional<std::vector<int>> optVec;
std::vector<int> myVector = {1, 2, 3, 4, 5};
optVec = myVector; // 使用已有的向量对象构造 optional 中的向量对象
```

4. **利用 `std::make_optional()` 工厂函数**：C++17 引入了 `std::make_optional()` 函数，它可以根据传入的参数类型推导出 `std::optional` 的模板参数，并创建对应类型的对象。

```cpp
auto optDouble = std::make_optional<double>(3.14); // 使用 make_optional() 创建 double 类型的 optional 对象
```

### 1.2 获取值

```cpp
#include <optional>
#include <iostream>

std::optional<int> optInt;

int value = optInt.value_or(10); // 如果 optional 中有值，则返回该值，否则返回默认值 10
std::cout << "Value: " << value << std::endl;

```



### 1.3 作为函数返回值

```cpp
#include <optional>
#include <iostream>

std::optional<int> readIntFromUser() {
    int value;
    if (std::cin >> value) {
        return value;
    } else {
        return std::nullopt; // 表示没有值
    }
}

int main() {
    std::optional<int> userInput = readIntFromUser();
    if (userInput.has_value()) {
        std::cout << "You entered: " << userInput.value() << std::endl;
    } else {
        std::cout << "No input provided." << std::endl;
    }
    return 0;
}

```



# 二 基础类型

## 1 数据类型

下面是各个固定宽度整数类型表示的十进制范围的表格：

| 类型       | 描述                                | 有符号/无符号 | 最小值                     | 最大值                     |
| ---------- | ----------------------------------- | ------------- | -------------------------- | -------------------------- |
| `int8_t`   | 有符号的 8 位整数                   | 有符号        | -128                       | 127                        |
| `uint8_t`  | 无符号的 8 位整数(存二进制和存Ox12) | 无符号        | 0                          | 255                        |
| `int16_t`  | 有符号的 16 位整数                  | 有符号        | -32,768                    | 32,767                     |
| `uint16_t` | 无符号的 16 位整数                  | 无符号        | 0                          | 65,535                     |
| `int32_t`  | 有符号的 32 位整数                  | 有符号        | -2,147,483,648             | 2,147,483,647              |
| `uint32_t` | 无符号的 32 位整数                  | 无符号        | 0                          | 4,294,967,295              |
| `int64_t`  | 有符号的 64 位整数                  | 有符号        | -9,223,372,036,854,775,808 | 9,223,372,036,854,775,807  |
| `uint64_t` | 无符号的 64 位整数                  | 无符号        | 0                          | 18,446,744,073,709,551,615 |

* 关于uint8_t

  `std::vector<uint8_t>` 存储的是无符号 8 位整数类型 (`uint8_t`) 的数据，这些数据实际上是以二进制形式存储的。无论您向 `std::vector<uint8_t>` 中添加的是十六进制表示的整数、二进制表示的整数还是其他格式的数据，它们最终都会以二进制形式存储在内存中。

  在 C++ 中，整数常量可以以十进制、十六进制或八进制表示。当您使用十六进制表示法时，例如 `0x12`，编译器会将其解释为一个整数值，并以二进制形式存储在内存中。同样，二进制表示法如 `"1010"` 也会被解释为整数值，并以二进制形式存储。

  因此，尽管您可能在代码中使用十六进制或二进制表示整数，但在内存中，它们实际上都是以二进制形式存储的。由于 `std::vector<uint8_t>` 存储的是字节，因此它可以容纳任何形式的数据，包括以十六进制或二进制表示的整数。

  ```cpp
  #include <iostream>
  #include <vector>
  #include <string>
  #include <iomanip>
  
  // std::vector<uint8_t> convertProtocolBodyToPacket(const std::string& protocolBody) {
  std::vector<uint8_t> convertProtocolBodyToPacket(std::vector<uint8_t> vec){
      uint8_t header = 0x12;
      std::vector<uint8_t> protocolPacket;
      protocolPacket.push_back(header);
  
      uint8_t bodyByte = 0;
      int bitCount = 0;  // 记录当前 bodyByte 中已经填充了多少位
  	// 二进制为数字
      for (auto d : vec) {
          bodyByte = (bodyByte << 1) | d;
          bitCount++;
  
          if (bitCount == 8) {  // 检查是否已填满 8 位
              protocolPacket.push_back(bodyByte);
              bodyByte = 0;
              bitCount = 0;
          }
      }
      
      // 二进制为字符
      //for (char bit : protocolBody) {
      //    bodyByte = (bodyByte << 1) | (bit - '0');
      //    bitCount++;
  
      //    if (bitCount == 8) {  // 检查是否已填满 8 位
      //        protocolPacket.push_back(bodyByte);
      //        bodyByte = 0;
      //        bitCount = 0;
      //    }
      //}
  
      // 如果还有未处理的位，将剩余部分写入 protocolPacket
      if (bitCount > 0) {
          bodyByte <<= (8 - bitCount);  // 左移剩余的位，使其成为完整的字节
          protocolPacket.push_back(bodyByte);
      }
  
      return protocolPacket;
  }
  
  int main1() {
      std::string body = "10011010";
      std::vector<uint8_t> data = { 0,1,0,0,1,0,1,1 };
      auto vec = convertProtocolBodyToPacket(data);
  
      // 以十六进制格式输出
      std::cout << "Protocol Packet: ";
      for (auto i : vec) {
          std::cout << "0x" << std::hex << std::setw(2) << std::setfill('0') << static_cast<int>(i) << " ";
      }
      std::cout << std::endl;
  
      return 0;
  }
  
  ```

  在上述示例中，将二进制数据转换为十进制是为了将其转换为字节（`uint8_t` 类型）。在封装协议时，我们通常将数据表示为字节的形式，因为在字节级别上进行数据传输是一种常见的做法。

  具体来说，在封装协议体时，我们需要将二进制数据分组成字节（8 位）的形式，并将每个字节添加到协议数据中。由于 C++ 中没有直接表示二进制字节的数据类型，因此我们首先将二进制数据转换为十进制数，然后再将其强制转换为 `uint8_t` 类型，最终存储到协议数据中。

  这种方法可以确保协议体中的每个字节都正确地表示为一个无符号的 8 位整数，并且与字节级别的数据传输相匹配。当然，您也可以直接将二进制数据存储为 `char` 类型或 `uint8_t` 类型的数组，但在这种情况下，您需要考虑如何处理不足一个字节的情况。

  

以下是一个示例代码，演示了如何封装具有协议头和协议体的数据：

```cpp
#include <iostream>
#include <vector>
#include <cstdint>

// 定义协议头和协议体的数据
const uint8_t protocolHeader = 0x12;
const std::string protocolBody = "10011010";

// 封装协议数据
std::vector<uint8_t> packageProtocol() {
    std::vector<uint8_t> protocolPacket;

    // 将协议头添加到协议数据中
    protocolPacket.push_back(protocolHeader);

    // 将协议体的二进制数据转换为十进制数，并添加到协议数据中
    uint8_t bodyByte = 0;
    for (char bit : protocolBody) {
        bodyByte = (bodyByte << 1) | (bit - '0');
        if (bodyByte & 0x80) {
            protocolPacket.push_back(bodyByte);
            bodyByte = 0;
        }
    }

    // 如果还有剩余的字节未添加，则添加到协议数据中
    if (bodyByte != 0) {
        protocolPacket.push_back(bodyByte);
    }

    return protocolPacket;
}

int main() {
    // 封装协议
    std::vector<uint8_t> protocolPacket = packageProtocol();

    // 输出封装后的协议数据
    std::cout << "Protocol Packet: ";
    for (uint8_t byte : protocolPacket) {
        std::cout << std::hex << std::setw(2) << std::setfill('0') << static_cast<int>(byte) << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

在这个示例中，我们首先定义了协议头和协议体的数据。然后，通过 `packageProtocol` 函数将协议数据封装起来。在封装过程中，我们将协议头直接添加到协议数据中，并将协议体的二进制数据转换为十进制数，然后将其以字节为单位添加到协议数据中。最后，我们在 `main` 函数中调用 `packageProtocol` 函数，并输出封装后的协议数据。

## 2 函数调用栈

[11](https://www.yigegongjiang.com/2022/%E5%87%BD%E6%95%B0%E8%B0%83%E7%94%A8%E6%A0%88%E4%B9%8B%E5%BD%BB%E5%BA%95%E7%90%86%E8%A7%A3/)

[22](https://zhuanlan.zhihu.com/p/103454656)

[33](https://mthli.xyz/stackful-stackless/)

# 三 标准库补充

| `std::`                             | exp                                      |
| ----------------------------------- | ---------------------------------------- |
| `std::conditional_t`                | 提供了在编译时根据条件选择类型           |
| `std::is_void`                      | 在编译时判断给定的类型是否是 `void` 类型 |
| `std::thread::hardware_concurrency` | 获取电脑支持的最大线程数                 |
| ``                                  |                                          |

* `std::conditional`

```cpp
#include <iostream>
#include <type_traits>

int main() {
    std::conditional<true, int, double>::type var1;  // var1 的类型是 int
    std::conditional<false, int, double>::type var2; // var2 的类型是 double

    return 0;
}

```

* `std::is_void`

```cpp
#include <iostream>
#include <type_traits>

int main() {
    std::cout << std::boolalpha; // 以布尔值形式输出
    
    std::cout << "int is void: " << std::is_void<int>::value << std::endl; // 输出 false
    std::cout << "void is void: " << std::is_void<void>::value << std::endl; // 输出 true

    return 0;
}

```

* `std::thread::hardware_concurrency`

```cpp
uint32_t threadSize = std::thread::hardware_concurrency();
```



# 四 数据结构

## std::cout

1. 控制输出的小数精度

```cpp
#include <iomanip>

double i = 2.334;
std::cout << std::fixed << setpricision(2) << i << endl;
```

2、 输入n组，含有m个整数

```cpp
int n, m;
while(cin >> n)
{
    while(n--)
    {
        cin >> m;
    }
}
```



3、 输入n组，字符串

* `cin >> s;`： 只能读取一个单词，遇到空格、回车返回
* `getline(cin, s);`：读取一行句子，遇到回车才返回

```cpp
int n;
string s;
while(cin >> n)
{
    getchar(); // 吸收掉输入n后的回车
    while(n--)
    {
        getline(cin, s);
    }
}
```



## std::iterator

| fun                    | exp                                                          |
| ---------------------- | ------------------------------------------------------------ |
| `std::advance(iter,n)` | 将迭代器iter向前或者向后移动n位，复数只适用于双向迭代器或随机迭代器 |



## std::tuple 

 元组中的每个元素可以是不同类型的数据，可以是基本类型、自定义类型或其他元组

| 函数                   | 描述                                                    |
| ---------------------- | ------------------------------------------------------- |
| `std::get`             | 获取元组中指定索引处的元素                              |
| `std::tuple_size`      | 返回元组中元素的数量                                    |
| `std::tuple_element`   | 返回元组中指定索引处的元素类型                          |
| `std::make_tuple`      | 创建一个包含给定参数的元组                              |
| `std::tie`             | 创建一个元组的引用，用于解包元组中的值                  |
| `std::tuple_cat`       | 将多个元组合并为一个元组                                |
| `std::tuple_element_t` | C++14引入的快捷方式，用于获取元组中指定索引处的元素类型 |
| `std::tuple_size_v`    | C++14引入的快捷方式，用于获取元组中元素的数量           |
| `std::swap`            | 交换两个元组的内容                                      |

```cpp
#include <tuple>

// 创建一个 std::tuple 对象，包含给定的参数
auto myTuple = std::make_tuple(arg1, arg2, arg3, ...);

```

## std::list

| 函数                                                         | 解释                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `splice(iterator position, list& x):`                        | 将列表 `x` 的所有元素移动到当前列表中，位置为 `position`,`x` 在操作之后变为空列表。 |
| `splice(iterator position, list& x, iterator i):`            | 将列表 `x` 中的单个元素 `i` 移动到当前列表中，位置为 `position` |
| `splice(iterator position, list& x, iterator first, iterator last)` | 将列表 `x` 中从 `first` 到 `last`（不包括 `last`）的元素移动到当前列表中，位置为 `position` |

```cpp
// splice()
#include <iostream>
#include <list>

int main() {
    // 初始化两个列表
    std::list<int> list1 = {1, 2, 3, 4, 5};
    std::list<int> list2 = {10, 20, 30, 40, 50};

    // 形式1：将list2的所有元素移动到list1的末尾
    list1.splice(list1.end(), list2);

    // 形式2：将list2中的单个元素移动到list1的开始
    auto it = list2.begin();
    std::advance(it, 2); // it指向list2中的第三个元素 (30)
    list1.splice(list1.begin(), list2, it);

    // 形式3：将list2中的一部分元素（从第二个到第四个）移动到list1的末尾
    auto first = list2.begin();
    auto last = list2.begin();
    std::advance(first, 1); // 指向第二个元素
    std::advance(last, 4);  // 指向第五个元素
    list1.splice(list1.end(), list2, first, last);
    return 0;
}

```

* 常用于移动自己的某个节点到某个位置

```cpp
// 1 移动it位置的节点到末尾，此时it不失效
std::list1 = {1,2,3};
auto it = list.begin();
std::advance(it,1);
list1.splice(list1.end(), list1, it);
```

## std::string

* 转化

| `string->`    | 函数                           |
| ------------- | ------------------------------ |
| `const char*` | `const char* p = str.to_ctr()` |
| `int`         | `int i = std::stoi(str)`       |

| `->std::string` | 函数                                        |
| --------------- | ------------------------------------------- |
| `const char*`   | `string str = std::string(p)`               |
| `int`           | 转化数值 `string str = std::to_string(num)` |

* 格式化字符串

```cpp
std::string result = std::format("The value of num is {} and the value of pi is {:.2f}", num, pi);
```



## std::string_view

`std::string_view` 是 C++17 引入的一种用于表示字符串的非所有权视图（view）。它提供了一种轻量级、非拥有（non-owning）的方式来引用和操作字符串数据，而无需复制字符串内容。这在需要只读访问字符串的场景中非常有用，可以避免不必要的内存分配和数据复制，从而提高性能。

1. **轻量级**：`std::string_view` 只包含一个指向字符串数据的指针和一个表示字符串长度的大小，因此其大小和效率类似于指针操作。
2. **非所有权**：`std::string_view` 不管理字符串的生命周期，它只是一个视图，因此不负责字符串内存的分配和释放。
3. **适配各种字符串类型**：`std::string_view` 可以适配 C 风格字符串（`const char*`）、`std::string`、字符串字面量等各种字符串类型。
4. **高效传递和操作**：由于不涉及复制操作，使用 `std::string_view` 作为函数参数可以避免不必要的开销，适合传递大字符串。

#### 1：基本使用
```cpp
#include <iostream>
#include <string>
#include <string_view>

void print_string(std::string_view sv) {
    std::cout << sv << std::endl;
}

int main() {
    const char* cstr = "Hello, World!";
    std::string str = "Hello, C++!";
    std::string_view sv1 = cstr;  // 从 C 风格字符串创建 string_view
    std::string_view sv2 = str;   // 从 std::string 创建 string_view
    std::string_view sv3 = "Hello, string_view!";  // 从字符串字面量创建 string_view

    print_string(sv1);
    print_string(sv2);
    print_string(sv3);

    return 0;
}
```

#### 2：截取子字符串
`std::string_view` 提供了方便的子字符串截取方法。
```cpp
#include <iostream>
#include <string_view>

int main() {
    std::string_view sv = "Hello, string_view!";
    std::string_view sub_sv = sv.substr(7, 11);  // 截取 "string_view"
    std::cout << sub_sv << std::endl;  // 输出: string_view

    return 0;
}
```

#### 3 处理不可变字符串
使用 `std::string_view` 可以避免对原始字符串的修改，从而保证数据的不可变性。
```cpp
#include <iostream>
#include <string_view>

void process_string(std::string_view sv) {
    // 只读操作，不会修改原始字符串
    std::cout << sv << std::endl;
}

int main() {
    std::string str = "Hello, World!";
    process_string(str);  // 可以传递 std::string
    process_string("Hello, C++!");  // 可以传递字符串字面量
    process_string(std::string_view("Temporary string_view"));  // 临时 string_view

    return 0;
}
```

### 注意事项
- `std::string_view` 只是一个视图，不能用于需要修改字符串的场景。
- 由于 `std::string_view` 不拥有字符串数据，因此需要确保原始字符串在 `std::string_view` 使用期间是有效的。
- 使用 `std::string_view` 可以避免不必要的字符串复制和内存分配，提高性能。

# 五 模板

## 1 模板函数返回类型自动推导

```cpp
template <typename T>
auto myFunction(T arg1, T arg2) -> decltype(arg1 + arg2) {
    // 函数体
}

```

，`auto` 关键字用于表示函数的返回类型将由后面的表达式推导得出，而 `decltype` 关键字用于获取表达式的类型。因此，`decltype(arg1 + arg2)` 将会推导出函数的返回类型，而不是显式地指定返回类型

## 2 判断模板具体类型

在C++中，模板（`template`）允许你编写与类型无关的代码，但有时候你可能需要在模板内部获取模板参数的具体类型 `T`，以便对该类型执行某些操作或进行类型推导。C++提供了一些方法和工具来实现这一目的。

### 方法1: 使用`typeid`操作符

如果你只是想在运行时获取`T`的类型信息，可以使用`typeid`操作符，它返回一个`std::type_info`对象。你可以将其与`type_info::name()`结合使用，来输出类型名称。

```cpp
#include <iostream>
#include <vector>
#include <typeinfo>

template <typename T>
void printType(const std::vector<T>& vec) {
    std::cout << "Type of T is: " << typeid(T).name() << std::endl;
}

int main() {
    std::vector<int> vec;
    printType(vec); // 输出 "Type of T is: i" (i 表示 int 类型)
    return 0;
}
```

### 方法2: 使用`std::is_same`进行类型比较

如果你想在编译时进行类型判断，可以使用`std::is_same`进行类型比较，以此判断`T`是否为特定类型。

```cpp
#include <iostream>
#include <vector>
#include <type_traits>

template <typename T>
void checkType(const std::vector<T>& vec) {
    if (std::is_same<T, int>::value) {
        std::cout << "T is int" << std::endl;
    } else if (std::is_same<T, double>::value) {
        std::cout << "T is double" << std::endl;
    } else {
        std::cout << "T is another type" << std::endl;
    }
}

int main() {
    std::vector<int> vec1;
    checkType(vec1); // 输出 "T is int"

    std::vector<double> vec2;
    checkType(vec2); // 输出 "T is double"

    std::vector<std::string> vec3;
    checkType(vec3); // 输出 "T is another type"
    return 0;
}
```

### 方法3: 使用`decltype`和`auto`

`decltype`和`auto`都是在C++11引入的特性，允许你在编译时推导类型。如果你在模板函数中需要捕获传入的模板参数类型，可以结合`decltype`来获得`T`的类型。

```cpp
#include <iostream>
#include <vector>

template <typename T>
void printElementType(const std::vector<T>& vec) {
    auto firstElement = vec[0]; // 使用 auto 自动推导类型
    std::cout << "Type of T is: " << typeid(decltype(firstElement)).name() << std::endl;
}

int main() {
    std::vector<int> vec = {1, 2, 3};
    printElementType(vec); // 输出 "Type of T is: i" (i 表示 int 类型)

    std::vector<double> vec2 = {1.0, 2.0, 3.0};
    printElementType(vec2); // 输出 "Type of T is: d" (d 表示 double 类型)

    return 0;
}
```

### 方法4: 使用模板特化

如果你需要为特定类型提供特殊的处理逻辑，可以使用模板特化来区分不同类型的处理方式。

```cpp
#include <iostream>
#include <vector>

template <typename T>
void handleVector(const std::vector<T>& vec) {
    std::cout << "Generic handleVector called" << std::endl;
}

template <>
void handleVector<int>(const std::vector<int>& vec) {
    std::cout << "Specialized handleVector for int called" << std::endl;
}

int main() {
    std::vector<int> vec1 = {1, 2, 3};
    handleVector(vec1); // 输出 "Specialized handleVector for int called"

    std::vector<double> vec2 = {1.0, 2.0, 3.0};
    handleVector(vec2); // 输出 "Generic handleVector called"

    return 0;
}
```



- 使用 `typeid(T).name()` 可以在运行时输出类型的名称（虽然这通常是平台相关的并且未必是易读的）。
- 使用 `std::is_same<T, Type>::value` 可以在编译时判断类型是否相同。
- 使用 `decltype` 和 `auto` 可以让编译器推导类型。
- 使用模板特化可以对不同类型进行不同的处理。



# 六 Cmake

## 0 预置量

| 名称               | 内容                            |
| ------------------ | ------------------------------- |
| `CMAKE_SOURCE_DIR` | 项目根目录,vs中打开的最顶级目录 |
| `SRC_FILE`         |                                 |

```cmake
cmake_minimum_required(VERSION 3.5)
project(MyProject VERSION 1.0 LANGUAGES CXX)

# 找第三方库
find_package(Qt5 COMPONENTS Widgets REQUIRED)

# 头文件搜索路径
include_directories(${CMAKE_SOURCE_DIR})
# 生成可执行文件
add_executable(MyExecutable main.cpp)
# 生成目标库
add_library(mylib STATIC source1.cpp)
# 链接库
target_link_libraries(MyExecutable PRIVATE Qt5::Widgets)

# 安装
install(TARGETS MyExecutable DESTINATION bin)
```

## 1 设置依赖

1. **add_dependencies**：

   - `add_dependencies`命令用于指定一个目标（target）依赖于其他目标。它不会设置编译器的链接选项，只是表示在构建某个目标之前，需要先构建其他的目标。

   - 该命令通常用于在构建某个目标之前，先构建该目标所依赖的其他目标。例如，在构建一个可执行文件之前，可能需要先构建一些库文件。

   - 确保依赖的声明在`add_dependencies`之后

   - `add_dependencies`命令的语法为：
     ```cmake
     add_dependencies(target-name dependency1 dependency2 ...)
     ```

## 2 设置输出目录

1. **CMAKE_RUNTIME_OUTPUT_DIRECTORY**：
   - 这个变量用于设置可执行文件（例如.exe文件）的输出目录。
   - 当你使用`add_executable()`命令定义可执行文件时，可以通过设置`CMAKE_RUNTIME_OUTPUT_DIRECTORY`变量来指定可执行文件的输出目录。
   - 例如，通过设置`set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)`，可将所有的可执行文件输出到项目根目录下的bin目录中。

2. **CMAKE_LIBRARY_OUTPUT_DIRECTORY**：
   - 这个变量用于设置共享库文件（例如.dll文件、.so文件等）的输出目录。
   - 当你使用`add_library()`命令定义共享库文件时，可以通过设置`CMAKE_LIBRARY_OUTPUT_DIRECTORY`变量来指定共享库文件的输出目录。
   - 例如，通过设置`set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)`，可将所有的共享库文件输出到项目根目录下的lib目录中。

3. **CMAKE_ARCHIVE_OUTPUT_DIRECTORY**：
   - 这个变量用于设置归档文件（静态库文件，例如.lib文件、.a文件等）的输出目录。
   - 当你使用`add_library()`命令定义静态库文件时，可以通过设置`CMAKE_ARCHIVE_OUTPUT_DIRECTORY`变量来指定静态库文件的输出目录。
   - 例如，通过设置`set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)`，可将所有的静态库文件输出到项目根目录下的lib目录中。

通过设置这些变量，你可以更加灵活地控制项目中各种类型文件的输出位置。

## 4 生成文件

cmake最终的生成文件有两类：要么生成库文件，要么是可执行文件

### 4.1 生成目标库

```cmake
add_library(library_name [STATIC | SHARED | MODULE] sources...)
```

- `library_name`: 库的名称。
- `STATIC | SHARED | MODULE`: 指定库的类型，分别表示静态库、动态库和可加载模块，默认为静态库。
- `sources...`: 库的源文件列表。

示例：
```cmake
# 创建一个名为 mylib 的静态库
add_library(mylib STATIC source1.cpp source2.cpp)
```

### 4.2 生成可执行文件

```cmake
add_executable(CSM
            ${PROJECT_SOURCES}

            CSM-CTC/csm_ctc.h CSM-CTC/csm_ctc.cpp CSM-CTC/csm_ctc.ui
            pagemanger.h pagemanger.cpp
        )
```

### 4.3 链接 目标库/可执行文件

这些库可以是系统库、第三方库或项目内部生成的库。

```cmake
target_link_libraries(target_name [PRIVATE|PUBLIC|INTERFACE] library1 [library2 ...])
```

- `target_name`：目标的名称，可以是通过 `add_executable` 或 `add_library` 命令定义的目标名称。
- `library1`, `library2` 等：要链接的库的名称。可以是系统库、第三方库或项目内部生成的库。

- `PRIVATE`：只有当前目标及其依赖目标可以访问链接库。
- `PUBLIC`：除了当前目标和其依赖目标外，还可以访问链接库的任何目标。
- `INTERFACE`：只有依赖目标可以访问链接库，而当前目标不能访问。

```cmake
# 将 MyExecutable 与 Qt Widgets 库链接
target_link_libraries(MyExecutable PRIVATE Qt5::Widgets)

# 将 MyLibrary 与 OpenSSL 和 Threads 库链接
target_link_libraries(MyLibrary PRIVATE OpenSSL::SSL Threads::Threads)

# 将 MyExecutable 与 MyLibrary 和 MyOtherLibrary 链接，同时使 MyOtherLibrary 对 MyExecutable 不可见
target_link_libraries(MyExecutable PRIVATE MyLibrary)
target_link_libraries(MyExecutable PUBLIC MyOtherLibrary)
```

## 5 链接三方库

1. `include_directories("../include")` 导入头文件目录

2. `find_package`用查找第三方库的lib文件，用于cmake编译。比如Boost、Qt、opencv等

2. 然后通过`target_link_libraries`将dll动态库链接到目标库或可执行文件中

```cmake
# 查找并加载 Qt5 的 Widgets 模块
find_package(Qt5 COMPONENTS Widgets REQUIRED)

# 链接 Qt5 的 Widgets 模块到目标库或可执行文件
target_link_libraries(my_target Qt5::Widgets)
```

```cmake
# lib
set(CMAKE_PREFIX_PATH "D:/self/GraduationProject/libs/opencv/build/x64/vc16/lib")
find_package(OpenCV REQUIRED)
# dll
target_link_libraries(my_target ${OpenCV_LIBS})
```



`CMAKE_PREFIX_PATH`是一个CMake变量，用于指定在`find_package`搜索依赖包时要搜索的路径。这个变量通常用于告诉CMake在哪里可以找到所需的依赖包。

具体来说，当你使用`find_package()`命令来查找某个依赖包时，CMake会按照以下顺序搜索依赖包：

1. 首先，它会搜索系统默认的安装路径。
2. 然后，它会搜索`CMAKE_PREFIX_PATH`变量中指定的路径----注意指定到lib库。
3. 最后，它会搜索其他默认路径。

因此，通过设置`CMAKE_PREFIX_PATH`变量，你可以告诉CMake在特定的路径下搜索依赖包。

对于Qt来说，如果你将Qt安装在非默认的路径下，你可以通过设置`CMAKE_PREFIX_PATH`来告诉CMake在Qt的安装路径下搜索Qt相关的模块。例如：

```cmake
set(CMAKE_PREFIX_PATH "/path/to/Qt")
```

这样CMake就会在指定的路径下搜索Qt相关的模块。

## 5 文件操作

下面是一些常见 `file` 命令用法的代码示例，展示了如何在 CMake 中使用这些命令来执行各种文件系统操作。

| 参数           | 功能             |
| -------------- | ---------------- |
| 创建目录       | `MAKE_DIRECTORY` |
| 复制文件       | `MOVE`           |
| 重命名         | `RENAME`         |
| 删除文件       | `REMOVE`         |
| 获取文件列表   | `GLOB`           |
| 读取文件       | `READ`           |
| 写入文件       | `WRITE`          |
| 追加写入       | `APPEND`         |
| 文件大小       | `SIZE`           |
| 时间戳         | `TIMESTAMP`      |
| 转换为指定路径 | `RELATIVE_PATH`  |

> 获取当前目录下的所有cpp h文件

```cmake
 file(GLOB_RECURSE SRC_FILES *.cpp *.c)

 add_executable(${PROJECT_NAME}
     ${SRC_FILES}

 )
```

> 创建一个或多个目录：

```cmake
cmake_minimum_required(VERSION 3.5)
project(CreateDirectoryExample)

# 创建单个目录
file(MAKE_DIRECTORY ${CMAKE_BINARY_DIR}/new_directory)

# 创建多个目录
file(MAKE_DIRECTORY ${CMAKE_BINARY_DIR}/dir1 ${CMAKE_BINARY_DIR}/dir2)
```



> 将文件从一个位置复制到另一个位置：

```cmake
# 假设有一个文件 source.txt
file(COPY ${CMAKE_SOURCE_DIR}/source.txt DESTINATION ${CMAKE_BINARY_DIR})
```

> 将文件从一个名称重命名为另一个名称：

```cmake
# 假设有一个文件 oldname.txt
file(RENAME ${CMAKE_SOURCE_DIR}/oldname.txt ${CMAKE_SOURCE_DIR}/newname.txt)
```

> 删除一个或多个文件：

```cmake
cmake_minimum_required(VERSION 3.5)
project(RemoveFileExample)

# 假设有一些文件要删除
file(REMOVE ${CMAKE_SOURCE_DIR}/file1.txt ${CMAKE_SOURCE_DIR}/file2.txt)
```

> 使用 `GLOB` 获取目录中所有匹配指定模式的文件列表：

```cmake
# 获取所有 .cpp 和 .h 文件
file(GLOB cpp_files ${CMAKE_SOURCE_DIR}/*.cpp)
file(GLOB header_files ${CMAKE_SOURCE_DIR}/*.h)

# 打印找到的文件
message("CPP files: ${cpp_files}")
message("Header files: ${header_files}")
```

> 读取文件内容并存储到变量中：

```cmake
cmake_minimum_required(VERSION 3.5)
project(ReadFileExample)

# 假设有一个文件 example.txt
file(READ ${CMAKE_SOURCE_DIR}/example.txt file_content)
message("File content: ${file_content}")
```

>  将内容写入文件：

```cmake
cmake_minimum_required(VERSION 3.5)
project(WriteFileExample)

# 写入内容到文件
file(WRITE ${CMAKE_BINARY_DIR}/output.txt "Hello, CMake!\n")
```

> 在文件末尾追加内容：

```cmake
cmake_minimum_required(VERSION 3.5)
project(AppendFileExample)

# 追加内容到文件
file(APPEND ${CMAKE_BINARY_DIR}/output.txt "This is appended text.\n")
```

> 获取文件的大小：

```cmake
cmake_minimum_required(VERSION 3.5)
project(FileSizeExample)

# 假设有一个文件 example.txt
file(SIZE ${CMAKE_SOURCE_DIR}/example.txt file_size)
message("File size: ${file_size} bytes")
```

> 获取文件的时间戳：

```cmake
cmake_minimum_required(VERSION 3.5)
project(FileTimestampExample)

# 假设有一个文件 example.txt
file(TIMESTAMP ${CMAKE_SOURCE_DIR}/example.txt file_timestamp)
message("File timestamp: ${file_timestamp}")
```

> 将文件的绝对路径转换为相对于指定目录的相对路径：

```cmake
cmake_minimum_required(VERSION 3.5)
project(RelativePathExample)

# 获取文件的相对路径
file(RELATIVE_PATH relative_path ${CMAKE_SOURCE_DIR} ${CMAKE_SOURCE_DIR}/subdir/example.txt)
message("Relative path: ${relative_path}")
```

这些示例展示了如何在 CMake 中使用 `file` 命令来进行文件系统操作，从而在构建过程管理项目的文件和目录。

## 6 层级调用

```
|--------------newWork  
|-----1---CMakeLists.txt
|
|--------channel
|--channel.h                     // 使用本项目构建的库
|--channel.cpp
|-2-CMakeLists.txt               // 生成channel动态库
|
|--------protocal
|-3-CMakeLists.txt
|--protocal.h                    // 使用channel动态库、三方库
|--protocal.cpp					 // 生成可执行文件
|
```

```cmake
// 1
cmake_minimum_required(VERSION 3.5)

project(network)

add_subdirectory(channel)

add_subdirectory(protocol)
```

```cpp
// 2
cmake_minimum_required(VERSION 3.5)

project(WDTech.CSM2020.Network.Protocol.channel)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

// 生成位置
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/../bins/dlls/${PROJECT_NAME})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/../bins/dlls/${PROJECT_NAME})
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/../bins/dlls/${PROJECT_NAME})

add_definitions(-D_CASE_API_EXPORT)

remove_definitions(-DUNICODE)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

// 打包资源文件 .h .cpp
file(GLOB SRC_FILES *.cpp *.c *h)

// 生成动态库
add_library(${PROJECT_NAME} SHARED
    ${SRC_FILES} 
)

// 三方库
set(SYS_LIBS
    ws2_32
)

set(3RD_LIBS
    zip/zlib1    
)

// 使用本项目构建的库
set(LOCAL_LIBS 
    WDTech.CSM2020.Utils
    WDTech.CSM2020.Coroutine.ThreadPool
    WDTech.CSM2020.Coroutine.Loop
    WDTech.CSM2020.Coroutine.Log    
)

// 链接库
target_link_libraries(${PROJECT_NAME} PRIVATE 
    ${SYS_LIBS}
    ${LOCAL_LIBS}
    ${3RD_LIBS}
)

// 确保生成四个文件 .dll  .cdb  .lib  .exp
set_target_properties(${PROJECT_NAME} PROPERTIES
    WINDOWS_EXPORT_ALL_SYMBOLS ON
    CXX_VISIBILITY_PRESET hidden
    VISIBILITY_INLINES_HIDDEN ON
)

endif()

```

```cmake
// 3
cmake_minimum_required(VERSION 3.5)

project(WDTech.CSM2020.Tools.Simulate)

if(NOT DEFINED ENV{QT_DIR})
	message("Not Define QT_DIR")
else()
    message("QT_DIR: $ENV{QT_DIR}")

    set(CMAKE_PREFIX_PATH $ENV{QT_DIR}) # Qt Kit Dir

//生成位置
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/../bins/${PROJECT_NAME})
    set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/../bins/${PROJECT_NAME})
    set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/../bins/${PROJECT_NAME})

    remove_definitions(-DUNICODE)

    set(CMAKE_AUTOUIC ON)
    set(CMAKE_AUTOMOC ON)
    set(CMAKE_AUTORCC ON)
// 查找三方库
    find_package(Qt5 COMPONENTS Widgets REQUIRED)

// 生成可执行文件
    add_executable(${PROJECT_NAME} WIN32
        main.cpp

        ${CMAKE_SOURCE_DIR}/includes/utils/create_dump.cpp
    )

    

    set(SYS_LIBS
        ws2_32

        Qt5::Widgets
    )

    set(3RD_LIBS
        zip/zlib1
    )
// 使用本项目构建的库
    set(LOCAL_LIBS 
		WDTech.CSM2020.network.channel   
    )

    target_link_libraries(${PROJECT_NAME} PRIVATE 

        ${SYS_LIBS}
        ${LOCAL_LIBS}
        ${3RD_LIBS}
    )

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

    add_dependencies(${PROJECT_NAME}
        ${PLUGIN_LIBS}
    )

    COPY_DLLS(PRJ_NAME ${PROJECT_NAME} 3RD_LIBS ${3RD_LIBS} LOCAL_LIBS ${LOCAL_LIBS} PLUGIN_LIBS ${PLUGIN_LIBS})
endif()
```

## 7 生成库生成文件

###  7.1 生成动态库

1. **.dll 文件**是实际的动态链接库，包含程序运行时所需的代码和数据。
2. **.pdb 文件**包含调试信息，帮助开发人员调试程序。
3. **.lib 文件**是导入库，包含符号信息，使编译和链接依赖于该 DLL 的程序成为可能。
4. **.exp 文件**记录了导出的符号，帮助链接器正确处理导出过程。

**动态链接库文件**：`.dll` 文件是动态链接库，包含了编译后的代码和数据。（一本书）

- **作用**：它包含实际的可执行代码和数据，供其他程序在运行时加载和使用。
- **用途**：在运行时，由应用程序或其他 DLL 文件加载，提供其中定义的功能和服务。

**程序数据库文件**：`.pdb` 文件包含调试信息。

- **作用**：提供函数名、变量名、源代码行号等调试信息，帮助开发人员调试程序。
- **用途**：调试过程中，调试器使用 `.pdb` 文件来显示源代码和相关调试信息，便于开发人员进行断点设置、查看变量值等操作。

**导入库文件**：`.lib` 文件用于在编译和链接过程中使用。

- **作用**：包含函数和数据的符号信息，指向 DLL 文件中实际代码和数据的位置。（目录）
- **用途**：在编译依赖于该 DLL 的应用程序时，编译器和链接器使用 `.lib` 文件来解析对 DLL 中符号的引用。它使得在链接过程中可以找到并链接到 DLL 中的导出函数和数据。

**导出文件**：`.exp` 文件包含导出符号的信息。（哪些章节可见）

- **作用**：列出所有从 DLL 中导出的函数和变量。
- **用途**：链接器在创建 DLL 文件时生成 `.exp` 文件，用于记录导出符号。这在一些复杂的链接过程中可能会用到，特别是在手动处理导出符号时。

```cmake
// 链接库
target_link_libraries(${PROJECT_NAME} PRIVATE 
    ${SYS_LIBS}
    ${LOCAL_LIBS}
    ${3RD_LIBS}
)

// 确保生成四个文件 .dll  .cdb  .lib  .exp
set_target_properties(${PROJECT_NAME} PROPERTIES
    WINDOWS_EXPORT_ALL_SYMBOLS ON
    CXX_VISIBILITY_PRESET hidden
    VISIBILITY_INLINES_HIDDEN ON
)
```



### 7.2 生成静态库

生成静态库时，通常会生成以下文件：

- **.lib 文件（静态库）**：包含了所有编译后的代码和数据，编译时将这些代码嵌入到你的可执行文件中，使得程序独立运行。
- **.pdb 文件（程序数据库，可选）**：包含调试信息，帮助开发人员在调试时查看源代码和程序状态。

| 库     | .dll     | .lib                                                         |
| ------ | -------- | ------------------------------------------------------------ |
| shared | 书的内容 | 书的目录，多个exe链接时候加载目录，执行时通过目录索引一本数的内容 |
| static | /        | 没有索引，直接加载书的内容。每个exe加载自己的lib             |













# 七 windows API

| API                | 功能                                            |
| ------------------ | ----------------------------------------------- |
| `GetProcAddress()` | 从指定的动态链接库（DLL）中获取一个函数的地址。 |
| ``                 |                                                 |
| ``                 |                                                 |
| ``                 |                                                 |
| ``                 |                                                 |

* `GetProcAddress()`

```cpp
// 获取指定函数的地址
void *DllUtils::dllSymbol(void *dll, const char *funcName)
{
    return GetProcAddress((HMODULE)dll, funcName);
}
```



# 八 位运算--协议

| 运算   | 功能                                                         | 作用                         |
| ------ | ------------------------------------------------------------ | ---------------------------- |
| 按位&  | `5 & 3`的二进制表示是 `0101 & 0011`，结果是 `0001`，即 `1    | 获取低8位字节，` val & 0xFF` |保留低n位|
| 按位\| | `5 |3` 的二进制表示是 `0101 |0011`，结果是 `0111`，即 `7`    | 字节左移，加上一位           |
| 异或^  | 二进制位不同时为1，5 ^ 3` 的二进制表示是 `0101 ^ 0011`，结果是 `0110`，即 `6 |                              |
| 取反~  | ~5` 的二进制表示是 `~0101`，结果是 `1010                     |                              |
| 左移<< | 右侧用0填充                                                  |                              |
| 右移>> | 左侧根据符号位填充（对无符号数`uint8_t`则用0填充)            |                              |
|        |                                                              |                              |

## 8.0 字节内部的低位和高位

在计算机科学和数字电子学中，低位（Least Significant Bit, LSB）在二进制数表示中位于右边，这种表示方式称为 **小端序**（Little-endian）。理解这种表示方法的原因需要从几个角度进行探讨，包括历史背景、数字表示的规范和计算机体系结构。

在二进制数系统中，每一位（bit）代表一个值的幂次方，这些幂次方是以2为基数。对于一个 `n` 位的二进制数：

- 最右边的位（即第 0 位）是 \(2^0\)，称为 **最低有效位**（LSB）。
- 最左边的位（第 `n-1` 位）是 \(2^{n-1}\)，称为 **最高有效位**（MSB）。

例如，二进制数 `1011`：

- 右边的位是 \(2^0\) 和 \(2^1\)，这些是低位。
- 左边的位是 \(2^2\) 和 \(2^3\)，这些是高位。

### 8.0.1 数学表示习惯

在传统的数学表示法中，数值是从右到左排列的，低位在右，高位在左。例如，十进制数 `1234` 表示为：

- `4` 在 \(10^0\) 位置（个位）。
- `3` 在 \(10^1\) 位置（十位）。
- `2` 在 \(10^2\) 位置（百位）。
- `1` 在 \(10^3\) 位置（千位）。

这种表示方式的逻辑和二进制数的排列方式是相同的，因此将低位放在右边是自然的选择。

### 8.0.2 计算机存储和表示

在计算机系统中，**内存地址**是从低到高顺序排列的，这种排列方式影响了数据的存储和访问顺序。在小端序系统中，数据的最低有效字节存储在最低的内存地址，这种方式有助于优化某些操作和提高处理器的效率。

现代大多数处理器采用小端序（Little-endian）模式来存储和处理数据。小端序的主要特点是：

- 数字的最低有效字节存储在最低的地址位置。
- 数据读取和写入更加简化和高效，尤其是对数据进行部分处理时。

例如，对于一个 `32` 位的整数 `0x12345678`，在小端序系统中，它将被存储为 `78 56 34 12`（从最低到最高地址）。

虽然dubug显示的整数还是12345678，但是实际存储是 78 56 34 12，查看时，系统自动将其转为大端序

## 8.1 封装协议顺序

封装协议需要注意两种顺序

### 8.1.1 字节序

有大端和小端之分，协议封装时，会给出：**低字节在前，高字节在后**等要求

1. 获取到的十进制==时间、长度、个数等值
2. 获取的结果是默认按照==大端序==：**高字节在前，低字节在后** 的字节序
3. 按照要求，调为小端序

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202406201054999.png" alt="image-20240620105412588" style="zoom: 80%;" />

![image-20240620105759246](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202406201057653.png)

```cpp
uint16_t protocalDataLen = 20;  // 默认大端序

// vector的顺序代表：内存顺序从小到大存储
std::vector<uint8_t> m_protocalPacket;

// 采用大端
m_protocalPacket[10] = static_cast<uint8_t>(protocalDataLen >> 8  & 0xFF); // 高字节在前
m_protocalPacket[11] = static_cast<uint8_t>(protocalDataLen & 0xFF); // 低字节在后

// 调为小端
m_protocalPacket[10] = static_cast<uint8_t>(protocalDataLen  & 0xFF); // 低字节在前
m_protocalPacket[11] = static_cast<uint8_t>(protocalDataLen >> 8 & 0xFF); // 高字节在后
```



### 8.1.2 位序

1. 按照bit位数封装成字节
2. 根据题目要求：**0~7bit位 存放 0~7数据**， 或者是 **0~7bit位 存放 7~0 数据**

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202406201039864.png" alt="image-20240620103900494" style="zoom:50%;" />



* 封装顺序：**0~7bit位 存放 7~0 数据**

```cpp

uint8_t bodyByte = 0; // 临时处理字节
int bitCount = 0;  // 记录当前 bodyByte 中已经填充了多少位

for (auto bit : vec) {
    bodyByte = (bodyByte << 1) | bit;  // 左移，加入一位(顺序存储)
    bodyByte = bodyByte  | (bit << bitCount);  // 左移，加入一位(逆序存储 或者 顺序存储+下面逆置函数)
    bitCount++;

    if (bitCount == 8) {  // 检查是否已填满 8 位
        protocolPacket.push_back(bodyByte);
        bodyByte = 0;
        bitCount = 0;
    }
}
// 不够8位，用0填充
if (bitCount > 0) {
	bodyByte <<= (8 - bitCount);
	m_protocalPacket[protocalIndex++] = bodyByte;
}
```

* 封装顺序：**0~7bit位 存放 0~7数

```cpp
// 在上述封装基础上，逆置字节数据的位数
uint8_t reverseBits(uint8_t n)
{
	uint8_t reversed = 0;
	for (int i = 0; i < 8; ++i)
	{
		reversed |= ((n >> i) & 0x01) << (7 - i);
	}
	return reversed;
}
```



## 8.2 获取指定位数bit

### 8.2.1 获取第k位bit

```cpp
#include <iostream>

int main() {
    int n = 29; // 例如，二进制为 11101
    int k = 3;  // 获取第 3 位（从 0 开始计数，实际是第 4 位）

    int bit = (n >> k) & 1; // 右移 k 位后，与 1 进行 AND 操作
    std::cout << "第 " << k << " 位的值是: " << bit << std::endl;

    return 0;
}

// 修改第k位为1
body |= (1 << k);
```



### 8.2.1 从低位（最后）获取n位

```cpp
#include <iostream>

int main() {
    unsigned int value = 12345; // 原始整数，二进制为 11000000111001
    int n = 8; // 我们想保留的比特位数

    unsigned int result = value & ((1 << n) - 1); // 直接使用位操作保留前 n 位 
    return 0;
}

```



### 8.3.2  获取高低字节

```cpp
uint16_t value = 305;
// 低字节
uint8_t lowerByte = static_cast<uint8_t>(value & 0xFF);
// 高字节
uint8_t highByte = static_cast<uint8_t>(value >> 8 & 0xFF);

     00000001 00110001  // dataSegmentLength (305 in binary)
&    00000000 11111111  // 0xFF (255 in binary)
---------------------
     00000000 00110001  // Result: only the low 8 bits are preserved

```

### 8.3.4 指定位取反

异或：位相同为0，不同为1

```cpp
#include <iostream>
#include <cstdint>  // for uint8_t

uint8_t flip_bit(uint8_t num, int n) {
    // 生成只在第 n 位为 1 的掩码
    uint8_t mask = 1 << n;
    
    // 按位异或，将第 n 位取反
    num ^= mask;
    
    return num;
}

```





## 8.3 打印16进制

```cpp
#include <iostream>
#include <vector>
#include <iomanip> // for std::hex, std::setw, and std::setfill

int main() {
    // 定义并初始化一个 vector<uint8_t>
    std::vector<uint8_t> vec = {0x1, 0xA, 0xFF, 0xB, 0x10};

    // 遍历 vec 中的每个元素并打印为16进制格式
    for (auto i : vec) {
        std::cout << "0x" 
                  << std::hex << std::setw(2) << std::setfill('0') 
                  << static_cast<int>(i) << " ";
    }

    // 打印换行符
    std::cout << std::endl;

    return 0;
}

```

`"0x"`：打印每个值的前缀，表示这是一个十六进制数。

`std::hex`：将输出格式设置为十六进制。

`std::setw(2)`：设置输出宽度为2个字符。

`std::setfill('0')`：用 `0` 填充不足的宽度。

`static_cast<int>(i)`：将 `i` 强制转换为 `int` 类型。这是因为 `uint8_t` 实际上是一个 `unsigned char`，直接输出时会被解释为字符。转换为 `int` 后，输出其整数值。

`" "`：在每个十六进制数之间添加一个空格



# 九 按结构体封装协议

```cpp
struct ZPW2000HostDataFrame
{
    uint8_t protocolVersion;
    uint16_t len;
    uint8_t sendSeq;
    uint8_t ackSeq;
    uint8_t type;
    uint8_t linkType;
    uint8_t reverse;
    int32_t time;
    char data[];    // 灵活数组 不计sizeof,不需要提前固定大小，使用时候分配 
};
void ZPW2000HostEmulatorForm::encapsulateDataProtocal()
{
    if (m_alarmCache.empty()) return;

	const uint32_t bufferLen = sizeof(ZPW2000HostDataFrame) + 7; // 使用时候分配
	char* databuffer = std::make_shared<char[]>(bufferLen).get();
    ZPW2000HostDataFrame* dataFrame = (ZPW2000HostDataFrame*)databuffer;

	auto sendSeq = m_sendSeq++;
	if (sendSeq > 240)
	{
		sendSeq = 1;
		m_sendSeq = 1;
	}

	dataFrame->protocolVersion = 0x20;
	dataFrame->len = 0x13; 
	dataFrame->sendSeq = sendSeq;
	dataFrame->ackSeq = m_ackSeq;
	dataFrame->type = 0x21;
	dataFrame->linkType = 0x10;
    dataFrame->reverse = 0x00;
	dataFrame->time = (int32_t)time(0);
	
    // 数据区内容+ 结束符
    m_sendBytes.clear();
	for (auto [lineIndex, alarmdata] : m_alarmCache)
	{
        std::vector<uint8_t> tmp (7, 0);
        tmp[0] = alarmdata.seq;
        tmp[1] = alarmdata.alarmType;
        tmp[2] = alarmdata.level;

        tmp[3] = 0x43;
        tmp[4] = 0x52;
        tmp[5] = 0x53;
        tmp[6] = 0x43;
        memcpy(dataFrame->data , tmp.data(), tmp.size()); // 用memcpy拷贝

        // send
        QByteArray byteData(databuffer, sizeof(ZPW2000HostDataFrame) + tmp.size());
        m_sendBytes.push_back(byteData);
	}
    return;
}
```



