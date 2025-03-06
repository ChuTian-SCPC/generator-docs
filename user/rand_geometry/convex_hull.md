### 构造函数

凸包的构造函数为:

```cpp
ConvexHull(int node_count = 1, T x_left_limit = 0, T x_right_limit = 0, T y_left_limit = 0, T y_right_limit = 0)
```

### 额外参数

凸包有一个额外参数`max_try`，默认为$10$，表示最多尝试的次数。

由于凸包生成不一定能够成功，所以至多尝试`max_try`次，如果失败则会抛出异常。

它们可以通过函数[获取或设置](/user/tools/setter_getter.md)。

### 示例

生成一个包含$10$个点的凸包，$x$和$y$的范围分别为$[-10， 10]$。

```cpp
#include "generator.h"
#include <iomanip>
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    ConvexHull<int> p(10);
    p.set_xy_limit("[-10,10]");
    p.gen();
    cout << p << endl;
    return 0;
}
```