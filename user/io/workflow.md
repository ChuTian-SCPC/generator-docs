工作流(Workflow)是将出题中的流程整合起来：

- 校验判题代码(Test Checker)

- 校验数据校验代码(Test Validator)

- [生成标准输入文件(Generate Inputs)](/user/io/inputs.md)

- [数据校验(Validate)](/user/io/validate.md)

- [生成标准输出文件(Generate Outputs)](/user/io/outputs.md)

- [对拍(Hack)](/user/io/hack.md)

- [比对(Compare)](/user/io/compare.md)

### 构造函数

- `Workflow(int time_limit = _setting::time_limit_inf)`: 构造一个工作流，时间限制为`time_limit`，默认为无限(`_setting::time_limit_inf`)。

### 部分成员变量

- `std::string std`: 标准输出文件的名称。

- `std::string checker`: 本地判题器的名称，默认采用`lcmp`判题。

- `std::string validator`: 数据校验器的名称。

- `int time_limit`: 对于hack和compare中比对程序的时间限制，也可认为是对于题目的时间限制，默认为无限(`_setting::time_limit_inf`)

- `int time_limit_for_std`: 对于std的时间限制，默认为无限(`_setting::time_limit_inf`)。

- `int time_limit_for_generator`: 对generator的时间限制，默认为无限(`_setting::time_limit_inf`)。

- `int time_limit_for_checker`: 对checker的时间限制，默认为无限(`_setting::time_limit_inf`)。

- `int time_limit_for_validator`: 对validator的时间限制，默认为无限(`_setting::time_limit_inf`)。

- `bool delete_fail_testcase`: 是否删除生成失败的测试点，包括生成标准输入文件、校验数据和生成标准输出文件时出现错误，默认为`true`。

- `bool skip_generated`: 是否跳过已经生成过的标准输入文件，默认为`false`。

- `bool cover_exist`: 参考[fill_outputs的cover_exist](/user/io/outputs.md)，默认为`true`。

- `bool copy_wrong_to_testcase`: 参考[hack的copy_wrong_to_testcase](/user/io/hack.md)，默认为`true`。

- `bool delete_correct`: 参考[hack的delete_correct](/user/io/hack.md)，默认为`true`。

- `bool detail_report_on_console`: 是否在控制台输出详细报告，默认为`false`。

- `bool detail_report_on_file`: 是否在文件中输出详细报告，默认为`true`。

这些成员变量可以通过[获取与设置](/user/tools/setter_getter.md)中的方法使用。

### 添加程序

参考[可执行路径与函数](/user/io/command_path_func.md)。

Workflow支持以`CommandPath`，`CommandFunc`和名称的方式添加程序，以及对于checker支持以[默认的方式添加](/user/io/checker.md)。

- `add_program<T>(T&& program)`: 添加一个程序，程序的类型为`T`，是能够构造为`CommandPath`或者`CommandFunc`的类型。

- `add_program(N&& name, T&& program)`: 添加一个程序，程序的类型为`T`，是能够构造为`CommandPath`或者`CommandFunc`的类型。名称为`name`, 类型是能够构造为`std::string`的类型。

- `set_std(T&& program)`: 设置`std`的名称，程序的类型为`T`，将先通过名称查找是否已经存在该程序，若不存在则添加该程序。

- `set_std(N&& name, T&& program)`: 设置`std`的名称，程序的类型为`T`，是能够构造为`CommandPath`或者`CommandFunc`的类型。名称为`name`, 类型是能够构造为`std::string`的类型。将先通过名称查找是否已经存在该程序，若不存在则添加该程序。

- `set_checker(T&& program)`: 设置`checker`的名称，程序的类型为`T`，将先通过名称查找是否已经存在该程序，若不存在则添加该程序。

- `set_checker(N&& name, T&& program)`: 设置`checker`的名称，程序的类型为`T`，是能够构造为`CommandPath`,`CommandFunc`或者`enum Checker`的类型。名称为`name`, 类型是能够构造为`std::string`的类型。将先通过名称查找是否已经存在该程序，若不存在则添加该程序。

- `set_validator(T&& program)`: 设置数据校验器的名称，程序的类型为`T`，将先通过名称查找是否已经存在该程序，若不存在则添加该程序。

- `set_validator(N&& name, T&& program)`: 设置数据校验器的名称，程序的类型为`T`，是能够构造为`CommandPath`或者`CommandFunc`的类型。名称为`name`, 类型是能够构造为`std::string`的类型。将先通过名称查找是否已经存在该程序，若不存在则添加该程序。

所有添加过的程序后续都可以通过名称来使用，如果不指定名称，则采用[程序的默认名称](/user/io/command_path_func.md#名称)。

- `test_validator(T&& path, ExpectedResult result = Any)`: 校验validator校验输入文件`path`的结果是否为`result`，`path`需要为能够构造为`Path`的类型。

- `test_checker(T1&& input, T2&& output, T3&& answer, ExpectedResult result = Any)`: 校验checker使用输入文件`input`，输出文件`output`，答案文件`answer`判题的结果是否为`result`，`input`，`output`，`answer`需要为能够构造为`Path`的类型。

### ExpectedResult

- `enum ExpectedResult`：校验validator和checker的期望结果。

    - `Pass`: 对于validator成功；Checker判题结果为AC。

    - `Fail`: 对于validator失败；Checker判题结果为WA。

    - `TLE`: 设置了对validator和checker的时间限制，并且validator和checker运行超过时间限制。

    - `Any`: 任意结果都可以。

在使用checker的时候可能会遇到checker本身出现问题(RE)，这种情况它只会匹配`Any`。如果期望为`Fail`，也是无法通过校验。

### 函数

- `make_inputs(int start, int end, T&& program)`: 使用`program`生成$start$到$end$的测试点，参考[生成标准输入文件](/user/io/inputs.md)。

- `make_inputs(int index, T&& program)`: 使用`program`生成第$index$个测试点，参考[生成标准输入文件](/user/io/inputs.md)。

- `fill_inputs(int count, T&& program)`: 使用`program`生成$count$个测试点，参考[生成标准输入文件](/user/io/inputs.md)。

- `fill_inputs(T&& program)`: 使用`program`生成$1$个测试点，参考[生成标准输入文件](/user/io/inputs.md)。

- `compare(Args&&... args)`: 比对，参考[Compare](/user/io/compare.md)。支持三种格式:

    - `compare(int start, int end, Args&&... args)`: 对`args`中的程序对拍$start$到$end$的测试点。

    - `compare(Args&&... args)`: 对`args`中的程序对拍所有的测试点。

    - `compare(int start, int end, T&& program, int next_start, int next_end, Args&&... args)`: 每三个一组，对`program`对拍$start$到$end$的测试点。

- `hack(G&& generator, T&& program, int max_try = 100, bool stop_when_wrong = true, int start_index = _setting::_auto_int)`: 对拍，参考[Hack](/user/io/hack.md)：

    - `generator`: 采用`generator`生成对拍的标准输入。

    - `program`: 采用`program`对拍。

    - `max_try`: 最大尝试次数，默认为$100$。

    - `stop_when_wrong`: 是否在第一次`program`对拍错误(WA,TLE)时停止，默认为`true`。

    - `start_index`: `generator`生成测试样例的起始索引，默认为自动选择。

**注意**：

    1. `Workflow`的`fill_inputs`不会考虑`testcases`中已经存在的输入文件。它只是根据前面使用过的`make_inputs`和`fill_inputs`来计算需要生成的输入文件的索引。

    2. `hack`是可以针对多个程序进行对拍，每个程序都是独立的，它们将会根据`genertor`的名称在`hack_floder`中划分出子文件夹。

### 流程

对于所有的都设置好之后，使用`run()`函数来运行工作流，最终的log会储存在当前文件夹下`summary.log`文件中。

其中`validate`,`hack`,`compare`都是可选的，若不设置则不会执行。

如果设置了`validator`，那么会在生成输入文件之后，自动使用`validator`来校验输入文件是否正确。建议使用`validator`来确保生成的输入是正确的。

生成输出文件会自动执行，所以一定要设置`std`。

如果要使用`hack`和`compare`，一定要设置`checker`，默认采用`lcmp`。

### 示例：

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

void gen() {
    std::cout << rand_int(100, 1000) << " " << rand_int(100, 1000) << std::endl;
}

void fail_val() {
    std ::cout << rand_int(1, 10) << " " << rand_int(1, 10) << " " << std::endl;
}

int main() {
    Workflow workflow;
    workflow.set_time_limit(1000);
    workflow.set_std("std.exe");
    workflow.make_inputs(1, 1, "gen.exe");
    workflow.make_inputs(7, "fail_gen.exe");
    workflow.add_program("large_gen", gen);
    workflow.set_validator("val.exe");
    workflow.fill_inputs(3, gen);
    workflow.fill_inputs(fail_val);
    workflow.hack("gen.exe", "wa.exe", 10);
    workflow.hack("gen.exe", "tle2.exe", 5, false, 8);
    workflow.hack("large_gen", "tle.exe", 2, false);
    workflow.hack("fail_gen", "error.exe", 1);
    workflow.hack("fail_gen", "wa.exe", 1);
    workflow.hack(fail_val, "std", 5);
    workflow.compare("wa", "wa2.exe");
    workflow.compare(4, 7, "tle", "error.exe");
    workflow.compare(1, 5, "tle2.exe", 6, 10,"tle3.exe");
    workflow.test_validator("./test_vc/pass.in", ExpectedResult::Pass);
    workflow.test_validator("./test_vc/error.in", ExpectedResult::Fail);
    workflow.test_checker("./test_vc/pass.in", "./test_vc/res.out", "./test_vc/ac.ans", ExpectedResult::Pass);
    workflow.test_checker("./test_vc/error.in", "./test_vc/res.out", "./test_vc/wa.ans", ExpectedResult::Fail);
    workflow.run();
    return 0;
}
```

可以得到一份类似的`summary.log`文件检查出题是否存在疏漏：

```
+------------+--------------------------------------------------------+
|Program Name|Path                                                    |
+------------+--------------------------------------------------------+
|error       |E:\code\ACM-generator\debug\error.exe                   |
+------------+--------------------------------------------------------+
|fail_gen    |E:\code\ACM-generator\debug\fail_gen.exe                |
+------------+--------------------------------------------------------+
|function1   |function                                                |
+------------+--------------------------------------------------------+
|function2   |function                                                |
+------------+--------------------------------------------------------+
|function3   |function                                                |
+------------+--------------------------------------------------------+
|gen         |E:\code\ACM-generator\debug\gen.exe                     |
+------------+--------------------------------------------------------+
|large_gen   |function                                                |
+------------+--------------------------------------------------------+
|lcmp        |E:\code\ACM-generator\src\basic\checker\windows\lcmp.exe|
+------------+--------------------------------------------------------+
|std         |E:\code\ACM-generator\debug\std.exe                     |
+------------+--------------------------------------------------------+
|tle         |E:\code\ACM-generator\debug\tle.exe                     |
+------------+--------------------------------------------------------+
|tle2        |E:\code\ACM-generator\debug\tle2.exe                    |
+------------+--------------------------------------------------------+
|tle3        |E:\code\ACM-generator\debug\tle3.exe                    |
+------------+--------------------------------------------------------+
|val         |E:\code\ACM-generator\debug\val.exe                     |
+------------+--------------------------------------------------------+
|wa          |E:\code\ACM-generator\debug\wa.exe                      |
+------------+--------------------------------------------------------+
|wa2         |E:\code\ACM-generator\debug\wa2.exe                     |
+------------+--------------------------------------------------------+
  Standard Program name  : std
  Checker name           : lcmp
  Validator name         : val
  Test Cases Count       : 6
  Hack Programs Count    : 6
  Compare Programs Count : 6
  Time Limit:
    std       : inf
    compare   : 1000ms / 2000ms
    hack user : 1000ms
    generator : inf
    validator : inf
    checker   : inf
  Setting :
    delete fail testcase          : true
    (input) skip generated        : false
    (output) cover exist          : true
    (hack) copy wrong to testcase : true
    (hack) delete correct         : true
    detail report on console      : false
    detail report on file         : true

Test Checker :
+------------+--------+-----+---------+----------------------------------------------------------+
|ShortName   |Expected|State|Pass Test|Log Message                                               |
+------------+--------+-----+---------+----------------------------------------------------------+
|pass_res_ac |AC      |AC   |Pass     |ok single line: '3'                                       |
+------------+--------+-----+---------+----------------------------------------------------------+
|error_res_wa|WA      |WA   |Pass     |wrong answer 1st lines differ - expected: '3', found: '4' |
+------------+--------+-----+---------+----------------------------------------------------------+

Test Validator :
+---------------------------------------------+--------+-------+---------+-----------------------------------+
|TestCase                                     |Expected|State  |Pass Test|Log Message                        |
+---------------------------------------------+--------+-------+---------+-----------------------------------+
|E:\code\ACM-generator\debug\test_vc\error.in |Fail    |Fail   |Pass     |FAIL Expected EOLN (stdin, line 1) |
+---------------------------------------------+--------+-------+---------+-----------------------------------+
|E:\code\ACM-generator\debug\test_vc\pass.in  |Success |Success|Pass     |                                   |
+---------------------------------------------+--------+-------+---------+-----------------------------------+

Generate(Inputs) :
+-------+--------------+----+-------+-------+-----------------------------------------------------+
|Case ID|Generator Name|Seed|State  |RunTime|Fail Message                                         |
+-------+--------------+----+-------+-------+-----------------------------------------------------+
|1      |gen           |1   |Success| 28ms  |                                                     |
+-------+--------------+----+-------+-------+-----------------------------------------------------+
|2      |function1     |2   |Success| 0ms   |                                                     |
+-------+--------------+----+-------+-------+-----------------------------------------------------+
|3      |function1     |3   |Success| 0ms   |                                                     |
+-------+--------------+----+-------+-------+-----------------------------------------------------+
|4      |function1     |4   |Success| 0ms   |                                                     |
+-------+--------------+----+-------+-------+-----------------------------------------------------+
|5      |function2     |5   |Success| 7ms   |                                                     |
+-------+--------------+----+-------+-------+-----------------------------------------------------+
|7      |fail_gen      |7   |RE     |       |FAIL random_t::next(long long n): n must be positive |
+-------+--------------+----+-------+-------+-----------------------------------------------------+
Meets ERROR in :
  E:\code\ACM-generator\debug\testcases\7.in

Validate :
+-------+-------+-------+-----------------------------------+
|Case ID|State  |RunTime|Fail Message                       |
+-------+-------+-------+-----------------------------------+
|1      |Success| 26ms  |                                   |
+-------+-------+-------+-----------------------------------+
|2      |Success| 25ms  |                                   |
+-------+-------+-------+-----------------------------------+
|3      |Success| 21ms  |                                   |
+-------+-------+-------+-----------------------------------+
|4      |Success| 24ms  |                                   |
+-------+-------+-------+-----------------------------------+
|5      |Fail   |       |FAIL Expected EOLN (stdin, line 1) |
+-------+-------+-------+-----------------------------------+
Meets ERROR in :
  E:\code\ACM-generator\debug\testcases\5.in

Generate(Outputs) :
+-------+-------+-------+
|Case ID|State  |RunTime|
+-------+-------+-------+
|1      |Success| 29ms  |
+-------+-------+-------+
|2      |Success| 27ms  |
+-------+-------+-------+
|3      |Success| 25ms  |
+-------+-------+-------+
|4      |Success| 24ms  |
+-------+-------+-------+

Hack :
Generator Name : fail_gen
+------------+------+--------------+--------------+-----------------------------------------------------+
|Hack Case ID|Seed  |error         |wa            |Fail Message                                         |
+------------+------+--------------+--------------+-----------------------------------------------------+
|1           |hack1 |generate ERROR|generate ERROR|FAIL random_t::next(long long n): n must be positive |
+------------+------+--------------+--------------+-----------------------------------------------------+
Generator Name : function3
+------------+------+--------------+-----------------------------------+
|Hack Case ID|Seed  |std           |Fail Message                       |
+------------+------+--------------+-----------------------------------+
|1           |hack1 |validate ERROR|FAIL Expected EOLN (stdin, line 1) |
+------------+------+--------------+-----------------------------------+
|2           |hack2 |validate ERROR|FAIL Expected EOLN (stdin, line 1) |
+------------+------+--------------+-----------------------------------+
|3           |hack3 |validate ERROR|FAIL Expected EOLN (stdin, line 1) |
+------------+------+--------------+-----------------------------------+
|4           |hack4 |validate ERROR|FAIL Expected EOLN (stdin, line 1) |
+------------+------+--------------+-----------------------------------+
|5           |hack5 |validate ERROR|FAIL Expected EOLN (stdin, line 1) |
+------------+------+--------------+-----------------------------------+
Generator Name : gen
+------------+-------+----------+-------+-------------------------------------------+
|Hack Case ID|Seed   |tle2      |wa     |Move Path                                  |
+------------+-------+----------+-------+-------------------------------------------+
|1           |hack1  |N/A       |WA 31ms|E:\code\ACM-generator\debug\testcases\5.in |
+------------+-------+----------+-------+-------------------------------------------+
|8           |hack8  |TLE 1115ms|Skip   |E:\code\ACM-generator\debug\testcases\6.in |
+------------+-------+----------+-------+-------------------------------------------+
|9           |hack9  |TLE 1101ms|Skip   |E:\code\ACM-generator\debug\testcases\7.in |
+------------+-------+----------+-------+-------------------------------------------+
|10          |hack10 |TLE 1106ms|Skip   |E:\code\ACM-generator\debug\testcases\8.in |
+------------+-------+----------+-------+-------------------------------------------+
|11          |hack11 |TLE 1110ms|N/A    |E:\code\ACM-generator\debug\testcases\9.in |
+------------+-------+----------+-------+-------------------------------------------+
|12          |hack12 |TLE 1112ms|N/A    |E:\code\ACM-generator\debug\testcases\10.in|
+------------+-------+----------+-------+-------------------------------------------+
Generator Name : large_gen
+------------+------+----------+-------------------------------------------+
|Hack Case ID|Seed  |tle       |Move Path                                  |
+------------+------+----------+-------------------------------------------+
|1           |hack1 |TLE 1120ms|E:\code\ACM-generator\debug\testcases\11.in|
+------------+------+----------+-------------------------------------------+
|2           |hack2 |TLE 1105ms|E:\code\ACM-generator\debug\testcases\12.in|
+------------+------+----------+-------------------------------------------+

Compare :
+-----------+-----+----------+--------------+--------------+-------+-------+
|Case \ Name|error|tle       |tle2          |tle3          |wa     |wa2    |
+-----------+-----+----------+--------------+--------------+-------+-------+
|1          |N/A  |N/A       |TLE(AC) 1550ms|N/A           |AC 25ms|WA 26ms|
+-----------+-----+----------+--------------+--------------+-------+-------+
|2          |N/A  |N/A       |TLE(AC) 1536ms|N/A           |WA 40ms|AC 22ms|
+-----------+-----+----------+--------------+--------------+-------+-------+
|3          |N/A  |N/A       |TLE(AC) 1537ms|N/A           |WA 23ms|AC 22ms|
+-----------+-----+----------+--------------+--------------+-------+-------+
|4          |RE   |TLE 2112ms|TLE(AC) 1530ms|N/A           |WA 22ms|AC 21ms|
+-----------+-----+----------+--------------+--------------+-------+-------+
|5          |RE   |TLE 2114ms|TLE(AC) 1557ms|N/A           |WA 21ms|AC 23ms|
+-----------+-----+----------+--------------+--------------+-------+-------+
|6          |RE   |TLE 2108ms|N/A           |TLE(WA) 1548ms|WA 22ms|AC 22ms|
+-----------+-----+----------+--------------+--------------+-------+-------+
|7          |RE   |TLE 2099ms|N/A           |TLE(WA) 1550ms|WA 21ms|AC 23ms|
+-----------+-----+----------+--------------+--------------+-------+-------+
|8          |N/A  |N/A       |N/A           |TLE(WA) 1544ms|WA 23ms|AC 20ms|
+-----------+-----+----------+--------------+--------------+-------+-------+
|9          |N/A  |N/A       |N/A           |TLE(AC) 1542ms|AC 22ms|WA 22ms|
+-----------+-----+----------+--------------+--------------+-------+-------+
|10         |N/A  |N/A       |N/A           |TLE(WA) 1552ms|WA 23ms|AC 21ms|
+-----------+-----+----------+--------------+--------------+-------+-------+
|11         |N/A  |N/A       |N/A           |N/A           |WA 21ms|AC 22ms|
+-----------+-----+----------+--------------+--------------+-------+-------+
|12         |N/A  |N/A       |N/A           |N/A           |WA 52ms|AC 22ms|
+-----------+-----+----------+--------------+--------------+-------+-------+
|Total      |RE   |TLE 2114ms|TLE(AC) 1557ms|TLE(WA) 1552ms|WA 52ms|WA 26ms|
+-----------+-----+----------+--------------+--------------+-------+-------+
Error Cases:
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|Program Name & Case ID|State         |Answer                                      |Checker Message                                                 |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|error 4               |RE            |                                            |                                                                |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|error 5               |RE            |                                            |                                                                |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|error 6               |RE            |                                            |                                                                |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|error 7               |RE            |                                            |                                                                |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|tle 4                 |TLE 2112ms    |                                            |                                                                |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|tle 5                 |TLE 2114ms    |                                            |                                                                |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|tle 6                 |TLE 2108ms    |                                            |                                                                |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|tle 7                 |TLE 2099ms    |                                            |                                                                |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|tle2 1                |TLE(AC) 1550ms|                                            |                                                                |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|tle2 2                |TLE(AC) 1536ms|                                            |                                                                |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|tle2 3                |TLE(AC) 1537ms|                                            |                                                                |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|tle2 4                |TLE(AC) 1530ms|                                            |                                                                |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|tle2 5                |TLE(AC) 1557ms|                                            |                                                                |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|tle3 6                |TLE(WA) 1548ms|E:\code\ACM-generator\debug\cmp\tle3\6.ans  |wrong answer 1st lines differ - expected: '140', found: '139'   |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|tle3 7                |TLE(WA) 1550ms|E:\code\ACM-generator\debug\cmp\tle3\7.ans  |wrong answer 1st lines differ - expected: '120', found: '119'   |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|tle3 8                |TLE(WA) 1544ms|E:\code\ACM-generator\debug\cmp\tle3\8.ans  |wrong answer 1st lines differ - expected: '176', found: '175'   |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|tle3 9                |TLE(AC) 1542ms|                                            |                                                                |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|tle3 10               |TLE(WA) 1552ms|E:\code\ACM-generator\debug\cmp\tle3\10.ans |wrong answer 1st lines differ - expected: '129', found: '128'   |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|wa 2                  |WA 40ms       |E:\code\ACM-generator\debug\cmp\wa\2.ans    |wrong answer 1st lines differ - expected: '1590', found: '1589' |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|wa 3                  |WA 23ms       |E:\code\ACM-generator\debug\cmp\wa\3.ans    |wrong answer 1st lines differ - expected: '1117', found: '1116' |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|wa 4                  |WA 22ms       |E:\code\ACM-generator\debug\cmp\wa\4.ans    |wrong answer 1st lines differ - expected: '1544', found: '1543' |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|wa 5                  |WA 21ms       |E:\code\ACM-generator\debug\cmp\wa\5.ans    |wrong answer 1st lines differ - expected: '153', found: '152'   |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|wa 6                  |WA 22ms       |E:\code\ACM-generator\debug\cmp\wa\6.ans    |wrong answer 1st lines differ - expected: '140', found: '139'   |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|wa 7                  |WA 21ms       |E:\code\ACM-generator\debug\cmp\wa\7.ans    |wrong answer 1st lines differ - expected: '120', found: '119'   |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|wa 8                  |WA 23ms       |E:\code\ACM-generator\debug\cmp\wa\8.ans    |wrong answer 1st lines differ - expected: '176', found: '175'   |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|wa 10                 |WA 23ms       |E:\code\ACM-generator\debug\cmp\wa\10.ans   |wrong answer 1st lines differ - expected: '129', found: '128'   |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|wa 11                 |WA 21ms       |E:\code\ACM-generator\debug\cmp\wa\11.ans   |wrong answer 1st lines differ - expected: '678', found: '677'   |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|wa 12                 |WA 52ms       |E:\code\ACM-generator\debug\cmp\wa\12.ans   |wrong answer 1st lines differ - expected: '1106', found: '1105' |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|wa2 1                 |WA 26ms       |E:\code\ACM-generator\debug\cmp\wa2\1.ans   |wrong answer 1st lines differ - expected: '91', found: '90'     |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+
|wa2 9                 |WA 22ms       |E:\code\ACM-generator\debug\cmp\wa2\9.ans   |wrong answer 1st lines differ - expected: '52', found: '51'     |
+----------------------+--------------+--------------------------------------------+----------------------------------------------------------------+



```
