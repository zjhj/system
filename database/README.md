## Mariadb
### 常用操作
创建用户：`create user 'nms'@'localhost' identified by 'xxxxxxxx';`
用户授权：`grant all on nms.* to nms@localhost;`
修改密码：`SET PASSWORD FOR 'username'@'host' = PASSWORD('newpassword');`
刷新操作：`flush privileges;`
