### 构造函数

无权重指定度数的树的构造函数为:

```cpp
DegreeTree(int node = 1, int begin_node = 1, bool is_rooted = false, int root = 1)
```

有点权和边权的构造函数参考[树的构造函数](/user/rand_tree/basic_tree_graph.md#构造函数)。

### 额外变量

指定度数的树通过`degrees`对度数进行限制。

`degrees`的类型是`std::vector<int>`，初始值均为$-1$，表示对这个点的度数随机。

关于变量的获取与设置方法，请参考[获取与设置](/user/tools/setter_getter.md)。

还可以通过以下函数设置每个点的度数：

- `set_degrees(int index, int degree)`：设置第`index`个点的度数为`degree`。`index`的范围是$[1,node\_count]$。

当`degrees`有一部分值被设置，一部分值为$-1$时，会随机给$-1$的部分赋值，保证设置的条件满足。

### 示例

1. 生成一个有$6$个结点的无权重无根**指定度数的树**，每个结点的度数分别为$\{3,1,3,1,1,1\}$。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    unweight::DegreeTree t(6);
    t.set_degrees({3, 1, 3, 1, 1, 1});
    t.gen();
    cout << t << endl;
    return 0;
}
```

2. 生成一个有$10$个结点的无权重无根**指定度数的树**，指定第$2$个结点的度数为$2$，第$6$个结点的度数为$4$。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    unweight::DegreeTree t(10);
    t.set_degrees(2, 2);
    t.set_degrees(6, 4);
    t.gen();
    cout << t << endl;
    return 0;
}
```

