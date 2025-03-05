### 构造函数

无权重的环图的构造函数为:

```cpp
CycleGraph(int node_count = 3, int begin_node = 1)
```

有点权和边权的构造函数参考[图的构造函数](/user/rand_tree/basic_tree_graph.md#构造函数)。

### 禁用函数

环图是无重边，无自环，一定连通，边数一定的图，以下函数被禁用：

```cpp
void set_multiply_edge(bool multiply_edge);
void set_connect(bool connect);
void set_self_loop(bool self_loop);
void set_edge_count(int count);
```

### 变量限制

环图的`node_count`必须大于等于$3$，其`edge_count`等于$node\_count$。

### 示例

生成一个没有权重的环图，结点数为$10$，不输出边数。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    unweight::CycleGraph g(10);
    g.set_output_edge_count(false);
    g.gen();
    cout << g << endl;
    return 0;
}
```
