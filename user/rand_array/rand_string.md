生成随机字符串时需要使用字符集，我们提供了一些[常用字符集](../enum/char_type.md)供您选择。如果您需要自定义字符集，可以自行参考[Testlib](https://github.com/MikeMirzayanov/testlib)库的相关文档。

### 函数

- `rand_string(int n, _enum::CharType type = _enum::LowerLetter)`：返回一个长度为`n`的随机字符串，字符集为`type`，默认是小写字母。

- `rand_string(int from, int to, _enum::CharType type = _enum::LowerLetter)`：返回一个长度在`[from, to]`之间的随机字符串，字符集为`type`，默认是小写字母。

- `rand_string(int n, std::string format)`：返回一个长度为`n`的随机字符串，字符集由`format`决定。

- `rand_string(int from, int to, std::string format)`：返回一个长度在`[from, to]`之间的随机字符串，字符集由`format`决定。

- `rand_string(std::string format)`：返回一个字符串，格式由`format`决定。

**注意**：对于传入的长度，其值不能够超过`vector_limit`的限制，如果需要修改，请参考[设置](../setting/setting.md)。

### 示例

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
    init_gen();
    string s1 = rand_string(10, UpperLetter);
    string s2 = rand_string(3, 10);
    string s3 = rand_string(10, "[!@#$%]");
    string s4 = rand_string(3, 10, "[a-e]");
    string s5 = rand_string(string_format("[0-7]{%d,%d}", 3, 10));
    cout << s1 << " " << s2 << " " << s3 << " " << s4 << " " << s5 << endl;
    return 0;
}
```
