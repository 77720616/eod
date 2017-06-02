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

我们非常推荐使用virtualenv 来创建独立的Python环境，这样就可以在不同的项目使用不同的包，而不是混杂在系统默认环境。

另外 一个 优点是可以不用管理员权限也可以安装包。通过以下命令安装virtualenv：

```
pip install virtualenv
```

安装完成后，通过以下命令创建一个独立的环境：

```
virtualenv my_env
```

通过这一步创建了包含了Python环境的my\_env/ 目录。所有你安装的Python的库文件都会存放在my\_env/lib/python3.5/site-packages 下。

如果系统中同时安装了Python2.x和Python3.X，你需要指定virtualenv用哪一个。你可以定位Python3安装的路径，并用其按如下方法创建：

```
zenx$ *which python3*
/Library/Frameworks/Python.framework/Versions/3.5/bin/python3
zenx$ *virtualenv my_env -p
/Library/Frameworks/Python.framework/Versions/3.5/bin/python3*
```

运行如下命令激活你的虚拟环境：

```
source
 my_env/bin/activate
```

shell提示符将包含你的虚拟环境名字，类似下面

```
(my_env)laptop:~ zenx$
```

你可以通过deactivate命令来退出当前虚拟环境。

你可以从这里找到更多关于virtualenv的信息[https://virtualenv.pypa.io/en/latest/](https://virtualenv.pypa.io/en/latest/)

你也可以使用virtualenvwrapper工具来更简单的创建和管理你的虚拟环境，详情参见[http://virtualenvwrapper.readthedocs.org/en/latest/](http://virtualenvwrapper.readthedocs.org/en/latest/)

## 用Pip安装Django

推荐使用pip来安装Django。Python3.5自带了pip，另外也可以从这里下载安装pip[https://pip.pypa.io/](https://pip.pypa.io/)en/stable/installing/。通过下面的命令来安装Django：

```
pip install Django==1.8.6
```

Django将被安装在当前虚拟环境的Python site-packages/目录中

下面在命令行中执行python后引入django的的方法可以检查Django是否被成功安装完成：

```
>>> import django
>>> django.VERSION
(1, 7, 0, 'final', 0)
```

类似上面的输出说明Django已经成功的安装在你的电脑中。

Django安装还有其他多种方式，详情参见[https://docs.djangoproject.com/en/1.8/topics/install/](https://docs.djangoproject.com/en/1.8/topics/install/)

## 创建你的首个项目

我们的首个项目是个完整的博客站点。Django提供了一个简单创建并初始化项目结构的命令，在shell中执行：

```
django-admin startproject mysite
```

这条命令创建了一个叫mysite的Djiang项目，项目结构如下：

```
xxx
```

这些文件具体作用如下：

manage.py:项目的命令行交互工具，封装了django-admin.py的工具，此文件不用修改。

mysite/:项目目录，包含了如下文件：

```
__init__.py:一个空文件，声明了该目录是Python的一个模块
settings.py:项目的配置文件，包含了初始化默认配置。
urls.py:项目路由配置文件，管理URL和视图的映射
wsgi.py:配置项目的wsgi参数
```

通常settings.py文件包含了一个基本配置，包含默认的SQLite数据库配置和默认加载的Django应用。我们在初始化项目的过程中会自动创建这些数据库表。

操作如下：

```
cd mysite
python manage.py migrate
会有类似下面的输出
xxx
```

默认应用的数据库已经创建，稍后我们讲介绍migrate命令的相关信息。

  


