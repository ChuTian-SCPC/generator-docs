### 构造函数

可以通过以下函数构造直线或者线段：

```cpp
Line()
Line(const Point<T>& start, const Point<T>& end)

Segment()
Segment(const Point<T>& start, const Point<T>& end)
```

### 成员变量

`Line`和`Segment`的成员变量有`start`和`end`表示起止点，可以通过通用的[获取与设置](/user/tools/setter_getter.md)方法进行设置和获取。

### 随机生成

可以使用类的函数`rand()`进行生成，也可以使用`rand_line()`和`rand_segment()`返回一个直线或者线段。

详见[Line和Segment的随机生成](/user/rand_geometry/basic_geometry.md#函数)。

### 运算支持

`Line`和`Segment`支持以下运算：

- `Point<T> to_vector()`：返回直线或者线段的向量，即`end` - `start`。

- `_ResultTypeT<T> operator^(const Point<T>& b)`：叉积，将`Line`或`Segment`看成一个向量。

- `_ResultTypeT<T> operator^(const _2Points<T>& l)`：叉积，将`Line`和`Segment`看成一个向量，其中`_2Points<T>`是指另一个`Line`或者`Segment`。

- `_ResultTypeT<T> operator*(const Point<T>& b)`：点积，将`Line`或`Segment`看成一个向量。

- `_ResultTypeT<T> operator*(const _2Points<T>& l)`：点积，将`Line`和`Segment`看成一个向量，其中`_2Points<T>`是指另一个`Line`或者`Segment`。

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
    Line<int> l1(p1, p2);
    Segment<int> l2 = rand_segment<int>("[1, 10]");
    cout << l1 << endl;
    cout << l2 << endl;
    cout << l1 * l2 << endl;
    return 0;
}
```
