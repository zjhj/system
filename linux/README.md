## X
系统安装时，如果没有装X，后续可以使用如下方式：
```
apt-get install gnome
systemctl set-default graphical.target
init 5
```

## GCC
64位系统通过-m32编译32位应用，安装以下库：
```
apt-get install gcc-multilib g++-multilib module-assistant
```

## VI
常用配置：
```
set nocompatible
set backspace=indent,eol,start
set ai
set tabstop=4
set encoding=utf-8
```

## PROC FS
进程号与/proc下的目录对应，其中文件用途：
|cmdline|启动该进程的命令行|
|----|----|
|CWD|当前工作目录的符号链接|
