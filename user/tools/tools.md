
## 字符串拼接

可以通过如下函数将多个支持<<操作符的类型拼接成一个字符串：

```cpp
template <typename... Args>
std::string string_join(std::string split, const Args&... args);

template <typename... Args>
std::string string_join(char split, const Args&... args);
```

其中`split`为分隔符，`args`为需要拼接的对象。

比如对于以下的代码：

```cpp
#include <vector>
#include <iostream>
// 前置声明
std::ostream& operator<<(std::ostream& os, const std::vector<int>& v) {
    os << "[";
    for (size_t i = 0; i < v.size(); i++) {
        if (i > 0) os << ", ";
        os << v[i];
    }
    return os << "]";
}

#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    vector<int> v{7, 8, 9};
    string s = string_join(" ", 123, 'c', 1.24, "hello world", v);
    cout << s << endl;
    return 0;  
}
```

会得到如下输出：

```
123 c 1.24 hello world [7, 8, 9]
```

## 字符串格式化

可以通过如下函数将字符串进行C风格的格式化：

```cpp
std::string string_format(const char* format, ...)
```

比如对于以下代码：

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    string s = string_format("[%d, %s]", 1, "321");
    cout << s << endl;
    return 0;  
}
```

会得到如下输出：

```
[1, 321]
```