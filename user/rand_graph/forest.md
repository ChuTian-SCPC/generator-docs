### 构造函数

无权重的森林的构造函数为:

```cpp
Forest(int node_count = 1, int edge_count = 0, int begin_node = 1)
```

有点权和边权的构造函数参考[图的构造函数](/user/rand_tree/basic_tree_graph.md#构造函数)。

### 禁用函数

森林是无向，无重边，无自环的图，以下函数被禁用：

```cpp
void set_direction(bool direction);
void set_multiply_edge(bool multiply_edge);
void set_self_loop(bool self_loop);
void set_connect(bool connect);
```

### 额外变量

`trees_size`表示每个子树的大小，默认是一个空集，表示随机生成。

关于变量的获取与设置方法，请参考[获取与设置](/user/tools/setter_getter.md)。

还可以通过以下函数设置子树大小：

- `add_tree_size(int tree_size)`：添加一个大小为`tree_size`的子树，其值需要大于$0$。

- `set_trees_size(std::vector<int> trees_size)`：设置所有子树大小。

如果子树的集合中有值，并且与`node_count`和`edge_count`不相符，则会用新的值替换掉`node_count`和`edge_count`的值。

### 示例

1. 生成一个$10$个点，$7$条边的无权重森林。

```cpp
#include "generator.h"
#include <iomanip>
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    unweight::Forest g(10, 7);
    g.gen();
    cout << g << endl;
    return 0;
}
```

2. 生成一个森林，它的子树大小为$\{2,3,4,5\}$。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    unweight::Forest g;
    g.set_trees_size({2, 3, 4, 5});
    g.gen();
    cout << g << endl;
    return 0;
}
```
