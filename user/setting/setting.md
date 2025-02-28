`setting.h`中定义了一些常用的设置。

其中变量名前面包含`_`的是内部使用的变量，用户一般不需要考虑；而不包含`_`的变量是用户可以按需调整的配置项或者是可能会使用到的。

当然，在某些特殊情况下，如果您确实需要对`_`开头的变量进行修改，也可以自行调整，但请注意这可能会内部逻辑产生影响，建议在充分了解其作用后再进行修改。

### 可修改配置项

- `vector_limit`：生成的随机数组的最大长度, 默认为$10^7$，在绝大部分情况下都不需要考虑修改，除非你需要生成的数组长度非常大。

- `node_limit`：生成的随机树，图以及几何图形的最大点数, 默认为$10^7$，同样在绝大部分情况下都不需要考虑修改。

- `edge_limit`：生成的随机树，图的最大边数, 默认为$10^7$，同样在绝大部分情况下都不需要考虑修改。

- `test_case_limit`：生成的随机测试用例文件(输入、输出)的最大数量, 默认为$10^3$，同样在绝大部分情况下都不需要考虑修改。

- `testcase_folder`：生成的随机测试用例文件(输入、输出)的文件夹名称, 默认为`testcases`。

- `compare_folder`：存放compare结果的文件夹名称, 默认为`cmp`。

- `hack_folder`：存放hack结果的文件夹名称, 默认为`hack`。

- `validate_folder`：存放validate结果的文件夹名称, 默认为`validate`。

- `input_suffix`：生成的随机测试用例文件(输入)的后缀名称, 默认为`.in`。

- `output_suffix`：生成的随机测试用例文件(输出)的后缀名称，默认为`.out`。

- `same_log_for_class`：控制在生成随机数组、树、图和几何时，对于同一随机函数中重复出现的相同警告信息，是否只显示一次。默认为`false`，即不显示重复信息。

- `time_limit_over_ratio`：在compare中，控制实际测试的时间为所给`time_limit`的倍数，默认为$2$。该值应大于等于$1$。

- `time_limit_check_ratio`：在compare中，控制对于超时为所给`time_limit`的倍数之内的代码进行结果正误的检测，默认为$2$。该值应小于等于`time_limit_over_ratio`。

- `default_seed`：控制是否使用默认的随机种子，默认为`true`，即使用默认的随机种子。

- `default_stable_seed`：控制使用默认的随机种子时，生成的随机数的种子中固定的部分，默认为空字符串。

- `default_hack_stable_seed`：控制在使用默认的随机种子并且`hack`时，生成的随机数的种子中固定的部分，默认为`hack`。

### 可能会使用的配置项

- `time_limit_inf`：表示时间限制为无限的数，默认为$-1$。

### 不建议修改配置项

- `_path_split`：当前系统路径分隔符。

- `_other_split`：其他系统路径分隔符。

- `_default_path`：默认的路径，为空字符串，用于一些函数参数表示不需要有这个文件路径时候的传参。

- `_checker_folder`：用于存常用默认checker的文件夹的名称。

- `_sub_checker_folder`：对应系统的checker的子文件夹的名称。

- `_lib_folder`：`generator.h`所在的文件夹的路径。

- `_function_count`：当前使用随机函数的数量，用于`compare`时使用`CommandFunc`时计数和区分。

- `_first_generator_argv`：generator的第一个默认参数，默认为`generator`。

- `_first_checker_argv`：checker的第一个默认参数，默认为`checker`。

- `_first_validator_argv`：validator的第一个默认参数，默认为`validator`。

- `_error_return`：当运行代码出现错误时的返回值，默认为$-1$。

- `_rand_sum_sum_limit`：在使用`rand_sum`时，对于该值以上的`sum`采用一种较快但不完全随机的策略，默认为$10^6$。