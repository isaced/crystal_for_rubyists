\newpage

# 并发与管道

还记得第一章节吗,我们做了一个并发的 hello world.回顾一下:

```ruby
channel = Channel(String).new
10.times do
  spawn {
    channel.send "Hello?"
  }
  puts channel.receive
end
```

在 crystal 中我们用关键字 spawn 令一些事务可以在没有锁死主线程的情况下后台运行。
为了达到这样的目的,spawn 创建了一个轻量线程名叫 Fiber (纤维),创建 fiber 成本低，所以你可以在一个单核心( core )中创建上万条 fiber.
Ok,既然我们可以让 fiber 后台运行，那如果我们想要 fiber 的返回值呢.这时，管道( Channel )就派上用场了


## Channel

顾名思义,Channel 就是一根接收方和输送方的管道,所以 Channel 可以通过 send 和 receive 方法彼此交互。让我们一步一步的分析上面的代码.

```ruby
channel = Channel(String).new
```

我们用 Channel(String).new 创建了一个管道,需要注意的是我们正在创建一个将会 send 和 receive 字符串类型的消息的管道。

```ruby
10.times do
  spawn {
    channel.send "Hello?"
  }
  puts channel.receive
end
```

我们先不看循环，我们正处于 spawn 中向管道发送数据。你可能会问“为什么我们要在后台发送数据”.
 send 方法是一种锁死操作，如果我们在 main 进程里面使用它就会永远锁死整个程序。看下这个:

```ruby
channel = Channel(String).new
channel.send "Hello?" # This blocks the program execution
puts channel.receive
```

上面的程序的输出是什么呢?实际上这个程序并没有执行完,因为它被 send 方法锁死了,好了我们现在知道了,继续!


```ruby
spawn {
  channel.send "Hello?"
}
puts channel.receive
```

我们只是用 spawn 在后台中通过管道发送了一个信息.然后我们用 channel.receive 接受它的返回.这个例子中消息是 ”hello?”,所以程序打印 hello? 并完成.