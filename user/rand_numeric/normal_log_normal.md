支持生成的随机数以正态分布或对数正态分布的形式。

### 构造函数

- `NormalDistribution<T>(T mean = 0, T stddev = 1)` : 构造一个正态分布随机数生成器，类型为`T`，默认为`double`。

- `LogNormalDistribution<T>(T mu = 0, T sigma = 1)` : 构造一个对数正态分布随机数生成器，类型为`T`，默认为`double`。

### 随机函数

- `T rand()` : 生成一个随机数。

- `T rand(T from, T to)` : 生成一个在 $[from, to]$ 区间内的随机数。

### 示例

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;
  
int main() {
    init_gen();
    NormalDistribution normal;
    std::cout << normal.rand() << std::endl;

    LogNormalDistribution<int> log_normal(2, 1);
    std::cout << log_normal.rand(1, 100) << std::endl;
    return 0;
}
```
