比对(Compare)有以下的一些作用：

1. 验证生成数据能否检测已知的错误解法。
   
2. 比较不同解法的正确性。
   
3. 在写题自测时，用于检查自己的代码与标准程序在哪些测试样例上存在差异。

测试需要有已经生成好的[标准输入](inputs.md)和[标注输出](outputs.md)。

比对会生成的数据会在工作目录下新建一个`compare_folder`文件夹放入，它的默认值是`cmp`。

如果需要修改请参考[设置](../setting/setting.md)。

### 结果存储规则

1. **CommandPath**：

   - 输出存储路径：`compare_folder/命令名称/`。示例：`gen.exe`的结果存储在`cmp/gen/`下。
  
   - log储存路径：`compare_folder/命名名称.log`。

2. **CommandFunc**：
   
   - 输出存储路径：`compare_folder/function序号/`。示例：如果有两个`CommandFunc`，第一个函数结果存储在`cmp/function1/`，第二个存储在`cmp/function2/`。
  
   - log储存路径：`compare_folder/function序号.log`。

**注意**：混用`CommandPath`和`CommandFunc`时，请确保命令名称不会与`function+序号`的命名方式冲突。

### 函数

可以通过以下函数调用：

- `compare(int start, int end, int time_limit, T checker, Args... args)`：测试编号从$start$到$end$的样例。

- `compare(int time_limit, T checker, Args... args)`：测试所有的样例。

如果需要限制时间则不能在Windows系统下使用`CommandFunc`，详见[Windows中CommandFunc的问题](../../developer/problem/windows.md)。

`T`可以是默认的checker也可以是自定义的checker，具体可以参考[本地判题和SPJ](checker.md)。

`Args`可以是可执行文件路径或者函数，具体可以参考[可执行路径与函数管理](command_path_func.md)。它可以是任意个可执行文件路径或者函数，表示要测试多个代码。

### 使用示例

假设对于A+B问题，有两个其他的解法：

1. wa.cpp

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int a, b;
    cin >> a >> b;
    if (a + b >= 100) cout << a + b - 1 << endl;
    cout << a + b << endl;
    return 0;
}
```

2. tle.cpp

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int a, b;
    cin >> a >> b;
    int sum = 0;
    for (int i = 1; i <= a; i++) sum++;
    for (int i = 1; i <= b; i++) sum++;
    cout << sum << endl;
    return 0;
}
```

然后可以通过如下代码对两种解法进行测试：

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
  compare(1000, lcmp, "wa.exe", "tle.exe");
  return 0;
}
```

其中时间限制为$1000ms$，采用lcmp作为checker，对`wa.exe`和`tle.exe`进行测试。