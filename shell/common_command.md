##常用的命令

`1. ps aux | grep xxxx`

`2. nginx -s reload 重启nginx`

`3. launchctl  unload  ~/Library/LaunchAgents/homebrew.mxcl.php56.plist (stop PHP)`

`4. launchctl  load  ~/Library/LaunchAgents/homebrew.mxcl.php56.plist (start PHP)`

`5. grep -rn "hello,world!" *  查找当前目录下所有包括hello world 的文件`

`6. mysqldump -P33061 -h127.0.0.1 -uuser -ppassword database table --default-character-set=utf8 --opt -Q -R --skip-lock-tables>/tmp/test.sql`

`7. php --ini  查找php配置文件`

`8. php -m  查看php当前模块`

`9. chown -R user:group 修改文件的所有者和所属组`

`10. cat /proc/cpuinfo | grep processor 查看当前有机子CPU核数`

`11. diff -ruNa 文件夹1 文件夹2  比较两个文件或者文件夹内容`

`12. lsof -i:端口号  查看端口占用`

`13. php --ri 扩展名称  查看扩展版本`

`14. php -r "phpinfo();" | grep configure  查看php 编译参数`

`15. vim 删除制定行 :g/^;/d(删除以；开头的行)  :/^$/d(删除空白行)`

`16. iftop 查看当前服务器流量`
