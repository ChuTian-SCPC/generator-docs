### 函数

- `rand_range<T>(T from, T to)`：返回一个类型为`std::pair<T, T>`的随机数对表示区间，`first`为区间左端点，`second`为区间右端点，`first`和`second`的范围为$[from，to]$。其中`T`默认均为long long。

- `rand_range<R, T, U>(T from, U to)`：返回一个类型为`std::pair<R, R>`的随机数对表示区间，`first`为区间左端点，`second`为区间右端点，`first`和`second`的范围为$[from，to]$。，其中`T`和`U`均要能转换为`R`，`R`,`T`,`U`默认均为long long。

### 示例

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
  init_gen();
  auto x = rand_range(1, 100);
  cout << x.first << " " << x.second << endl;
  return 0;
}
```