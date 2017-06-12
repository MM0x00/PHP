# php 在线实验环境


## 软件简介

PHP是用于Web开发的服务器端脚本语言，但也可以用作通用编程语言。PHP可以添加到直接HTML中，或者可以与各种模板引擎和Web框架一起使用。PHP代码通常由解释器处理，该解释器可以作为Web服务器上的本地模块实现，也可以作为通用网关接口（CGI）来实现。

所属类别是编程语言

特点：

1. PHP 独特的语法混合了 C、Java、Perl 以及 PHP 自创新的语法。

2. PHP可以比CGI或者Perl更快速的执行动态网页——动态页面方面，与其他的编程语言相比，

   PHP是将程序嵌入到HTML文档中去执行，执行效率比完全生成htmL标记的CGI要高许多；

   PHP具有非常强大的功能，所有的CGI的功能PHP都能实现。

3. PHP支持几乎所有流行的数据库以及操作系统。

4. 最重要的是PHP可以用C、C++进行程序的扩展


## 软件官网

http://www.php.net/

## Dockerfile 使用方法

### 使用命令行
对于通过命令行界面（CLI）运行的PHP项目，可以执行以下操作。

Dockerfile在您的PHP项目中创建一个
```
FROM php:7.0-cli
COPY . /usr/src/myapp
WORKDIR /usr/src/myapp
CMD [ "php", "./your-script.php" ]
```
然后，运行命令来构建和运行Docker映像：
```
$ docker build -t my-php-app .
$ docker run -it --rm --name my-running-app my-php-app
```
### 运行一个PHP脚本
对于许多简单的单个文件项目，您可能会发现编写完整的不方便Dockerfile。在这种情况下，您可以直接使用PHP Docker镜像来运行PHP脚本：
```
$ docker run -it --rm --name my-running-script -v "$PWD":/usr/src/myapp -w /usr/src/myapp php:7.0-cli php your-script.php
```
### 与Apache
更常见的是，您可能希望与Apache httpd一起运行PHP。方便的是，有一个与Apache Web服务器一起打包的PHP容器的版本。

Dockerfile在您的PHP项目中创建一个
```
FROM php:7.0-apache
COPY src/ /var/www/html/
```
哪里src/是包含所有PHP代码的目录。然后，运行命令来构建和运行Docker映像：
```
$ docker build -t my-php-app .
$ docker run -d --name my-running-app my-php-app
```
我们建议您添加自定义php.ini配置。COPY它/usr/local/etc/php通过向上面的Dockerfile添加一行并运行相同的命令来构建和运行：
```
FROM php:7.0-apache
COPY config/php.ini /usr/local/etc/php/
COPY src/ /var/www/html/
```
哪里src/是包含所有PHP代码的目录，并config/包含您的php.ini文件。

## 资源链接

- http://www.php.net/
- http://www.runoob.com/php/php-tutorial.html
- https://hub.docker.com/_/php/
