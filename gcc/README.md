## 编译开关
-v：查看默认的开关情况，如有--enable-default-pie则代表PIE已默认开启，可通过编译时添加-no-pie关闭。<br>
-fno-stack-protector：不开启堆栈溢出保护，即不生成canary<br>
-static：使用静态链接。<br>
