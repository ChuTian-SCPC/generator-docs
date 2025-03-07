### 构造函数

三角形的构造函数为:

```cpp
Triangle(T x_left_limit = 0, T x_right_limit = 0, T y_left_limit = 0, T y_right_limit = 0)
```

三角形是一个特殊的[凸包](/user/rand_geometry/convex_hull.md)，它是固定点数为$3$的凸包。

### 禁用函数

三角形点数固定，以下函数禁用：

```cpp
void set_node_count(int node_count)
```

### 默认输出

三角形默认输出与凸包不同，它的`output_node_count`默认为`false`，即不输出点数。

详见[三角形默认输出方式](/user/rand_geometry/basic_geometry.md#特例triangle)。

### 示例

生成一个三角形，$x$和$y$的范围分别为$[-10, 10]$。

```cpp
#include "generator.h"
#include <iomanip>
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    Triangle<int> p;
    p.set_xy_limit("[-10,10]");
    p.gen();
    cout << p << endl;
    return 0;
}
```