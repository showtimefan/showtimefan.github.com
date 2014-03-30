---
title: Mac Lion搭建Web服务器
author: showtimefan
layout: post
tags:
  - Mac
  - Apache
  - Web服务器
  
---

#####要想在Mac下进行web开发，搭建个Web服务器是势在必行

### 一, 启动Apache 

Mac lion自带了Apache，你只需将其开启即可。

1：在系统偏好设置-共享，里面打开Web共享。

2：终端下输入```sudo apachectl start```启动

启动后在浏览器中可以通过```http://localhost```访问，这时默认的路径是在```/Library/WebServer/Documents/```

### 二, 配置虚拟主机

实际开发中往往并不把项目存放在默认路径```/Library/WebServer/Documents/```中，同时多个项目，也需要自己的访问方式

1：修改Apache的配置文件

```sudo vi /etc/apache2/httpd.conf```,去掉
	
	# Virtual hosts
	#Include /private/etc/apache2/extra/httpd-vhosts.conf

的注释符号```#```,保存退出。

2：配置虚拟主机

```sudo vi /etc/apache2/extra/httpd-vhosts.conf```

添加

	<VirtualHost *:80> 
		DocumentRoot "/Users/username/Desktop/WorkState/site" 
		ServerName site.com 
		ErrorLog "/private/var/log/apache2/localhost-error_log" 
		CustomLog "/private/var/log/apache2/localhost-access_log" common 
	</VirtualHost>
	
3:修改Host文件

```sudo vi /etc/hosts```

添加

```127.0.0.1 site.com```

这时候就可以用浏览器访问 site.com

##注意事项

如果浏览器访问site.com出现Permission Denied 403访问权限错误。可能原因有项目的访问权限受限，apache项目配置中的权限错误。下面仅附上一种解决方案

```chmod 755 Documents```

##参考文章连接

[在Mac OS X中配置Apache ＋ PHP ＋ MySQL](http://chapter31.com/2012/06/05/apache-permission-denied-on-mac-osx-lion/)

[Apache 虚拟主机 VirtualHost 配置](http://www.neoease.com/apache-virtual-host/)

[Apache Permission Denied on Mac OSX Lion](http://chapter31.com/2012/06/05/apache-permission-denied-on-mac-osx-lion/)


		