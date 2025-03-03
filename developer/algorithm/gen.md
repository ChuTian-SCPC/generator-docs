### 描述

生成器的设计比较复杂，总体上描述是：

- 基类`_Gen`，其中函数`virtual void generate()`是调用生成器的接口，所有类的`gen()`函数都是调用这个接口。

- `_BasicGen<T>`继承`_Gen`，里面的`T*`指向类，可以获取和设置类的成员变量。

- `_GenSwitch`内部有一个`_Gen*`，所有的类都继承它，可以修改`_Gen*`以实现切换生成器。

以上是最基础的类，所有的生成器类都是从`_Gen`派生而来，所有的类也都继承了`_GenSwitch`。

比如要看`Tree`和`TreeGen`，就会看到：

`Tree`的继承路线是：

```
Tree<NodeType, EdgeType>
|
|
_GenTree<NodeType, EdgeType>
|
+------------------------------------------------------+
|                                                      |
_RandomFuncTree<NodeType, EdgeType>                    _TreeGenSwitch
|                                                      |
+--------------+                                       |
|              |                                       |
_BasicTree     _RandomFunction<NodeType, EdgeType>     _GenSwitch
|
|
_BasicTreeGraph

```

`TreeGen`的继承路线是：
```
TreeGen<NodeType, EdgeType>
|
|
BasicTreeGen<Tree, NodeType, EdgeType>
|
|
_BasicGen<TreeType<NodeType, EdgeType>>
|
|
_Gen
```

`Tree`，`Graph`和`Geometry/Polygon`都有Basic的生成器，它包括了一些都会使用到的函数，比如`__add_edge`，`__init`，`__judge_limit`等。

总体上步骤为：

1. `__init`：

    一. 自己的初始化`__self_init`，主要包括对一些随机设置的值，比如基环树没有设置环大小时，需要随机初始化一个值。

    二. 检查是否存在无法生成的情况`__judge_limits`，其中自己特有的一些检查是` __judge_self_limit`。

    三. 初始化，将边，点权等需要清空的变量清空。

2. `__generate_tree/__generate_graph/__generate_geometry`生成需要的类。

在一般情况下，继承相应的生成器已经能够解决问题，继承相应的Basic生成器能够解决大部分问题。

如果想要完全自行控制生成器的行为，可以继承`_BasicGen`或者`_Gen`，从底层一步步构建。

#### 设计的原因

在之前的版本中，对于`Tree`有两种生成方式，分别是`RandomFather`和`Pruefer`。

这两种生成方法来自[OI-WIKI](https://oi-wiki.org/contest/problemsetting/#%E7%94%9F%E6%88%90%E9%9A%8F%E6%9C%BA%E6%A0%91)的介绍。

但是其中还有一个方案是从$[i\times low, i\times hight]$中选择$i$的父亲，这如何实现我并没有思路。

在查看了许多其他generator的设计方案，我发现都是将生成的策略作为一个函数。

我认为这样的耦合度太高，是我不喜欢的一种设计方向：如果用户需要采取新的策略，就很难再简单地使用；对于我则每次考虑可能需要新加一个生成算法的时候，就在原本已经很长的类里面再塞一堆代码，还要考虑有些不一致的部分怎么取不同的名字区分开，比如`RandomFather`和`Pruefer`不同的初始化到底是通过不同的函数名还是加上if判断呢？

所以我决定使用策略模式，将生成器拆解出来，这样在我想要添加不同的生成算法时，不用考虑修改原本的代码。

这样不仅仅是我可以将类解耦，用户也可以自行定义自己的生成器进行使用。这与我最初想要设计一个易用且自由的generator相符。

其中`set_tree_generator`，`set_graph_generator`和`set_geometry_generator`不采用统一的`set_generator`是因为之前`Tree`设置不同的生成器用的就是`set_tree_generator`，虽然在这次重构中，对于一些接口都进行了删除、修改。但是我依旧尽量最小化地改动原有的接口，出于对原本`set_tree_generator`的统一，不得不进行了如此的设计。

当然并不存在十全十美的设计方案，这套方案所带来的弊端就是生成器与原本的类中成员变量的交互变的异常困难，不仅设置获取有额外的开销，更困难的实在模板下难以编写和检查。

虽然这对于一般的使用并不会造成影响，但是想要修改则会需要大量的时间去了解代码的含义。

所以他对于开发不是一个好的代码，也让我想要让其他人帮忙维护时面对比以往更大的困难。

如果你有认为更好的设计方案，可以提出[Issue](https://github.com/ChuTian-SCPC/ACM-generator/issues/new)或者[Discussion](https://github.com/ChuTian-SCPC/ACM-generator/discussions/new/choose)帮助我改进项目！