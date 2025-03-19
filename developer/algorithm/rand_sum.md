`rand_sum`的原型是[Testlib](https://github.com/MikeMirzayanov/testlib)中的`rnd.partition`。

其中`rand_sum(int size, T sum)`和`rand_sum(int size, T sum, T min_part)`则是直接调用testlib的接口。

但是有的时候出题会遇到：有$T(1\le T\le 10^5)$组数据，每组数据一个$n(1\le n\le 10^5)$，保证$n$的总和不超过$10^6$。

面对这样的数据就没有办法用`rnd.partition`去生成$n$了。

`rand_sum`实现了一个有上下界限制的版本，但是这个算法**不是**均匀随机的。

考虑到随机一个长度为$n$的数组，总和为$sum$，数值为$[from,to]$的问题等价于：随机一个长度为$n$的数组，总和为$sum - n\times from$，数值为$[0, to - from]$。

所以问题等同于随机数组中对于元素上界有限制。

在查阅一些资料之后，目前我并没有找到一个均匀随机，且时间复杂度能够让人接受的算法去解决对于数组元素有上界限制的方案。

如果您有更好的方案，欢迎提出[Issue](https://github.com/ChuTian-SCPC/ACM-generator/issues/new)或者[PR](https://github.com/ChuTian-SCPC/ACM-generator/pulls)。

最初的方案是对于每个元素随机一个值$v = \text{rand}(0, \min\{from, sum\})$，然后将$sum$减去$v$。

但是这样的方案存在一个问题：在很多情况下，尤其是$from$和$sum$接近的时候，前面的数值会远比后面大，且$0$的情况会非常多。

所以现在采取以下的策略：

主要思路是每次随机将“一份”值给一个元素，且这个元素当前的值加上这份值的和小于等于$from$。

将设置中的值`_rand_sum_sum_limit`记作$l$。

对于$sum$较小的情况，即$sum\lt l$时，“一份”的值是$1$。

对于$sum$较大的时候，“一份”是$\cfrac{sum}{l}$，由于这个值是固定的，为了增加更多随机性，即不让数组元素都为这个值的倍数，会加上一个随机增减量$m$，为这个值的$5\%$。

当$sum$减少到较小情况时，再采取处理较小的策略。

这样生成的数组会相对比较均衡。