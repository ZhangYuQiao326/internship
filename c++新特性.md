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





