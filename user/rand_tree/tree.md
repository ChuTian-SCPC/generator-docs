### 构造函数

详见[Tree的构造函数](/user/rand_tree/basic_tree_graph.md#特例tree)

### 额外函数

树可以使用一个枚举来选择使用的生成算法：

```cpp
enum TreeGenerator {
    RandomFather,
    Pruefer
};
```

其中，`RandomFather`是随机选取前面的点作为父亲，生成的期望树高是 $O(\log n)$；

`Pruefer`是随机`Pruefer`序列生成树，生成的期望树高是 $O(\sqrt{n})$。

默认使用的是`RandomFather`。

可以参考[OI Wiki](https://oi-wiki.org/contest/problemsetting/#%E7%94%9F%E6%88%90%E9%9A%8F%E6%9C%BA%E6%A0%91)中相关的介绍。

可以通过以下函数指定生成树的方式：

- `set_tree_generator(TreeGenerator tree_generator)`：设置生成树的方式为`RandomFather`或者`Pruefer`。

- `use_random_father()`：使用`RandomFather`的方式生成树。

- `use_pruefer()`：使用`Pruefer`的方式生成树。

### 示例

1. 生成一个没有权重的无根树，结点数为$10$，结点编号从$0$开始。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;


int main() {
    init_gen();
    unweight::Tree t(10, 0);
    t.gen();
    cout << t << endl;
    return 0;
}
```

2. 生成一个有边权的无根树，结点数为$10$，结点编号从$1$开始，边权为整数，范围为$[-10, 10]$，采用pruefer序列生成树的方式随机。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;


int main() {
    init_gen();
    edge_weight::Tree<int> t;
    t.set_node_count(10);
    t.set_edges_weight_function([]() {
        return rand_int(-10, 10);
    });
    t.use_pruefer();
    t.gen();
    cout << t << endl;
    return 0;
}
```

3. 生成一个有点权的有根树，结点数为$10$，结点编号从$1$开始，根结点随机选取，点权为浮点数，范围为$[0, 1]$，输出$3$位小数。

```cpp
#include "generator.h"
#include <iomanip>
using namespace std;
using namespace generator::all;

void output_real(ostream& os, const node_weight::NodeWeight<double>& e) {
    os << fixed << setprecision(3) << e.w();
}

void output_tree(ostream& os, const node_weight::Tree<double>& t) {
    os << t.node_count() << " " << t.root() << endl;
    auto w = t.nodes_weight();
    for (int i = 0; i < w.size(); i++) {
        w[i].set_output(output_real);
        os << w[i] << " \n"[i == w.size() - 1];
    }
    
    for (auto& e : t.edges()) {
        if (rand_bool()) e.set_swap_node(true);
        os << e << endl;
    }
}

int main() {
    init_gen();
    int n = 10;
    node_weight::Tree<double> t(n, 1, true);
    t.set_root(rand_int(1, n));
    t.set_nodes_weight_function([]() {
        return rand_real("[0, 1.000]");
    });
    t.set_output(output_tree);
    t.gen();
    cout << t;
    return 0;
}
```

4. 生成一个有点权，有边权的有根树，结点数为$5$，结点编号为从$1$开始的$5$个奇数，根节点编号为$1$且不输出，点权为整数，范围为$[-10, 10]$，边权为小写字符。

```cpp
#include "generator.h"
#include <iomanip>
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    both_weight::Tree<int, char> t(5);
    for (int i = 1; i <= 5; i++) t.set_node_indices(i, 2 * i - 1);
    t.set_nodes_weight_function([](){
        return rand_int(-10, 10);
    });
    t.set_edges_weight_function([](){
        return rand_char();
    });
    t.set_output_root(false);
    t.gen();
    cout << t << endl;
    return 0;
}
```
