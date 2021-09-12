# system
os and some platforms

## netsh
### netsh实现端口转发（配置完毕重启生效）
- 端口转发指令：`netsh interface portproxy add v4tov4 listenaddress=localaddress listenport=localport connectaddress=destaddress connectport=destport`
- 涉及服务：IPHelper（一般已配置自动启动）、RemoteAccess
```
sc config RemoteAccess start=auto
sc start RemoteAccess
```
- 注册表相关：`reg add HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v IPEnableRouter /D 1 /f`

### 防火墙管理
- 启停：`netsh advfirewall set allprofiles state [on|off]` （旧版：`netsh firewall set opmode mode=[enable|disable]`）
- 允许or禁止ping：`netsh advfirewall firewall add rule name="ALL ICMP V4" dir=in action=[allow|block] protocol=icmpv4`
- 导入/导出配置：`netsh advfirewall [import|export] "c:\tmp\wfconf.wfw"`
- 新增/删除端口：`netsh advfirewall firewall [add|delete] rule name="XXXXXX" [dir=in action=allow] protocol=tcp localport=xxxx`
- 设置日志记录：`netsh firewall set currentprofile logging filename "c:\tmp\pfirewall.log"`
- 防火墙重置：`netsh advfirewall reset`
