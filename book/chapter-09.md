\newpage

# 宏和元编程

我们喜欢 ruby 是因为他的动态性和元编程，可是和 ruby 不一样的是,crystal 是一种编译语言，这就导致了他们之间有一些关键性的区别:

- 没有 `eval`.
- 没有 `send`.

在 crystal 中,我们使用 macro 来获得上述两个行为和元编程,你可以把 macro 当做修饰代码的代码。P.S.编译期间 macro 被扩展成了代码.看这个:

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

在这个例子中，我们创建了一个 macro 名叫 define_method.我们只是把 macro 称为一个普通的方法。然后 macro 就会被扩展成：

```ruby
  def foo
    1
  end
```

酷！我们居然在编译期间得到了 eval 行为。
Macro 很强大，但是有一条规则你不能打破:

***一个 macro 应该被扩展到一个合法的 crystal 项目中。***
