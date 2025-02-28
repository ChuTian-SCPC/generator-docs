对拍(Hack)可以针对一些错解生成能卡掉它的样例。

对拍需要准备标程std，数据生成器generator，判题器checker和需要hack的程序。

运行hack程序得到的结果会在工作目录下新建一个`hack_folder`文件夹放入，默认值为`hack`。

如果需要修改请参考[设置](/user/setting/setting.md)。

### 函数

```cpp
void hack(
    T1 generator_program, T2 std_program, T3 compare_program, T4 checker_program, 
    int time_limit, bool limit_std_runtime = false, int max_try = 100, 
    bool stop_when_wrong = true, bool copy_wrong_to_testcase = true, 
    bool delete_correct = true);
```

其中参数的含义为：

- `generator_program`：数据生成器，需要为[可执行路径或函数](/user/io/command_path_func.md)。

- `std_program`：标程，需要为[可执行路径或函数](/user/io/command_path_func.md)。

- `compare_program`：需要hack的程序，需要为[可执行路径或函数](/user/io/command_path_func.md)。

- `checker_program`：判题器，需要为[checker](/user/io/checker.md)。

- `time_limit`：对于hack的程序的时间限制。

- `limit_std_runtime`：上面的时间限制是否同时对标程限制，默认为`false`。

- `max_try`：最多对拍的组数，默认为$100$。

- `stop_when_wrong`：当对拍出WA或者TLE时是否立刻停止，默认为`true`。

- `copy_wrong_to_testcase`：是否将让该解出错的样例放入测试样例中，默认为`true`。

- `delete_correct`：是否将该解对的测试样例删除，默认为`true`。

**注意**：

如果`compare_program`或`std_program`需要限制时间则不能在Windows系统下使用`CommandFunc`。

同样也不建议checker在Windows系统下使用`CommandFunc`。

详见[Windows中CommandFunc的问题](/developer/problem/windows.md)。

### 时间限制

hack的时间限制与compare不同，它不会有额外的运行时间，一旦超时就会视为错误。

### generator默认参数

数据生成器的默认参数为`default_hack_stable_seed`和编号组合，默认值为`hack`。

即生成的第一组hack样例等同于命令行`gen.exe hack 1 > 1.in`，第二组样例等同于`gen.exe hack 2 > 2.in`，以此类推。

如果想要自行设置随机种子，可以查看[给generator设置随机种子](/user/io/inputs.md#随机种子)。

### 使用示例

同样对于A+B问题，假设你有一个想要卡掉的解法`wa.exe`，你可以使用如下代码进行对拍：

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    hack("gen.exe", "std.exe", "wa.exe", lcmp, 1000);
    return 0;  
}
```