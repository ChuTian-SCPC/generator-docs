### 构造函数

无权重的菊花带链的构造函数为:

```cpp
FlowerChain(int node = 1, int begin_node = 1, bool is_rooted = false, int root = 1, int flower_size = -1)
```

有点权和边权的构造函数参考[树的构造函数](/user/rand_tree/basic_tree_graph.md#构造函数)。

### 额外变量

- `flower_size`：菊花图的结点个数。

- `chain_size`：链的结点个数。

默认情况下`flower_size`是$-1$，表示随机菊花图的结点个数。

它们的范围为$[0,node\_count]$。

关于变量的获取与设置方法，请参考[获取与设置](/user/tools/setter_getter.md)。

此外还可以通过以下函数设置菊花图和链的结点个数：

```cpp
set_flower_chain_size(int flower_size, int chain_size)
```

**注意**：这个会判断$flower\_size+chain\_size$是否等于`node_count`，如果不等于，会将`node_count`设置为$flower\_size+chain\_size$。

### 示例

生成一个有$10$个结点的无权重无根**菊花带链**，菊花图结点个数为$6$，链的结点个数为$4$。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;


int main() {
    init_gen();
    unweight::FlowerChain t(10);
    t.set_flower_size(6);
    t.gen();
    cout << t << endl;
    return 0;
}
```