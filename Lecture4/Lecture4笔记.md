# Lecture4: Data Wrangling

这节课的主题是数据处理。

介绍的东西不多，但都很实用，这类型的工具有很多，主要目的是指导我们可以“这样”处理数据。

## **本节主要涉及一些关于数据处理的工具**和命令

- `|`为pipe，可将一个进程的输出作为另一个进程的输入；在第一节中有提及

- `sed`，不同于 `vim`的命令行编辑模式，`sed`是流编辑模式。
- `uniq`用于处理重复数据，与 `sort`搭配使用
- `sort`主要用于排序文件内容，按行排序。
- `tail`用于显示指定的行到末位位置的内容，与之相对应的是 `head`。
- `awk`用于文本处理
- `paste`用于合并文件的列，与之相对应的是 `cut`，按指定的分隔符分成多列。
- `gnuplot`是一个命令式绘图程序；在示例中绘制了频数直方图
- `convert`，貌似是Linux下才有；用于格式转换
- `tee`读取标准输入的内容，并将其内容输出成文件；在第一节中有提及。用法为`tee [-ai][--help][--version][file]`
- `wc`计算文件中的某些数目，如 `wc -l`计算行数
- `bc`可做计算器使用

## 正则表达式

正则表达式的语法同样很多，但值得欣慰的是，它独立于语言，不同的编程语言使用基本相同的正则表达式语法；关于详细语法这里无法展开也没有能力展开，想了解更多可以参考[这里](https://www.regular-expressions.info)。

课程中包括 `sed`， `grep`和 `awk`均可使用正则表达式，它们本身的功能也不止于此。像 `sed`还可以对数据进行修改，删除等。

**一些常用的模式：**

- `.`表示除换行符外的所有字符
- `*`匹配前面的子表达式0次或多次
- `+`匹配前面的子表达式1次或多次
- `[A-Z]`匹配所有大写字母，同理 `[a-z]`匹配所有小写字母
- `^`行的开头，`$`行的末尾
- `(RX1|RX2)`与RX1或RX2相匹配的内容

**例子如下：**

```bash
cat test.txt | grep "aaa" # 匹配test.txt中含"aaa"子串的字符串
cat test.txt | grep '[A-Z]' #匹配test.txt中含字符'A~Z'的字符串

cat test.txt | awk {print $2} #以空格为分隔符，打印每一行第二个字段
```

习题中练习正则表达式的[网站](https://regexone.com/lesson/letters_and_digits?)，挺不错的，可以做一下。

## 排序与归类

`sort`是按每行从首字母开始，按照ASCII码值大小升序对行文本进行排序，并标准输出，下面是一些简单的参数选项：

| 参数 | -u         | -r   | -o                                           | -t<char>             | -k     | -n             |
| ---- | ---------- | ---- | -------------------------------------------- | -------------------- | ------ | -------------- |
| 效果 | 去除重复行 | 降序 | 将排序结果写入文件（因为sort输出是标准输出） | 指定排序时的分隔字符 | 指定域 | 按数值大小排序 |

`uniq`通常与 `sort`成双出现， `uniq`将使行中相同的文本只输出一次，下面是一些简单的参数选项：

| 参数 | -u             | -c             | -d           |
| ---- | -------------- | -------------- | ------------ |
| 效果 | 单独不重复的行 | 不重复行且计数 | 仅含重复的行 |

一些简单用法：

```bash
cat test.txt | sort -r | uniq -c   #将test.txt中的文本按行降序排序后去掉重复行打印输出，并计数重复出现的行文本数量
cat test.txt | sort | uniq -d #输出排序文件中重复的行一次
```



# 数据可视化

本节中采用`gnuplot`进行频数直方图绘制。

macOS下可命令行安装：

```bash
brew install gnuplot
```

参考教程中朴素的例子，

```bash
cat test.txt | sort | uniq -c| tail -n10 | awk '$1 != 8 {print $1}'| gnuplot -p -e 'set boxwidth 0.5; plot "-" using 1:xtic(2) with boxes'
```

效果如图

![](/Users/wocaibujiaoquanmei/Markdown/missing-semester-2020exercises/gnuplot使用示例.png)

但事实上， `gnuplot`能绘制多种函数的图像，用法也比较多。

## 格式转换

主要使用 `convert`，用法示例如下：

```bash
convert A.png A.jpg #将png文件转换为jpg文件
```

此外，`convert`还支持不同参数实现不同功能，如

```bash
convert -resize 50%x50% A.jpg B.jpg #按比例缩小为原来的1/4
convert -rotate 90 A.jpg B.jpg      #顺时针旋转90°
convert -monochrome A.jpg B.jpg			#将图片变为黑白
```

