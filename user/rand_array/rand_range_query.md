### 函数

- `rand_range_query<T>(int q, T from, T to)`：返回一个类型为`std::vector<std::pair<T, T>>`的随机数对数组表示$q$个区间，每个区间的左端点和右端点的范围为$[from，to]$。其中`T`默认均为long long。

- `rand_range_query<R, T, U>(int q, T from, U to)`：返回一个类型为`std::vector<std::pair<R, R>>`的随机数对数组表示$q$个区间，每个区间的左端点和右端点的范围为$[from，to]$。其中`T`和`U`均要能转换为`R`，`R`,`T`,`U`默认均为long long。

- `rand_range_query<T>(int q, T from, T to, T lower)`：返回一个类型为`std::vector<std::pair<T, T>>`的随机数对数组表示$q$个区间，每个区间的左端点和右端点的范围为$[from，to]$，且区间长度总和不小于$lower$。其中`T`默认均为long long。

- `rand_range_query<R, T, U, F>(int q, T from, U to, F lower)`：返回一个类型为`std::vector<std::pair<R, R>>`的随机数对数组表示$q$个区间，每个区间的左端点和右端点的范围为$[from，to]$，且区间长度总和不小于$lower$。其中`T`，`U`和`F`均要能转换为`R`，`R`,`T`,`U`,`F`默认均为long long。

- `rand_range_query<T>(int q, T from, T to, T lower, T upper)`：返回一个类型为`std::vector<std::pair<T, T>>`的随机数对数组表示$q$个区间，每个区间的左端点和右端点的范围为$[from，to]$，且区间长度总和范围为$[lower，upper]$。其中`T`默认均为long long。

- `rand_range_query<R, T, U, F, S>(int q, T from, U to, F lower, S upper)`：返回一个类型为`std::vector<std::pair<R, R>>`的随机数对数组表示$q$个区间，每个区间的左端点和右端点的范围为$[from，to]$，且区间长度总和范围为$[lower，upper]$。其中`T`，`U`，`F`和`S`均要能转换为`R`，`R`,`T`,`U`,`F`,`S`默认均为long long。

**注意**：区间长度为$to - from + 1$。

### 示例

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
  init_gen();
  auto x1 = rand_range_query(10, 1, 100);
  for (auto p : x1) cout << p.first << " " << p.second << endl;
  auto x2 = rand_range_query(10, 1, 100, 100);
  for (auto p : x2) cout << p.first << " " << p.second << endl;
  auto x3 = rand_range_query(10000, 1, 1e6, 1e9, 2e9);
  for (auto p : x3) cout << p.first << " " << p.second << endl;
  return 0;
}
```
