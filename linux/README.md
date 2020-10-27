## Shell相关
显示二进制文件导致屏幕乱码，可以输入`tput sgr0`恢复。
测试屏幕乱码：`echo -e '\xe'`，恢复也可以使用：`echo -e '\xf'`。  
- 数据输入时，除了使用回车键结束输入外，也可以使用ctrl+d。不同之处在于，回车键会附加\n数据，ctrl+d不会。

## X
系统安装时，如果没有装X，后续可以使用如下方式：
```
apt-get install gnome
systemctl set-default graphical.target
init 5
```

### vncserver
重启指令：`systemctl restart vncserver@:1.service`

## KVM
virsh用于管理虚拟机，destroy用于强制重启。

## GCC
64位系统通过-m32编译32位应用，安装以下库：
```
apt-get install gcc-multilib g++-multilib module-assistant
```

## VI
常用配置（~/vimrc）：
```
set nocompatible
set backspace=indent,eol,start
set ai
set tabstop=4
set encoding=utf-8
```
进入16进制编辑模式：`%!xxd`，恢复使用：`%!xxd -r`，保存修改需要恢复后再保存。<br>
将4个空格替换为制表符：`:%s/\s\s\s\s/\t/g`

## PROC FS
进程号与/proc下的目录对应，其中文件用途：
|文件名|用途|
|----|----|
|cmdline|启动该进程的命令行|
|CWD|当前工作目录的符号链接|

进程地址空间  
1. 代码段(text)：代码段也称正文段或文本段，通常属于只读，用于存放程序执行代码(即CPU执行的机器指令)。
2. 数据段(Data)：通常用于存放程序中已初始化且初值不为0的全局变量和静态局部变量。数据段属于静态内存分配(静态存储区)，可读可写。
3. BSS段(Block Started by Symbol)：
- 未初始化的全局变量和静态局部变量
- 初始值为0的全局变量和静态局部变量(依赖于编译器实现)
- 未定义且初值不为0的符号(该初值即common block的大小)

## FIND
### 时间参数
linux文件状态有三个时间参数：atime、mtime、ctime，可以使用stat命令进行查看<br>
- atime: 最近一次访问文件的时间，显示一个文件的内容或者运行一个shell脚本会更新文件的atime。可用ls -lu命令查看。kernel版本2.6.30之前，linux的核心开发人员针对Ext3/Ext4文件系统的性能进行了讨论，其中包括atime。在kernel 2.6.30之前，文件系统中默认会及时更新atime，而在此之后的版本里，只有发生以下三种情况之一才会更新atime
  - 将分区mount的挂载的时候指定采用非relatime方式
  - atime小于ctime或者小于mtime的时候
  - 本次的access time和上次的atime超过24个小时
- mtime: 代表最近一次文件内容被修改的时间。可用ls -l 命令查看。
- ctime: 代表最近一次文件状态改变的时间 ,是status change time，是在写入文件、更改所有者、权限或链接设置时随Inode的内容更改而更改，即文件状态最后一次被改变的时间。可用ls -lc 命令查看。<br>

以-mtime举例说明：<br>

| 参数 | 含义 |
| -------- | ---------------------------------------------------- |
| -mtime n | n为数字，意思为在n天之前的一天之内被更改过内容的文件 |
| -mtime +n | 列出在n天之前（不含n天本身）被更改过内容的文件名     |
| -mtime -n | 列出在n天之内（含n天本身）被更改过内容的文件名       |

### 改名
根据inode查找修改（6417为通过ls -li看到的inode号）：`find . -inum 6417 -exec mv {} 1.rar \;`<br>

### 命令执行
通过find根据inode来删除文件：
```
find . -inum 264744 -exec rm -i  {} \;
```

### 查找suid、guid
- suid: `find . -perm /4000 -print`
- sgid: `find . -perm /2000 -print`

## CONVERT
图形转换命令，修改为400*600，不按原比例缩放的命令行格式：
```
convert -resize 400x600! img_8398.jpg hj.jpg
```
