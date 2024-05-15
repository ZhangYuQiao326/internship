# c++17

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



# 基础类型

## 1 数据类型

下面是各个固定宽度整数类型表示的十进制范围的表格：

| 类型       | 描述               | 有符号/无符号 | 最小值                     | 最大值                     |
| ---------- | ------------------ | ------------- | -------------------------- | -------------------------- |
| `int8_t`   | 有符号的 8 位整数  | 有符号        | -128                       | 127                        |
| `uint8_t`  | 无符号的 8 位整数  | 无符号        | 0                          | 255                        |
| `int16_t`  | 有符号的 16 位整数 | 有符号        | -32,768                    | 32,767                     |
| `uint16_t` | 无符号的 16 位整数 | 无符号        | 0                          | 65,535                     |
| `int32_t`  | 有符号的 32 位整数 | 有符号        | -2,147,483,648             | 2,147,483,647              |
| `uint32_t` | 无符号的 32 位整数 | 无符号        | 0                          | 4,294,967,295              |
| `int64_t`  | 有符号的 64 位整数 | 有符号        | -9,223,372,036,854,775,808 | 9,223,372,036,854,775,807  |
| `uint64_t` | 无符号的 64 位整数 | 无符号        | 0                          | 18,446,744,073,709,551,615 |

## 2 函数调用栈

[11](https://www.yigegongjiang.com/2022/%E5%87%BD%E6%95%B0%E8%B0%83%E7%94%A8%E6%A0%88%E4%B9%8B%E5%BD%BB%E5%BA%95%E7%90%86%E8%A7%A3/)

[22](https://zhuanlan.zhihu.com/p/103454656)

[33](https://mthli.xyz/stackful-stackless/)

# 标准库补充

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



# 数据结构

 **std::tuple ：**元组中的每个元素可以是不同类型的数据，可以是基本类型、自定义类型或其他元组

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

# 模板

## 1 模板函数返回类型自动推导

```cpp
template <typename T>
auto myFunction(T arg1, T arg2) -> decltype(arg1 + arg2) {
    // 函数体
}

```

，`auto` 关键字用于表示函数的返回类型将由后面的表达式推导得出，而 `decltype` 关键字用于获取表达式的类型。因此，`decltype(arg1 + arg2)` 将会推导出函数的返回类型，而不是显式地指定返回类型



# Cmake

## 0 预置量

| 名称               | 内容                            |
| ------------------ | ------------------------------- |
| `CMAKE_SOURCE_DIR` | 项目根目录,vs中打开的最顶级目录 |



## 1 设置依赖

1. **add_dependencies**：

   - `add_dependencies`命令用于指定一个目标（target）依赖于其他目标。它不会设置编译器的链接选项，只是表示在构建某个目标之前，需要先构建其他的目标。

   - 该命令通常用于在构建某个目标之前，先构建该目标所依赖的其他目标。例如，在构建一个可执行文件之前，可能需要先构建一些库文件。

   - 确保依赖的声明在`add_dependencies`之后

   - `add_dependencies`命令的语法为：
     ```cmake
     add_dependencies(target-name dependency1 dependency2 ...)
     ```

2. **target_link_libraries**：

   - `target_link_libraries`命令用于将目标（target）链接到一个或多个库。它设置了链接器的选项，以便将指定的库链接到目标中。

   - 该命令通常用于指定目标需要链接的第三方库或自定义库。

   - `target_link_libraries`命令的语法为：
     ```cmake
     target_link_libraries(target-name library1 library2 ...)
     ```

## 2 设置依赖包要索的路径

`CMAKE_PREFIX_PATH`是一个CMake变量，用于指定在搜索依赖包时要搜索的路径。这个变量通常用于告诉CMake在哪里可以找到所需的依赖包。

具体来说，当你使用`find_package()`命令来查找某个依赖包时，CMake会按照以下顺序搜索依赖包：

1. 首先，它会搜索系统默认的安装路径。
2. 然后，它会搜索`CMAKE_PREFIX_PATH`变量中指定的路径。
3. 最后，它会搜索其他默认路径。

因此，通过设置`CMAKE_PREFIX_PATH`变量，你可以告诉CMake在特定的路径下搜索依赖包。

对于Qt来说，如果你将Qt安装在非默认的路径下，你可以通过设置`CMAKE_PREFIX_PATH`来告诉CMake在Qt的安装路径下搜索Qt相关的模块。例如：

```cmake
set(CMAKE_PREFIX_PATH "/path/to/Qt")
```

这样CMake就会在指定的路径下搜索Qt相关的模块。

## 3 设置输出目录

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
