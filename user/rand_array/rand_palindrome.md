### 函数

- `rand_palindrome(int n, int p, _enum::CharType type = _enum::LowerLetter)`：返回一个长度为$n$的字符串，其中至少有长度为$p$的回文子串，字符集为`type`，默认是小写字母。

- `rand_palindrome(int n, int p, std::string format)`：返回一个长度为$n$的字符串，其中至少有长度为$p$的回文子串，字符集由`format`决定。

**注意**：

- 对于传入的长度$n$，其值不能够超过`vector_limit`的限制，如果需要修改，请参考[设置](/user/setting/setting.md)。

- 回文串的长度$p$应该小于等于$n$。

### 示例

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
  init_gen();
  string s1 = rand_palindrome(10, 5);
  string s2 = rand_palindrome(10, 10, "[012]");
  cout << s1 << " " << s2 << endl;
  return 0;
}
```
