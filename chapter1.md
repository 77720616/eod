# 创建一个博客

通过本书，你可以学习到如何通过Django创建完整的项目。本章节将教会你如何安装Django，和如何用Django创建一个简单的博客。本章的目的将使你了解Django如何运行，不同的组件如何交互，掌握如何用Django实现基本功能性的项目的项目。Django通过框架组件对底层的细节进行隐藏。

本章涵盖以下知识点：

* 安装Django并创建首个项目
* 设计模型和模型整合
* 创建管理后台
* 用QuerySet 和managers
* 创建视图、模版和URL
* 在列表视图中加入分页
* 使用基于类的视图

## 安装Django

如果你已经安装了Django，可以跳过直接看下一节。Django作为一个Python包可以安装在大多数Python环境中。如果你还没有安装Django，跟着我一起来在本地开发环境装吧。

Django可以完美运行在Python2.7和3.x版本环境下，本书代码均在Python3里。如果你使用的是Linux和Mac OS X，Python默认已经安装好了。如果你确定自己的电脑是否安装了Python，可以在命令行中输入python，如果你看到类似如下输出，则表示已经安装：

```py
Python 3.4.1 (default, Jun  6 2015, 08:19:56)
[GCC 4.2.1 Compatible Apple LLVM 6.0 (clang-600.0.51)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

如果你电脑上的Python版本低于3，或者尚未安装，可以到Python网站下载并安装[https://www.python.org/downloads/](https://www.python.org/downloads/)

一旦使用了Python 3 ，不用另外安装database。此版本内建了SQLite 数据库。SQLite是个轻量级的数据库，用来支持你做Django开发。如果你要在生产环节部署Django，可以选择更加强有力的数据库系统，例如PostgreSQL，MySQL，或者Oracle。你可以找多关于Django支持的数据库信息[https://docs.djangoproject.com/en/1.8/topics/install/\#database-installation](https://docs.djangoproject.com/en/1.8/topics/install/#database-installation)

## 创建一个独立的Python环境





