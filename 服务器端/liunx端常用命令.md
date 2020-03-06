> 应用安装

centos

```bash
// 安装
yum install xxx 
// 更新
yum-update 			
```

ubuntu

```bash
// 安装
apt install xxx / apt-get install xxx 	
// 更新
apt update / apt-get update							
```

> liunx

文件基础操作

```bash
// 清屏
clear
// 查看文件
ls
// 查看所有文件
ls -a
// 查看文件详细
ls -l
// 切换目录
cd xxx
// 切换到根目录
cd /
// 切换到用户组目录
cd ~
// 删除文件
rm xxx
// 删除文件夹
rm -rf xxx
// 复制文件到目录
cp a b
// 复制文件夹到目录
cp -r a b
// 移动/重命名
mv a b
// 移动强覆盖
mv -f a b
// 当前工作目录
pwd
// 创建文件
touch xxx
// 创建文件夹
mkdir xxx
// 显示文件内容
cat xxx
编辑文件
// vi/vim xxx
```

进程

```bash
// 显示所有进程
ps
// 进程过滤
ps -ef | grep xxx
// 查询端口占用
lsof -i:xxxx
// 杀进程
kill pid
```

权限

```bash
// 提升至root权限
sudo xxx
// 切换root用户
su
// 切换root用户(并切换环境变量)
su -
// 开启文件/文件夹全部权限
chmod 777 xxx
// 添加执行权限
chomd -x xxx
```

其他

```bash
// 程序安装目录
which xxx
// 确定主机与外部连接状态
ping ip
// 查看网络配置 (ip地址 mac地址)
ifconfig
```

> nginx

```bash
// 配置文件位置
nginx -t
// 强制重启
nginx -s reopen
// 重新加载nginx配置文件，然后重启nginx(处理完所有请求后再停止服务)
nginx -s reload
// 强制停止nginx
nginx -s stop
// 停止Nginx服务(处理完所有请求后再停止服务)
nginx -s quit
// 显示版本
nginx -v
// 帮助
nginx -v
// 杀死所有nginx进程
killall nginx
```

> service管理nginx时

```bash
service nginx status | stop | start | restart
```

> pm2

```bash
// 启动应用
pm2 start xxx
// 启动四个应用实例(4个应用程序会自动进行负载均衡,cluster mode模式)
pm2 start xxx -i 4
// 当文件变化时自动重启应用
pm2 start xxx --watch
// pm2启动的应用列表
pm2 list 
// 显示每个应用程序的CPU和内存占用情况
pm2 monit   
// 所有日志
pm2 logs
// 指定日志
pm2 logs xxx
// 清空所有日志文件
pm2 flush
// 停止所有的应用程序
pm2 stop all
// 停止指定id的应用程序
pm2 stop id
// 重启所有应用
pm2 restart all
// 重启 cluster mode下的所有应用
pm2 reload all
// 关闭并删除所有应用
pm2 delete all 
删除指定id的应用程序
pm2 delete id
```

> gitlab

```bash
// 读取最新配置
gitlab-ctl reconfigure
// 启动gitlab所有服务
gitlab-ctl start
// 停止gitlab所有服务
gitlab-ctl stop
// 重启gitlab所有服务
gitlab-ctl restart
// gitlab所有服务状态
gitlab-ctl status
```

