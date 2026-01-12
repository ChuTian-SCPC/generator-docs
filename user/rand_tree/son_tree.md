### 构造函数

无权重指定儿子数的树的构造函数为:

```cpp
SonTree(int node = 1, int begin_node = 1, int root = 1)
```

有点权和边权的构造函数参考[树的构造函数](/user/rand_tree/basic_tree_graph.md#构造函数)。

### 禁用函数

由于儿子结点是有根树的概念，所以`SonTree`必须是有根树。

以下函数禁用:

```cpp
void set_is_rooted(bool is_rooted);
```

### 额外变量

指定儿子数的树通过`sons`变量来指定每个结点的儿子数。

`sons`的类型是`std::vector<int>`，初始值均为$-1$，表示这个点的儿子数随机。

关于变量的获取与设置方法，请参考[获取与设置](/user/tools/setter_getter.md)。

还可以通过以下函数设置每个点的度数：

- `set_sons(int index, int son)`：设置第`index`个点的度数为`son`。`index`的范围是$[1,node\_count]$。

当`sons`有一部分值被设置，一部分值为$-1$时，会随机给$-1$的部分赋值，保证设置的条件满足。

### 示例

1. 生成一个有$6$个结点的无权重有根**指定儿子数的树**，每个结点的儿子数分别为$\{2,0,3,0,0,0\}$。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    unweight::SonTree t(6);
    t.set_sons({2, 0, 3, 0, 0, 0});
    t.gen();
    cout << t << endl;
    return 0;
}
```

2. 生成一个有$10$个结点的无权重有根**指定儿子数的树**，指定根为第$2$个结点，指定第$1$个结点的儿子数为$8$。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    unweight::SonTree t(6);
    t.set_root(2);
    t.set_sons(1, 8);
    t.gen();
    cout << t << endl;
    return 0;
}
```

3. 生成一个$3$层的满二叉树、

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    int k = 3;
    int n = (1 << k) - 1;
    unweight::SonTree t(n);
    vector<int> p = rnd.perm(n, 1);
    t.set_root(p[0]);
    for (int i = 0; i < (1 << (k - 1)) - 1; i++) {
        t.set_sons(p[i], 2);
    }
    t.gen();
    cout << t << endl;
    return 0;
}
```