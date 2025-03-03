在所有类（树，图，几何）中，都有默认的生成方法。

但是许多方法都是我个人的思路，它不一定是符合均匀随机的，也不一定是符合一些特殊需求的。

对于想要自己实现生成器的情况，也有方法可以自定义生成器。

对于每个类，其内部都有一个`Gen*`类型的指针，指向一个生成器。

- 对于树使用`set_tree_generator(Gen*)`设置生成器。

- 对于图使用`set_graph_generator(Gen*)`设置生成器。

- 对于几何使用`set_geometry_generator(Gen*)`设置生成器。

每一个类都有一个默认生成器，它的名字是`类Gen`，比如`Tree`是`TreeGen`，`Graph`是`GraphGen`，`ConvexHull`是`ConvexHullGen`。

在生成器中的成员变量`_context`表示原本的类，它是这个类的引用，可以对这个类的成员变量进行获取和修改。

从最容易实现的角度，你可以继承这些默认的生成器，然后重写函数生成函数：

- 对于树重写`__generate_tree()`。

- 对于图重写`__generate_graph()`。

- 对于几何重写`__generate_geometry()`。

这是最简单的修改方式，也是绝大部分情况下足够使用的，如果需要修改更多的逻辑，可以查看相关的源代码去重写对应的函数。

当然如果你能够详细了解`Gen`的逻辑，你也可以完全从底层构建一套生成器，如果你对此感兴趣，可以详见[Gen的设计](/developer/algorithm/gen.md)。

比如对于一棵树，你希望随机的父亲结点只会在它前两个结点中选择，但是这是原本生成器所不提供的，你可以自定义生成的方式：

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

class MySelfGen : public edge_weight::TreeGen<int> {
public:
    MySelfGen(edge_weight::Tree<int>& t) : edge_weight::TreeGen<int>(t) {}
protected:
    virtual void __generate_tree() override {
        for (int i = 1; i < this->_context.node_count(); i++) {
            __add_edge(i, max(0, i - 2));
        }
    }

};

int main() {
    init_gen();
    edge_weight::Tree<int> t;
    t.set_edges_weight_function([]() { return rand_int(1, 10);});
    t.set_tree_generator(new MySelfGen(t));
    t.set_node_count(10);
    t.gen();
    cout << t;
    return 0;
}
```

在一般情况下，即使使用自定义的生成器，也建议明确类型，而不是使用泛型编程，除非你对泛型编程足够了解。

比如上面自定义的`MySelfGen`应该继承`edge_weight::TreeGen<int>`，而尽量不要在没把握的情况下使用泛型：

```cpp
template <typename EdgeType>
class MySelfGen : public edge_weight::Tree<EdgeType>;
```