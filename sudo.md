## sudo
### sudo不需要切换身份就可以以其他用户身份执行命令，通常是以root身份来执行。
* 并非所有人都可以执行sudo命令，仅有规范到/etc/sudoers内的用户才能够执行sudo这个命令。
* 一开始默认只有root可以执行sudo
* sudo的用法，sudo [-b] [-u 新使用者账号]，选项与参,-b将后续命令放到后台执行不与目前的shell产生影响，-u想切换的用户，默认不填是root
* 例子，sudo -u cyx touch /tmp/test.txt。切换成cyx用户创建文件。需要执行一串命令的话sudo -u cyx sh -c "一串命令"。如果中途需要换行美观加\\直接回车即可

### sudo的执行流程
1、当用户执行sudo的时候，系统在/etc/sudoers文件查找用户是否能够执行sudo
2、若用户有权限执行，则让用户输入密码【用户自己的密码】来确认身份。
3、若密码正确，则执行后续命令【root用户执行sudo不需要输入密码】
4、如果切换身份与是本人，也不需要输入密码

### sudo权限的增加方法
* root用户执行visudo修改/etc/sudoers，让这个账号能获得全部或者部分的root功能。
* 1、可以手动执行visudo，在大约89行的地方，模仿root   ALL=(ALL)增加一行属于想增加用户的内容。
* 2、可以手动编辑sudoers，也是差不多98行，可以看到 root  ALL=(ALL) ALL
* 四个组件意义是用户账号，登录者的来源主机名【即指定信任来源主机】，可切换的身份，可执行的命令【这里需要绝对路径】
* 可执行命令的限制，也可以限制可传入参数，如myuser ALL=(root) !/usr/bin/passwd,/usr/bin/passwd [A-za-z*],!/usr/bin/passwd root 前面的感叹号代表不可执行的意思
* 设置一个用户组可以sudo，需要修改的是，%用户组代替原有用户名的地方，意思即为此用户组可以执行sudo
* 特殊的方法，不需要泄露root密码，既可以让用户获得root权限，使用方法为admin ALL=(root) /bin/su -，这样既可以让用户执行sudo su -然后输入自己密码进入root权限。

### 其他还有可以设置免密等功能，但是感觉用的比较少，暂不记录
