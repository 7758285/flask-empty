Flask Empty(CN)
===========

[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/italomaia/flask-empty?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Flask-Empty 是一个简单的flask骨架代码,用了cookiecutter创建项目代码。修正了几个小问题,根据自己的习惯集成了mako模版引擎。源仓库地址是https://github.com/italomaia/flask-empty

使用方法
=====
```shell
# if cookiecutter is not installed
sudo pip install cookiecutter

# using cookiecutter // linux/Mac
cookiecutter https://github.com/7758285/flask-empty

# answer the prompt and you're done!
```

安装
=====
鼓励用virtualenvwrapper去安装
```
pip install virtualenvwrapper
```
为你的项目创建虚拟环境,和安装相关依赖
```
mkvirtualenv my_project
pip install -r requirements/dev.txt  # dev environment if local
pip install -r requirements/prod.txt  # prod environment if server
```

你可以根据你的需要去改变依赖选项

重要的几个文件
==============================

**extensions.py** 

所有需要初始化的扩展实例都放在这里

**config.py** 

预先设置的配置类,在启动项目前首先必须设置它

**main.py** 
 
 _Empty_ 类继承了_Flask_类,重载了一些需要去安装的扩展,一个index _View_,和context processors等等。对于大多数的
 特性都有默认的设置。(查看**empty.py**能够更好的了解_Empty_)
 
**database.py** 

安装第三方数据库支持驱动,默认用sqlachemy *orm*。

**PROJECT_NAME.ini** 

这个文件是生产环境下被用来在[uwsgi](https://github.com/unbit/uwsgi)部署用的. 可以这样使用它:

```
uwsgi --ini your_project.ini
```

**manage.py** 

增加了一些非常有用的命令来提高开发生产力。需要查看提供了哪些命令运行**python manage.py**

## 问题

注意Flask-Script参数-d不能用在Flask-Empty下。如果你不想开启调试模式去启动内部的服务器实例,用**config.Config**去重新自己的配置,比如:

```python
# 加载config.Config, 里面配置了DEBUG=False
# -r 是Flask-Script的no-reload模式下启动程序的参数
python manage.py -r -c Config
```

如果 [environment config named APP_CONFIG is set](http://flask.pocoo.org/docs/config/#configuring-from-files)
被使用, 能够重载一些其他的参数

其他主题
============

## Templates

There are some error templates bundled with flask-empty by default. All empty right now. Just fill them up for
your project.

## Macros

You can use the jinja2 macros available in **templates/macros** to easily integrate your jinja2 templates with
flask extensions like wtforms and commons tasks like showing flash messages. Available macros, **formhelpers**
and **flashing** are very useful.

## Blueprints

Add your blueprints using **src/config.Config.BLUEPRINTS** as documented in the file itself. A blueprint can be add
using the path to the Blueprint or a tuple. Make sure your blueprint has a views.py and
it has a **app** Blueprint instance and you're ready to go. If unsure, check out **flask-empty/blueprint/**
for an empty blueprint example. You can also copy **flask-empty/blueprint/** to create blueprints.

With flask-empty, blueprints can live in the project root or in a special folder called **apps** in the project root.


# Supported Extensions

## Flask-SQLAlchemy

While creating your project, Flask-Empty will ask you if you wish to enable SQL support. Confirm if you do so
and Flask-SQLAlchemy will be available and configured through **database.py**.

_ps: currently, db-create will only create your models if they are imported somewhere in your application.
By **somewhere**, try the *same module where your Blueprint instance is defined*.

## Flask-Mongoengine

As mongodb is really cool, supporting it is a must. Just say yes at the prompt when asked
and Flask-Mongoengine will be setup for you.

## Flask-WTF

Flask-WTF is the "the facto" extension for handling forms with Flask. It is simply great, and Flask-Empty
supports it! Just say "yes" during project creation and Flask-WTF support will be on.

## Flask-Admin

Just create an admin.py file in your blueprint, define your admin models inside and change
**LOAD_MODULES_EXTENSIONS** to also pre-load admin, like this:

```
LOAD_MODULES_EXTENSIONS = ['views', 'models', 'admin']
```

## Other Extensions



Examples
========
If my explanation above is as crappy as I think it is, you're gonna want/need to take a look at **examples/**. They
are a very nice starting point to learn how to configure your project. Wort-case-scenario, just copy it, rename it,
configure it and be happy!

FAQ
===
**Is flask-empty _boilerplate_ compatible with flask 0.x? Cuz' that's what my app uses.**

Right now, flask-empty is a very simple project where many good practices and code examples were glued together.
Until recently I was focused in keeping backward compatibility with flask 0.8. Well, **that goal is no more**.
 Flask-empty will be compatible with the latest version of Flask and, by chance, with previous versions.
 Things will be easier this way.

**So, which is the oldest version where flask-empty works?**

In my last test, version 0.9, but no guarantees here.

**I think flask-empty should have _this_ and _that_ configured by default. Will you add support?**

My current goals are:

* Make flask-empty real easy to start a project with
* Keep things simple and robust

If your suggestion is simple, **VERY** useful and has little overhead, I'll probably consider adding it to the
project. If you make the code and send a pull request, then I'll consider it real hard. Now, if your suggestion is
 rejected or advised in a different approach, don't get sad (you're awesome ;).

**I just made a cool example with flask-empty and want to add it to examples.**

Pull request it for evaluation ;)
Just keep in mind that good examples are short (not really...) and focused in it's showcase.
