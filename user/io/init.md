在使用`testlib.h`时，需要在前面使用注册函数：

- `void registerGen(int argc, char *argv[], int randomGeneratorVersion)`：注册数据生成器（generator）。

- `void registerTestlibCmd(int argc, char *argv[])`：注册判题器（checker）。

- `void registerValidationCmd(int argc, char *argv[])`：注册校验器（validator）。

对于以上函数，有稍微简单的替代函数：

- `void init_gen(int argc, char *argv[])`：等同于`registerGen(argc, argv, 1)`。

- `void init_checker(int argc, char *argv[])`：等同于`registerTestlibCmd(argc, argv)`。

- `void init_validator(int argc, char *argv[])`：等同于`registerValidationCmd(argc, argv)`。

**注意**：

由于可执行文件必须通过命令行参数进行调用，因此请务必使用上述带有命令行参数`argc`和`argv`的版本！

如果只是单纯需要规避`testlib.h`的警告进行一些测试，可以使用`init_gen()`,`init_checker()`,`init_validator()`中任意一个。

比如你写了一个generator，源文件是`gen.cpp`，编译的可执行文件为`gen.exe`。

那么在`gen.cpp`中，需要这样写：

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

然后再写一个`cmd.cpp`用于调用`gen.exe`批量生成输入文件：

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    make_inputs(1, 5, "gen.exe");
    return 0;  
}
```

只有这样生成的输入文件才会有不同的随机种子，从而有不同的随机值。

如果你是通过函数写generator的话，在一般情况下你不需要考虑上述问题，也不需要使用`init_gen(argc,argv)`和`init_gen()`，比如：

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
