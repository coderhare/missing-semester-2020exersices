# answer



- **Shebang**： 以`#!` 开头，在开头字符之后，可以有一个或数个空白字符，后接解释器的「绝对路径」，用于调用解释器。

​	如 `#!/usr/bin/python`

​	Shebang允许脚本和数据文件充当系统命令，无需在调用时由用户指定解释器，从而对用户和其它程序隐藏其实现细节。

​	注意`#!`必须一起书写，否则将可能出现#作为注释符的情况

- **curl**命令：

**Example**：

简单模式：

```shell
$ curl http://example.com
```

详细（verbose）模式：

```shell
$ curl --verbose http://example.com
```

```shell
$ curl -v http://example.com
```

下载（output）：

```shell
$ curl --output output.html http://example.com/
```

```shell
$ curl -o output.html http://example.com/
```

[重定向](https://zh.wikipedia.org/wiki/重定向)：（curl默认不会[重定向](https://zh.wikipedia.org/wiki/重定向)）

```shell
$ curl --location output.html http://example.com/
```

```shell
$ curl -L output.html http://example.com/
```

参考自https://zh.wikipedia.org/wiki/CURL

- 直接执行./semester会提示 Permission Denied，因为缺少权限。可通过chmod a+rw semester 或 sh semester来获取权限

