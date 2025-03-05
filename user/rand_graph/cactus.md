### 构造函数

无权重的仙人掌的构造函数为:

```cpp
Cactus(int node_count = 1, int edge_count = 0, int begin_node = 1) 
```

有点权和边权的构造函数参考[图的构造函数](/user/rand_tree/basic_tree_graph.md#构造函数)。

### 禁用函数

仙人掌是无重边，无自环，一定连通的无向图，以下函数被禁用：

```cpp
void set_direction(bool direction);
void set_multiply_edge(bool multiply_edge);
void set_self_loop(bool self_loop);
void set_connect(bool connect);
```

### 示例

生成一个有$10$个结点，$10$条边的无权重仙人掌图。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    unweight::Cactus g(10, 10);
    g.gen();
    cout << g << endl;
    return 0;
}
```