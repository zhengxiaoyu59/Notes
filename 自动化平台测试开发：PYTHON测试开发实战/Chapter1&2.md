## 1. 搭建Python环境
下载Python3.6，配置环境变量。
 

## 2. 搭建Django环境
> 安装Django，`pip install Django==3.0.7`

或者使用`pip3 install Django==3.0.7`。可以通过pip3 list查看是否已安装。


## 3. Django开发入门
### 3.1 Django简介
Django 是一个由 Python 编写的一个开放源代码的 Web 应用框架，本身基于 MVC 模型。特点有强大的数据库功能、自带后台等。

#### MVC 模型
MVC 模式是软件工程中的一种软件架构模式，把软件系统分为三个基本部分：  
- 模型（Model）：编写程序应有的功能，负责业务对象与数据库的映射(ORM)。  
- 视图（View）：图形界面，负责与用户的交互(页面)。  
- 控制器（Controller）：负责转发请求，对请求进行处理。  

用户操作流程图：

 
#### MTV 模型
Django 的 MTV 模式本质上和 MVC 是一样的，也是为了各组件间保持松耦合关系，只是定义上有些许不同，分别是指：  
- 模型（Model）：编写程序应有的功能，负责业务对象与数据库的映射(ORM)。  
- 模板（Template）：负责如何把页面(html)展示给用户。  
- 视图（View）：负责业务逻辑，并在适当时候调用 Model和 Template。  

除了以上三层之外，还需要一个 URL 分发器，它的作用是将一个个 URL 的页面请求分发给不同的 View 处理，View 再调用相应的 Model 和 Template。  

用户操作流程图：


 
用户通过浏览器向服务器发起一个请求(request)，这个请求会去访问视图函数：  
a.如果不涉及数据调用，视图函数直接返回一个模板也就是一个网页给用户。  
b.如果涉及数据调用，视图函数调用模型，模型去数据库查找数据，然后逐级返回。  
视图函数把返回的数据填充到模板中，最后返回网页给用户。





### 3.2 创建项目
> 在cmd中，cd到想要创建的文件夹路径，执行`django-admin startproject [projectname]`

 
目录说明
- zxyautotest: 项目的容器。  
- manage.py: 一个实用的命令行工具，可让你以各种方式与该 Django 项目进行交互。  
- HelloWorld/__init__.py: 一个空文件，告诉 Python 该目录是一个 Python 包。  
- HelloWorld/asgi.py: 一个 ASGI 兼容的 Web 服务器的入口，以便运行你的项目。  
- HelloWorld/settings.py: 该 Django 项目的设置/配置。  
- HelloWorld/urls.py: 该 Django 项目的 URL 声明; 一份由 Django 驱动的网站"目录"。  
- HelloWorld/wsgi.py: 一个 WSGI 兼容的 Web 服务器的入口，以便运行你的项目。  

### 3.3 启动服务
> `cd [projectname]`进入项目，输入命令`python manage.py runserver`

默认端口8000，改动端口使用python manage.py runserver 127.0.0.1:[端口号]（不可跨域）  
或者python manage.py runserver 0.0.0.0:[端口号]（代表任何IP都可访问）  

在浏览器中输入本机IP地址：127.0.0.1:8000，见到下图即正常启动。

 

### 3.4 构建Django后端
#### 1. 构建Django后端
另启一个cmd，进入工程所在目录，  
使用`python manage.py makemigrations`创建model  
使用`python manage.py migrate`创建数据表  


#### 2. 创建admin（登录后端用）
`python manage.py createsuperuser`，输入账号、邮箱、密码，创建超管账号  


#### 3. 登录Django后端
在浏览器中输入 http://127.0.0.1:8000/admin 访问后端，使用刚创建的账号登录  


#### 4. 汉化Django后端
在setting.py文件中，切换为中文和时区  


### 3.5 创建应用
执行`python manage.py startapp apitest`，在工程目录下创建apitest文件夹及文件  


在setting.py 中加入"apitest"，将apitest应用添加到项目中  


### 3.6 创建视图


### 3.7 创建映射
在url.py中创建关联映射  


### 3.8 创建模板
在apitest下创建templates文件夹，创建login.html  

在url.py中创建关联映射  

在views.py中创建login函数  

 
 
## 4. MySQL数据库使用
在Navicat中连接MySQL数据库，IP地址127.0.0.1  

在Django中，默认连接的是SQLite，将SQLite连接改成MySQL连接，修改settings.py  

```python
DATABASES = {
    'default': {
        # 'ENGINE': 'django.db.backends.sqlite3',
        # 'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'zxyautotest',
        'USER': 'root',
        'PASSWORD': '123456',
        'HOST': '127.0.0.1',
        'PORT': '3306'
    }
}
```


在zxyautotest/_init_.py文件中输入  

```python
import pymysql  
pymysql.install_as_MySQLdb()
```


在Navicat中创建数据库  


#### 安装PyMySQL
执行`pip3 install PyMySQL`  

在settings.py中添加  
```python
pymysql.version_info = (1, 3, 13, "final", 0)
pymysql.install_as_MySQLdb()
```
 
#### 迁移同步数据库和表结构
`python manage.py makemigrations`  
`python manage.py migrate`
