\newpage

# C绑定

很多C库都很有用，我们应该充分利用他们而不是去重写他们。
在 crystal 中,借助 bindings 来使用已存在的C库超级简单,
即使是 crystal 本身都在用C库.比如:crystal 使用 libpcre 
来实例化 Regex.下面是 Crystal 自己调用 libpcre 的例子:

```ruby
@[Link("pcre")]
lib LibPCRE
...
end
```

连接 libpcre 你只需要3行代码,我们使用 lib 关键字来把属于同一个库的方法和类型分为一组。

并且从 Lib 开始你的C库声明很流畅.

现在我们用 fun 关键字绑定到C functions 中.

```ruby
@[Link("pcre")]
lib LibPCRE
  type Pcre = Void*
  fun compile = pcre_compile(pattern : UInt8*, options : Int, errptr : UInt8**, erroffset : Int*, tableptr : Void*) : Pcre
end
```

这里我们用 matching 类型绑定到 libpcre 的编译 function 中。如此，
就能在 crystal 代码中轻松地获取 C function 了。

```crystal
LibPCRE.compile(..)
```
