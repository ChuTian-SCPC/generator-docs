### 函数

- `rand_bracket_seq(int len, std::string brackets = "()")`：返回一个长度为`len`的随机括号序列，括号集由`brackets`决定，默认为`()`。

- `rand_bracket_seq(int from, int to, std::string brackets = "()")`：返回一个长度在`[from, to]`之间的随机括号序列，括号集由`brackets`决定，默认为`()`。

`brackets`表示两两成对的合法括号匹配项，比如`()`表示`(`对应的括号是`)`，比如`()[]`表示`(`对应的括号是`)`，`[`对应的括号是`]`。

**注意**：

- 对于传入的长度，其值不能够超过`vector_limit`的限制，如果需要修改，请参考[设置](/user/setting/setting.md)。

- 传入的长度$len$应该是偶数，或者是$from$和$to$表示的范围包括偶数。

- `brackets`的长度应该是偶数。

### 示例

```cpp
#include "generator.h"
using namespace std;
using namespace generator::all;

int main() {
  init_gen();
  string s1 = rand_bracket_seq(10);
  string s2 = rand_bracket_seq(5, 11, "()[]{}");
  cout << s1 << " " << s2 << endl;
  return 0;
}
```