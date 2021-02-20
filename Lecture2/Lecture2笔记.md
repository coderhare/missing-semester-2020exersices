# shell中写脚本

ps:这节课的内容挺多的。

在shell中，可以编写脚本，可以像高级语言一样写变量，循环，流程控制语句，如 `if`， `case`， `while`等

可赋值变量，如 `foo=bar`

注意 `‘’`和 `""`的区别，类似于Python的单引号和双引号字符串

`ls *.xx`意为查找当前目录下.xx后缀的文件

如`ls *.s`为查找.s后缀的

### **本节中提到的一些$用法：**

- `$?` 获取上条命令的错误代码（返回值）
- `$_`获取上条命令的最后一个参数
- `$1`到 `$9`为脚本的参数，`$1`是第一个，以此类推
- `$(pwd)`获取当前目录
- `$(date)`获取当前日期
- `$0`获取该文件名
- `$#`获取该脚本的参数个数
- `$$`获取当前进程的PID
- `$@`获取脚本的所有参数

使用echo输出的例子：

`!!`(bangbang)会将上条命令显示在命令行

[![img](https://github.com/coderhare/missing-semester-2020exersices/raw/main/images/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-02-18%20%E4%B8%8B%E5%8D%8811.19.53.png)](https://github.com/coderhare/missing-semester-2020exersices/blob/main/images/屏幕快照 2021-02-18 下午11.19.53.png)



**在shell中可做逻辑运算,同样遵循「短路连通」的规则**

比如说，

```shell
true && echo "hello world"
```

第一个参数为true，所以会执行第二条命令

```shell
false; echo "hello world"
```

分号的作用使得两条命令独立，因此不影响后面的命令执行

`<(命令)` 如 `cat <(ls) <(ls ..)` 会执行括号内部的命令，然后输出存储到一个临时文件中，文件的标识符交给左边的命令，在这里，整个命令完成了当前目录产生文件与其父目录产生文件连接的功能

`shellcheck`可用于bash, sh,ksh,dash等，不支持zsh,使用方法和下载在GitHub[这里](https://github.com/koalaman/shellcheck)可找到

`-R`递归，如 `ls -R`递归列出目录结构

命令一般通过 `STDOUT`返回输出，错误通过 `STDERR`返回，使用返回码和退出状态来报告执行的情况，值为0意为着无错误，不为0的数字分别代表不同的错误。

```bash
echo "Starting program at $(date)" # 打印日期

echo "Running program $0 with $# arguments with pid $$"

for file in "$@"; do
    grep foobar "$file" > /dev/null 2> /dev/null
    # 如果模式不匹配，grep的退出状态为1
    # 重定向STDOUT 和STDERR 到一个”黑洞“，因为不需要使用，这些信息不会被找到
    if [[ $? -ne 0 ]]; then
        echo "File $file does not have any foobar, adding one"
        echo "# foobar" >> "$file"
    fi
done
```

这个脚本的逻辑还是好懂的，其中 `if A;B xx fi`意为如果A，执行B， `fi`限定作用域

若一个目录下有 `foo`， `foo1`， `foo2`，`foo10`，`bar` ，执行 `rm foo?`将删除 `foo1`和 `foo2`，而执行 `foo*`将删除这堆文件中除 `bar`的所有文件。

`{}`的用法：{}是字符串扩展替换的一个命令，可做笛卡尔积，用法为 `{...}/{...}`，下面举例

```bash
# 将创建文件foo/a, foo/b, ... foo/h, bar/a, bar/b, ... bar/h
touch {foo,bar}/{a..h}
convert image.{png, jpg} #将扩展为convert image.png image.jpg
```



## 查找文件

**`find`命令用法视参数不同产生组合较多：**

```shell
#course中提到的例子
find . -mtime -1 //mtime为modify time，修改时间， 此处参数为1即一天
find . -name src -type d //.表示当前目录,即为当前目录下使用find; name，type为查找的参数
find . -path '**/test/*.py' -type f //**表示0及以上个目录，语句的功能为查找test目录下的py文件
find . -name "*.tmp" -exec rm {} \;  //找到符合条件的文件后执行rm命令，分号标志结束

#可install fd，功能类似find，默认使用正则表达式
```

`locate XX`会查找文件系统中具有指定子串的路径，由于是通过数据库的索引查找，效率很高

## 查找内容

按照正则表达式的模式匹配来寻找含某些代码段的文件

```shell
#ack, acg, 可作为grep的替换方案
#grep的用法很多，下面举一些例子
grep foobar mcd.sh    #用于查找mcd.sh中内容中含foobar的行
rg -u --file--without-match "^#\!" -t sh #寻找文件中缺少#! 的sh文件
rg -t py 'import request' #寻找文件中含 "import request"的py文件
```

## 查找命令行

`history` 命令可以显示历史使用的命令,可结合使用 `Ctrl + R`来倒序搜索，比如说 `history | grep find`可以达到寻找历史命令行中含 `find` 的命令

`fzf`是一个模糊搜索的工具，用法较麻烦

如果你是在 `zsh`的环境下，可以安装 `oh-my-zsh`,上面有不少有用的插件可以安装

## 提到的一些有用的工具：

以下为macos的安装方式，不同系统可按实际情况对号入座，可按个人需求下

```shell
brew install tldr #给出不同工具的例子，可视为man的精简版,可减少命令的学习成本
brew install tree #以树形结构显示出目录结构
brew install broot #类似上面的tree，匹配做得可能更好用些
brew install nnn   #文件管理器
brew install ranger #文件管理器
```

