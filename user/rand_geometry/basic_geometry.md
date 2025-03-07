这里的几何只涉及二维几何。

### 类型限制

它们的类型`T`应该为**有符号整型**或者**浮点型**。

由于点积，叉积等运算的限制，它们的类型`T`不能为`unsigned`类型。

可能涉及到`long long`的乘法越界，所以在有`__int128`的情况下会采用`__int128`作为计算结果的类型，而没有的情况下会采用`long long`作为计算结果的类型。

具体的是在点积和叉积运算中，如果`T`是整型，且有`__int128`，则会采用`__int128`作为计算结果的类型，否则会采用`long long`作为计算结果的类型；如果`T`是浮点型，会采用`double`作为计算结果类型。

由于这样的情况可能会造成结果出现错误，所以如果没有`__int128`最好不要使用`long long`作为类型。

### 使用方法

每个几何图形都有默认的输出格式，一般情况下满足大部分需求。如果需要自定义输出格式，详见[自定义输出格式](/user/tools/set_output.md)。

#### 基本元素

对于基本元素：点(Point)，线段(Segment)，直线(line)使用`rand()`一个范围随机，或者使用`rand_类型()`获得一个随机的该类型。

#### 函数

比如对于点`Point`，类本身有以下函数可以随机：

- `rand(T left, T right)`：随机一个点，$x$和$y$的范围分别为$[left, right]$。

- `rand(T x_left, T x_right, T y_left, T y_right)`：随机一个点，$x$的范围为$[x\_left, x\_right]$，$y$的范围为$[y\_left, y\_right]$。

- `rand(std::string format)`：随机一个点，根据[几何范围解析](/user/rand_geometry/format.md)限制$x$和$y$。

也可以通过`rand_point`获得一个随机的点：

- `rand_point(T left, T right)`：返回一个点，$x$和$y$的范围分别为$[left, right]$。

- `rand_point(T x_left, T x_right, T y_left, T y_right)`：返回一个点，$x$的范围为$[x\_left, x\_right]$，$y$的范围为$[y\_left, y\_right]$。

- `rand_point(std::string format)`：返回一个点，根据[几何范围解析](/user/rand_geometry/format.md)限制$x$和$y$。

**注意**：基本元素内部**并不**包含对于$x$和$y$范围限制的变量，**不可以**像下面的几何图形通过`set_x_limit`和`set_y_limit`等函数设置。

##### 示例

```cpp
#include "generator.h"
#include <iomanip>
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    Point<int> p1;
    p1.rand(10, 20, 30, 40);
    Point<int> p2 = rand_point<int>("[10, 20] [30, 40]");
    cout << p1 << endl;
    cout << p2 << endl;
    return 0;
}
```

#### 几何图形

对于几何图形：凸包(ConvexHull)，三角形(Triangle)，简单多边形(SimplePolygon)在设置好范围之后，使用`gen()`随机。

对于几何图形，都有默认的生成方式，如果需要自定义生成方式，详见[自定义生成器](/user/tools/set_generator.md)。

**注意—**：生成的几何图形都是非严格的，即存在三点共线的情况。

对于单纯的使用来说，并不需要详细了解生成使用的算法。

如果你想要详细了解几何图形的生成算法，详见[开发者手册：几何的随机算法](/developer/algorithm/geometry.md)。

#### 几何图形共同的成员变量

- `node_count`：点的数量。

- `points`：点的集合。

- `x_left_limit`：点的$x$坐标的左边界。

- `x_right_limit`：点的$x$坐标的右边界。

- `y_left_limit`：点的$y$坐标的左边界。

- `y_right_limit`：点的$y$坐标的右边界。

- `output_node_count`：是否输出点，默认为`true`。

以上变量基本可以通过[获取与设置](/user/tools/setter_getter.md)中的方法使用，除此之外还可以通过以下函数设置$x$和$y$坐标的边界：

- `set_x_limit(int x_left_limit, int x_right_limit)`：设置$x$坐标的边界。

- `set_x_limit(std::string format)`：根据[范围解析](/user/rand_numeric/format.md)设置$x$坐标的边界。

- `set_y_limit(int y_left_limit, int y_right_limit)`：设置$y$坐标的边界。

- `set_y_limit(std::string format)`：根据[范围解析](/user/rand_numeric/format.md)设置$y$坐标的边界。

- `set_xy_limit(int x_left_limit, int x_right_limit, int y_left_limit, int y_right_limit)`：设置$x$和$y$坐标的边界。

- `set_xy_limit(std::string format)`：根据[几何范围解析](/user/rand_geometry/format.md)设置$x$和$y$坐标的边界。

#### 输出格式

所有几何图形通用的输出格式为：

第一行一个正整数$n$表示点的数量，如果`output_node_count`为`false`，则不输出。

接下来$n$行，每行两个整数$x,y$，表示一个点的坐标。

##### 特例：Triangle

对于三角形，输出格式为：

第一行输出六个数$x_1,y_1,x_2,y_2,x_3,y_3$，表示三角形的三个点，之间以一个空格隔开。