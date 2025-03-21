### Graph

主要考虑在一定连通的情况下，做法是先生成一棵树保证连通，然后再往上加边。

### BipartiteGraph

如果要求强制连通，则生成方式比较复杂，因为虽然一棵树是二分图，但是不能够保证分完之后左部和右部的大小符合要求。

现将左部和右部分开，对于左部随机结点的度数，要求至少为$1$，总和为$node\_count - 1$；右部同理。

每次找度数为$1$的结点，然后再它对面的部分找一个度数大于$1$的结点连边，直到两边都只存在一个度数为$1$的结点，将它们相连。

在无重边的情况下，边的个数最多是$left\times right$。

对于随机左部的情况，二分求得左（右）部需要的最小点数$l$，然后随机$[l, node\_count -l]$作为左部大小。

### DAG

生成方式类似[RandomFather](/developer/algorithm/tree.md#randomfather)，保证随机$u$和$v$的关系一定是$u$的位次小于$v$的位次。

保证连通的话，生成连通部分的方案就是采用`RandmFather`。

### CycleGraph

环图比较简单，生成一个排列，然后相邻的两个结点连边即可。

### WheelGraph

轮图同环图，只不过将第一个结点拎出来与其余结点连边。

### GridGraph

网格图求边数上限比较麻烦，枚举一下行数然后求上限：$row\times (column - 1) + column \times (row - 1) - 2 \times (row \times column - node\_count)$。

将点按照行列拍好后，对于一定要连通的先将每行连起来，然后将一列连起来。

随机边则随机一个点，然后随机一个方向，看这个方向能不能连边。

### PseudoTree/PseudoInTree/PseudoOutTree

先用`CycleGraph`生成一个环，剩余点类似于[RandomFather](/developer/algorithm/tree.md#randomfather)，随机取前面一个点与之相连。

### Cactus

仙人掌最多有$node\_count - 1 + (node\_count - 1) / 2$条边。

因为一条边只能属于一个简单环，而简单环最小为$3$，每加入一个环，边数加一，所以要让环的数量尽可能多。

并且由于连通，考虑新加入一个点集，它们只能和前面有且只有一个点构成新的一个环，所以点集大小为$2$。而且第一个点集大小为$3$。

由于连通需要$node\_count - 1$条边，最多有$(node\_count - 1) / 2$个点集（第一个点集大小为$3$，其余为$2$），得到边数上界。

生成也是如此，将需要额外加边的点集分好，然后将剩余的点随机分入这些点集或者单独放入新的点集。

对于除了第一个点集，其他都会从前面选一个点，然后一起作为新的点集使用`CycleGraph`生成一个环，对于点集小于$3$的情况进行特判。

### Forest

使用`Link`，将$node\_count-edge\_count$棵树合并到一起。

### StartReachableGraph

生成一颗有根树，根为`start`，然后随机加边。