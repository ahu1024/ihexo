---
title: WampServer本地环境多域名配置
comments: false
tags:
  - wamp
date: 2018-03-28 08:59:36
updated: 2018-03-28 08:59:36
---
> Wamp就是Windows Apache Mysql PHP集成安装环境，即在window下的apache、php和mysql的服务器软件。PHP扩展、Apache模块，开启/关闭鼠标点点就搞定，再也不用亲自去修改配置文件了，WAMP它会去做。再也不用到处询问php的安装问题了，WAMP一切都搞定了，这个软件在win平台上使用的较多。
...................................................................................................

## wampServer 的Apaches config配置

- 找到wamp安装目录的 apache 的 httpd.conf 文件，例如：`E:\wamp\bin\apache\apache2.2.8\conf\httpd.conf`
- 文件中查找 Virtual hosts，去掉下面include行前面的#修改为：

```
#Virtual hosts
Include conf/extra/httpd-vhosts.conf
//这样就在配置文件中引入了httpd-vhosts.conf文件。
```

- 在目录如E:\wamp\bin\apache\apache2.2.8\conf\extra 下面找到刚刚包含进来的文件：httpd-vhosts.conf，打开文件在最后面添加配置文件：

```
<VirtualHost *:80>
    ServerAdmin   Pich
    DocumentRoot  "E:/www"  
    ServerName    www.Pich.com     
    ServerAlias   www.Pich.com
    ErrorLog      "logs/ www.Pich.com  -errlo.log"
    CustomLog     "logs/  www.Pich.com  -access.log" common
    <directory "E:/www">
        Options FollowSymLinks
        AllowOverride all
        Order Deny,Allow
        Deny from all
        Allow from all
    </directory> 
</VirtualHost>
//其中 ServerAdmin、ErrorLog 、CustomLog为可选配置，也可以不对其进行配置。
```

## 本地计算机hosts配置

- 打开系统文件目录：C:\WINDOWS\system32\drivers\etc,找到hosts文件。在最下面添加刚才配置的域名 使域名生效。如：

```
127.0.0.1       www.Pich.com
//自己可以根据需要多配置几个
```

- 重启apache服务。就ok了

## 注意事项

- 配置好以后原来的localhost就不可以使用了，只要在E:\wamp\bin\apache\apache2.2.8\conf\extra\httpd-vhosts.conf上添加

```
<VirtualHost *:80>
    ServerAdmin  Pich
    DocumentRoot "e:/wamp/www"  
    ServerName   localhost   
    ServerAlias  localhost
    ErrorLog     "logs/ www.Pich.com  -errlo.log"
    CustomLog    "logs/ www.Pich.com  -access.log" common
    <directory   "e:/wamp/www">
        Options FollowSymLinks
        AllowOverride all
        Order Deny,Allow
        Deny from all
        Allow from all
    </directory>
</VirtualHost>
```

- 然后在C:\WINDOWS\system32\drivers\etc\hosts 把 `#127.0.0.1       localhost `注释去掉或者加上这句
- 在哪看你所有的是什么端口?就在 E:\wamp\bin\apache\apache2.2.8\conf\extra\httpd-vhosts.conf
- apache的默认虚拟主机根目录地址为../Apache Software Foundation/Apache2.2/htdocs 目录下，**需要对httpd.conf文件进行修改才能指向其他目录**。在httpd.conf文件下找到这段：

```
<Directory />
      AllowOverride none
      Require all denied
</Directory>

修改为：

<Directory />
    #允许指向外部的目录进行访问  
    Options Indexes FollowSymLinks  
    AllowOverride None  
</Directory>
```

**本地wamp的Internal Server Error 500 错误解决方法**
- 本地wamp下调试url重写，加入htaccess文件后提示：500 Internal Server Error ...，而删除这个文件网站又可以正常访问，其实就是没有开启url重写的功能。开启一下就可以。
- WAMP下htaccess出错的解决方法：
  打开wamp安装目录，搜一下 httpd.conf 这个文件，找到后打开
  搜一下“LoadModule rewrite_module modules/mod_rewrite.so”，找到这一行，去掉前面的“#”
  查一下htaccess文件的规则语法是否有错误
- 重启wamp。
- 本地wamp开启了url重写功能或者网站没有htaccess文件后，仍然出现500 Internal Server Error...，检查网站config配置文件的路径和参数是否正确。

2018年3月28日09:13:04
----
> *新的版本多处手动更改变为默认配置*