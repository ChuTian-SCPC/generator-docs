### 构造函数

无权重的链的构造函数为:

```cpp
Chain(int node = 1, int begin_node = 1, bool is_rooted = false, int root = 1)
```

有点权和边权的构造函数参考[树的构造函数](/user/rand_tree/basic_tree_graph.md#构造函数)

### 示例

生成一个没有权重的无根树（链），结点数为$10$，结点编号从$1$开始。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;


int main() {
    init_gen();
    unweight::Chain t(10);
    t.gen();
    cout << t << endl;
    return 0;
}
```

