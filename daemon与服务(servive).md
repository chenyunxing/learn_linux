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




*** 以下了解即可 ***
* 服务的依赖性问题
init在管理员自己手动处理服务时是没有办法协助唤醒依赖程序的。  
* 运行级别的分类
Linux提供7个运行级别，分别是0-6，其中比较重要的是1、单人维护模式，3、纯命令模式，5、图形界面。运行级别在/etc/rc.d/rc[0-6]/SXXdaemon（XX是数字，意思是启动的顺序）连接到/etc/ini.d/daemon，链接文件名（SXXdaemon），因为有XX顺序的存在，因此可以唤醒依赖服务
* 指定运行级别默认要启动的服务
1. 默认启动： chkconfig daemon on
2. 默认不启动： chkconfig daemon off
3. 查看默认为启动与否：chkconfig --list daemon
