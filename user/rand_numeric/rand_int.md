### 函数

- `rand_int<T>(T n)`：返回一个范围是$[0，n)$类型为`T`的随机整数，`T`默认为int。

- `rand_int<T>(T from, T to)`：返回一个范围是$[from，to]$类型为`T`的随机整数，`T`默认为int。

- `rand_int<R, T, U>(T from, U to)`：返回一个范围是$[from，to]$类型为`R`的随机整数，其中`T`和`U`均要能转换为`R`，`R`,`T`,`U`默认均为long long。

- `rand_int<T>(std::string format)`：根据字符串format解析得到的区间范围，返回一个符合该范围类型为`T`的随机整数，`T`默认为long long。详解[整型格式解析](/user/rand_numeric/format.md#整数范围)。

### 示例

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    int a1 = rand_int(5);
    int a2 = rand_int(3, 6);
    short x = -1;
    long long y = 1LL;
    int a3 = rand_int<int>(x, y);
    int a4 = rand_int("[1, 4)");
    cout << a1 << " " << a2 << " " << a3 << " " << a4 << endl;
    return 0;  
}
```

### 扩展支持

在testlib中，`unsigned int`, `unsigned long`, `unsigned long long`这些类型是**不支持**的。

这也会导致即使`T`是`long long`，但是$from$和$to$的范围超过了`long long`，也会导致生成失败。

比如以下代码是会在生成时候fail的：

```cpp
#include "testlib.h"

using namespace std;

int main(int argc, char* argv[]) {
    registerGen(argc, argv, 1);

    long long ll_min = numeric_limits<long long>::min();
    long long ll_max = numeric_limits<long long>::max();
    unsigned int ui_max = numeric_limits<unsigned int>::max();
    unsigned long ul_min = numeric_limits<unsigned long>::min();
    unsigned long ul_max = numeric_limits<unsigned long>::max();
    unsigned long long ull_min = numeric_limits<unsigned long long>::min();
    unsigned long long ull_max = numeric_limits<unsigned long long>::max();
    unsigned long long ull_mid = (unsigned long long)ll_max + 1ULL;

    long long a = rnd.next(ll_min, ll_max);
    unsigned int b = rnd.next(ui_max);
    unsigned long c = rnd.next(ul_min, ul_max);
    unsigned long long d = rnd.next(ull_min, ull_max);
    unsigned long long e = rnd.next(ull_mid);

    cout << a << " " << b << " " << c << " " << d << " " << e << endl;
    
    return 0;
}

```

但是通过generator可以生成这些类型的数据：

```cpp
#include"generator.h"

using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    
    long long ll_min = numeric_limits<long long>::min();
    long long ll_max = numeric_limits<long long>::max();
    unsigned int ui_max = numeric_limits<unsigned int>::max();
    unsigned long ul_min = numeric_limits<unsigned long>::min();
    unsigned long ul_max = numeric_limits<unsigned long>::max();
    unsigned long long ull_min = numeric_limits<unsigned long long>::min();
    unsigned long long ull_max = numeric_limits<unsigned long long>::max();
    unsigned long long ull_mid = (unsigned long long)ll_max + 1ULL;
    
    long long a = rand_int(ll_min, ll_max);
    unsigned int b = rand_int(ui_max);
    unsigned long c = rand_int(ul_min, ul_max);
    unsigned long long d = rand_int(ull_min, ull_max);
    unsigned long long e = rand_int(ull_mid);
    cout << a << " " << b << " " << c << " " << d << " " << e << endl;
    return 0;
}

```