<div align="center">
    <h1>Generator</h1>
</div>

你是否希望在使用[Testlib](https://github.com/MikeMirzayanov/testlib)出题时：

- 对于generator不需要写批处理脚本。

- 测试数据强度，以及针对错解随机hack数据。

- 能够方便地生成树，包括具有特殊性质的树（链、菊花图、指定高度的树、限制最大度数的树、限制最大儿子数的树、菊花带链）。

- 能够方便地生成图，包括具有特殊性质的图（二分图、有向无环图、环图、轮图、网格图、基环树、仙人掌、森林）。

- 能够方便地生成凸包、简单多边形。

Generator是基于testlib.h库封装的一个出题辅助工具库。

它实现了以上的功能，并且提供了较高的扩展性。

### 快速开始

#### 在使用前请确保

   C++编译器支持C++11及以上版本。

#### 引入头文件

将`testlib.h`,`generator.h`和文件夹`checker`放入同一个目录下。

放在**标准库位置**或**工作目录**均可。

在代码中使用命令空间：`using namespace generator::all`。

#### 生成输入输出文件

以A+B问题为例，生成的样例会放在`testcases`文件夹下，输入输出文件分别以`.in`和`.out`结尾。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

void gen_code() {
  cout << rand_int(1, 100) << " " << rand_int(1, 100) << endl;
}

void std_code() {
  int a, b;
  cin >> a >> b;
  cout << a + b << endl;
}

int main() {
  fill_inputs(5, gen_code); // 生成五组输入文件
  fill_outputs(std_code); // 对于所有输入文件生成相关输出文件
  return 0;
}

```

或者出题需要生成一棵树，你可以用：

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

void gen_code() {
  int n = rand_int("[1, 1e6]");
  unweight::Tree tree(n); 
  tree.gen(); // 生成一棵n个节点的树，树没有点权和边权，节点边号为1~n
  cout << tree << endl;
}

int main() {
  fill_inputs(5, gen_code);
  return 0;
}
```

#### 测试其他代码

出题时，可能会遇到：

- 有一些其他的解法是否正确。
  
- 测试随机数据的强度是否能卡掉一些错解。
  
比如现在有两个**可执行文件**`other_std.exe`和`wa_code.exe`，分别是其他解法和错解的代码。

```cpp  
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
  compare(1000, lcmp, "other_std.exe", "wa_code.exe");
  return 0;
}
```

#### 对拍

对于一些错解，可以通过对拍将能卡掉这个错解的样例加入测试中。

同样对于A+B问题，比如有一个错解的可执行文件是`wa_code.exe`。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

void gen_code() {
  cout << rand_int(1, 100) << " " << rand_int(1, 100) << endl;
}

void std_code() {
  int a, b;
  cin >> a >> b;
  cout << a + b << endl;
}

int main() {
  // 用gen_code生成测试样例，std_code生成正确答案，使用lcmp作为checker。
  // 对于wa_code时间限制是1000ms，在结果不正确时，将该样例添加到测试样例。
  hack(gen_code, std_code, "wa_code.exe", lcmp, 1000);
  return 0;
}
```