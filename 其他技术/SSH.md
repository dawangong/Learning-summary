1. ssh简介

   - 英文名：Secure Shell（安全协议外壳）
   - 概述：ssh是专为远程登陆会话和其他网络服务提供安全性的协议
   - 默认端口：22，安全协议版本sshv2（sshv1有漏洞）
   - ssh服务端功能： ssh远程链接和sftp服务
   - 实际用途：远程安全连接linux服务器

2. 什么是ssh服务：SSH服务端是一个守护讲程，SSH服务端的进程名为sshd，负责实时监听远程SSH客户端的远程连接请求，并进行处理。ssh客户端包含ssh以及像scp(远程拷贝） slogin(远程登陆) sftp(安全FTP文件传输）等应用程序。

3. ssh的工作机制：本地的ssh客户端先发送一个连接请求到远程的ssh服务端，服务端检查连接的客户端发送的数据包和IP地址，如果确认合法，就会发送密钥给 SSH的客户端，此时，客户端本地再将密钥发回给服务端，自此连接建立。

4. ssh的配置文件：

   - 客户端配置文件：ssh_config
   - 服务器配置文件：sshd_config

   > 服务器推荐修改默认端口号

   | **命令参数**         | **参数说明**                                                 |
   | -------------------- | ------------------------------------------------------------ |
   | Port                 | 指定sshd进程监听的端口号，默认为22.可以使用多条指令监听多个端口.默认将在本机的所有网络接口上监听，但是可以通过ListenAddress指走只在某个特定的接口上监听. |
   | ListenAddress        | 指定监听并提供服务相应的网卡地址信息                         |
   | Protocol             | 2 —— SSH版本选择。一代有漏洞故这里一般不考虑                 |
   | UseDNS               | 指定定sshd是否应该对远程主机名进行反向解折，以检查此主机名是否与其IP地址真实对应.默认值为"yes”. |
   | PermitEmptyPasswords | 是否允许密码为空的用户远程登录.默认为"no"                    |

5. ssh命令：

   - 查看ssh版本 ：```$ ssh -V```
   - 指定用户登陆：```$ ssh username@ip```
   - 指定端口登陆：```$ ssh -p port username@ip```
   - 远程主机1跳到远程主机2：```$ ssh -t remoteserver1 ssh remoteserver2```

6. scp命令：

   - 上传本地文件到服务器: ```scp /path/filename username@ip:/path/```
   - 上传本地文件夹到服务器: ```scp -r local_dir username@ip:remote_dir```
   - 从服务器下载文件:  ```scp username@ip:/path/filename /var/www/local_dir（本地目录）```
   - 从服务器下载文件夹: ```scp -r username@servername:/www/remote_dir/（远程目录） /www/local_dir（本地目录）```

7. sftp命令：

   - 查看服务器资源: ```ls```
   - 查看 本地资源: ```lls```
   - 切换服务器目录: ```cd```
   - 切换本地目录: ```lcd```
   - 上传: ```put /path/filename / path(远程目录)```
   - 下载: ```get /path/filename / path(本地目录)```