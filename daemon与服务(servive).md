## 系统启动时第一个运行的是init脚本程序
* 服务的启动、关闭与查看等方式  
所有的服务启动脚本放置于/etc/init.d/目录，基本上这里的软件都可以通过如下方法操作  
1.启动：/etc/init.d/daemon start  
2.关闭：/etc/init.d/daemon stop  
3.重启：/etc/init.d/daemon restart  
4.查看状态:/etc/init.d/daemon status  
* 服务启动的分类
init中的服务主要是根据服务是独立启动或者由总管程序管理进行分类  
1、 独立启动模式(stand alone): 服务独立启动，该服务直接常驻内存，提供本机或用户的服务操作，反应速度快  
2、 超级守护进程(super daemon):由特殊的xinetd或者inetd这两个总管程序提供socker对应或者端口对应的管理。没有被请求时不会启动，被请求时xinetd会唤醒对应服务，请求结束服务也结束.好处是可以通过super daemon来执行服务的时程、连接需求等控制，确定是唤醒服务需要一点延迟。  
### systemctl管理服务
* systemctl [command] [unit]
start: 启动服务  
stop:关闭服务  
restart: 重启服务  
reload: 不关闭后面的unit情况下重新加载配置文件，让配置文件生效
enable: 下次开机时服务会被启动  
disable: 下次开机不会启动  
status : 列出unit的状态，有没有执行，开机是否执行，登录等信息  
is-active: 目前有没有在运行中  
is-enable: 开机时有没有要默认启动服务  
比如要查看atd这个服务，systemctl status atd.service

### 通过systemctl
* systemctl [command] [--type=TYPE] [-all]
* command有，list-units,依据unit显示目前启动的unit,加上--all才会列出没有启动的。list-unit-files,依据/usr/lib/systemd/system/内的文件，把所有文件列表显示。TYPE就是下面写出的unit类型分类


###  *** 以下了解即可 ***
* 服务的依赖性问题
init在管理员自己手动处理服务时是没有办法协助唤醒依赖程序的。  
* 运行级别的分类
Linux提供7个运行级别，分别是0-6，其中比较重要的是1、单人维护模式，3、纯命令模式，5、图形界面。运行级别在/etc/rc.d/rc[0-6]/SXXdaemon（XX是数字，意思是启动的顺序）连接到/etc/ini.d/daemon，链接文件名（SXXdaemon），因为有XX顺序的存在，因此可以唤醒依赖服务
* 指定运行级别默认要启动的服务
1. 默认启动： chkconfig daemon on
2. 默认不启动： chkconfig daemon off
3. 查看默认为启动与否：chkconfig --list daemon

### unit类型分类
* 可以通过ll /usr/lib/systemd/system/| grep -E '(vsftpd|multi|cron)'，查看vsdtpd,crond,multi-user这几个服务的设unit
* .service一般服务类型，.socket内部程序数据交换的服务
* .target 执行环境类型，一般是一群unit的集合
* .mount .automount文件系统挂载相关服务
* .path 检测特定文件或者目录类型
* .timer 循环执行的服务
