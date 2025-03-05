### 构造函数

无权重的有向无环图的构造函数为:

```cpp
DAG(int node_count = 1, int edge_count = 0, int begin_node = 1)
```

有点权和边权的构造函数参考[图的构造函数](/user/rand_tree/basic_tree_graph.md#构造函数)。

### 禁用函数

有向无环图是有向，无自环的图，以下函数被禁用：

```cpp
void set_direction(bool direction);
void set_self_loop(bool self_loop);
```

### 示例

生成一个没有权重的有向无环图，结点数为$10$，边数为$15$。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;


int main() {
    init_gen();
    unweight::DAG g(10, 15);
    g.gen();
    cout << g << endl;
    return 0;
}
```