# Lecture4:answer

**1. 点击[这里](https://regexone.com/)开始练习**

**2. Find the number of words (in `/usr/share/dict/words`) that contain at least three `a`s and don't have a `'s` ending. What are the three most common last two letters of those words? `sed`'s `y` command, or the `tr` program, may help you with case insensitivity. How many of those two-letter combinations are there? And for a challenge: which combinations do not occur?**

统计含至少三个`a`且不以 `'s`结尾的单词。

使用tr处理大小写问题，使用grep来指定模式，`wc -l`统计单词数目

```bash
cat /usr/share/dict/words | tr "[:upper:]" "[:lower:]" | grep ".*[a].*[a].*[a].*[^\'][^s]$" | wc -l
2830 #打印出的数字
```

打印后面两个字母出现次数最多的三个，在前面基础上先分好后两个字母，然后再用 `sort` 排序 `uniq -c` 计数

```bash
cat /usr/share/dict/words | tr "[:upper:]" "[:lower:]" | grep ".*[a].*[a].*[a].*[^\'][^s]$" | awk '{print substr($0, length()-1)}' | sort | uniq -c | sort | tail -n3

 256 te
 273 on
 286 ly     #后三个字母情况
```

**3. To do in-place substitution it is quite tempting to do something like `sed s/REGEX/SUBSTITUTION/ input.txt > input.txt`. However this is a bad idea, why? Is this particular to `sed`? Use `man sed` to find out how to accomplish this.**

**4.Find your average, median, and max system boot time over the last ten boots. Use `journalctl` on Linux and `log show` on macOS, and look for log timestamps near the beginning and end of each boot. **

`on macos` 

```bash
log show | grep -E 'Previous shutdown cause'                                                               
2021-03-05 08:18:11.685067+0800 0xb7       Default     0x0                  0      0    kernel: (AppleSMC) Previous shutdown caus: 5
2021-03-06 08:53:25.196930+0800 0xb7       Default     0x0                  0      0    kernel: (AppleSMC) Previous shutdown caus: 5
2021-03-07 08:17:28.183644+0800 0xb7       Default     0x0                  0      0    kernel: (AppleSMC) Previous shutdown caus: 5
```

