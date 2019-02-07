\newpage

# 为什么是 Crystal？

也许你已经在写 Ruby，并且作为主要生产工具，并享受于此。为什么还要了解 Crystal？

让我们花一分钟回顾一下 Ruby 最大的弱点是什么？对于我来说有以下三点：

-   并发
-   速度
-   文档

Ruby 有哪些很酷的地方?

-   块
-   Vaguely functional *(怎么翻译？)*
-   语法非常简单
-   关注开发者快乐
-   快速启动并运行
-   动态类型

所以我们可以从像 Ruby 一样的语言中学到很多，很好的处理并发，运行飞快。我们不想牺牲匿名函数，漂亮的语法，不用写一个 `AbstractFactoryFactoryImpls` 就可以完成工作。

我觉得那个语言就是 *Crystal*。

现在：Crystal 不是很完美，但正在变得更好。但重点是*学习*，使用一种非常熟悉但又不同的语言，可以学会很多东西。

用 Crystal 来一个 "Hello World" ：

```ruby
puts "Hello, world!"
```

Crystal 并发版 "Hello World" ：

```ruby
channel = Channel(String).new
10.times do
  spawn {
    channel.send "Hello?"
  }
  puts channel.receive
end
```

Ruby 可能会是这个样子:


```ruby
10.times.map do
  Thread.new do
    puts "Hello?"
  end
end.each(&:join)
```

差不多了，不过请注意与 Ruby *类似*的地方 ：

-   语法相同
-   变量虽然是静态类型的，但有类型推导，所以我们不需要声明类型

还是有一些 *不同* ：

-   静态编译有时候会让我们抓狂

还有 ：

    $ time ./hello
    ./hello  0.00s user 0.00s system 73% cpu 0.008 total

    $ time ruby hello.rb
    ruby hello.rb  0.03s user 0.01s system 94% cpu 0.038 total

5 倍速提升，but 无关紧要的性能测试。

无论如何，我希望你明白我的观点：有很多 Crystal 的东西在语法上与 Ruby 相似让你有种 “家” 的感觉，它的优点也是 Ruby 最大的弱点，即使你没有在日常工作中使用，我认为你也可以通过把玩 Crystal 来学到很多东西。
