### 构造函数

无权重限制最大儿子数的树的构造函数为:

```cpp
MaxSonTree(int node = 1, int begin_node = 1, int root = 1, int max_son = -1)
```

有点权和边权的构造函数参考[树的构造函数](/user/rand_tree/basic_tree_graph.md#构造函数)

### 禁用函数

由于儿子结点是有根树的概念，所以`MaxSonTree`必须是有根树。

以下函数禁用:

```cpp
void set_is_rooted(bool is_rooted);
```

### 额外变量

限制最大儿子数的树通过`max_son`对度数进行限制。

`max_son`默认为$-1$，即随机度数。

对于`max_son`的限制为：

- $node\_count = 1$时，$max\_son = 0$。

- $node\_count \ge 2$时，$max\_son$的范围是$[1, node\_count - 1]$。

- 对于$max\_son \gt node\_count - 1$，限制相当于不存在，但依旧可以使用`gen()`生成。

关于变量的获取与设置方法，请参考[获取与设置](/user/tools/setter_getter.md)。

### 示例

生成一个有$10$个结点的无权重**二叉树**，即它的最大儿子数为$2$，根为默认值$1$。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;


int main() {
    init_gen();
    unweight::MaxSonTree t(10);
    t.set_max_son(2);
    t.gen();
    cout << t << endl;
    return 0;
}
```