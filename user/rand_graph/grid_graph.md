### 构造函数

无权重的网格图的构造函数为:

```cpp
GridGraph(int node_count = 1, int edge_count = 0, int begin_node = 1, int row = -1)
```
有点权和边权的构造函数参考[图的构造函数](/user/rand_tree/basic_tree_graph.md#构造函数)。

### 禁用函数

网格图是无自环的，以下函数被禁用：

```cpp
void set_self_loop(bool self_loop);
```

### 额外变量

- `row`：网格图的行数，默认为-1$，表示随机行数。

- `column`：网格图的列数。

它们的范围为$[1,node\_count]$。

关于变量的获取与设置方法，请参考[获取与设置](/user/tools/setter_getter.md)。

此外还可以通过以下函数设置行和列大小：

```cpp
set_row_column(int row, int column, int ignore = 0)
```

其中，`ignore`表示最后一行少的点数，它应该小于$column$。

它会计算新的结点数$n = row\times column - ignore$，如果$node\_count \neq n$，会将`node_count`设置为$n$。

考虑到网格图边数上限比较难计算，在随机`row`的情况下，会计算出最大可能的边数`m`，如果`edge_count`大于它，会将`edge_count`设为`m`。

### 示例：

1. 生成一个没有权重的无向网格图，结点数为$9$，$3$行$3$列，$12$条边。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    unweight::GridGraph g(9, 12);
    g.set_row(3);
    g.gen();
    cout << g << endl;
    return 0;
}
```

2. 生成一个没有权重的有向网格图，结点数为$10$，设置边数为$100$，最后因为随机`row`将它换成上限$26$。
```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    unweight::GridGraph g(10, 100);
    g.set_direction(true);
    g.gen();
    cout << g << endl;
    return 0;
}
```