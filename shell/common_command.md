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
