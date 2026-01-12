`CountRange<T>`表示限制一个值出现的次数在范围之中。

### 构造函数

```cpp
CountRange(T value, long long from = 0LL, long long to = _setting::count_range_inf)
```

### 成员变量

- `T value`：表示要限制的数值。

- `long long from`：表示出现次数的下限，默认为$0$。

- `long long to`：表示出现次数的上限，默认为`_setting::count_range_inf`。

以上变量基本可以通过[获取与设置](/user/tools/setter_getter.md)中的方法使用。

也可以通过以下函数设置`from`和`to`：

- `void set_range(long long from, long long to)`

- `void set_range(std::string s)`：根据字符串s解析得到的区间范围设置。详解[整型格式解析](/user/rand_numeric/format.md#整数范围)。

**注意**：格式解析不支持`inf`。

### 示例

保证随机生成的序列中一定存在$1$个$1$。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    std::vector<CountRange<int>> vars;
    vars.push_back(CountRange<int>(1, 1, 1));
    for (int i = 2; i <= 100; i++) {
        vars.push_back(CountRange<int>(i));
    }
    auto p = rand_vector(20, vars); 
    println(p);
    return 0;
}
```

