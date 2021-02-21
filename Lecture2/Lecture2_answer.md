## 1.  `ls`命令的一些操作：

- `ls -a`显示所有文件
- `ls -lh`将尺寸以可读的格式显示
- `ls -ltr`将文件按修改时间排序显示
- `ls`默认单色，如需彩色显示需要可修改 `~/`目录下的 `.bash_profile` 和 `.bashrc`文件，在第一个文件中添加 `if [ -f "$HOME/.bashrc" ];then . "$HOME/.bashrc" fi`，再在 `.bashrc`中添加 `alias ls='ls --color'`

## 2. 编写要求的macro函数和polo函数

注：由于笔者使用zsh，不同shell的同学可以改一下#!

```shell
#!/bin/zsh
   macro(){
   		 MACRO=$(pwd)
       echo "Now: $(pwd)"
   }
   macro
```



```shell
#!/bin/zsh
#polo function
polo() {
       echo "Before: $(pwd)"
       cd $MACRO
       echo "Now: $(pwd)"
   }
   polo
```

注意，正常情况下使用 `./xx.sh` 和 `sh xx.sh`如其中包含 `cd`命令，则执行时产生一个子shell去执行脚本，并不会对原来的终端产生影响，因此可使用 `source xx.sh`来使子shell不产生。



## 3.测试一条很少出错的命令

```shell
#! /bin/usr/env zsh

 	cnt=0

  until [["$?" -ne 0]]; do cnt=$((cnt+1)) ./exp2_3.sh &> out.txt 
  	done

    echo "found error fater runs"

    cat out.txt
#参考了课程的题解   
```

## 4.在 `find`的 `-exec`命令找到的文件全都打包成zip文件

```bash
find . -name "*.sh" -exec zip compressed.zip {} \;
```

## 5. write a command that recursively finds all HTML files in the folder and makes a zip with them

注： `xargs`使我们的命令将标准输入作为参数

```bash
find . -type f -name "*.html" | xargs -d '\n' tar -cvzf archive.tar.gz
```

## 6.(Advanced) Write a command or script to recursively find the most recently modified file in a directory. More generally, can you list all files by recency?

