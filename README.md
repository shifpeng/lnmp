## 一、蜘蛛项目：
- svn地址：`svn://139.224.30.29/home/svn`

### 1、拉项目到本地

拉取项目到本地目录`xx/xx/zz`下
比如我的本地：`/Users/steven/SvnGitRepository/zz`，里面包含蜘蛛的所有项目

### 2、pull镜像：
```shell
docker pull shifupeng/lnmp:zz_v1.0
```

### 3、启动容器：
```shell
docker run -dit -p 80:80 -p 443:443 -p 3306:3306 -p 9000:9000 -v /xxx/zz:/www -v /xxx/mysql:/data/mysql --privileged=true --name=lnmp -d shifupeng/lnmp:zz_v1.0
```

### 4、配置本地HOST：

```shell
127.0.0.1 cs.zhizhuchuxing.com
127.0.0.1 cs1.zhizhuchuxing.com
127.0.0.1 fo.zhizhuchuxing.com
127.0.0.1 hotel.zhizhuchuxing.com
127.0.0.1 wx.zhizhuchuxing.com
# 127.0.0.1 img.zhizhuchuxing.cn
```




配置完成

## 二、度啦啦项目

- svn地址：`svn://139.224.30.29/home/svn/dll`

### 1、拉项目到本地

拉取项目到本地目录`xx/xx/dll`下
比如我的本地：`/Users/steven/SvnGitRepository/dll`，里面包含度啦啦的所有项目

### 2、pull镜像：

```shell
docker pull shifupeng/lnmp:dll_v1.0
```

### 3、启动容器：

```shell
docker run -dit -p 80:80 -p 443:443 -p 3306:3306 -p 9000:9000 -v /xxx/dll:/www -v /xxx/mysql:/data/mysql --privileged=true --name=lnmp -d shifupeng/lnmp:dll_v1.0
```

### 4、配置本地HOST：

```shell
127.0.0.1 dllcs.dlltrip.com
127.0.0.1 dllcs1.dlltrip.com
127.0.0.1 dllfo.dlltrip.com
127.0.0.1 dllhotel.dlltrip.com
127.0.0.1 dllwx.dlltrip.com
```




配置完成

## 三、自己使用的LNMP(PHP版本7.3.24)

### 1、pull镜像：

```shell
docker pull shifupeng/lnmp:v1.0
```

### 2、启动容器：

```shell
docker run -dit -p 80:80 -p 443:443 -p 3306:3306 -p 9000:9000 -v /xxx/dll:/www -v /xxx/mysql:/data/mysql --privileged=true --name=lnmp -d shifupeng/lnmp:v1.0
```

### 3、连接(Connect)

```shell
# 容器名称与上一步保持一致

docker exec -it lnmp /bin/bash
```

### 4、状态(Status)

```shell
ps aux|grep nginx

ps aux|grep mysql

ps aux|grep php-fpm

# 或者(Or)

systemctl status nginx

systemctl status mysqld

systemctl status php7
```



### 5、初始密码(Default password)

```shell
cat /var/log/mysqld.log|grep 'A temporary password'

# 或

password=`cat /var/log/mysqld.log|grep 'A temporary password'`;password=${password:91};echo $password
```

### 6、初始化(initialize)

如你的mysql数据是全新的，那么你可以在`^1.11` or `^1.11`-nosql版本中，使用 `mysql_init` 脚本将数据库密码初始化为：`ASDFqwer1234####`

### 7、警告(Warning)



> 请保持清醒头脑，明确自己是在容器内还是在服务器本身执行命令，以及-v挂载对文件的影响，以免造成不可挽回的损失
>
> 当前Node和Python较火，故增加了对node.js的支持



### 8、配置(Config)

```shell
#配置文件路径(Config file path)

# Nginx

/usr/local/nginx/conf/nginx.conf

# MySQL

/etc/my.cnf

# PHP

/usr/local/php7/lib/php.ini

/usr/local/php7/etc/php-fpm.conf

/usr/local/php7/etc/php-fpm.d/www.conf

# 如对配置文件比较熟悉，也可以通过宿主机挂载使用自定义的配置文件
```

### 9、PHP扩展(PHP extension)

```shell
# 默认已安装部分扩展在目录：/usr/local/php5/lib/php/extensions/no-debug-non-zts-20170718/

# 如果要启用指定扩展，则需要修改php.ini，加上

extension=xxx.so

# xxx为PHP扩展的文件名，然后重启php

systemctl restart php7
```

