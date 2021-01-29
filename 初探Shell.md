# 初探shell

> **Shell**（也称为**壳层**）在[计算机科学](https://zh.wikipedia.org/wiki/電腦科學)中指“为用户提供用户界面”的软件，通常指的是[命令行界面](https://zh.wikipedia.org/wiki/命令行界面)的解析器。一般来说，这个词是指[操作系统](https://zh.wikipedia.org/wiki/作業系統)中提供访问[内核](https://zh.wikipedia.org/wiki/内核)所提供之服务的程序。Shell也用于泛指所有为用户提供操作界面的程序，也就是程序和用户[交互](https://zh.wikipedia.org/w/index.php?title=交互&action=edit&redlink=1)的层面。因此与之相对的是[内核](https://zh.wikipedia.org/wiki/内核)（英语：**Kernel**），内核不提供和用户的交互功能。                                                                  --wiki关于shell的词条

Linux和macOS下可使用自带的终端，我的macOS是mojave系统，默认使用bash，后面的版本已改为zsh

zsh下安装oh my zsh可达到配置不同主题，自动补全等效果，此外还有不少别的插件，使使用体验更加流畅，可以尝试。（不是必选项

切换命令

```shell
 chsh -s /bin/zsh
```

更换为bash同理，此为本人所选主题ys

![屏幕快照 2021-01-29 下午3.14.07](/Users/wocaibujiaoquanmei/Desktop/屏幕快照 2021-01-29 下午3.14.07.png)

第一节没什么内容，主要讲了一些命令的用法

**echo是一个功能比较丰富的命令**

用法为

```shell
echo 文本
```

比如说类似exercises里头的用法

![image-20210129153346868](/Users/wocaibujiaoquanmei/Library/Application Support/typora-user-images/image-20210129153346868.png)

注意要区别「绝对路径」和「相对路径」的概念，「绝对路径」强调“唯一，完整”，可以用 `pwd`来显示；「相对路径」强调相对于当前位置。

Linux/macOS的文件系统和Windows的不一样，简单地理解是，Linux拥有一个顶级目录结构，且是唯一的，路径以斜线开头；而Windows采取分区的方式存放目录，每个分区都有一个根（root）。

**一些提到的命令：基本上都是缩写，如cd意为change directory**

`which 文本`用于查找文本，并返回其绝对路径；

`cd 文本`， 用于切换目录，其中 `cd ~`可以回到home目录， `cd -`是回到上一个所在的目录；

`ls`用于显示指定目录下的内容；

`mv a b`可用来移动文件或将文件改名，接受两个参数；

`cp a b`可用于复制文件，接受两个参数为路径；

`rm `用于移除文件，在Linux上默认不是递归的；

`mkdir`用于创建目录；

`rmdir`用于移除目录；

`man`用于查阅相关手册；

`< file ` 用于将文件的内容作为程序输入；

`> file`

`> file` 用于将程序输出作为文件的内容；

`>> file` 与 `> file` 的区别在于，前者是附加，后者是覆盖；

`cat`用于连接文件并打印到标准输出设备；

`|` pipe运算符，意为管道，用于将一个程序输出作为另一个程序输入；

`find`用于查找给定目录下的符合给定条件的文件；

`open`用于打开指定的文件，会选择默认的打开方式；

除此之外，上述部分命令还可以提供参数，以及种类丰富的命令，可到网上查询或查阅相关书籍。



对于某些操作，我们可能缺少权限，在Linux下，有一个顶级管理员root，可以通过 `sudo su` 来切换为root，`sudo`命令使我们能够达到“为所欲为”的效果。比如说course中提到的 `echo 1060 | sudo tee brightness` 达到了修改brightness的效果。

第一节课没什么内容，细节的东西建议查阅相关资料。
