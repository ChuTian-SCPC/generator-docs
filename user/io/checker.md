在生成标准输入和输出文件后，通常需要对其他程序的运行结果进行[比对](compare.md)，或针对特定错误解法进行[对拍](hack.md)。这些操作都涉及对程序输出的评判。

### 判题机制

判题系统采用`testlib.h`编写的checker进行评判。在`checker`文件夹中已内置了多种常用checker：

```cpp
enum Checker {
    lcmp,  // 忽略空格的比较（Codeforces常用的方式）
    yesno, // 忽略大小写的yes/no判断
    rcmp4, // 浮点数比较（误差≤10^-4）
    rcmp6, // 浮点数比较（误差≤10^-6）
    rcmp9, // 浮点数比较（误差≤10^-9）
    wcmp   // 严格字符比较
}
```

如需特殊评判需求（如SPJ）或默认checker无法满足需求，可参照testlib.h规范自行编写checker。

自行编写的checker可以是可执行文件路径或者函数，具体可以参考[可执行路径与函数管理](command_path_func.md)。

**Windows系统限制**：请勿在Windows系统下使用CommandFunc形式的checker，详见[Windows中CommandFunc的问题](../../developer/problem/windows.md)。

### 时间限制

判题时，会有时间限制，以毫秒(ms)作为单位，如果不想有限制，可以使用`time_limit_inf`作为参数。

对于存在时间限制的情况：

- 实际判题的时间会是`time_limit`的`time_limit_over_ratio`倍。

- 实际用checker检查该解正误的时间是`time_limit`的`time_limit_check_ratio`倍。

相关参数可在[设置](../setting/setting.md)中调整。

此目的在于，对于一些可能需要卡掉的超时解，如果他实际运行时间是时间限制很小的一个倍数之内的话，可能会因为测评机波动以及一些优化方式卡进去，出题人可以判断在这种情况下是否应该加强数据或者减少时间限制。

**注意**：本地测评结果受硬件性能影响，仅供参考，不能完全代表在线评测系统（OJ）上的表现。

### 测评结果

- AC ：答案正确。

- WA ：答案错误。

- TLE ：超时`time_limit_over_ratio`倍以上。

- TLE(AC) ：超时`time_limit_check_ratio`倍之内，并且答案正确。

- TLE(WA) ：超时`time_limit_check_ratio`倍之内，并且答案错误。

- ERROR ：程序运行错误。可能是因为RE或者其他情况导致崩溃，需要检查是代码本身问题还是其他情况。