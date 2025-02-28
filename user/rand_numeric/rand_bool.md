### 函数

- `rand_bool()`：返回一个随机的bool值。

### 示例

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    bool a = rand_bool();
    cout << a << endl;
    return 0;  
}
```