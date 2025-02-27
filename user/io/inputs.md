生成的数据会在工作目录下新建一个`testcase_folder`文件夹放入，它的默认值是`testcases`。

标准输入文件以`input_suffix`结尾，它的默认值是`.in`。

如果需要修改请参考[设置](../setting/setting.md)。

### 函数

可以通过以下函数生成数据：

- `make_inputs(int start, int end, T program)`：生成编号从$start$到$end$的标准输入文件。

- `make_inputs(int index, T program)`：生成编号为$index$的标准输入文件。

- `fill_inputs(int sum, T program)`：从编号$1$开始查找，生成$sum$个未被使用的最小编号的标准输入文件。例如，如果已有编号$2,3,5$，当$sum=3$时，将生成编号$1,4,6$。

- `fill_inputs(T program)`：从编号$1$开始查找，生成$1$个未被使用的最小编号的标准输入文件。

以上的`program`都必须是可执行文件路径或者函数，在一般情况下是可转换为`Path`的类型或者可转换为`std::function<void()>`的类型，具体可以参考[可执行路径与函数管理](command_path_func.md)。

### 使用示例

你有两种方式生成标准输入文件：

以A+B问题为例。

1. 使用可执行文件(`CommandPath`)

你可以按照常规使用`testlib.h`的方式，写一个generator编译成可执行文件，然后再写一个代码调用可执行文件。

可执行文件`gen.exe`的代码：

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main(int argc, char* argv[]) {
    init_gen(argc, argv);
    cout << rand_int(1, 100) << " " << rand_int(1, 100) << endl;
    return 0;  
}
```

调用可执行文件生成测试样例的代码：

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    make_inputs(1, 5, "gen.exe");
    return 0;  
}
```

2. 使用函数(`CommandFunc`)

你可以将generator和生成多个测试样例的代码写在一个文件里面：

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

void gen() {
    cout << rand_int(1, 100) << " " << rand_int(1, 100) << endl;
}

int main() {
    make_inputs(1, 5, gen);
    return 0;  
}
```

使用函数方式生成数据时，需要特别注意**全局变量的状态管理**。

由于`gen()`函数在生成多个测试样例时会被重复调用，如果函数中使用了全局变量且未在每次调用时重置，可能会导致生成的测试数据不符合预期。

以下示例展示了全局变量对生成结果的影响：

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int test = 1;  // 全局变量

void gen() {
    cout << test << endl;  // 输出当前值
    test++;                // 修改全局变量
}

int main() {
    make_inputs(1, 5, gen);  // 生成5个测试样例
    return 0;  
}
```

运行上述代码后，生成的$5$个输入文件中的值分别为$1$,$2$,$3$,$4$,$5$。这是因为全局变量`test`在每次调用`gen()`时被修改并保留其状态，导致输出结果递增

### 随机种子

对于generator，为了使随机结果不同，需要设置随机种子。

在**默认情况下**，随机种子为测试样例的编号。

即对于上述generator的代码，它相当于执行了如下的命令行指令：

```bash
gen.exe 1 > 1.in
gen.exe 2 > 2.in
gen.exe 3 > 3.in
gen.exe 4 > 4.in
gen.exe 5 > 5.in
```

如果想修改随机种子，有以下方案：

1. 修改`default_stable_seed`。

参考[设置](../setting/setting.md)，可以修改`default_stable_seed`，从而改变随机种子：

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    default_stable_seed = "test";
    make_inputs(1, 5, "gen.exe");
    return 0;  
}
```

这等同于命令行指令：

```bash
gen.exe test 1 > 1.in
gen.exe test 2 > 2.in
gen.exe test 3 > 3.in
gen.exe test 4 > 4.in
gen.exe test 5 > 5.in
```

2. 设置`CommandPath`或`CommandFunc`的命令行参数。

可以参照[设置命令行参数](command_setting.md)自行实现所需要的命令行参数。

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    CommandPath p("gen.exe", "setting seed by myself!");
    make_inputs(1, p);
    return 0;  
}
```
