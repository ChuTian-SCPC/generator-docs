在所有类（树，图，几何）中，都有默认的输出格式，是大部分题目中常用的输入格式。

并且在一些类中，会有相关的函数对输出格式进行设置。

如果这些还不能满足你的需求，你可以通过`void set_output(OutputFunction func)`对输出格式进行自定义。

`OutputFunction`是一个`std::function<void(std::ostream&, const _TYPE&)>`，其中`_TYPE`是类的类型。

比如对于一棵树，你希望输出的格式是：

第一行一个正整数$n$表示结点数。

接下来$n-1$行，每行两个正整数$u,v(1\le u\lt v\le n)$表示$u$和$v$之间有一条边。

由于在默认的输出格式中，并没有方法设置结点编号一定要小的在前面，所以你需要自定义输出格式：

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

void myself_print(ostream& os, const unweight::Tree& t) {
    os << t.node_count() << endl;
    for (auto e : t.edges()) {
        if (e.u() > e.v()) cout << e.v() << " " << e.u() << endl;
        else cout << e.u() << " " << e.v() << endl;
    }
}

int main() {
    init_gen();
    unweight::Tree t(10);
    t.gen();
    t.set_output(myself_print);
    cout << t;
    return 0;
}
```

