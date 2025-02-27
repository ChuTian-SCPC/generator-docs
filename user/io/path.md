`Path`类用于处理文件路径相关操作，提供了路径的构造、获取、拼接、转换等功能。该类支持跨平台操作，能够自动处理Windows和Linux系统的路径分隔符差异。

### 构造函数

- `Path()`

- `Path(const std::string& s)`

- `Path(const char *s)`

- `Path(const Path& other)`

- `Path(Path&& other) noexcept`

- `Path(std::string&& s) noexcept`

### 常用成员函数

- `void set_path(const char* path)`

- `void set_path(Path other_path)`

- `std::string path() const`

- `std::string& path_ref()`

- `const char* cname() const`: 获取C风格字符串形式的路径。

- `void full()`: 将路径转换为绝对路径。

- `Path full_path()`: 返回当前路径的绝对路径, 不改变当前路径。

- `Path join(const Args&... args)`: 将当前路径与多个路径片段拼接，不改变当前路径。

- `operator<<`: 支持通过流输出路径。

### 使用示例

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    Path p("."); // 当前目录
    cout << p << endl;
    p.full();
    Path p2 = p.join("test");
    cout << p << endl;
    cout << p2 << endl;
    return 0;  
}
```
比如上面的代码，假设当前所在目录是`E:\generator`，输出结果为：
```
.
E:\generator
E:\generator\test
```
