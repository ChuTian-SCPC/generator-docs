#### 描述

在树和图中，每个结点都有一个编号，比如题目中经常会描述：“有一棵树，结点编号为$1$到$n$”。

所以就需要一个变量来描述结点编号，最初的情况下，使用了`下标+偏移量`的方式来描述结点编号。

但是在之后，我采用了`node_indices`作为结点编号的描述方式。

`node_indices`是一个整数数组，表示第$i$个点的编号为`node_indices[i]`。

#### 获取与设置

除了[常规的获取与设置方法](/user/tools/setter_getter.md)，还可以用以下函数：

- `set_node_indices(int index, int number)`：将第`index`个点的编号设置为`number`。这里`index`范围为$1$到$node\_count$。

在默认情况下，会采用`default_node_indices()`来设置结点编号。

`default_node_indices()`的默认行为是`下标+偏移量`的方式，第$i$个点的编号为$i + begin\_node$。

在`node_count`或者`begin_node`改变的时候，也会重新设置结点编号。

如果`node_indices`的长度与`node_count`不一致，也会重新设置结点编号。

所以你如果要自行设置结点编号，需要注意在设置完`node_count`和`begin_node`之后再设置结点编号，并且注意它的长度要与`node_count`一致。

#### 示例

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    unweight::Tree t;
    t.set_node_count(5);
    t.set_node_indices({-1, -2, -3, -4, -5}); // 为了显示不同，采用负数
    t.gen();
    cout << t;
    return 0;
}
```

#### 设计的原因

在最初的方案中，并没有考虑到要使用专门的变量描述结点编号，这也导致了`Node`类的设计成为了描述的点权的类。

这样的设计带来了一定的歧义，但是同样也在有些地方使得代码更好写。

设计`_node_indices`的原因主要有两点：

- 二分图的常见输出格式中，有一种是左部和右部分别编号，这也就使得`下标+偏移量`的方式不够直观。

- 对于`Link`，`TreeLink`这样合并几个树，图的类，如果需要用户自行控制结点编号是一件很麻烦的事情。

为了能够简化支持二分图的输出格式，简化树和图在合并时对于结点编号重新编号的心智负担。我考虑将结点额外添加一个编号的属性，这样结点对于编号就不是一个双射了。

在最初设计的时候，我忽略掉了`_Node`的存在，也导致了`node_index`的设计独立了出来。

最终我还是将错就错地采用了`node_indices`的方式来描述结点编号。

为了使前后变化尽可能小，在绝大部分情况下，它依旧是类似于`下标+偏移量`的方式。

所以在没有特殊需求下，并不需要手动设置结点编号。