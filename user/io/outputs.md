会在`testcase_folder`文件夹下读取输入文件并生成输出文件，它的默认值是`testcases`。

标准输出文件以`output_suffix`结尾，它的默认值是`.out`。

如果需要修改请参考[设置](../setting/setting.md)。

### 函数

- `make_outputs(int start, int end, T program, int time_limit = _setting::time_limit_inf)`：生成编号从$start$到$end$的标准输出文件。

- `make_outputs(int index, T program, int time_limit = _setting::time_limit_inf)`：生成编号为$index$的标准输出文件。

= `fill_outputs(T program, bool cover_exist = true, int time_limit = _setting::time_limit_inf)`：对于所有标准输入文件生成标准输出文件，`cover_exit`表示对于已经存在的标准输出文件是否要覆盖。

以上的`program`都必须是可执行文件路径或者函数，在一般情况下是可转换为`Path`的类型或者可转换为`std::function<void()>`的类型，具体可以参考[可执行路径与函数管理](command_path_func.md)。

以上的`time_limit`表示限制标程运行的时间，默认为不限制。

如果需要限制时间则不能在Windows系统下使用`CommandFunc`，详见[Windows中CommandFunc的问题](../../developer/problem/windows.md)。

### 使用示例

类似[生成标准输入文件](inputs.md#使用示例),你同样可以用两种方法(`CommandPath`和`CommandFunc`)生成标准输出文件。

上述说明了`CommandFunc`在Windows系统下存在的问题。

以使用`CommandPath`生成A+B问题的标准输出为例：

写一个`std.cpp`并编译成`std.exe`：

```cpp
#include <bits/stdc++.h>

using namespace std;

int main() {
    int a, b;
    cin >> a >> b;
    cout << a + b <<endl;
    return 0;
}
```

同样再写一个调用它的代码：

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    fill_outputs("std.exe");
    return 0;  
}
```

当然你可以结合生成标准输出文件一起使用：

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    make_inputs(1, 5, "gen.exe");
    fill_outputs("std.exe");
    return 0;  
}
```


