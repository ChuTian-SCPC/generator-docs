该函数用于根据输入整数序列构造一个索引频次数组，使用偏移量调整索引计算方式,返回一个 vector<int> 作为结果。

返回数组中，每个元素的值表示对应索引+偏移量的出现次数。数组的索引从$0$开始。

比如传入的数组为$\{3,1,2\}$，偏移量为1，则返回的数组中， $1$ 会出现 $3$ 次； $2$ 会出现 $1$ 次； $3$ 会出现 $2$ 次。。

### 函数

- `shuffle_index(Iter begin, Iter end, int offset = 0)`：返回一个频次统计数组，其中索引$i$处的值表示输入序列中$i + offset$位置上的元素值。

    其中`Iter`的类型为迭代器，且需要满足：
    
    - `Iter` 必须是输入迭代器。

    - 两个迭代器必须指向同一容器内的合法元素范围。
  
    - `Iter` 所指的值需为整型。
- `vector<int> shuffle_index(vector<int> v, int offset = 0)`：返回一个频次统计数组，其中索引$i$处的值表示输入序列中$i + offset$位置上的元素值。

**注意**：

- 数组中元素不能为负数。

- 数组中元素值的总和不能够超过`vector_limit`的限制，如果需要修改，请参考[设置](/user/setting/setting.md)。

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
  int v1[] = {1, 2, 3};
  vector<int> v2 = {3, 1, 2};
  auto p1 = shuffle_index(v1, v1 + 3);
  auto p2 = shuffle_index(v2, 2);
  cout << p1 << p2;
  return 0;
}
```