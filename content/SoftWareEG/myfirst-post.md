---
title: "前后端分离1"
date: 2022-05-10T11:08:11+08:00
draft: false
---


## 1、前后端项目合并

### 后端项目

#### 项目创建/运行

​	在前端项目同级命令行中打开终端，输入`django-admin startproject 项目名称`

​	cd进该目录，输入 `python manage.py runserver`，运行该项目，终端上出现链接

#### 新建组件

​	再次在终端上输入`python manage.py startapp xxx`，创建出`xxx`组件

#### 配置数据库

​	找到第一次创建出的文件夹下，找到`settings.py`文件，找到如下代码

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}
```

​	如果想要更换为自己的`mysql`数据库，可以参考以下设置进行更改

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'xxx',				# 数据库名称
        'USER': 'root'				# 连接数据库的用户名称
        'PASSWORD': 'xxxx'			# 用户密码
        'HOST': '127.0.0.1'			 # 访问的数据库的主机ip地址
        'PORT': '3306'				# 默认mysql访问端口
    }
}
```

运行 `python manage.py migrate`
