1. ssh简介

   - 英文名：Secure Shell（安全协议外壳）
   - 概述：ssh是专为远程登陆会话和其他网络服务提供安全性的协议
   - 默认端口：22，安全协议版本sshv2（sshv1有漏洞）
   - ssh服务端功能： ssh远程链接和sftp服务
   - 实际用途：远程安全连接linux服务器
2. 什么是ssh服务：SSH服务端是一个守护讲程，SSH服务端的进程名为sshd，负责实时监听远程SSH客户端的远程连接请求，并进行处理。ssh客户端包含ssh以及像scp(远程拷贝） slogin(远程登陆) sftp(安全FTP文件传输）等应用程序。
3. ssh的工作机制：本地的ssh客户端先发送一个连接请求到远程的ssh服务端，服务端检查连接的客户端发送的数据包和IP地址，如果确认合法，就会发送密钥给 SSH的客户端，此时，客户端本地再将密钥发回给服务端，自此连接建立。
4. SSH登陆方式
   - 用户名密码登陆
     - 当客户端发起ssh请求，服务器会把自己的公钥发送给用户；
     - 用户会根据服务器发来的公钥对密码进行加密；
     - 加密后的信息回传给服务器，服务器用自己的私钥解密，如果密码正确，则用户登录成功。
   - 基于密钥的登录
     - 将客户端的公钥拷贝到服务端；
     - 当客户端再次发送一个连接请求，包括ip、用户名；
     - 服务端得到客户端的请求后，会到authorized_keys中查找，如果有响应的IP和用户，就会随机生成一个字符串，例如：qwer；
     - 服务端将使用客户端拷贝过来的公钥进行加密，然后发送给客户端；
     - 得到服务端发来的消息后，客户端会使用私钥进行解密，然后将解密后的字符串发送给服务端；
     - 服务端接受到客户端发来的字符串后，跟之前的字符串进行对比，如果一致，就允许免密码登录。

1. ssh的配置文件：

   - 客户端配置文件：ssh_config
   - 服务器配置文件：sshd_config

   > 服务器推荐修改默认端口号

   | **命令参数**           | **参数说明**                                                 |
   | ---------------------- | ------------------------------------------------------------ |
   | Port                   | 指定sshd进程监听的端口号，默认为22.可以使用多条指令监听多个端口.默认将在本机的所有网络接口上监听，但是可以通过ListenAddress指走只在某个特定的接口上监听. |
   | AddressFamily          | 地址家族，any表示同时监听ipv4和ipv6地址                      |
   | ListenAddress          | 0.0.0.0 ==> 监听本机所有ipv4地址 ::  ==>监听本机所有ipv6地址 |
   | LoginGraceTime         | 2m  ==>限定用户认证时间为2min                                |
   | PermitRootLogin        | 是否允许root账户ssh登录.默认no.                              |
   | MaxAuthTries           | 指定每个连接最大允许的认证次数。默认值是 6                   |
   | MaxSessions            | 最大允许保持多少个连接。默认值是 10                          |
   | Protocol               | 2 ==> SSH版本选择。一代有漏洞故这里一般不考虑                |
   | PermitEmptyPasswords   | 是否允许密码为空的用户远程登录.默认为"no"                    |
   | PasswordAuthentication | 是否允许密码验证 默认 yes                                    |
   | PubkeyAuthentication   | 是否开启公钥验证 默认 yes                                    |
   | UseDNS                 | 指定定sshd是否应该对远程主机名进行反向解折，以检查此主机名是否与其IP地址真实对应.默认值为"yes”. |

2. ssh命令：

   - 查看ssh版本 ：```$ ssh -V```
   - 指定用户登陆：```$ ssh username@ip```
   - 指定端口登陆：```$ ssh -p port username@ip```
   - 远程主机1跳到远程主机2：```$ ssh -t remoteserver1 ssh remoteserver2```

3. scp命令：

   - 上传本地文件到服务器: ```scp /path/filename username@ip:/path/```
   - 上传本地文件夹到服务器: ```scp -r local_dir username@ip:remote_dir```
   - 从服务器下载文件:  ```scp username@ip:/path/filename /var/www/local_dir（本地目录）```
   - 从服务器下载文件夹: ```scp -r username@servername:/www/remote_dir/（远程目录） /www/local_dir（本地目录）```

4. sftp命令：

   - 查看服务器资源: ```ls```
   - 查看 本地资源: ```lls```
   - 切换服务器目录: ```cd```
   - 切换本地目录: ```lcd```
   - 上传: ```put /path/filename / path(远程目录)```
   - 下载: ```get /path/filename / path(本地目录)```
   - 文件上传下载带 -r