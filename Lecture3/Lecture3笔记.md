## vim简介

> **Vim**是从[vi](https://zh.wikipedia.org/wiki/Vi)发展出来的一个[文本编辑器](https://zh.wikipedia.org/wiki/文本编辑器)。其代码补完、编译及错误跳转等方便编程的功能特别丰富，在程序员中被广泛使用。和[Emacs](https://zh.wikipedia.org/wiki/Emacs)并列成为[类Unix系统](https://zh.wikipedia.org/wiki/类Unix系统)用户最喜欢的编辑器。
>
> Vim的第一个版本由[布莱姆·米勒](https://zh.wikipedia.org/wiki/布萊姆·米勒)在1991年发布。最初的简称是**V**i **IM**itation，随着功能的不断增加，正式名称改成了**V**i **IM**proved。现在是在[开放源代码](https://zh.wikipedia.org/wiki/开放源代码)方式下发行的[自由软件](https://zh.wikipedia.org/wiki/自由软件)。

#### **vim的五种基本模式：**

- normal：不同于一般的文本编辑器，在普通模式下，主要进行移动光标和删除文本，拷贝粘贴文本等操作而非直接编辑文本

- insert：在此模式下进行文本编辑，就跟正常的打字情境一样。

- replace：用于替换文本

- visual：用于选择文本块

- command-line：使用命令行来进行操作

  ![vim基本模式切换](https://github.com/coderhare/missing-semester-2020exersices/blob/main/images/vim基本模式切换.jpeg)

## 模式的切换及使用

#### **普通模式（normal mode)下：**

- **运动命令**：如下表；可以通过加参数修改移动的距离，如 `20h`表示左移20格

| 按键     | 功能（移动光标）                      |
| -------- | ------------------------------------- |
| h        | 左移一格                              |
| l        | 右移一格                              |
| j        | 下移一格                              |
| k        | 上移一格                              |
| w        | 向前移动一个单词                      |
| b        | 向后移动一个单词                      |
| e        | 移动到下一个单词的末尾                |
| 0        | 移动到行首                            |
| $        | 移动到行尾                            |
| ^        | 移动到行的第一个非空字符              |
| gg       | 移动到文件首行                        |
| G        | 移动到文件末行                        |
| f + x    | 移动到当前光标后本行第一个为x的字符处 |
| F + x    | 移动到当前光标前本行第一个为x的字符处 |
| t + x    | 移动到当前光标后本行第一个为x的字符前 |
| T + x    | 移动到当前光标前本行第一个为x的字符后 |
| Ctrl + u | 向上回滚                              |
| Ctrl + d | 向下回滚                              |
| %        | 在匹配的括号两端横跳                  |

- **编辑：**

`c`命令和 `d`命令是类似的。 `y`命令为拷贝，`p`为粘贴。

| **按键**         | 功能                                     |
| ---------------- | ---------------------------------------- |
| u                | 撤销掉前一步更改，包括非普通模式下的更改 |
| de               | 删除单词的末尾                           |
| dw               | 删除单词                                 |
| ce               | 删除单词的末尾并进入插入模式             |
| dd               | 删除特定行                               |
| cc               | 删除特定行并进入插入模式                 |
| x                | 删除当前光标处字符                       |
| r + x            | 将当前光标处字符替换为x                  |
| ctrl + r         | reundo，将撤销的操作给撤销掉             |
| yw               | 拷贝单词                                 |
| yy               | 拷贝当前行                               |
| ~（波浪号）      | 将字符大小写转换                         |
| di + { 或 di + } | 删除括号内的内容                         |
| da               | 删除括号                                 |
| o                | 新建一行并进入插入模式                   |
| da'              | 删除 `’`之间的字符包括 `‘`               |



#### **插入模式（insert mode）下：**

默认情况下，我们通过按键 `i`进入插入模式，但是需要的话，也可以进行更精确的操作

| 按键 | 功能                         |
| ---- | ---------------------------- |
| a    | 在光标后面插入               |
| A    | 在当前光标所在行末尾插入     |
| i    | 从光标所在处插入             |
| I    | 在当前光标所在行首插入       |
| o    | 在当前行下面新建一行，并插入 |
| O    | 在当前行上面新建一行，并插入 |

#### 替换模式（replace mode）下：

主要进行替换文本的操作。



#### 可视模式（visual mode）下：

**进入visual mode可以进行绝大部分普通模式下的编辑**

- `v`进入基本的visual mode
- `V`进入 visual-line mode
- `Ctrl + v`进入visual-block mode



#### **命令行模式（command-line mode)下:**

- `w`保存文件
- `q`退出，不保存修改
- `q!`强制退出
- `qa`退出所有标签页
- `wq!`保存文件并强制退出
- `help xx`关于xx的帮助, 注意：`help :w`是关于 `:w`的帮助， `help w`是关于按键 `w`的帮助
- `line1, line2, d`删除从line1到line2的行之间的文本。
- `tabnew`创建一个新的标签页，`tabnew xx.file`创建xx.file的新的标签页；此外， `tabp`返回上一个标签页， `tabn`返回下一个标签页。
- `set nu`设置行号，建议在配置文件中修改一劳永逸（见下面

原视频中并没有展开介绍vim的标签页，vim的标签页对于使用vim的操作性而言是很有用的，如图为editors.md的两个标签页 ，使用`tabnew editors.md`

![屏幕快照 2021-02-27 下午3.02.11](https://github.com/coderhare/missing-semester-2020exersices/blob/main/images/vim%E4%BD%BF%E7%94%A8%E7%A4%BA%E4%BE%8B.png)



**注意，除了上述的几种基本模式之外，还有一些派生模式，参见[这里](https://zh.wikipedia.org/wiki/Vim)。**

## 一些配置

朴素的vim在我看来还是不太好用的，关于vim有不少有用的配置可以按个人喜好配置。

进入vim的配置文件，发现里面空荡荡的

```bash
vim ~/.vimrc
```

你可以按照网上的教程进行配置，推荐加入 `语法高亮` 和 `设置行号` 以及 `tab缩进`

```bash
"语法高亮.
syntax on
"行号.
set nu
"缩进.
set tabstop=4
set shiftwidth=4
set expandtab
set smarttab
```

[这里](https://missing.csail.mit.edu/2020/files/vimrc)是视频中的老师的vim配置。

关于vim的命令实在是很多，与之相比课程中涉及的都是非常基础的，使用vim对于本身语法存在问题的小白而言与IDE相比效率是不高的，要想使用效率高需要走可能颇为曲折的路线。
