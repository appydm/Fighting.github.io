title: Tail命令
author: Fighting
tags:
  - linux
  - shell
  - tail
categories:
  - linux
date: 2018-01-12 09:48:00
---
### 简介

tail命令用于输入文件中的尾部内容。tail命令默认在屏幕上显示指定文件的末尾10行。如果给定的文件不止一个，则在显示的每个文件前面加一个文件名标题。如果没有指定文件或者文件名为“-”，则读取标准输入。

注意：如果表示字节或行数的N值之前有一个”+”号，则从文件开头的第N项开始显示，而不是显示文件的最后N项。N值后面可以有后缀：b表示512，k表示1024，m表示1 048576(1M)。

### 参数说明

```shell
--retry：即是在tail命令启动时，文件不可访问或者文件稍后变得不可访问，都始终尝试打开文件。使用此选项时需要与选项“——follow=name”连用；
-c<N>或——bytes=<N>：输出文件尾部的N（N为整数）个字节内容；
-f<name/descriptor>或；--follow<nameldescript>：显示文件最新追加的内容。“name”表示以文件名的方式监视文件的变化。“-f”与“-fdescriptor”等效；
-F：与选项“-follow=name”和“--retry"连用时功能相同；
-n<N>或——line=<N>：输出文件的尾部N（N位数字）行内容。
--pid=<进程号>：与“-f”选项连用，当指定的进程号的进程终止后，自动退出tail命令；
-q或——quiet或——silent：当有多个文件参数时，不输出各个文件名；
-s<秒数>或——sleep-interal=<秒数>：与“-f”选项连用，指定监视文件变化时间隔的秒数；
-v或——verbose：当有多个文件参数时，总是输出各个文件名；
--help：显示指令的帮助信息；
--version：显示指令的版本信息。
```

<!--more-->

### 示例

#### 显示文件末尾内容

```shell
$ tail -n 5 log2014.log
```

#### 循环查看文件内容

```shell
$ tail -f test.log
```

#### 从第5行开始显示文件

```shell
$ tail -n +5 log2014.log
```