title: Mysql创建用户总结
date: 2012-09-06
slug: mysql-user-creation
intro: Mysql如何创建用户

在mysql下创建用户是家常便饭的事，每次都去google，各种不同版本看的眼花，不如自己记录一下，以后用得着。

用root账户登录mysql，敲入并执行下列指令可以创建一个新的数据库并赋予myuser用户从任何主机任意操作该数据库

    create database mydb;
 
    CREATE USER 'myuser'@'localhost' IDENTIFIED BY 'mypassword';
    CREATE USER 'myuser'@'%' IDENTIFIED BY 'mypassword';
 
    GRANT ALL PRIVILEGES ON mydb.* TO 'myuser'@'localhost';
    GRANT ALL PRIVILEGES ON mydb.* TO 'myuser'@'%';
 
    FLUSH PRIVILEGES;

为什么我们要添加两个用户呢？原因是mysql认为localhost是个特殊的主机，因此不能通过%匹配它（真够SB)。所以如果你要在本机通过unix socket而不是tcp连接访问数据库，就要加这条了。此外相同的用户可以有不同的密码和权限组合，数量取决于你有几个这样的user-host配对。

如果你想修改密码的话，请执行下列指令：

    SET PASSWORD FOR 'myuser'@'localhost' = PASSWORD('newpass');
    SET PASSWORD FOR 'myuser'@'%' = PASSWORD('newpass');
    FLUSH PRIVILEGES;