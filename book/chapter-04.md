\newpage

# 创建一个新项目

到目前为止，我们只使用 `crystal` 命令来运行我们的代码。

实际上 `crystal` 命令非常有用而且可以干更多事情。(查看 `crystal --help` 阅读更多)

For example we can use it to create a new Crystal project.

    $ crystal init app sample
      create  sample/.gitignore
      create  sample/LICENSE
      create  sample/README.md
      create  sample/.travis.yml
      create  sample/shard.yml
      create  sample/src/sample.cr
      create  sample/src/sample/version.cr
      create  sample/spec/spec_helper.cr
      create  sample/spec/sample_spec.cr
    Initialized empty Git repository in /Users/serdar/crystal_for_rubyists/code/04/sample/.git/

哎哟不错哦，`crystal` 帮我们创建了一个新的项目，让我们看看它为我们具体做了什么。

  - 创建一个名为 sample 的新文件夹
  - 创建 LICENSE 许可
  - 创建 `.travis.yml` 让我们轻松支持 Travis 持续集成
  - 创建 `shard.yml` 用于依赖管理
  - 初始化新的 Git 仓库
  - 创建 README 自述文件
  - 创建 `src` 和 `spec` 文件夹用于存放源代码和测试代码 （我们很快将会提到）

让我们运行起来吧。

    $ cd sample
    $ crystal src/sample.cr

啥都没有! Yay :)

现在我们创建了我们的第一个 Crystal 项目，接下来我们来使用一些外部库。

## 使用 Shards 依赖管理

我们使用 `shards` 来进行项目依赖管理，`shards` 就像 `bundler`，`shard.yml` 就像 `Gemfile`。

我们打开 `shard.yml`.

```yaml
name: sample
version: 0.1.0

authors:
  - sdogruyol <dogruyolserdar@gmail.com>

license: MIT
```

这是默认的 `shard.yml` 文件，其中包含了描述一个项目最基本的信息，比如：

- `name` 指定项目名称
- `version` 指定项目版本，Crystal 本身采用 [semver](http://semver.org/) 版本号规约，所以我们最好也这样。
- `authors` 项目作者，默认会读取你电脑上 Git 全局配置的用户名。
- `license` 指定项目的开源许可证类型，默认是 `MIT`

这很好，但我们能用 `shard.yml` 做什么呢？我们可以使用这个文件添加外部库（也称为依赖）并管理它们，甚至不用担心任何文件夹路径什么的，是不是很方便？

现在我们知道 `shards` 真正的能力， 让我们添加 [Kemal](https://github.com/sdogruyol/kemal) 到 `shard.yml` 文件来构建一个简单的 Web 应用程序吧 :)

打开 `shard.yml`. 首先我们需要添加 `Kemal` 作为项目依赖项，像这样：

```yaml
dependencies:
  kemal:
    github: kemalcr/kemal
    version: 0.17.2
```

好，现在添加 `Kemal` 到我们项目，首先得安装它。

    $ shards install
    Updating https://github.com/kemalcr/kemal.git
    Updating https://github.com/luislavena/radix.git
    Updating https://github.com/jeromegn/kilt.git
    Installing kemal (0.17.2)
    Installing radix (0.3.5)
    Installing kilt (0.3.3)

好了，现在我们的项目中已经集成了 `Kemal`，然后打开 `src/sample.cr` 文件

```ruby
require "./sample/*"
require "kemal"

module Sample

  get "/" do
    "Hello World!"
  end

end

Kemal.run
```

看看我们怎么使用 `require` 在应用中访问 `Kemal`。

运行起来

    $ crystal src/sample.cr
    [development] Kemal is ready to lead at http://0.0.0.0:3000

打开 `localhost:3000` 可以看到它已经跑起来了

现在你知道如何添加依赖并使用别人的 `shard` 了 :)
