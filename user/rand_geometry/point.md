### 构造函数

可以通过以下函数构造一个点：

```cpp
Point()
Point(T x, T y)
```

在不传参的时候，默认$x$和$y$都等于$0$。

### 成员变量

`Point`的成员变量有`x`和`y`，除了可以通过通用的[获取与设置](/user/tools/setter_getter.md)方法之外还提供了以下函数:

- `T& operator[](int idx)`：`idx`为$0$时返回$x$坐标，`idx`为$1$时返回$y$坐标。

- `T& operator[](char c)`：`c`为`x`或`X`时返回$x$坐标，`c`为`y`或`Y`时返回$y$坐标。

- `T& operator[](std::string s)`：和上述相同，相当于`operator[](s[0])`。

### 随机生成

可以使用类的函数`rand()`进行生成，也可以使用`rand_point()`返回一个点。

详见[Point的随机生成](/user/rand_geometry/basic_geometry.md#函数)。

### 运算支持

`Point`支持以下运算：

- `Point operator+(const Point& b)`：点的加法。

- `Point& operator+=(const Point& b)`：点的加法赋值。

- `Point operator-(const Point& b)`：点的减法。

- `Point& operator-=(const Point& b)`：点的减法赋值。

- `_ResultTypeT<T> operator^(const Point& b)`：叉积。

- `_ResultTypeT<T> operator*(const Point& b)`：点积。

- 比较运算符。

其中`_ResultTypeT<T>`可以参考[点积、叉积的返回类型](/user/rand_geometry/basic_geometry.md#类型限制)。

### 示例

```cpp
#include "generator.h"
#include <iomanip>
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    Point<int> p1(1, 2);
    Point<int> p2 = rand_point<int>("[1, 10]");
    cout << p1 << endl;
    cout << p2 << endl;
    Point<int> p3 = p1 + p2;
    cout << p3 << endl;
    return 0;
}
```
