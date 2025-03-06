### 构造函数

简单多边形的构造函数为：

```cpp
SimplePolygon(int node_count = 1, T x_left_limit = 0, T x_right_limit = 0, T y_left_limit = 0, T y_right_limit = 0)
```

### 示例

生成一个包含$10$个点的简单多边形，$x$和$y$的范围分别为$[-10， 10]$。

```cpp
#include "generator.h"
#include <iomanip>
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    SimplePolygon<int> p(10);
    p.set_xy_limit("[-10,10]");
    p.gen();
    cout << p << endl;
    return 0;
}
```