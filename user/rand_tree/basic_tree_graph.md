### 基础形式

树和图的函数都在命名空间`generator::rand_graph`下，这已经被`generator::all`包含了。

它们所有的实现都在`basic`命名空间下，但是这部分的内容在常规使用下是不需要了解的。

它们都被分成了四种形式，比如对于`Tree`：

- `unweight::Tree`：无点权，无边权的树。

- `node_weight::Tree<NodeType>`：有点权，无边权的树。

- `edge_weight::Tree<EdgeType>`：无点权，有边权的树。

- `both_weight::Tree<NodeType, EdgeType>`：有点权，有边权的树。

其中`NodeType`是点权类型，`EdgeType`为边权类型。

在设置有点权或者有边权的情况下需要设置生成点权或者边权的函数。

除此之外，用法都是一致的。

### 生成函数设置

对于点权`nodes_weight_function`，它的类型是`std::function<NodeType()>`，其中`NodeType`是点权的类型。

对于边权`edges_weight_function`，它的类型是`std::function<EdgeType()>`，其中`EdgeType`是边权的类型。

在有点权和边权的情况下，需要通过`set_nodes_weight_function`和`set_edges_weight_function`来设置生成点权和边权的函数。

获取该变量的方法请见[获取与设置](/user/tools/setter_getter.md)，注意在没有或者没设置点权或边权的情况下，获取的是`nullptr`。

### 点权和边

对于**有点权**的情况，会有`nodes_weight`表示点权，它的类型是`std::vector<_Node<NodeType>>`。

对于边，会有`edges`表示边，它的类型是`std::vector<_Edge<EdgeType>>`。

它们输出的格式请见[点和边的输出格式](/user/rand_tree/node_edge.md)。

它们**不能**直接设置，只能够获取，使用的方法请见[获取](/user/tools/setter_getter.md)。

对于**无点权**的情况，也不能获取它的点权。

### 使用方式

对于所有的树和图，在设置好之后，调用`gen()`函数即可生成，然后使用`std::ostream& <<`进行输出。

每个树和图都有默认的输出格式，一般情况下满足大部分需求。如果需要自定义输出格式，详见[自定义输出格式](/user/tools/set_output.md)。

每个树和图都有默认的生成方式，如果需要自定义生成方式，详见[自定义生成器](/user/tools/set_generator.md)。

### 示例

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;


int main() {
    init_gen();
    edge_weight::Tree<int> t;
    t.set_edges_weight_function([]() { return rand_int(1, 10);});
    t.set_node_count(10); // 设置10个点
    t.gen();
    cout << t << endl;

    unweight::Graph g(10, 15); // 10个点，15条边
    g.gen();
    cout << g << endl;
    return 0;
}
```
