## 使用教程(Quick start)


### 下载(Download)
```
# 主流版本
docker pull shifupeng/lnmp:v1.0
```
### 启动(Start)
```
# 端口映射自行指定,容器名称自行指定为lnmp
docker run -dit --privileged=true --name=lnmp shifupeng/lnmp:v1.0

# 高级用法(Advanced usage)
docker run -dit \
-p 80:80 \
-p 443:443 \
-p 3306:3306 \
-p 9000:9000 \
-v /xxx/www:/www \
-v /xxx/mysql:/data/mysql \
--privileged=true \
--name=lnmp \
-d shifupeng/lnmp:v1.0
```


### 连接(Connect)
```
# 容器名称与上一步保持一致
docker exec -it lnmp /bin/bash
```
### 状态(Status)
```
ps aux|grep nginx
ps aux|grep mysql
ps aux|grep php-fpm
# 或者(Or)
systemctl status nginx
systemctl status mysqld
systemctl status php7
```
### 初始密码(Default password)
```
cat /var/log/mysqld.log|grep 'A temporary password'
# 或
password=`cat /var/log/mysqld.log|grep 'A temporary password'`;password=${password:91};echo $password
```
### 初始化(initialize)
```
如你的mysql数据是全新的，那么你可以在^1.11 or ^1.11-nosql版本中，使用 mysql_init 脚本将数据库密码初始化为：ASDFqwer1234####
```
### 警告(Warning)
```
# 请保持清醒头脑，明确自己是在容器内还是在服务器本身执行命令，以及-v挂载对文件的影响，以免造成不可挽回的损失
# 当前Node和Python较火，故增加了对node.js的支持
```
### 配置(Config)
```
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
### PHP扩展(PHP extension)
```
# 默认已安装部分扩展在目录：/usr/local/php7/lib/php/extensions/no-debug-non-zts-20170718/
# 如果要启用指定扩展，则需要修改php.ini，加上
extension=xxx.so
# xxx为PHP扩展的文件名，然后重启php
systemctl restart php7
```

如：安装xdebug
```
curl -O https://xdebug.org/files/xdebug-2.5.0.tgz
tar -zxf xdebug-2.5.0.tgz
cd xdebug-2.5.0
phpize
./configure --with-php-config=--with-php-config=/usr/local/php5/bin/php-config  # 这里为自己环境中的php-config
make
make install
Installing shared extensions:     /usr/lib/php/extensions/no-debug-non-zts-20131226/
```
然后在php.ini中配置`zend_extension=xdebug.so
`

重启nginx，检查是否安装成功
`
service nginx restart
`

```
[root@e1bc93894c4c no-debug-non-zts-20131226]# php -m | grep xdebug
xdebug
```
xdebug配置
```
[Xdebug]
zend_extension ="/usr/local/php5/lib/php/extensions/no-debug-non-zts-20131226/xdebug.so"
xdebug.profiler_enable=on
;xdebug.trace_output_dir="/usr/local/php5/lib/php/extensions/no-debug-non-zts-20131226/"
;xdebug.profiler_output_dir="/usr/local/php5/lib/php/extensions/no-debug-non-zts-20131226/"
xdebug.remote_enable=on
xdebug.remote_handler=dbgp
xdebug.remote_port=9010  
xdebug.remote_host=10.11.12.35  # 宿主机的Ip
```
记得PHPstom的debug端口也要设置成9010



### 切换php版本
`pvm 5`
