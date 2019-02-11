\newpage

# 类型与方法重载

Crystal 和 Ruby 很像，但它不是 Ruby。

Crystal 是一种静态数据类型并且需要编译的语言。大多数时候，你不用指定数据类型。因为编译器足够智能可以进行`类型推断`。

好，既然这样，那么我们为什么需要数据类型呢？让我们从下面的例子开始:

```ruby
def add(x, y)
  x + y
end

add 3, 5 # 8
```

上面的这些在 Ruby 中是一样的，我们只是定义了一个让两个数字求和的方法，要是我们试着求和一个数字和字符串呢？

```ruby
add 3, "Serdar"
```

先让我们在 Ruby 里面试一试

```ruby
types.cr:2:in `+': String can't be coerced into Fixnum (TypeError)
	from types.cr:2:in `add'
	from types.cr:5:in `<main>'
```

得到了一个 `TypeError`，但是我们不用在 Ruby 中关心类型啊，其实这是一个`运行时错误`，意味着你的程序会在运行期间崩溃。

然后我们在 Crystal 里面试一试

    Error in ./types.cr:5: instantiating 'add(Int32, String)'

    add 3, "Serdar"
    ^~~

    in ./types.cr:2: no overload matches 'Int32#+' with types String
    Overloads are:
    - Int32#+(other : Int8)
    - Int32#+(other : Int16)
    - Int32#+(other : Int32)
    - Int32#+(other : Int64)
    - Int32#+(other : UInt8)
    - Int32#+(other : UInt16)
    - Int32#+(other : UInt32)
    - Int32#+(other : UInt64)
    - Int32#+(other : Float32)
    - Int32#+(other : Float64)
    - Int32#+()

    x + y
      ^

上面的输出语句看起来挺吓人的，不过实际上它们很强大，我们的 Crystal 虽然没有编译但仍然告诉我们 Crystal 里没有对 `Int32#+`方法重载，并且向我们展示了其他可能的重载类型，Crystal 的这种机制就相当于我们常说的 `编译时错误`，意味着我们的代码没有编译成功，并且在程序运行之前就捕捉到了错误。

现在让我们添加一些数据类型并且在方法中限制成 `Number` 类型.

```ruby
def add(x : Number, y : Number)
  x + y
end

puts add 3, "Serdar"
```

运行

    Error in ./types.cr:5: no overload matches 'add' with types Int32, String
    Overloads are:
    - add(x : Number, y : Number)

    puts add 3, "Serdar"
         ^~~

太棒了，我们的程序又一次没能编译成功，但这次的错误输出更短和更准确。我们只是在 `x` 和 `y` 中使用了类型限制。Crystal 就已经聪明到它可以阻止我们使用带`字符串`的方法。

## 方法重载

我们刚才看到了一些重载，现在让我们谈谈方法重载，方法重载就是在一些方法之间出现的一个现象，虽然他们可以拥有相同方法名称，但是他们的参数的数量却不同。所以这些方法实际上是不同的，让我们重载我们的 `add` 方法，让他变成可以接受一个字符串。

```ruby
def add(x : Number, y : Number)
  x + y
end

def add(x: Number, y: String)
  x.to_s + y
end

puts add 3, 5

puts add 3, "Serdar"
```

运行起来

    $ crystal types.cr
    8
    3Serdar

以上就是实际操作中的方法重载，Crystal 能够分辨出我们所说的带有数字的方法和带有字符串的方法的区别，并且能够调用准确地调用他们，您可以根据需要定义多个重载方法。
