###### json-server 的安装使用
1.全局安装json-server（确保已经装过node环境）
```
npm install json-server -g
```
2.创建一个json文件，文件名任意。

3.让json-server指向监测文件并指定监测端口
```
json-server 文件名.js -p xxxx
```
>tips：登录设置的主页地址，可以得到对应json的路由结构，比如：
```
http://localhost:4000
```
4.通过json-server -h 可以看到如下配置项：
```
index.js [options] <source>

Options:
  --config, -c               Path to config file   [default: "json-server.json"]
  --port, -p                 Set port                            [default: 3000]
  --host, -H                 Set host                       [default: "0.0.0.0"]
  --watch, -w                Watch file(s)                             [boolean]
  --routes, -r               Path to routes file
  --middlewares, -m          Paths to middleware files                   [array]
  --static, -s               Set static files directory
  --read-only, --ro          Allow only GET requests                   [boolean]
  --no-cors, --nc            Disable Cross-Origin Resource Sharing     [boolean]
  --no-gzip, --ng            Disable GZIP Content-Encoding             [boolean]
  --snapshots, -S            Set snapshots directory              [default: "."]
  --delay, -d                Add delay to responses (ms)
  --id, -i                   Set database id property (e.g. _id) [default: "id"]
  --foreignKeySuffix, --fks  Set foreign key suffix (e.g. _id as in post_id)
                                                                 [default: "Id"]
  --quiet, -q                Suppress log messages from output         [boolean]
  --help, -h                 Show help                                 [boolean]
  --version, -v              Show version number                       [boolean]

Examples:
  index.js db.json
  index.js file.js
  index.js http://example.com/db.json
```

###### json-server 中的数据操作（模拟后台）
1.过滤数据,比如：
```
http://localhost:4000/news?id=1
```
>在自己封装的ajax中写法如下：

```
ajax({url: "http://localhost:4000/news",data: 'id=1'}).then()
```
2.属性操作，比如：
```
http://localhost:4000/news?views.length=2
```
>在自己封装的ajax中写法如下：
```
ajax({url: "http://localhost:4000/news", data: 'views.length=2'}).then()
```
3.分割：
- _start：开始参数
- _end：结束参数
- _limit：限制数量
>下面是示例
```
// 从第一条数据开始获取5篇新闻
http://localhost:4000/news?_start=0&_limit=5
```
4.排序
- _sort=xxx：排序依据的属性xxx
- _order=ASC||DESC：默认升序（ASC）
- 示例：

```
http://localhost:4000/news?_sort=views&_order=DESC
```
5.模糊查找
```
// 查找title中含有 "前端" 字样的新闻 
http://localhost:4000/news?title_like=前端
```
6.运算
- _gte：大于某值
- _lte：小于某值
- _ne：排除某值

7.全文检索
>查找对象所有value中包含指定值的数据
```
http://localhost:4000/news?q=强拆
```

###### 使用json-server生成数据
 ```
module.exports = () => {
	const data = { users: [] };
	// Create 1000 users
	for (let i = 0; i < 1000; i++) {
		data.users.push({ id: i, name: `user${i}` })
	}
	return data;
};

//使用json-server本身模拟数据
```

###### json-server 的其他使用
1.通过生成package.json可以diy自己的指令
```
npm init
```
2.移动设备访问
- 通过 json server 建立的rest api服务默认可以在局域网中通过WIFI访问接口。
- windows下面通过 ipconfig 查找到电脑的局域网地址.
- mac设备是通过 ifconfig | grep "inet " | grep -v 127.0.0.1 查看。
比如我的电脑局域网ip是 192.168.0.6,在手机上访问 http://192.168.0.6:3003 即可。

3.自定义路由
>可以通过自定义路由的形式，简化数据结构，或是建立高弹性的web api，例如：
```
{
  "/news/:id/show": "/news/:id",
  "/topics/:id/show": "/news/:id"
    
}
//访问 /news/1/show 和 topics/1/show 均返回指定的 /news/1 内容。
```
>tips：需要注意的是，路由必须以 / 开头

###### 使用Mock.js生成数据
1.安装：
```
npm install mockjs --save
```
2.待续...
