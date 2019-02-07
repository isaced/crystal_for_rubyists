\newpage

# 安装 Crystal


二进制安装程序
-----------------

Crystal 官方提供二进制安装程序，你可以获取 releases 和 nightlies 两个版本，二进制安装程序是最快最简单的安装 Crystal 的方法，因为 Crystal 是用 Crystal 编写，所以编译 Crystal 编译器实际需要编译 3 次！这样会很慢，但二进制安装程序将会很快的。

Crystal 有一个优美的 [安装页面](http://crystal-lang.org/docs/installation/index.html),
我建议你去看一下下载正确的版本。

请注意，本书已经使用 Crystal 0.12.0 进行了测试，如果您使用 nightly 最新版本，可能会有一些差异。

源码安装
-----------

如果从源代码构建，您可能会构建 nightly 版本，因此请准备好迎接代码示例中的一些错误，本书所用版本为 0.10.0。

[Crystal README](http://crystal-lang.org/docs/installation/from_source_repository.html) 有很好的源码构建说明，只需要跟着文档就好。

### 未来

本书编写时的版本是 0.12.0，虽然语言本身非常稳定，但标准库和一些主要子系统不停在修改中，我将在每个新版本中微调它。

如果你执行

    $ crystal

它会输出一堆帮助信息，恭喜你已拥抱 Crystal。
