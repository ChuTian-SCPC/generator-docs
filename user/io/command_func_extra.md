`CommandFunc`接受的是一个可转换为`std::function<void()>`的类型。

但是如果存在需求一定要传参怎么办？

比如对于A+B问题的测试点$1$限制范围为$1\le n\le 10$, 而测试点$2$限制范围为$1\le n\le 10^9$。

如果写两个类似的generator是一件令人恼火的事情，可以通过以下两种手段解决这个问题：

1. lambda捕获

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

function<void()> gen(int n) {
  return [n]() {
    cout << rand_int(1, n) << " " << rand_int(1, n) << endl;
  };
}

int main() {
  make_inputs(1, gen(10));
  make_inputs(2, gen(1e9));
  return 0;
}
```

2. `std::bind`

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

void gen(int n) {
  cout << rand_int(1, n) << " " << rand_int(1, n) << endl;
}

int main() {
  make_inputs(1, bind(gen, 10));
  make_inputs(2, bind(gen, 1e9));
  return 0;
}
```