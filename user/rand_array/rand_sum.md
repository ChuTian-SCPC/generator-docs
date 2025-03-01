通常出题时会遇到：$T$组数据，每组数据有一个限制，$T$组数据总和也不会超过一个值。这个需求就可以通过`rand_sum`实现。

### 函数

- ` rand_sum<T>(int size,T sum)`：返回一个长度为$size$的随机数组`vector<T>`，数组的和为$sum$，且数组元素为正整数($\ge 1$)。

- `rand_sum<T>(int size,T sum,T min_part)`：返回一个长度为$size$的随机数组`vector<T>`，数组的和为$sum$，且数组元素大于等于`min_part`。

- `rand_sum<T>(int size, T sum, T from, T to)`：返回一个长度为$size$的随机数组`vector<T>`，数组和为$sum$，且数组元素范围为$[from,to]$。

- `rand_sum<R, S, T, U>(int size, S sum, T from, U to)`：返回一个长度为$size$的随机数组`vector<R>`，数组和为$sum$，且数组元素范围为$[from,to]$。

前三个函数中`T`需要为整型。

最后一个函数的`R`需要为整型，`S`，`T`，`U`需要为能转换成`R`的类型。

**注意**：

- 对于传入的长度，其值不能够超过`vector_limit`的限制，如果需要修改，请参考[设置](/user/setting/setting.md)。

- 有上下界的生成算法**并不**是均匀随机的，如果需要深入理解实现算法详见[rand_sum随机算法](/developer/algorithm/rand_sum.md)

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
    auto v1 = rand_sum(5, 10);
    auto v2 = rand_sum(5, 20, 3);
    auto v3 = rand_sum(5, 20, 3, 5);
    auto v4 = rand_sum<long long>(10, 1e10, 10, 2e9);
    cout << v1 << v2 << v3 << v4 << endl;
    return 0;
}
```