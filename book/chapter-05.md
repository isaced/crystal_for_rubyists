\newpage

# 测试

Rubyists 喜欢测试，所以在我们走向远方之前，让我们先谈谈测试。Crystal 又一个内置的测试框架叫 `spec`，它和 `RSpec` 非常相似。

让我们继续第四章创建的项目

`crystal` 为我们创建了项目结构

    $ cd sample && tree
    -- LICENSE
    -- README.md
    -- shard.yml
    -- spec
      -- sample_spec.cr
      -- spec_helper.cr
    -- src
      -- sample
        -- version.cr
      -- sample.cr

看到 `spec` 这个目录了吗？ 是的 Crystal 为我们创建了这个文件夹和第一个 spec 测试文件。在 Crystal 里一个文件通过对应的 `_spec` 文件进行测试，因为我们项目的命名为 `sample`，对应创建了一个文件名为 `sample.cr` 和其 `spec/sample_spec.cr` 的 spec 测试文件。

还有一点，在这里 `spec` 和 `unit test` 是同样意思。

让我们打开 `spec/sample_spec.cr`

```ruby
require "./spec_helper"

describe Sample do
  # TODO: Write tests

  it "works" do
    false.should eq(true)
  end
end
```

现在这个文件非常有趣，有三个重要的关键字 `describe`、`it`、`should`。

这些关键字用于 `spec` 且有以下含义：

- `describe` 对 specs 进行归组
- `it` 在双引号间用于给 spec 一个标题定义.
- `should` 用于对 spec 作出假设

如你所见这个文件有一个 `describe` 组名为 `Sample`，`it` 给了一个标题为 `works`， which makes the
assumption that false `should` equal true.

你也许会问 “我们怎么运行这些测试？”，答案当然是 `crystal` 命令。

    $ crystal spec
    F

    Failures:

      1) Sample works
         Failure/Error: false.should eq(true)

           expected: true
                got: false

         # ./spec/sample_spec.cr:7

    Finished in 0.69 milliseconds
    1 examples, 1 failures, 0 errors, 0 pending

    Failed examples:

    crystal spec ./spec/sample_spec.cr:6 # Sample works

Yay! 我们的测试失败（红色）了，阅读输出我们可以很容易知道是哪个测试（spec）失败了，`Sample` 组里标题为 `works` 的测试，也就是 `Sample works`，好了让我们来让其通过。

```ruby
require "./spec_helper"

describe Sample do
  # TODO: Write tests

  it "works" do
    true.should eq(true)
  end
end
```

重新运行测试（spec）

    $ crystal spec

    .

    Finished in 0.63 milliseconds
    1 examples, 0 failures, 0 errors, 0 pending

绿色！这就是你开始前需要知道的全部内容，接下来下一章：FizzBuzz。
