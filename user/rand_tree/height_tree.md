### 构造函数

无权重指定高度的树的构造函数为:

```cpp
HeightTree(int node = 1, int begin_node = 1, int root = 1, int height = -1)
```

有点权和边权的构造函数参考[树的构造函数](/user/rand_tree/basic_tree_graph.md#构造函数)。

### 禁用函数

由于树的高度是有根树的概念，所以`HeightTree`必须是有根树。

以下函数禁用:

```cpp
void set_is_rooted(bool is_rooted);
```

### 额外变量

指定高度的树通过`height`表示树的高度。

`height`默认为$-1$，表示随机高度。

对于`height`的限制为：

- $node\_count = 1$时，$height = 1$。

- $node\_count \ge 2$时，$height$的范围为$[2,node\_count]$。

关于变量的获取与设置方法，请参考[获取与设置](/user/tools/setter_getter.md)。

### 示例

生成一个没有权重的有根树，根为默认值$1$，结点数为$10$，结点编号从$1$开始，限制它的高度为$3$。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;


int main() {
    init_gen();
    unweight::HeightTree t(10);
    t.set_height(3);
    t.gen();
    cout << t << endl;
    return 0;
}
```