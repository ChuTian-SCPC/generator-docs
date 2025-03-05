树和图共同的部分参考[树和图基础](/user/rand_tree/basic_tree_graph.md)。

### 图共同的成员变量

- `node_count`：图的结点数。

- `edge_count`：图的边数。

- `begin_node`：结点编号起始值，默认为$1$。

- `direction`：是否为有向图，默认为`false`，即无向图。

- `multiply_edge`：是否允许重边，默认为`false`，即无重边。

- `self_loop`：是否允许自环，默认为`false`，即无自环。

- `connect`：是否强制连通，默认为`false`，即不强制连通。

- `node_indices`：结点编号，默认为$[begin\_node, node\_count + begin\_node]$。

- `nodes_weight_function`：生成点权的函数，只有在有点权时才有效。

- `edges_weight_function`：生成边权的函数，只有在有边权时才有效。

- `edges`：图的边。

- `nodes_weight`：图的点权，只有在有点权时才有效。

- `swap_node`：在输出时候是否会随机交换结点顺序，通常情况下对有向图默认为`false`，无向图默认为`true`。

- `output_node_count`：在输出时是否输出结点数，默认为`true`。

- `output_edge_count`：在输出时是否输出边数，默认为`true`。

以上变量基本可以通过[获取与设置](/user/tools/setter_getter.md)中的方法使用，需要特别注意的有：

#### `edges`和`nodes_weight`

`edges`和`nodes_weight`的情况与[树edges和nodes_weight的获取](/user/rand_tree/basic_tree.md#edges和nodesweight)相同。

#### `direction`和`swap_node`

在设置`direction`的时候，如果与原本的值不同，是会将`swap_node`修改：

对`direction`是`true`，即有向图的时候，`swap_node`为`false`;

对`direction`是`false`，即无向图的时候，`swap_node`为`true`。

这也是`swap_node`的默认值。

除了二分图，它虽然是无向图，但是`swap_node`为`false`。

这也是设计`swap_node`的[思路](/developer/algorithm/swap_node.md)。

### 输出格式

所有的图的通用输出格式为:

第一行两个正整数$n,m$分别表示树的结点数和边数，以一个空格隔开。

如果`output_node_count`为`false`，则不输出$n$；`output_edge_count`为`false`，则不输出$m$。

如果有点权，接下来一行输出$n$个点权$v$，之间以一个空格隔开。

$v$的输出格式以[点权的输出格式](/user/rand_tree/node_edge.md#输出格式)为准，你可以自定义输出格式。

接下来$m$行，每行两个正整数$u,v$，以及在有边权的情况下一个边权$w$，表示$u$和$v$之间有一条边，边权为$w$。

$u$，$v$和$w$输出格式以[边的输出格式](/user/rand_tree/node_edge.md#e8be93e587bae6a0bce5bc8f-1)为准，你可以自定义输出格式。

**注意**：输出最后是没有换行的。

#### 特例：二分图

二分图的输出支持以下几种格式:

```cpp
enum NodeOutputFormat {
    Node,      // 只输出结点数
    LeftRight, // 输出左部大小和右部大小
    NodeLeft,  // 输出结点数和左部大小
    NodeRight  // 输出结点数和右部大小
};
```

可以通过以下函数指定输出格式:

```cpp
set_node_output_format(NodeOutputFormat format)
use_format_node()
use_format_left_right()
use_format_node_left()
use_format_node_right()
```

与通用输出格式不同的是，它会将输出$n$的地方替换成指定的格式，如果有两个变量，中间以一个空格隔开。

比如对于`LeftRight`，第一行输出三个正整数$l,r,m$分别表述左部大小，右部大小和边数，中间均以一个空格隔开。

### 生成算法

对于单纯的使用来说，并不需要详细了解生成使用的算法。

如果你想要详细了解生成使用的算法，可以参考[开发者手册：图的随机算法](/developer/algorithm/graph.md)