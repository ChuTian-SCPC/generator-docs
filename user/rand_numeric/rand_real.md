### 函数

- `rand_real()`：返回一个范围是$[0,1)$类型为double的随机浮点数。

- `rand_real<R, T>(T n)`：返回一个范围是$[0,n)$类型为`R`的随机浮点数，`T`需要是能转化为double的类型，`R`需要是浮点型，默认为double。

- `rand_real<R, T, U>(T from,U to)`：返回一个范围是$[from,to)$类型为`R`的随机浮点数，`T`和`U`需要是能转化为double的类型，`R`需要是浮点型，默认为double。

- `rand_real<T>(std::string format)`：根据字符串format解析得到的区间范围，返回一个符合该范围类型为`T`的随机浮点数，`T`默认为double。详解[浮点型格式解析](/user/rand_numeric/format.md#浮点数范围)。

### 示例

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    double a1 = rand_real();
    float a2 = rand_real<float>(0.01);
    double a3 = rand_real(0.01, 0.02f);
    double a4 = rand_real("[1e-2, 1e-1]");
    printf("%lf %lf %lf %.2lf\n", a1, a2, a3, a4);
    return 0;  
}
```