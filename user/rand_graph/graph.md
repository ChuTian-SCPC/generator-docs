### 构造函数

无权重的图的构造函数为:

```cpp
Graph(int node_count = 1, int edge_count = 0, int begin_node = 1)
```

有点权和边权的构造函数参考[图的构造函数](/user/rand_tree/basic_tree_graph.md#构造函数)。

### 示例

1. 生成一个有$10$个结点，$15$条边的无权重无向图，要求图一定连通。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;


int main() {
    init_gen();
    unweight::Graph g(10, 15);
    g.set_connect(true);
    g.gen();
    cout << g << endl;
    return 0;
}
```

2. 生成一个有$10$个结点，$15$条边的有边权无向图，图有两个边权，都是范围为$[1, 100]$的整数。
```cpp

#include <iostream>
#include <utility>

// 前置声明
std::ostream& operator<<(std::ostream& os, const std::pair<int, int>& p) {
    os << p.first << " " << p.second;
    return os;
}

#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    edge_weight::Graph<pair<int,int>> g(10, 15);
    g.set_edges_weight_function([]() {
        return make_pair(rand_int(1, 100), rand_int(1, 100));
    });
    g.gen();
    cout << g << endl;
    return 0;
}
```

3. 生成一个有$10$个结点，$15$条边的有点权有向图，点权是范围为$[1,100]$的整数，结点编号从$0$开始，允许重边，自环。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;


int main() {
    init_gen();
    node_weight::Graph<int> g(10, 15);
    g.set_direction(true);
    g.set_multiply_edge(true);
    g.set_self_loop(true);
    g.set_begin_node(0);
    g.set_nodes_weight_function([](){
        return rand_int(1, 100);
    });
    g.gen();
    cout << g << endl;
    return 0;
}
```