### 函数

- `rand_abs()`：返回一个范围是$(-1,1)$类型为double的随机浮点数。

- `rand_abs<T>(T n)`：

    - 如果`T`是整型，返回一个范围是$(-n,n)$类型为`T`的随机整数；

    - 如果`T`是浮点型，返回一个范围是$(-n,n)$类型为`T`的随机浮点数。

- `rand_abs<T>(T from, T to)`：

    - 如果`T`是整型，返回一个范围是$[-to,-from]\cup[from,to]$类型为`T`的随机整数；

    - 如果`T`是浮点型，返回一个范围是$(-to,-from]\cup[from,to)$类型为`T`的随机浮点数。

- `rand_abs<R, T, U>(T from, U to)`：

    - 如果`R`是整型，返回一个范围是$[-to,-from]\cup[from,to]$类型为`R`的随机整数；
    
    - 如果`R`是浮点型，返回一个范围是$(-to,-from]\cup[from,to)$类型为`R`的随机浮点数。
    
    - 其中`T`和`U`均要能转换为`R`，`R`默认为double。

- `rand_abs<T>(std::string format)`：

    - 根据字符串format解析得到的区间范围，
    
    - 如果`T`是整型，返回一个绝对值符合该范围类型为`T`的随机整数，详解[整型格式解析](/user/rand_numeric/format.md#整数范围)。

    - 如果`T`是浮点型，返回一个绝对值符合该范围类型为`T`的随机浮点数，详解[浮点型格式解析](/user/rand_numeric/format.md#浮点数范围)。

    - `T`默认为double。

### 示例

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    int a1 = rand_abs(1);
    int a2 = rand_abs(1, 2);
    long long a3 = rand_abs<long long>(1, 1e18);
    int a4 = rand_abs<int>("[1, 3)");
    cout << a1 << " " << a2 << " " << a3 << " " << a4 << endl;

    double b1 = rand_abs();
    double b2 = rand_abs(1.0);
    float b3 = rand_abs<float>(1.0, 2.0);
    double b4 = rand_abs<double>("[1.2e-2, 1)");
    printf("%lf %lf %lf %.3lf\n", b1, b2, b3, b4);
    return 0;  
}
```