`CommandPath`和`CommandFunc`都有一个变量`_enable_default_args`表示是否启用默认的命令行参数。

如果你不想启用默认的命令行参数，可以使用`set_enable_default_args(false)`来禁用。

当`CommandPath`和`CommandFunc`的使用如下构造函数时，`_enable_default_args`默认为`false`：

```cpp
template<typename T, typename = typename std::enable_if<IsPathConstructible<T>::value>::type>
CommandPath(T&& s, std::string args);

template<typename T, typename = typename std::enable_if<IsFunctionConvertible<T>::value>::type>
CommandFunc(T&& func, std::string args);
```

命令行参数的类型是`std::string`。你可以通过如下方法获取和设置它：

- `std::string args() const`: 获取命令行参数。

- `std::string& args_ref()`: 获取命令行参数的引用。

- `void set_args(std::string args)`: 设置命令行参数。

- `void add_args(const Args&... args)`: 在后面添加命令行参数，以空格隔开。

- `clear_args()`: 清空命令行参数。

**注意**：

如果你设置了`_enable_default_args`为`false`，那么所有默认的命令行参数都不会添加，**包括**对于输入输出文件的重定向。

比如对于一个生成输入的可执行文件`gen.exe`，原本它默认的命令行参数为`gen.exe 1 > 1.in`。

如果你设置了`_enable_default_args`为`false`，并且设置它的命令行参数为`2`，那么调用的时候它相当于命令行执行`gen.exe 2`, 而不是`gen.exe 2 > 1.in`。

需要注意的是，上述行为在不同系统和条件下的行为表现存在**差异**：

- 对于Linux系统，使用`CommandPath`**不会**对输入输出重定向，因为它的实现方式是通过命令行重定向（如`> 1.in`）实现的。

- 对于其他情况，包括Windows系统和使用`CommandFunc`的时候，对于输入输出不需要自行添加重定向的命令行参数，因为它们是通过`freopen`或者重定向句柄实现的。

如果你设置了`_enable_default_args`为`true`，但是使用了`set_args`等方法设置命令行参数，那么默认的命令行参数会添加到后面，可能会出现未知的行为。

### 使用示例

如果你有传入参数的需求，比如`testlib.h`有一个`opt`的特性你需要使用：

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main(int argc, char* argv[]) {
  init_gen(argc, argv);
  int n = opt<int>("n");
  int m = opt<int>("m");
  cout << n << " " << m << endl;
  cout << rand_int(n, m) << endl;
  return 0;
}
```

这时候你如果使用`make_inputs`那么得到的结果会是相同的。

你又希望能够生成的随机数有随机性，你可以将`_enable_default_args`设为`true`，也可以自行设置随机种子：

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
  for (int i = 1; i <= 5; i++) {
    CommandPath p("gen_opt.exe", "-n=10 -m=20");
    p.set_enable_default_args(true); // 或者可以使用 p.add_args(i);
    make_inputs(i, p);
  }
  return 0;
}
```