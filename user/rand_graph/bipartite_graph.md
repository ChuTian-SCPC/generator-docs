### 构造函数

无权重的二分图的构造函数为:

```cpp
BipartiteGraph(int node_count = 1, int edge_count = 0, int begin_node = 1, int left = -1)
```

有点权和边权的构造函数参考[图的构造函数](/user/rand_tree/basic_tree_graph.md#构造函数)。

### 禁用函数

二分图是无自环的无向图，以下函数被禁用：

```cpp
void set_direction(bool direction);
void set_self_loop(bool self_loop);
```

### 额外变量

- `left`：左部的结点数，默认为$-1$，表示随机左部结点数。

- `right`：右部的结点数。

- `_different_part`：是否采用左部和右部分别编号，默认为`false`。

- `node_output_format`：结点输出格式，详见[二分图输出格式](/user/rand_graph/basic_graph.md#特例二分图)，默认为`Node`。

左部和右部分别编号是指左部的结点编号为$[begin\_node, left+begin\_node]$，右部的结点编号为$[begin\_node,right+begin\_node]$。

它们的范围为$[0,node\_count)$。

比如对于一个二分图，左部有$3$个结点，右部有$4$个结点，结点编号从$1$开始，那么左部的结点编号为$\{1,2,3\}$，右部的结点编号为$\{1,2,3,4\}$。

类似[UOJ#78二分图最大匹配](https://uoj.ac/problem/78)中的格式就是如此。

关于变量的获取与设置方法，请参考[获取与设置](/user/tools/setter_getter.md)。

此外还可以通过以下函数设置左部和右部大小：

```cpp
set_left_right(int left, int right)
```

**注意**：这个会判断$left + right$是否等于$node\_count$，如果不等于，会将$node\_count$设置为$left + right$。

### 示例

1. 生成一个$10$个结点，$15$条边的二分图，左右部随机大小。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;


int main() {
    init_gen();
    unweight::BipartiteGraph g(10, 15);
    g.gen();
    cout << g << endl;
    return 0;
}
```

2. 生成一个$10$个结点，$9$条边的二分图，左部结点个数为$3$，对左部和右部分别编号，要求一定连通，输出格式为`LeftRight`，即分别输出左部和右部的大小。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;


int main() {
    init_gen();
    unweight::BipartiteGraph g(10, 9);
    g.set_left(3);
    g.set_connect(true);
    g.set_different_part(true);
    g.use_format_left_right();
    g.gen();
    cout << g << endl;
    return 0;
}
```