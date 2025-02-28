CF在出题时要求要有数据校验器，检查生成数据的格式是否正确。如何编写数据校验器请自行查阅[Testlib](https://github.com/MikeMirzayanov/testlib)的文档。

此功能依旧是为了解决需要通过命令行调用数据校验器来检查数据的问题。

### 函数

- `validate(int start, int end, T program, std::string case_name = _setting::testcase_folder)`：校验编号从$start$到$end$的样例。

- `validate(T program, std::string case_name = _setting::testcase_folder)`：校验所有的样例。

以上的`program`都必须是可执行文件路径或者函数，在一般情况下是可转换为`Path`的类型或者可转换为`std::function<void()>`的类型，具体可以参考[可执行路径与函数管理](command_path_func.md)。

`case_name`表示要校验数据所在的子文件夹的名称，默认为测试样例所在的文件夹。

**注意**：在Windows系统中建议不要用`CommandFunc`做为数据校验器，详见[Windows中CommandFunc的问题](../../developer/problem/windows.md)。

### 使用示例

对于A+B问题，我们编写数据校验器`val.cpp`：

```cpp
#include "testlib.h"
using namespace std;

int main(int argc, char* argv[]) {
    registerValidation(argc, argv);
    int a = inf.readInt(1, 100, "a");
    inf.readSpace();
    int b = inf.readInt(1, 100, "b");
    inf.readEoln();
    inf.readEof();
    return 0;  
}
```

然后可以使用以下代码调用校验器校验标准输入：

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    validate("val.exe");
    return 0;  
}
```