概率表的目的在于多次使用相同的概率分布随机时，避免每次重复计算。

### 构造函数

- `ProbTable<KeyType>()`：默认构造函数，构造一个空的概率表。

- `ProbTable<KeyType>(KeyType key, ValueType value)`：构造一个概率表，其中只有一个键值对`(key, value)`。

- `ProbTable<KeyType>(const Con& map)`：构造一个概率表，其中map的类型为`std::map<KeyType, ValueType>`或者`std::unordered_map<KeyType, ValueType>`，其中`ValueType`为整型。

### 其他函数：

- `void add(const KeyType& key, ValueType value)`：添加一个键值对`(key, value)`到概率表中。

    - 如果`value`小于$0$，则会被忽略。

- `void add(const Con& map)`：添加一个map中的所有键值对到概率表中。

    - map中值小于$0$的键将会被忽略。

- `void clear()`：清空概率表。

- `KeyType rand() const`：随机返回一个键值对中的键，随机数生成的概率由概率表决定。

    - 概率表不能为空。

    - 概率表中所有值的总和必须大于$0$。

    - 概率表的最大容量不能超过`vector_limit`的限制，如果需要修改，请参考[设置](/user/setting/setting.md)，

### 性能测试：

参考`test_numeric.hpp`的性能测试：

测试构造一个包含$1000$个键值对的概率表，用它随机$100$次。

- `rand_prob origin`：v0.9.0及之前的实现。

- `rand_prob basic`：每次随机传入`std::map`。

- `rand_prob with prob table`：每次随机传入`ProbTable`。


```
benchmark name                       samples       iterations    est run time
                                     mean          low mean      high mean
                                     std dev       low std dev   high std dev
-------------------------------------------------------------------------------
rand_prob origin                               100             1    129.271 ms 
                                         703.63 us    684.793 us    738.601 us 
                                            127 us    79.2491 us    203.138 us

rand_prob basic                                100             1    73.1354 ms 
                                        691.357 us    670.768 us    727.541 us 
                                          135.3 us    87.0047 us    197.377 us

rand_prob with prob table                      100             4     5.8144 ms 
                                        16.3337 us    14.8488 us     21.184 us 
                                         12.264 us     4.1088 us    27.3145 us
```

