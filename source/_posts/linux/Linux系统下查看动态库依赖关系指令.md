title: Linux系统下查看动态库依赖关系指令（ldd）
author: Fighting
date: 2025-01-04 23:43:31
tags:
---
#### Linux系统下查看动态库依赖关系指令（ldd）
> LDD用来打印或者查看程序运行所需的共享库,常用来解决程序因缺少某个库文件而不能运行的一些问题。ldd不是一个可执行程序，而只是一个shell脚本。使用ldd可以很方便的查看库与库之间的依赖关系，存放路径等等；对于排查链接不到库的问题很有帮助；

**1、ldd命令全称**
ldd命令全称为list dynamic dependencies（列出动态依赖），是Linux下常用的命令之一。它可以用来显示一个可执行文件或者共享库（动态链接库）所依赖的共享库。

**2、ldd参数说明**
–help 获取指令帮助信息；
–version 打印指令版本号；
-d,–data-relocs 执行重定位和报告任何丢失的对象；
-r, --function-relocs 执行数据对象和函数的重定位，并且报告任何丢失的对象和函数；
-u, --unused 打印未使用的直接依赖；
-v, --verbose 详细信息模式，打印所有相关信息；

**3、简单示例**
![Example Image](/images/pasted-0.png)
```
ldd libffi.so.7
```
可以看到，libffi.so.7库需要依赖libc.so.6，而libc.so.6的位置在/lib/aarch64-linux-gnu/libc.so.6 ，它的开始位置是0x0000ffff9ee7a000

**4、查看缺少的依赖库**
如果当前的动态库因为缺少依赖库而无法链接，那么可以通过ldd查看缺少的依赖库。

![Example Image](/images/pasted-1.png)

结果中可以看出，yh_ofd2img_ARRACH_64.so库需要依赖libQt5PrintSupport.so.5，而yh_ofd2img_ARRACH_64.so却找不到，方便排查。

<!-- more -->

**5、ldd指令详细介绍**
1、ldd是Linux中的一个重要命令，用于打印可执行文件或共享库所依赖的动态链接库信息。下面详细介绍ldd指令的功能和用法。

命令格式： ldd [选项] <可执行文件或共享库>

2、功能描述： ldd命令显示一个可执行文件或共享库所依赖的动态链接库列表。它会递归地检查文件所依赖的所有库，并显示它们的路径。通过ldd命令可以了解一个程序运行所需的库文件，以及这些库文件是否存在、版本是否匹配等信息。

3、常用选项： -v, --verbose：显示详细的调试信息，包括版本号、加载方式等。 -u, --unused：只显示未使用的直接依赖库。 -r, --function-relocs：在关联库中显示函数的重定位信息。 -d, --data-relocs：在关联库中显示数据的重定位信息。 –help：显示帮助信息。 –version：显示版本信息。

4、使用示例： (1) 查看可执行文件所依赖的库： ldd /path/to/executable

(2) 查看共享库的依赖关系： ldd /path/to/shared_library.so

(3) 显示详细的依赖库信息： ldd -v /path/to/executable

(4) 只显示未使用的直接依赖库： ldd -u /path/to/executable

(5) 显示函数和数据的重定位信息： ldd -r /path/to/executable

5、输出解读： 对于每个所依赖的库，ldd会显示它的路径，并用以下格式标记其状态： => 文件路径：正常找到并链接。 => not found：未找到该库文件。 => version mismatch：版本不匹配。 => incompatible：与可执行文件或其他库不兼容。 => symbol not found：找不到某个符号。

另外，ldd命令还可以显示库所需的其他库。通过观察输出结果，在开发调试过程中可以及时了解和解决动态链接库的相关问题。

使用ldd命令可以帮助开发人员、系统管理员等快速了解程序运行所需的库文件是否存在、版本是否匹配，从而排查库依赖问题。在调试和部署过程中，ldd是一个非常有用的工具，能够提高开发效率和减少出错的可能性。