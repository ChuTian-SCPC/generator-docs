`CommandPath`和`CommandFunc`，它们是用来处理包含命令行参数的路径和函数的类。

对于一般的用户并不需要深入了解它们的实现细节，在一般的使用场景下也不需要显式调用它们的构造函数。

在使用`testlib.h`时，当你写了一个generator之后，需要通过命令行参数设置随机种子；在你使用checker，validator的时候也需要通过命令行调用，这些事情在默认情况下被简化了。

除非你明确地需要使用非默认的命令行参数，否则不建议调用它们包含命令行参数的构造函数和对他们进行参数的设置和修改。

如果你需要使用非默认的命令行参数，你可以参考[设置命令行参数](/user/io/command_setting.md)。

对于大部分用户，你只需要知道它们的作用即可。

`CommandPath`表示一个**可执行文件**的路径，它常用的构造函数如下：

```cpp
template<typename T, typename = typename std::enable_if<IsPathConstructible<T>::value>::type>
CommandPath(T&& s);
```

`T`是一个可转换为`Path`的类型，详见[路径](path.md)。

`CommandFunc`表示一个函数，它常用的构造函数如下：

```cpp
template<typename T, typename = typename std::enable_if<IsFunctionConvertible<T>::value>::type>
CommandFunc(T&& s);
```

`T`是一个可转换为`std::function<void()>`的类型，包括函数指针，lambda函数，仿函数，std::bind等。
