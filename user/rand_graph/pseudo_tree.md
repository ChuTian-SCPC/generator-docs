### 构造函数

无权重的基环（外向、内向）树的构造函数为：

```cpp
PseudoTree(int node_count = 3, int begin_node = 1, int cycle = -1)    // 基环树
PseudoInTree(int node_count = 3, int begin_node = 1, int cycle = -1)  // 基环外向树
PseudoOutTree(int node_count = 3, int begin_node = 1, int cycle = -1) // 基环内向树
```

有点权和边权的构造函数参考[图的构造函数](/user/rand_tree/basic_tree_graph.md#构造函数)。

### 禁用函数

基环树是无重边，无自环，一定连通，边数一定的无向图；基环外向树和基环内向树与基环树的不同点是有向图。

以下函数被禁用：

```cpp
void set_direction(bool direction);
void set_multiply_edge(bool multiply_edge);
void set_self_loop(bool self_loop);
void set_connect(bool connect);
void set_edge_count(int count);
```

### 额外变量

`cycle`表示环的大小，默认为$-1$，表示随机环的大小。

由于`cycle`的大小要大于等于$3$，所以`node_count`也有此限制。

关于变量的获取与设置方法，请参考[获取与设置](/user/tools/setter_getter.md)。

### 示例

1. 生成一个没有权重的基环树，结点数为$10$，不输出边数。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    unweight::PseudoTree g(10);
    g.set_output_edge_count(false);
    g.gen();
    cout << g << endl;
    return 0;
}
```

2. 生成一个没有权重的基环外向树，结点数为$10$，环大小为$5$。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    unweight::PseudoOutTree g(10);
    g.set_cycle(5);
    g.gen();
    cout << g << endl;
    return 0;
}
```