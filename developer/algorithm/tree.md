### Tree

#### RandomFather

先随机一个从$0$到$node\_count$的排列$p$，如果是有根树，找到等于$root$的$p_i$，将它和$p_0$交换。

对于第$i(1\le i\le node\_count)$个点，从$p_0$到$p_{i-1}$随机一个$j$，连一条$p_j$到$p_i$的边。

#### Pruefer

随机一个pruefer序列，然后转化为树。

根据定义，随机一个长度为$node\_count$的数组$times$，数组元素大于等于$0$，总和为$node\_count - 2$，将这个数组随机打乱成一个pruefer序列。

将pruefer序列转化为树。

### Chain

链的生成器继承自`RandomFather`，与之不同的部分是将$p_{i-1}$与$p_i$相连。

由于$p_0$在初始化的时候已经被换成了根，所以链的根一定是其中一端。

### Flower

菊花图的生成器继承自`RandomFather`，与之不同的部分是将$p_0$与$p_i$相连。

由于$p_0$在初始化的时候已经被换成了根，所以菊花图的根一定是中心点。

### HeightTree

将根放在高度为$1$的位置，随机将剩余点放到其他层$[2,height]$层，保证其他每个高度都至少有一个点。

对于每个点，在比他高度减$1$的那一层随机一个点作为它的父亲。

### MaxDegreeTree

生成器继承自`Pruefer`，区别在于通过pruefer序列的定义，对$times$随机的时候设置一个上限$max\_degree - 1$。

即随机生成一个长度为$node\_count$的数组，数组元素的范围为$[0, max\_degree - 1]$，总和为$node\_count - 2$。

### MaxSonTree

和`MaxDegreeTree`的思路类似，用$max\_son$作为上界，但是pruefer序列是描述无根树的，需要考虑特殊情况。

即$times[root] = max\_son$时，找到一个点$i$满足$times[i]\neq max_son$，交换$times[root]$和$times[i]$。

### FlowerChain

使用`TreeLink`，将一个菊花图和一个链合并到一起。
