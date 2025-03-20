这个图是指对于一个有向图，从一个指定点出发可以到达其他所有的点。

### 构造函数

无权重的单源可达图的构造函数为：

```cpp
StartReachableGraph(int node_count = 1, int edge_count = 0, int begin_node = 1, int start = 1)
```

有点权和边权的构造函数参考[图的构造函数](/user/rand_tree/basic_tree_graph.md#构造函数)。

### 禁用函数

单源可达图是有向图，保证连通。

以下函数被禁用：

```cpp
void set_direction(bool direction);
void set_connect(bool connect);
```

### 额外变量

`start`表示源点是第几个点，默认为$1$。

关于变量的获取与设置方法，请参考[获取与设置](/user/tools/setter_getter.md)。

其中需要注意的是，它的逻辑与[root的设置和获取](/user/rand_tree/basic_tree.md#root)类似，可以参考。

### 示例

生成一个没有权重$10$个点$15$条边的单源可达图，保证第$2$个点可以到达其他所有点。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
  init_gen();
  unweight::StartReachableGraph g(10, 15);
  g.set_start(2);
  g.gen();
  cout << g << endl;
  return 0;
}
```

