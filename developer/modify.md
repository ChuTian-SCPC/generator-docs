`src`文件夹下是原始的模块化代码，它们最后通过[xmake](https://github.com/xmake-io/xmake)合并成一个头文件`generator.h`。

你可以在修改完对应模块的代码之后使用:

```bash
xmake l cli.amalgamate -o .
```

来重新生成头文件。
