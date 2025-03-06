### ConvexHull/Triangle

根据[StackOverflow](https://stackoverflow.com/questions/6758083/how-to-generate-a-random-convex-polygon)上的方案去构造。

唯一区别在于上面的方案中会保证不存在包含$0$的向量，而我采用的方案可能会存在$(0,y)$和$(x,0)$的向量。

为了使没有重点，也就不能有$(0,0)$向量，所以要把$x=0$和$y=0$的情况避开。

而`max_try`的采用也是没有办法的办法，目前没有找到固定范围内凸包点数上下界的限制是多少，也不知道如何在固定区域实现最多的点。

对于严格凸包，我依然没有什么解决方案。

原本计划在给定点上增加一定数目随机，然后将三点共线的情况删去。

但是经过一些测试发现，不同的点数和范围限制，出现三点共线的点占生成点数的百分比差别会很大，目前没想到一个好的调整策略。

如果你有更好的方案，欢迎提交[Issue](https://github.com/ChuTian-SCPC/ACM-generator/issues/new)或者[PR](https://github.com/ChuTian-SCPC/ACM-generator/pulls)。

### SimplePolygon

随机简单多边形我一直没有找到一个好的方案去做，所以目前的方案也是我不满意的，但是先实现了一版。

目前方案是deepseek给的一个方案：随机$node\_count$个点，然后求出质心，以质心做极角排序，然后依次连接。

如果你有更好的方案，欢迎提交[Issue](https://github.com/ChuTian-SCPC/ACM-generator/issues/new)或者[PR](https://github.com/ChuTian-SCPC/ACM-generator/pulls)。