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
