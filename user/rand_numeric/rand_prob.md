### 函数

- `rand_prob(const Con& map)`：

    - map的类型为`std::map<T, U>`或者`std::unordered_map<T, U>`，其中`U`为整型。

    - 返回一个类型为`T`的随机数，随机数生成的概率由map决定。

    - map中所有值的总和为$sum$，一个随机数$x$的生成概率为$\frac{map[x]}{sum}$。

    - 所以map中所有值的总和必须大于$0$，且任意一个值都不能小于$0$。

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
    return 0;
}
```