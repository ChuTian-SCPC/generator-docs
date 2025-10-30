### 函数

- `KeyType rand_prob(const Container& map)`：

    - map的类型为`std::map<KeyType, ValueType>`或者`std::unordered_map<KeyType, ValueType>`，其中`ValueType`为整型。

    - 返回一个类型为`KeyType`的随机数，随机数生成的概率由map决定。

    - map中所有值的总和为$sum$，一个随机数$x$的生成概率为$\frac{map[x]}{sum}$。

    - 所以map中所有值的总和必须大于$0$，且任意一个值都不能小于$0$。

- `KeyType rand_prob(const ProbTable<KeyType>& prob)`：
    - prob的类型为`ProbTable<KeyType>`，详见[概率表(ProbTable)](/user/rand_numeric/prob_table.md)。

    - 返回一个类型为`KeyType`的随机数，随机数生成的概率由prob决定。

**注意**：如果多次随机采用相同的概率分布，建议使用`ProbTable`减少时间开销。

### 示例

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    map<char, int> m = {
      {'a', 3},
      {'b', 1},
      {'c', 6}
    };
    // 随机的字符时，'a'的概率为3/10，'b'的概率为1/10，'c'的概率为6/10
    char x = rand_prob(m);
    cout << x << endl;

    ProbTable<char> p(m);
    cout << rand_prob(p) << endl;
    return 0;
}
```