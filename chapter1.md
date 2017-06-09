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

## 运行项目开发环境

Django自带了一个轻量级的web服务器，方便调试代码，不用花时间调试。而且在Django运行期间，还会自动检测代码的变化。当代码更新时候，会自动重启。

在项目目录中执行下列命令，运行开发服务器

```
python manage.py runserver
```

输出大致如下：

```
xxx
```

此时，我们在浏览器中访问[http://127.0.0.1:8000/](http://127.0.0.1:8000/)。你将看到下面的页面，提示你项目已经成功运行。

```
xxx
```

你也可以制定Django开发服务器运行在指定的ip和端口上，甚至还可以指定一个自定义的配置文件，例如：

```
python manage.py runserver 127.0.0.1:8001 \
--settings=mysite.settings
```

这样在遇到多个环境都有不同配置时候，方便处理。切记这样的配置只适合开发环境，在生产环境，建议使用WSGI方式运行程序，前面加上流行的web服务器，类似Apache，Gunicorn， uWSGI。搭配其他web服务器详见[https://docs.](https://docs.)djangoproject.com/en/1.8/howto/deployment/wsgi/.

在13章会讲述如何生产环境中的Django配置

## 项目设置

## 项目和应用

## 创建一个应用

## 设计博客数据模型

下面我们开始设计博客项目的数据模型，Django内置的一个Python类django.db.models.Model可以完成这个工作。继承这个类的子类的每个属性都对应一个数据表的属性。我们在models.py中定义每个模型，Django提供了API可以很便利的对数据进行操作。

首先，我们先在models.py定义Post模型：

```
xx
```

这是博客博文的数据模型，我们定义了如下字段：

title：该字段储存博客标题，CharField类型，自动转换SQL数据库中的为VARCHAR类型

slug：该字段储存URL，该类型仅能储存字母，数字，下划线和中划线，用这个字段存储博客文章优美，适合SEO的URL，增加unique\_for\_date属性记录博客博文的时间。Django可以避免同一时间多个post的拥有相同的slug

author：该字段是外键，定义一个 多对一的关系，即多个博文是一个作者，一个作者写多个博文的关系。Django在关系模型中创建外键。在此项目中，我们继承了Django认证组件中的User 模型。我们通过related\_name属性指定反向关系的命名，从User到Post。我们在后面章节会介绍更多。

body：该字段是博文的内容，使用TextField 类型，在数据库中会自动转为TEXT类型。

publish:该字段保存了博文发表的时间。我们使用Djiang中的timezone now 方法结果作为默认值

created:该字段保存了博文的创建时间。因为我们使用了auto\_now\_add，所以保存的是博文创建的时间。

updated: 该字段保存了博文的最后一次修改时间，因为我们用了 auto\_now ，所以会保存博文最后一次的保存时间。

status：该字段显示博文的状态，我们用choices属性，所以只能从给定的值中选择一个。

如上所示，Django自带了多种类型的数据类型来定义数据模型，可从这里找到更多关于Django数据类型的信息：[https://docs.djangoproject.com/](https://docs.djangoproject.com/)en/1.8/ref/models/fields/

模型中的Meta类包含了元数据，我们告诉Django，对数据的查询结果，默认通过publish字段来做降序排序。通过使用-号前缀来指定降序排序。

**str**方法是默认指定对象备注的方法，Django经常使用，比如在admin管理后台。

```
如果你用的是Python2.X，记得在Python3中所有字符串天生支持unicode，因此我们只需要用__str__()方法，__unicode__() 方法已经被淘汰。
```

因为我们要处理datatimes，所以我们需要在环境中安装pytz模块，这个模块提供了python和SQLite的timezone处理。在shell或者当前虚拟环境中shell中使用以下命令安装：

```
pip install pytz
```

Django自带了timezone-aware datetimes,你可以在settings.py的USE\_TZ字段激活或者关闭支持。默认是True。

### 激活你的应用

In order for Django to keep track of our application and 创建这个模型的数据库，我们需要激活它，方法是在settings.py中INSTALL\_APPS设置中增加一行blog，例如下面：

```
xxx
```

现在Django明白我们的应用是激活状态才可以introspect its models

创建并应用migrations

```
makemigrations blog
Migrations for 'blog':
  blog/migrations/0001_initial.py
  - Create model Post
```

```
sqlmigrate blog 0001
bash -cl "/Users
an/alienv/bin/python /Applications/PyCharm.app/Contents/helpers/pycharm/django_manage.py sqlmigrate blog 0001 /Users
an/PycharmProjects/doe"
BEGIN;
--
-- Create model Post
--
CREATE TABLE "blog_post" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "title" varchar(250) NOT NULL, "slug" varchar(250) NOT NULL, "body" text NOT NULL, "publish" datetime NOT NULL, "created" datetime NOT NULL, "updated" datetime NOT NULL, "status" varchar(10) NOT NULL, "author_id" integer NOT NULL REFERENCES "auth_user" ("id"));
CREATE INDEX "blog_post_slug_b95473f2" ON "blog_post" ("slug");
CREATE INDEX "blog_post_author_id_dd7a8485" ON "blog_post" ("author_id");
COMMIT;
```

```
>
 migrate
bash -cl "/Users
an/alienv/bin/python /Applications/PyCharm.app/Contents/helpers/pycharm/django_manage.py migrate /Users
an/PycharmProjects/doe"
Operations to perform:
  Apply all migrations: admin, auth, blog, contenttypes, sessions
Running migrations:
  Applying blog.0001_initial... OK
  Applying blog.0002_auto_20170606_2324... OK
```

创建Admin管理后台来管理模型

创建一个超级用户

将模型注册进Admin管理后台

让我们将blog模型注册进Admin管理后台，编辑blog应用中的admin.py文件，内容类似如下：

```
from django.contrib import admin
from .models import Post
# Register your models here.
​
admin.site.register(Post)
```

定制Admin中模型的显示内容

我们来定制Admin管理后台，修改bolg模块中的admin.py文件修改如下：

```
from django.contrib import admin
from .models import Post
# Register your models here.
​
​
class PostAdmin(admin.ModelAdmin):
  list_display = ('title','slug','author','publish','status')
​
admin.site.register(Post,PostAdmin)
​
```

如上图所示可以看到，显示的属性列表正是我们在list\_display中指定的那些。页面的右边新增了一个边栏让你可以对list\_filter中指定的字段对帖子过滤。页面上面增加了一个搜索框，我们可以在其中搜索search\_fields属性内容。在搜索框的下面还有一栏，可以通过时间快速导航，这是通过date\_hierachy属性来实现的。另外可以看到所有博文都按照Status和Publish两个属性来排序的，可以通过ordering属性来设置。

让我们来试试点击“Add post”链接，你将看到一些改变，当你键入博文的title时，slug字段会自动生成。为了实现这个功能，我们需要告诉Django to prepopulate the slug field with the input of the title field 使用prepopulated\_fields 属性，同样现在author字段通过一个查找widget显示，当有大量用户的时候，比下拉框选择好很多，见下面截图：

```
img
```

只用几行代码，我们就可以自定义在Admin管理后台模型显示方法。本书稍后，我们将详细描述这些

使用QuerySet 和managers

现在我们已经实现强大的管理后台来管理博客内容，是时候学习如何从数据库来检索这些信息，Django自带了强大的数据库API来让我们创建，检索，升级和删除对象，Django 的ORM（Object-relateional Mapper）兼容MySQL，PostgreSQL，SQLite和Oracle，你可以在项目中的Settings.py DATABASES中定义使用哪个数据库，Django也可以同时运行在多个数据库，而且你可以自由操作这些数据。

当你创建数据模型后Django提供了免费的API来喝数据库交互，你可以在这里找到更多数据模型的参考：

[https://docs.djangoproject.com/en/1.8/ref/models/.](https://docs.djangoproject.com/en/1.8/ref/models/.)

### 创建对象

打开终端，输入如下命令打开Python shell

```
python manage.py shell
```

输入如下语句：

```
>
>
>
  from django.contrib.auth.models import User
>
>
>
  from blog.models import Post
>
>
>
  user = User.object.get(username='admin')
>
>
>
 post = Post.objects.create(title='One more post',slug='one-more-post',body='Post body',author=user)
>
>
>
  post.save()
```

让我们来一起分析下这些代码，首先我们先检索用户名时admin的User对象：

```
user = User.objects.get(username='admin')
```

get\(\)方法允许我们从数据库检索单个对象。Note that this method expects one result that matches the query.如果数据库没有查询到结果，这个方法将抛出一个DoesNotExist异常，二如果数据库返回超过一个的结果，它会抛出一个MultipleObjectsReturned的异常。Both exceptions are attributes of the model class that the query is being performed on.

我么可以创建一个Post实例，指定title, slug,body，并且我们设置user为我们上一步检索出的结果：

```
 post = Post.objects.create(title='One more post',slug='one-more-post',body='Post body',author=user)
```

目前这个对象只保存在内存中，还没有在数据库中persisted

最后，我们用save\(\)方法将对象保存到数据库中：

```
post.save()
```

这个动作一个insert SQL statement behind the scenes，我们看到了如何先内存中创建一个对象再将其persist到数据库中，其实我们也可以用create\(\)方法直接在数据库中创建：

```
Post.objects.create(title='One more post',slug='one-more-post',body='Post body',author=user)
```

### 更新对象

让我们来看如何修改对象，例如修改title：

```
>
>
>
  post.title = 'New title'
>
>
>
  post.save()
```

这个操作时候，save将执行一个UPDATE SQL 操作。

```
所做的修改至到执行save()方法时，才会实例化到数据库中
```

### 检索对象

Django 的ORM系统基于QuerySet，一个QuerySet 是一个数据库对象筛选后的集合。上文已经学会了如何用get（）方法查询单个对象。每个Django模型至少有一个manager，默认的manager就是对象，You get a QuerySet object by using your models manager. 如果想从数据库表中取出所有对象，只需要使用all（）method在默认objects manager，like this：

```
>
>
>
  all_posts = Post.objects.all()
```

这样我们创建了从数据库表中一个返回所有对象的QuerySet。Notethat this QuerySet has not been executed yet. Django QuerySets are lazy; they are only evaluated when they are forced to do it. This behavior makes QuerySets very ef cient. If we don't set the QuerySet to a variable, but instead write it directly on the Python shell, the SQL statement of the QuerySet is executed because we force it to output results:

```
>
>
>
  Post.objects.all()
<
QuerySet [
<
Post: New title
>
, 
<
Post: One more post
>
, 
<
Post: greeting morning in wenstday
>
, 
<
Post: foo
>
]
>
```

### 使用filter\(\)方法

如果想对一个QuerySet做过滤，可以使用filter（）

方法，如下例，我们可以检索所有在2017年发布的博文：

```
>
>
>
  part_posts = Post.objects.filter(publish__year=2017)
```

同样，我们可以通过多个字段过滤，例如，我们可以检索所有username为admin，发布于2017年的博文：

```
>
>
>
  part_posts = Post.objects.filter(publish__year=2017,author__username='admin')
```

下面的语句同样可以实现一样的结果：

```
Post.objects.filter(publish__year=2017)\
 filter(author__username='admin')
```

```
我们在对检索结果进行过滤时使用两个下划线(publish__year),同时在访问关系模型也使用两个下划线(author__username)
```

### 使用exclude\(\)

我们可以使用exclude（）方法来从QuerySet排除确定的结果，例如，我们可以检索所有开头不为Why的2015年的博文：

```
Post.objects.filter(publish__year=2015)\
  .exclude(title__startswith='Why')
```

使用order\_by\(\)

可以用order\_by\(\)方法对结果字段进行排序，例如我们可以检索所有对象，并用title字段排序：

```
Post.objects.order_by('title')
```

默认是升序排序，也可以想下面例子一样用负号前缀做倒序排序：

```
Post.objects.order_by('-title')
```

### Deleting objects

如果要删除一个对象,可以从一个对象的实例删除，可以参考以下例子：

```
post = Post.objects.get(id=1)
post.delete()
```

  


