## 随机奇数

### 函数

- `rand_odd<T>(T n)`：返回一个范围是$[0，n)$类型为`T`的随机奇数，`T`默认为int。

- `rand_odd<T>(T from, T to)`：返回一个范围是$[from，to]$类型为`T`的随机奇数，`T`默认为int。

- `rand_odd<R, T, U>(T from, U to)`：返回一个范围是$[from，to]$类型为`R`的随机奇数，其中`T`和`U`均要能转换为`R`，`R`,`T`,`U`默认均为long long。

- `rand_odd<T>(std::string format)`：根据字符串format解析得到的区间范围，返回一个符合该范围类型为`T`的随机奇数，`T`默认为long long。详解[整型格式解析](/user/rand_numeric/format.md#整数范围)。

### 示例

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    int a1 = rand_odd(5);
    int a2 = rand_odd(3, 6);
    short x = -1;
    long long y = 1LL;
    int a3 = rand_odd<int>(x, y);
    int a4 = rand_odd("[1, 4)");
    cout << a1 << " " << a2 << " " << a3 << " " << a4 << endl;
    return 0;  
}
```

## 随机偶数

### 函数

- `rand_even<T>(T n)`：返回一个范围是$[0，n)$类型为`T`的随机偶数，`T`默认为int。

- `rand_even<T>(T from, T to)`：返回一个范围是$[from，to]$类型为`T`的随机偶数，`T`默认为int。

- `rand_even<R, T, U>(T from, U to)`：返回一个范围是$[from，to]$类型为`R`的随机偶数，其中`T`和`U`均要能转换为`R`，`R`,`T`,`U`默认均为long long。

- `rand_even<T>(std::string format)`：根据字符串format解析得到的区间范围，返回一个符合该范围类型为`T`的随机偶数，`T`默认为long long。详解[整型格式解析](/user/rand_numeric/format.md#整数范围)。

### 示例

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    int a1 = rand_even(5);
    int a2 = rand_even(3, 6);
    short x = -1;
    long long y = 1LL;
    int a3 = rand_even<int>(x, y);
    int a4 = rand_even("[1, 4)");
    cout << a1 << " " << a2 << " " << a3 << " " << a4 << endl;
    return 0;  
}
```
