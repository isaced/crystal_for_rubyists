\newpage

# 宏和元编程

我们喜欢 Ruby 是因为他的动态性和元编程，可是和 Ruby 不一样的是，Crystal 是一种编译型语言，这就导致了他们之间有一些关键性的差异：

- 没有 `eval`.
- 没有 `send`.

在 Crystal 中,我们使用宏 `Macro` 来获得上述两个行为和元编程，你可以把 `Macro` 当做编写/修改代码的代码。
P.S：编译期间 `Macro` 会被扩展成代码，看这个:

```ruby
macro define_method(name, content)
  def {{name}}
    {{content}}
  end
end

define_method foo, 1
# This generates:
#
#     def foo
#       1
#     end

foo # => 1
```

在这个例子中，我们创建了一个宏名叫 `define_method`，我们只时像一个普通方法一样调用一个宏。然后宏会被扩展成：

```ruby
  def foo
    1
  end
```

酷！我们居然在编译期间得到了 `eval` 能力。

宏 `Macro` 很强大，但是有一条规则你不能打破：

***一个宏 `Macro` 应该被扩展到一个有效的 Crystal 程序中。***
