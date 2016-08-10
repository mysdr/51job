# 项目名:pikapika

# 介绍
>皮卡丘，十万伏特！
>pikapika，振奋人心的口号！
>主要对各种招聘网站进行简历爬取，进行存储整理优化。

>你有才你就来!

>这个项目是因为HR想要看简历
>而且还需要很多简历


# 进展：
一期：51job  2016/5 

# PikaPika部署说明

# 软件要求
>go环境  1.6  beego框架1.6
>mysql数据库(建议数据库遵循中国-北京时间)

# 部署顺序：
1.设置项目路径

	GOPATH="/home/username/path"

2.进入路径拉下项目

	cd  /home/username/path
	git clone https://www.github.com/hunterhug/51job

3.进入51job/sh 运行init.sh补充外围包

	./init.sh

4.进入51job/model将51job.sql导入数据库(可以忽略，因为开启服务时自动建表，但是可能出现问题)


##  开启爬虫服务
6.进入51job/server，运行webserver.go开启爬虫服务，端口默认8099，可以更改
 	
 	go run webserver.go

或者
	
	go build webserver.go
	./webserver
 
 配置账户密码51job/pika/args.go

	var companyname=""
	var userName = ""
	var password = ""

 配置文件在51job/cons/cons.go

	//数据库配置
	const (
		//数据库账号:数据库密码@tcp(数据库ip:端口号)/数据库名?编码等
		Db = "root:112344@tcp(localhost:3306)/beego_blog?charset=utf8&loc=Local"
		//数据库日志
		LogPath = "../log/db.log"
		//开启日志？
		OpenDbLog = false
		//用户头像保留地
		ImagePath = "../data/img/"
	)

默认爬虫日志不保存在本地，如果需要保存在本地，请打开51job/log/log.go

	// 保存爬虫日志到本地？
	var openlog = false

## 开启网站服务
 7.开启小蜜蜂，安装bee工具

	go install github.com/beego/bee
 	cd 51job/web
 	bee run

如果小蜜蜂安装失败，请按照以下操作

	cd 51job/web
	go build main.go
	./main
	
配置文件在51job/web/conf/app.conf
	
	httpaddr = "127.0.0.1" //地址
	httpport = 8088         //端口
	mysqluser = "root"
	mysqlpass = "45454"
	mysqlurls = "127.0.0.1"
	mysqlport = 3306
	mysqldb   = "51job"
	pikapika="127.0.0.1:8099" //爬虫控制台地址

<img src='https://raw.githubusercontent.com/hunterhug/51job/master/img/step1.png' />
<img src='https://raw.githubusercontent.com/hunterhug/51job/master/img/step2.png' />

请自行修改

# 访问链接
[http://localhost:8099/](http://localhost:8099/) 爬虫控制台

[http://localhost:8088/](http://localhost:8088/) 网站

