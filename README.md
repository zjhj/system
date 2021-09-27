# 操作系统及一些平台软件的备忘

## [linux相关](linux/)

## [windows相关](windows/)

## [数据库](database/)

## [Gcc](gcc/)

## GitHub
- 大文件提交出现异常情况（比如`remote: fatal error in commit_refs`），可以通过`git gc`解决（有说需要在前面加`git fsck`）
- 设置socks代理：`git config --global http.proxy socks5://10.0.2.2:12808`
- 查看配置信息：`git config --global -l`

## JRE
JNLP连接远程控制端时，出现网络连接中断的提示，有可能是安全配置问题，可以尝试修改JRE的lib\security目录下的java.security文件，屏蔽jdk.tls.disabledAlgorithms=SSLv3...的相关内容即可。

## Apache Httpd
###配置代理上网（windos作代理服务，类unix作客户端，适合内网机器更新软件等操作）
httpd修改httpd.conf，下面几个so前面的注释符去掉：
```
#LoadModule proxy_module modules/mod_proxy.so
#LoadModule proxy_connect_module modules/mod_proxy_connect.so
#LoadModule proxy_http_module modules/mod_proxy_http.so
#LoadModule proxy_ftp_module modules/mod_proxy_ftp.so
#LoadModule access_compat_module modules/mod_access_compat.so
```
尾部添加如下内容（白名单形式可以通过`Deny from all, Allow from xxxx/xx`的形式）：
```
ProxyRequests   On
<Proxy *>
    Order allow,deny
	Allow from all
# Deny from 10.10.10.0/24
</Proxy>
```
再修改前面的`Define SRVROOT`为httpd的安装目录，以及`Listen xx`的端口，启动即可。
