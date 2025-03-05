`Link`支持你将多个树和图合并成一个图。

`TreeLink`支持你将多棵树合并成一棵树。

### 构造函数

无权重`Link`的构造函数为：

```cpp
Link(int extra_edge_count = 0, _enum::LinkType link_type = _enum::LinkType::Shuffle)
```

无权重`TreeLink`的构造函数为:

```cpp
TreeLink(_enum::TreeLinkType link_type = _enum::TreeLinkType::Shuffle)
```

有点权和边权的构造函数参考[树和图的构造函数](/user/rand_tree/basic_tree_graph.md#构造函数)。

### 额外参数

`extra_edge_count`是`Link`的一个额外参数，表示的是在合并的时候额外增加的边数，默认为$0$。

`link_type`是枚举类，类型为`LinkType`和`TreeLinkType`，默认为`Shuffle`。

关于变量的获取与设置方法，请参考[获取与设置](/user/tools/setter_getter.md)。

### 合并方式

枚举类`LinkType`和`TreeLinkType`定义如下：

```cpp
enum class LinkType {
    Direct,
    Increase,
    Shuffle,           
    Dedupe
};

using MergeType = LinkType;

enum class TreeLinkType {
    Direct,
    Increase,
    Shuffle            
};
```

比如有两个图，它们结点的编号分别是$\{1,2,3,4\}$和$\{3,4,5\}$。

#### Direct

直接将结点编号合并，但是并不会减少结点，上面的编号将会合并成$\{1,2,3,4,3,4,5\}$。

所以它的边也不会减少，但是可能会看起来有重边，即使它们原本不是同一条边。

比如第一个图有一条$3$号点到$4$号点的边，第二个图也有一个$3$号点到$4$号点的边，合并之后会输出两个`3 4`，但实际上它们储存的值是不同的，也不会被认为是重边。

#### Increase

将结点编号按照当前的`begin_node`递增，比如上面两个图的`begin_node`分别是$1$和$3$。

合并类的`begin_node`是$0$，那么上面编号就会合并为$\{0,1,2,3,4,5,6\}$。

#### Shuffle

与Increase步骤相同，更多的他会将对应的顺序给打乱。

比如Increase是$\{0,1,2,3\}$对应第一个图的点，$\{4,5,6\}$对应第二个图的点。

而`Shuffle`可能会是$\{3,5,1,2\}$对应第一个图的点，$\{4,0,6\}$对应第二个图的点。

这样边就不会看起来有规律，比如将一个菊花图和链合并，很难会出现某个编号之前的结点是菊花图，之后是链。

#### Dedupe

这**只有**`Link`有这种合并方式。

它会将点去重合并，比如上述点会合并为$\{1,2,3,4,5\}$。

所以对于`Direct`中说的情况会被视为重边，如果限制不能有重边，那么这条边就会被去重。

对于有点权的情况，它会将第一次出现的值作为新的点权，比如两个图点权分别是$\{10,20,30,40\}$和$\{-10,-20,-30\}$，那么点权会被合并为$\{10,20,30,40,-30\}$。

### 额外函数

#### set_target

`Link`是继承`Grahp`，`TreeLink`是继承`Tree`。

你可以直接通过按照[设置图属性](/user/rand_graph/basic_graph.md)设置`Link`，按照[设置树属性](/user/rand_tree/basic_tree.md)设置`TreeLink`。

你也可以用以下函数传入一个树或者图作为目标：

```cpp
set_target(TG<NodeType, EdgeType>& target)
```

对于树转换成`Link`或者图转换成`TreeLink`：

 - 树的`is_root`和图的`direction`相互转换。

 - `begin_node`，`swap_node`，`output_node_count`，`nodes_weight_function`，`edges_weight_function`相同。

**注意**：添加树或者图为目标的时候，只会关注他的基本属性，不会保证他的特殊属性，比如传入一个有向无环图，合并之后的图**并不一定**能满足有向无环图的定义。

#### add_source

可以通过以下函数将一个树或图添加进合并项：

```cpp
add_source(TG<NodeType, EdgeType>& source)
```

添加的树和图可以不用生成，如果没有生成，会根据传入的设定自动生成相应的树和图。

### 示例

1. 将一个图设为目标图，添加进不同的树和图使用`Link`进行合并。

```cpp
#include "generator.h"
#include <iomanip>
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    unweight::Graph target;
    target.set_direction(true);
    unweight::Link l;
    l.set_target(target);
    unweight::Tree t1(4);
    l.add_source(t1);
    unweight::HeightTree t2(5);
    t2.set_height(3);
    l.add_source(t2);
    unweight::Graph g1(7, 7);
    l.add_source(g1);
    unweight::CycleGraph g2(5);
    l.add_source(g2);
    l.set_extra_edges_count(10);
    l.gen();
    cout << l << endl;
    return 0;
}
```

2. 将两棵有点权的树用`TreeLink`合并，合并后的树是有根树，结点的起始编号为$2$，根为第$2$个结点（编号为$3$），可以使用不同的随机函数对两个树的点权进行随机。

```cpp
#include "generator.h"
#include <iomanip>
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    node_weight::TreeLink<int> t;
    node_weight::Tree<int> t1(4);
    node_weight::Chain<int> t2(10);
    // 用正负数显示区别
    t1.set_nodes_weight_function([]() {
        return rand_int(1, 10);
    });
    t2.set_nodes_weight_function([]() {
        return rand_int(-10, -1);
    });
    t.add_source(t1);
    t.add_source(t2);
    t.set_is_rooted(true);
    t.set_begin_node(2);
    t.set_root(2);
    t.gen();
    cout << t << endl;
    return 0;
}
```
