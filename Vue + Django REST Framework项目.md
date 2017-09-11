# Vue + Django REST Framework项目

## 准备工作

>安装node

```bash
node -v
```

>安装cnpm

```bash
安装cnpm教程：https://npm.taobao.org/
```

```bash
cnpm install
```

```bash
cnpm run dev
```

### 项目初始化

>使用pip安装虚拟环境

```bash
pip3 install virtualenv
```

>在工作目录下创建虚拟环境

```bash
virtualenv DjangoEnv
```

>进入虚拟环境目录

```bash
source ./bin/activate
```

>接下来所有模块都只会安装到该目录

```bash
pip3 freeze
```

>退出虚拟环境

```bash
deactivate
```

>安装Django

```bash
pip3 install -i https://pypi.douban.com/simple django
```

```bash
pip3 install -i https://pypi.douban.com/simple markdown django-filter
```

>安装Django Rest Framework

```bash
pip3 install -i https://pypi.douban.com/simple djangorestframework
```

![Alt text](http://ww1.sinaimg.cn/large/dc05ba18gy1fj6lw90umuj228012c7gd.jpg)

>创建Django项目

![Alt text](http://ww1.sinaimg.cn/large/dc05ba18gy1fj6m5mfttyj21760qsgpv.jpg)

>启动Django项目

```bash
启动服务：python manage.py runserver
```

![Alt text](http://ww1.sinaimg.cn/large/dc05ba18gy1fj6trqid39j21mu11ggs5.jpg)

![Alt text](http://ww1.sinaimg.cn/large/dc05ba18gy1fj6tqrl8s3j21ta0cc0vs.jpg)

>创建目录

```bash
python manage.py startapp users
python manage.py startapp trade
python manage.py startapp goods
python manage.py startapp user_operation
```

### Centos7服务器环境配置

>下载mysql的repo源

```bash
wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
```

>安装mysql-community-release-el7-5.noarch.rpm包

```bash
rpm -ivh mysql-community-release-el7-5.noarch.rpm
```

```bash
安装这个包后，会获得两个mysql的yum repo源：
/etc/yum.repos.d/mysql-community.repo
/etc/yum.repos.d/mysql-community-source.repo
```

>安装mysql

```bash
yum install mysql-server
yum install mysql-devel
```

>更改/var/lib/mysql权限为当前用户

```bash
chown -R root:root /var/lib/mysql
chown -R root:root /var/lib/mysql-file
```

>重启服务

```bash
service mysqld restart
```

>重置登录密码

```bash
mysql> use mysql;
mysql> update user set password=password('123456') where user='root';
mysql> flush privileges;
```

>查看现有用户,密码及允许连接的主机

```bash
mysql> SELECT User, Password, Host FROM user;
```

>查看权限

```bash
show grants;
```

>设置远程登录权限

```bash
update user set Host='xx.xx.xx.xx' where Host = 'xx.xx.xx.xx';
```

```bash
mysql> GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '123456' WITH GRANT OPTION;
```

```bash
mysql> GRANT ALL PRIVILEGES ON *.* TO 'root'@'223.74.34.112' IDENTIFIED BY '123456' WITH GRANT OPTION;
```

>刷新权限

```bash
mysql> flush privileges;
```

>手动安装mysqlclient

```bash
tar -zxvf mysqlclient-1.3.12.tar.gz -C ./
cd mysqlclient-1.3.12
python setup.py install
```

>安装依赖包

```bash
pip3 install -i https://pypi.douban.com/simple pillow
```

如果安装失败，可以手动安装

```bash
pip3 install -i https://pypi.douban.com/simple mysqlclient
```

Command "python setup.py egg_info" failed with error code 1 in /tmp/pip-build-2yKTjY/mysqlclient/

```bash
pip3 install django-cors-headers
```

```bash
pip3 install -i https://pypi.douban.com/simple django-crispy-forms
```

```bash
pip3 install -i https://pypi.douban.com/simple django-import-export
```

```bash
pip3 install -i https://pypi.douban.com/simple django-reversion
```

```bash
pip3 install -i https://pypi.douban.com/simple django-formtools
```

```bash
pip3 install -i https://pypi.douban.com/simple httplib2
```

```bash
pip3 install -i https://pypi.douban.com/simple six
```

```bash
pip3 install -i https://pypi.douban.com/simple xlwt xlsxwriter
```

>创建superuser

```bash
python manage.py createsuperuser
Username: admin
邮箱: xxxx@163.com
Password: admin123
Password (again): admin123
Superuser created successfully.
```

### 启动Django项目

```bash
python manage.py runserver 服务器IP地址:5600
```

![Alt text](http://ww1.sinaimg.cn/large/dc05ba18gy1fjb6dehy88j211n0ddq39.jpg)

![Alt text](http://ww1.sinaimg.cn/large/dc05ba18gy1fjb6f5gozxj210v0in40v.jpg)

```bash
输入创建superuser时设置的Username、Password
```

![](http://ww1.sinaimg.cn/large/dc05ba18gy1fjb6gx1kj0j21hc0cl0ta.jpg)

### 前后端分离优缺点

>为什么要进行前后端分离

* pc、app、pad多端适应
* SPA开发模式开始流行 -> 后端提供API接口、前端负责数据展示
* 前后端开发职责不清
* 开发效率问题，前后端互相等待
* 前端一直配合着后端，能力受限
* 后台开发语言和模板高度耦合，导致开发语言依赖严重

>前后端分离缺点

* 前后端学习门槛增加
* 数据依赖导致文档重要性增加
* 前端工作量加大
* SEO的难度加大，爬虫去请求页面的时候拿不到数据，数据都通过ajax提交请求
* 后端开发模式迁移增加成本

### Restful Api

```bash
restful api是目前前后端分离的最佳实践
```

* 轻量，直接通过http，不需要额外的协议，post/get/put/delete操作
* 面向资源，一目了然，具有自解释性
* 数据描述简单，一般通过json或者xml做数据通信

>Restful架构

* 每一个url代表一种资源
* 客户端和服务端之间，传递这种资源的某种表现层
* 客户端通过四个HTTP动词，对服务器进行操作，实现"表现层状态转化"

### Vue基本概念

* 前端工程化
* 数据双向绑定 -> 加速项目重构
* 组件化开发 -> 加速项目重构
* webpack -> 将所有东西转化为Js文件
* vue、vuex -> 组件间通信、vue-router -> 组件间跳转、axios -> 异步HTTP请求
* ES6、babel -> 转化器，将ES6语法转换成ES5语法，以保证可以在不同浏览器中运行

