### 函数

- `rand_vector<T>(int size, std::function<T()> func)`：返回一个长度为$size$的随机数组`vector<T>`，数组元素为`func()`的返回值。

- `rand_vector<T>(int from, int to, std::function<T()> func)`：返回一个长度范围为$[from, to]$的随机数组`vector<T>`，数组元素为`func()`的返回值。

**注意**：对于传入的长度，其值不能够超过`vector_limit`的限制，如果需要修改，请参考[设置](/user/setting/setting.md)。

### 示例

可以通过`rand_vector`生成随机数组，也能通过嵌套生成随机二维数组：

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int gen() {
  return rand_int(0, 9);
}
template <typename T>
ostream& operator<<(ostream& os, const vector<T>& v) {
    for (int i = 0; i < v.size(); i++) {
        os << v[i] << " ";
    }
    os << endl;
    return os;
}
int main() {
  init_gen();
  auto v1 = rand_vector<int>(10, gen);
  auto v2 = rand_vector<double>(5, 10, []() {
    return rand_real("[1.000000, 2.000000]");
  });
  // 生成多维数组
  auto v3 = rand_vector<vector<int>>(10, []() {
    return rand_vector<int>(10, gen);
  });
  cout << v1 << v2;
  for (auto& v : v3) cout << v;
  return 0;
}
```