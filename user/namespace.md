Generator所有的代码均在`generator`命名空间下， 在通常情况下使用`using namespace generator::all`即可。

命名空间更详细地划分为：

- `namespace generator::tools` : 一些工具函数。

- `namespace generator::_msg` : 用于输出log的类和函数。

- `namespace generator::_setting` : 全局设置变量。

- `namespace generator::_enum` : 枚举类型。

- `namespace generator::io` : 生成输入输出文件，判题相关函数。

- `namespace generator::rand_numeric` : 随机数值。

- `namespace generator::rand_array` : 随机数列，包括字符串。

- `namespace generator::rand_graph` : 随机树和图。

    - `namespace generator::rand_graph::unweight` : 无权树和图。

    - `namespace generator::rand_graph::node_weight` : 带点权的树和图。

    - `namespace generator::rand_graph::edge_weight` : 带边权的树和图。

    - `namespace generator::rand_graph::both_weight` : 带点权和边权的树和图。

- `namespace generator::rand_geometry` : 随机几何。