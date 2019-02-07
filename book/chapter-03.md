\newpage

# 编写你的第一个 Crystal 程序

好的！让我们来看看：为了称自己为 “X 程序员”，你必须在 X 中写下 “Hello，world”，所以让我们开始吧。打开一个文本文件，我使用 `vim`，因为我是那种人，但使用你想要的任何东西，Crystal 程序以 `.cr` 后缀结尾：

```
$ vim hello.cr
```

写下这句诗：

```ruby
puts "Hello World!"
```

通过 `crystal` 命令运行：

```
$ crystal hello.cr
Hello World!
```

它应该运行并打印输出且没有错误，如果出现错误，请仔细检查你是否有双引号，错误看起来像这样：

```
$ crystal hello.cr
Syntax error in ./hello.cr:1: unterminated char literal, use double quotes for strings

puts 'Hello World!'
```

顺便说一句，`Crystal` 命令非常适合快速运行代码，但速度很慢，每次会先编译再运行程序，让我们看看运行该程序需要多少时间。

```
$ time crystal hello.cr
crystal hello.cr  0.30s user 0.20s system 154% cpu 0.326 total
```

就一个 `Hello World` 花费了 0.326 秒? 现在确实很慢。

你可以使用 `build` 命令将其编译为 Native Code，而不是同时执行编译和运行两个步骤。

```
$ crystal build hello.cr
```

然后运行你的程序，UNIX 中平常干的那样：

```
$ time ./hello
./hello  0.00s user 0.00s system 87% cpu 0.006 total
```

你应该会看到 "Hello, world." 打印在屏幕上，并且速度比之前快了 50 倍。 :) 恭喜!
