环境：centos7.3

1、erlang 安装参考命令
```
https://packagecloud.io/rabbitmq/erlang/install#bash-rpm
```

2、执行官方快速安装脚本
```
curl -s https://packagecloud.io/install/repositories/rabbitmq/erlang/script.rpm.sh | sudo bash
```

3、rabbitmq-server 安装参考命令
```
https://packagecloud.io/rabbitmq/rabbitmq-server/install#bash-rpm
```

4、执行官方快速安装脚本
```
curl -s https://packagecloud.io/install/repositories/rabbitmq/rabbitmq-server/script.rpm.sh | sudo bash
```

5、执行yum安装  参考文档 https://www.jianshu.com/p/f71b3a142344
```
yum install erlang 
yum install rabbitmq-server
```

常规使用
```
开启rabbit-server: systemctl start rabbitmq-server
查看状态：rabbitmqctl status

开启控制台：

rabbitmq-plugins enable rabbitmq_management

rabbitmqctl start_app


添加用户密码配置文件：
vi /etc/rabbitmq/rabbitmq.conf

#默认用户名
default_user = guest
#默认密码
default_pass = guest
#远程用户访问
loopback_users = none


然后重启rabbitmq：systemctl restart rabbitmq-server




# rabbitmqctl list_queues
关闭应用
# rabbitmqctl stop_app
启动应用，和上述关闭命令配合使用，达到清空队列的目的
# rabbitmqctl start_app
清除所有队列
# rabbitmqctl reset
更多用法及参数，可以执行如下命令查看
# rabbitmqctl
（1）首先关闭rabbitmq: rabbitmqctl stop_app
（2）还原： rabbitmqctl reset
（3）启动： rabbitmqctl start_app
（4）添加用户： rabbitmqctl add_user root root
（5）设置权限：rabbitmqctl set_permissions -p / root ".*" ".*" ".*"
（6）查看用户： rabbitmqctl list_users
（7）删除用户：rabbitmqctl delete_user root
（8）修改密码：rabbitmqctl change_password root 123456
（9）清除密码：rabbitmqctl clear_password root







6、安装rabbitmq-c

cd /data/soft/
wget -c https://github.com/alanxz/rabbitmq-c/releases/download/v0.8.0/rabbitmq-c-0.8.0.tar.gz
tar -zxvf rabbitmq-c-0.8.0.tar.gz
cd rabbitmq-c-0.8.0
./configure --prefix=/usr/local/services/rabbitmq-c-0.8.0 && make && make install





7、安装amqp扩展  https://pecl.php.net/package/amqp

cd /data/soft/
wget -c https://pecl.php.net/get/amqp-1.10.0.tgz
tar zxf amqp-1.10.0.tgz
cd amqp-1.10.0
/usr/local/services/php7/bin/phpize
./configure --with-php-config=/usr/local/services/php7/bin/php-config --with-amqp --with-librabbitmq-dir=/usr/local/services/rabbitmq-c-0.8.0
make && make install





8、开启amqp扩展
vim /usr/local/services/php7/etc/php.ini
extension=/usr/local/services/php7/lib/php/extensions/no-debug-non-zts-20190902/amqp.so

重启php-fpm



9、代码安装 
composer require php-amqplib/php-amqplib




使用
写队列
RabbitMQTool::instance(队列名名)->wMq(写入内容);
读队列
RabbitMQTool::instance(队列名名)->rMq(取出数量);



RabbitMQ的四种交换机介绍
https://www.jianshu.com/p/469f4608ce5d
```
