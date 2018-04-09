---
title: GitBook-Guide
tags:
  - GitBook
date: 2018-04-06 05:21:17
updated: 2018-04-06 05:21:17
description: 
---

> GitBook 是一个基于 Node.js 的命令行工具，可使用 Github/Git 和 Markdown 来制作精美的电子书，GitBook 并非关于 Git 的教程。GitBook支持输出多种文档格式：静态站点,PDF,eBook, 单HTML网页,JSON：一般用于电子书的调试或元数据提取。使用GitBook制作电子书，必备两个文件：README.md和SUMMARY.md 。
...................................................................................................


# 安装Gitbook

## 本地安装

### 环境和依赖
* NodeJS (v4.0.0 and above is recommended)
* Windows, Linux, Unix, or Mac OS X

### 使用 NPM 安装

```
$ npm uninstall gitbook gitbook-cli -g // 卸载旧版
$ npm install gitbook-cli gitbook -g // 安装新版（2018年4月6日03:34:49）
$ gitbook -V
  CLI version: 2.3.2
  GitBook version: 3.2.3  
```
### 测试

初始化项目文档

```
$ gitbook init ./directory // 创建文件并初始化项目
$ cd directory
```

初始化完成后，直接使用 `serve` 命令创建网页版书进行本地预览

```
$ gitbook serve  // 项目运行在  http://localhost:4000
```

至此，不出意外项目基本跑通。回顾扩展常用命令：

```
gitbook init ./directory // 创建文件并初始化项目
gitbook install 目录  (安装gitbook需要的插件)
gitbook serve 文件目录 生成目录 (启用gitbook 可以在 http://localhost:4000/ 访问)
gitbook build 文件目录 生成目录 (生成站点)
gitbook pdf 文件目录 生成目录 (生成pdf)

gitbook help //列出gitbook所有的命令
gitbook --help //输出gitbook-cli的帮助信息

gitbook ls //列出本地所有的gitbook版本
gitbook ls-remote //列出远程可用的gitbook版本
gitbook fetch 标签/版本号 //安装对应的gitbook版本
gitbook update //更新到gitbook的最新版本
gitbook uninstall 2.0.1 //卸载对应的gitbook版本

gitbook build --gitbook=2.0.1 //生成时指定gitbook的版本, 本地没有会先下载
gitbook build --log=debug //指定log的级别
gitbook builid --debug //输出错误信息
```


# GitBook 目录结构
```
├── .gitignore  // 忽略文件
├── book.json   // 打包配置文件（可选，自建）
├── README.md   // 序言（必备）
├── SUMMARY.md  // 文件目录信息
├── GLOSSARY.md // 词汇表文件,出现该文件中的词汇，鼠标放到词汇上会给出词汇示意。（可选，自建）
├── LANGS.md/  // 多语言配置文件
├── others/*    // 根目录里除了 .ignored 都会拷贝到打包文档里
├── chapter-1/  // 大标题
|   ├── README.md
|   └── something.md
└── chapter-2/
    ├── README.md
    └── something.md
```

## Glossary 实例：
```
## Git
分散式版本控制软件

## Markdown
Aaron Swartz 跟John Gruber共同设计的排版语言
```

## Summary 实例：

```
* [Introduction](README.md)

* [article-1](chapter-1/article-1.md)
    * [article-2](chapter-1/article-2.md)

### Part II
* [article-3](chapter-2/article-3.md)
* [article-4](chapter-2/article-4.md)


### Part III
* [Part III](chapter-3/README.md)
    * [article-3](chapter-3/article.md)
```

## 多语言

gitbook支持多语言。每一种语言都应该按照正常的gitbook子目录和文件命名格式，LANGS.md 放在根目录下：

```
# Languages

* [English](en/)
* [中文](zh/)
```

# Book.json 配置

> GitBook 提供了三类文档主题： Book 文档、API文档、FAQ文档。我们常用的就是 Book 文档模式，如果我们需要使用 API 文档模式或者 FAQ 文档模式，需引入文档对应的主题插件。

```
{
    "title": "标题",
    "description": "书本描述",
    "author": "作者信息",
    "output.name": "site",
    "language": "使用的语言",
    "gitbook": "指定gitbook版本 '>=3.2.3' ",
    "root": "指定存放 GitBook 文件的根目录 '.' ",
    "structure": { // 设置 Readme, Summary, Glossary等对应的文件
        "readme": "introduction.md"
    },
    "links": { // 在侧边栏添加链接
        "sidebar": {
            "Blog": "http://www.peichenhu.cn",
            "GitHub": "http://www.peichenhu.cn",
            "repository": "http://www.peichenhu.cn",
        }
    },
    "plugins": [  //提前配置 gitbook install 安装，插件地址https://plugins.gitbook.com/
        "-lunr", // 去除默认加载插件加前缀“-”
        "chart" // 添加插件
    ],

    "pluginsConfig": { // 插件配置
        "theme-default": {
            "showLevel": true // true 显示标题前面的数字索引，默认不显示。
        }
       }
    }
}

```

插件网址：[https://plugins.gitbook.com/](https://plugins.gitbook.com/)

**常用插件**
```
theme-faq FAQ文档
theme-api API文档
Disqus - Disqus 评论
Search Plus - 支持中文搜索
Prsim - 使用 Prism.js 高亮代码
Advanced Emoji - 支持 emoji 表情
Github - 添加github图标
Github Buttons - 添加项目在 Github 上的 star、fork、watch 信息
Ace Plugin - 支持ace
Emphasize - 为文字加上底色
KaTex - 支持数学公式
Include Codeblock - 用代码块显示包含文件的内容
Splitter - 使侧边栏的宽度可以自由调节
Mermaid-gb3 - 支持渲染 Mermaid 图表
Puml - 支持渲染 uml 图
Graph - 使用 function-plot 绘制数学函数图
Chart - 绘制图形
Sharing-plus - 分享当前页面
Tbfed-pagefooter - 为页面添加页脚
Expandable-chapters-small - 使左侧的章节目录可以折叠
Sectionx - 将页面分块显示
GA - Google 统计
3-ba - 百度统计
Donate - 打赏插件
Local Video - 使用 Video.js 播放本地视频
Simple-page-toc - 自动生成本页的目录结构
Anchors - 添加 Github 风格的锚点
Anchor-navigation-ex - 添加Toc到侧边悬浮导航以及回到顶部按钮
Edit Link - 链接到当前页源文件上
Sitemap-general - 生成sitemap
Favicon - 更改网站的 favicon.ico
Todo - 添加 Todo 功能
Terminal - 模拟终端样式
Copy-code-button - 为代码块添加复制按钮
Alerts - 添加不同 alerts 样式的 blockquotes
Include-csv - 显示 csv 文件内容
Musicxml - 支持 musicxml 格式的乐谱渲染
Klipse - 集成 Kplise (online code evaluator)
Versions-select - 添加版本选择的下拉菜单
Rss - 添加 rss 订阅功能
```
