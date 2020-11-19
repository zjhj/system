## GPG

### gpg & github
- gpg只能用于提交使用
- gpg --gen-key，用于生成GPG KEY，注意邮箱需要和github注册邮箱一致
- gpg --armor --export KEY_ID，输出公钥添加到github的gpg key
- gpg -k，可以获得KEY_ID
- git config --global user.signingkey KEY_ID
- git config --global commit.gpgsign true，设置默认使用gpg签名提交
- 但操作后，仍然没有verified标记，什么情况？

### gpg more 
