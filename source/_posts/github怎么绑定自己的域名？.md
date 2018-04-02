---
title: github怎么绑定自己的域名？
comments: false
tags:
  - GitHub
  - 域名
date: 2018-04-01 11:04:59
updated: 2018-04-01 11:04:59
---

> git 是一个分布式版本控制软件，最初由林纳斯·托瓦兹（Linus Torvalds）创作，于2005年以GPL发布。该词源自英国俚语，意思大约是“混账”.

> GitHub是通过Git进行版本控制的软件源代码托管服务，由GitHub公司（曾称Logical Awesome）的开发者Chris Wanstrath、PJ Hyett和Tom Preston-Werner使用Ruby on Rails编写而成。

[GitHub](https://github.com/)
[GitHub Jobs 找工作](https://jobs.github.com/) 
[代码片段粘贴箱 Gist](https://gist.github.com/)
[GitHub 站点短连接生成器](https://git.io/)
[GitHub 桌面程序](https://desktop.github.com/)
[Gitbook](https://www.gitbook.com)
[Gitbook 开发者API](https://developer.github.com/)
[GitHub 学生开发工具包](https://education.github.com/)
[GitHub 服务器状态监测](https://status.github.com/)

...................................................................................................

1. 向你的 username.gihub.io 仓库添加一个CNAME(一定要*大写*)文件.文件中填写
```
example.com
```

2. 域名商控制台 域名解析 DNS 配置中添加 2 条记录(第一条访问地址`example.com`,第二条访问地址`www.example.com`)
```
@          A             username.github.io
www      CNAME           username.github.io
```

3. 等待你的 DNS 配置生效对DNS的配置不是立即生效的，过10分钟再去访问你的域名看看有没有配置成功 

4. 其他
免费域名(.tk|.cf|.ga|.gq|.ml)注册：[freenom](https://my.freenom.com/)