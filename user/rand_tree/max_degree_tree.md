### 构造函数

无权重限制最大度数的树的构造函数为:

```cpp
MaxDegreeTree(int node = 1, int begin_node = 1, bool is_rooted = false, int root = 1, int max_degree = -1)
```

有点权和边权的构造函数参考[树的构造函数](/user/rand_tree/basic_tree_graph.md#构造函数)

### 额外变量

限制最大度数的树通过`max_degree`对度数进行限制。

对于**有根树**，度数是指入度和出度之和。

`max_degree`默认为$-1$，即随机度数。

对于`max_degree`的限制为：

- $node\_count = 1$时，$max\_degree = 0$。

- $node\_count = 2$时，$max\_degree = 1$。

- $node\_count \ge 3$时，$max\_degree$的范围是$[2, node\_count - 1]$。

- 对于$max\_degree \gt node_count - 1$，限制相当于不存在，但依旧可以使用`gen()`生成。

关于变量的获取与设置方法，请参考[获取与设置](/user/tools/setter_getter.md)。

### 示例

生成一个没有权重的无根树，结点数为$10$，结点编号从$1$开始，限制它结点最大度数为$3$。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;


int main() {
    init_gen();
    unweight::MaxDegreeTree t(10);
    t.set_max_degree(3);
    t.gen();
    cout << t << endl;
    return 0;
}
```