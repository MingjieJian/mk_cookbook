# 不需要输入密码的SSH key

如果想不用密码登陆某主机的话，需要用到ssh key：

`ssh-keygen -t rsa -b 4096 -C "你的邮箱地址"`

在生成ssh key的时候不输入密码的话，即使之后将公钥复制到了远程主机(`ssh-copy-id -i .ssh/id_rsa.pub git@12.56.224.61 `)，ssh的hi和还是需要输入密码的。

这个时候将identity添加到私钥里就可以了：

`ssh-add -K ~/.ssh/id_rsa`

以上。

--0619追加：

上面的方法只能临时添加ssh-key，在bash窗口关闭了之后就没用了；所以一劳永逸的解决办法是先生成一个没有密码的密钥对，将公钥添加到远程主机，然后在本地编辑/创建`.ssh/config`文件如下：

```
Host server_name
  Hostname server.ip.address
  User server_user_name
  IdentityFile path/to/rsa/file
```

就可以了。这样做之后还能直接`ssh server_name`，简单省事。

参考：
http://martincl2.me/archives/937
https://vra.github.io/2017/07/09/ssh-config/
https://www.jianshu.com/p/6761199bedba
https://stackoverflow.com/questions/21095054/ssh-key-still-asking-for-password-and-passphrase
