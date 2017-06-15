## 在Mac上同时安装两个PHP版本（php5.6 与 php7.1）

#### 1. 更新homebrew

```
brew update
brew upgrade 
```
	
<font color="red">注：brew upgrade 谨慎执行，该命令会更新你电脑上所有通过brew install的包</font>

#### 2. 安装php56(如果你有，可以跳过)

```
brew install php56 php56-memecached php56-mongodb php56-mbstring
```

#### 3. 安装php71

```
// 解除brew php link
brew unlink php
// 更新包
brew tap homebrew/dupes
brew tap homebrew/php
// 安装PHP71
brew install php71
// 安装PHP71 扩展
brew install php71-mongodb php71-memcached php71-mcrypt
```

#### 4. 安装php-vserion 管理cli脚本的PHP版本

```
brew tap homebrew/php-version
brew install php-version
	
```
	
#### 5. 自定义脚本支持PHP-FPM切换版本

1. 创建一个脚本，

	```
	touch php-switch
	```
	
2. 将下面的内容放到php-switch文件中<font color="red">（记得把xxxx换成自己用户名，或者写nobody也行）如果版本不一致自行修改</font>

	```
	#!/bin/bash
	if [ ! -n "$1" ];then
	    echo 'Please input php version:'
	    echo -e $(ps aux | grep php)
	    exit
	fi
	if [ $1 = "5.6" ];then
	    $(brew --prefix php71)/sbin/php71-fpm stop
	    $(brew --prefix php56)/sbin/php56-fpm start
	else
	    sudo pkill memcached
	    memcached -m 64 -p 11211 -d -u xxxx -l 127.0.0.1
	    $(brew --prefix php56)/sbin/php56-fpm stop
	    $(brew --prefix php71)/sbin/php71-fpm start
	fi	
	```
3. 使用

	```
	php-swicth 7.1  // 切换到php71版本
	php-swicth 5.6  // 切换到php56版本
	```

### 附录：

#### php-version的使用方法：

1. 查看当前所有的PHP版本 ```php-version```
2. 切换到某个版本，```php-version 7.1```

