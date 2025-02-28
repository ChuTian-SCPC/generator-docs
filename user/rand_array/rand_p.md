### 函数

- `rand_p<T>(T n)`：返回一个长度为$n$的随机排列`vector<T>`，从$0$开始。

- `rand_p<T, E>(T n, E s)`：返回一个长度为$n$的随机排列`vector<E>`，从$s$开始。

**注意**：对于传入的长度，其值不能够超过`vector_limit`的限制，如果需要修改，请参考[设置](/user/setting/setting.md)。

### 示例

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

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
    auto v1 = rand_p(5);
    auto v2 = rand_p(6, 'b');
    cout << v1 << v2;
    return 0;
}
```