## su命令
* su命令是一个方便的命令，可用 切换用户身份进行操作，基本用法为
* su [-lm] [-c "命令字符串"] [username]
* su -代表切换成root身份，并且以root的login-shell方式登录系统。su -l username，与su - 类似但是是切换成username用户。-m与-p类似都是表示不读取新使用者的配置文件，使用当前的环境设置。-c仅进行一次命令

## 总结
* 要完整切换新用户环境，包括email，user,path等地址必须使用[su - username]或[su -l username]
* 如果只想使用一次root命令，可以使用[su - -c "命令"]来执行。
* 使用root切换其他用户不需要使用密码
