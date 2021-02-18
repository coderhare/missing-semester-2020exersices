

ps:这节课的内容挺多的。



在shell中，可以编写脚本，可以像高级语言一样写变量，循环，流程控制语句

可赋值变量，如 `foo=bar`

注意 `‘’`和 `""`的区别，类似于Python的单引号和双引号字符串

`ls *.xx`意为查找当前目录下.xx后缀的文件

如`ls *.s`为查找.s后缀的 

**本节中提到的一些$用法：**

- `$?` 获取上条命令的错误代码（返回值）

- `$_`获取上条命令的最后一个参数
- `$(pwd)`获取当前目录
- `$(date)`获取当前日期
- `$0`获取该文件名
- `$#`获取该脚本的参数个数
- `$$`获取当前进程的PID
- `$@`获取脚本的所有参数

使用echo输出的例子：



`!!`(bangbang)会将上条命令显示在命令行



在shell中可做逻辑运算,同样遵循「短路连通」的规则

比如说，

```shell
true && echo "hello world"
```

 第一个参数为true，所以会执行第二条命令

```shell
false; echo "hello world"
```

 分号的作用使得两条命令独立，因此不影响后面的命令执行

`<(命令)`  如 `cat <(ls) <(ls ..)` 会执行括号内部的命令，然后输出存储到一个临时文件中，文件的标识符交给左边的命令，在这里，整个命令完成了当前目录产生文件与其父目录产生文件连接的功能



`shellcheck`可用于bash, sh,ksh,dash等，不支持zsh,使用方法和下载在GitHub[这里](https://github.com/koalaman/shellcheck)可找到



`-R`递归，如 `ls -R`递归列出目录结构



**`find`命令用法视参数不同产生组合较多：**

```shell
//course中提到的例子
find . -mtime -1 //mtime为modify time，修改时间， 此处参数为1即一天
find . -name src -type d //.表示当前目录,即为当前目录下使用find; name，type为查找的参数
find . -path '**/test/*.py' -type f //**表示0及以上个目录，语句的功能为查找test目录下的py文件
find . -name "*.tmp" -exec rm {} \;  //找到符合条件的文件后执行rm命令，分号标志结束

//可install fd，功能类似find，默认使用正则表达式
```

`locate XX`会查找文件系统中具有指定子串的路径，由于是通过数据库的索引查找，效率很高

**与正则表达式有关的一些命令：**

```shell
//ack, acg, 可作为grep的替换
grep foobar mcd.sh    //用于查找mcd.sh中内容中含foobar的行
rg -u --file--without-match "^#\!" -t sh //寻找文件中缺少#! 的sh文件
```

`history` 命令可以显示历史使用的命令,可结合使用 `Ctrl + R`来倒序搜索

`fzf`是一个模糊搜索的工具，用法较麻烦

**提到的一些有用的工具：**

以下为macos的安装方式，不同系统可按实际情况对号入座

```bash
brew install tldr //给出不同工具的例子，可视为man的精简版,可减少命令的学习成本
brew install tree //以树形结构显示出目录结构
brew install broot //类似上面的tree，匹配做得可能更好用些
```

