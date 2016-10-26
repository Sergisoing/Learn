##PHP-FPM 在Ubuntu上的一个小Bug
###问题描述 

在Ubuntu14.0* 系列（我也不知道那个版本会解决这个问题），想要重启或者停止PHP-FPM会报一个notice（`unknown instance on reload`）然后就没下文啦。

###解决办法

1. ps aux | grep php-fpm ,kill 所有的进程ID，然后重启
2. sudo pkill php-fpm，干掉所有的php-fpm进程,然后service php-fpm restart
