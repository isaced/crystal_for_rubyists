\newpage

# C 绑定 `Bindings`

很多 C 库都很有用，我们应该充分利用他们而不是去重写他们。
在 Crystal 中，借助 bindings 来使用已存在的 C 库超级简单，即使是 Crystal 本身都在用一些 C 库，比如 `libpcre` 来实例化 `Regex`，下面是 Crystal 链接 `libpcre` 的例子:

```ruby
@[Link("pcre")]
lib LibPCRE
...
end
```

链接 `libpcre` 只需要 3 行代码，我们使用 `lib` 关键字来把属于同一个库的方法和类型分为一组，并且从 `Lib` 开始你的 C 库声明很简单。

现在我们用 `fun` 关键字绑定到 C 函数中。

```ruby
@[Link("pcre")]
lib LibPCRE
  type Pcre = Void*
  fun compile = pcre_compile(pattern : UInt8*, options : Int, errptr : UInt8**, erroffset : Int*, tableptr : Void*) : Pcre
end
```

这里我们用对应的类型绑定 `libpcre` 编译函数，就能在 Crystal 代码中轻松地访问这个函数了。

```crystal
LibPCRE.compile(..)
```
