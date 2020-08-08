## 编译开关
-v：查看默认的开关情况，如有--enable-default-pie则代表PIE已默认开启，可通过编译时添加-no-pie关闭。<br>
-fno-stack-protector：不开启堆栈溢出保护，即不生成canary<br>
-static：使用静态链接。<br>
-Wall：打开所有告警信息的开关？包括：-Waddress、-Warray-bounds=1 (only with ‘-O2’)等等，具体参考gcc的手册64页（version:8.3.0）。<br>
### pthread相关
编译时涉及pthread相关，由于pthread非linux默认，需使用-lpthread参数进行编译。
