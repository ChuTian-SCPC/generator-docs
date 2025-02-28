生成随机字符时需要使用字符集，我们提供了一些[常用字符集](../enum/char_type.md)供您选择。如果您需要自定义字符集，可以自行参考[Testlib](https://github.com/MikeMirzayanov/testlib)库的相关文档。

### 函数

- `rand_char(_enum::CharType type = _enum::LowerLetter)`：根据常用字符集返回一个随机字符，默认类型为$26$个小写字母。

- `rand_char(std::string format)`：根据传入的字符集返回一个随机字符。

### 示例

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    char a1 = rand_char();
    char a2 = rand_char(UpperLetter);
    char a3 = rand_char("[@#%$!&]");
    cout << a1 << " " << a2 << " " << a3 << endl;
    return 0;  
}
```