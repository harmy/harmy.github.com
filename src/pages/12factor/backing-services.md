Title: IV. 后端服务
Slug: backing-services

### 把后端服务(*backing services*)当作附加资源

*后端服务* 是指程序运行所需要的通过网络调用的各种服务，如数据库([MySQL](http://dev.mysql.com/)，[CouchDB](http://couchdb.apache.org/))，消息/队列系统([RabbitMQ](http://www.rabbitmq.com/)，[Beanstalkd](http://kr.github.com/beanstalkd/))，SMTP邮件发送服务([Postfix](http://www.postfix.org/))，以及缓存系统([Memcached](http://memcached.org/))。

类似数据库的后端服务，通常由部署应用程序的系统管理员一起管理。除了本地服务之外，应用程序有可能使用了第三方发布和管理的服务。示例包括SMTP(例如 [Postmark](http://postmarkapp.com/))，数据收集服务（例如 [New Relic](http://newrelic.com/) 或 [Loggly](http://www.loggly.com/)），数据存储服务（如[Amazon S3](http://http://aws.amazon.com/s3/)），以及使用API访问的服务(例如 [Twitter](http://dev.twitter.com/), [Google Maps](http://code.google.com/apis/maps/index.html), [Last.fm](http://www.last.fm/api))。

**12-Factor应用不会区别对待本地或第三方服务。** 对应用程序而言，两种都是附加资源，通过一个url或是其他存储在 [配置][2] 中的服务定位/服务证书来获取数据。12-Factor应用的任意 [部署][0] ，都应该可以在不进行任何代码改动的情况下，将本地MySQL数据库换成第三方服务(例如 [Amazon RDS](http://aws.amazon.com/rds/))。类似的，本地SMTP服务应该也可以和第三方SMTP服务(例如Postmark)互换。上述2个例子中，仅需修改配置中的资源地址。

每个不同的后端服务是一份 *资源* 。例如，一个MySQL数据库是一个资源，两个MySQL数据库(用来数据分区)就被当作是2个不同的资源。Twelve-factor应用将这些数据库都视作 *附加资源* ，这些资源和它们附属的部署保持松耦合。

![一种部署附加4个后端服务](/images/attached-resources.png)

部署可以按需加载或卸载资源。例如，如果应用的数据库服务由于硬件问题出现异常，管理员可以从最近的备份中恢复一个数据库，卸载当前的数据库，然后加载新的数据库 -- 整个过程都不需要修改代码。

[0]: http://www.harmy.me/pages/codebase.html
[1]: http://www.harmy.me/pages/dependencies.html
[2]: http://www.harmy.me/pages/config.html
[3]: http://www.harmy.me/pages/backing-services.html
[4]: http://www.harmy.me/pages/build-release-run.html
[5]: http://www.harmy.me/pages/processes.html
[6]: http://www.harmy.me/pages/port-binding.html
[7]: http://www.harmy.me/pages/concurrency.html
[8]: http://www.harmy.me/pages/disposability
[9]: http://www.harmy.me/pages/devprod-parity.html
[10]: http://www.harmy.me/pages/logs.html
[11]: http://www.harmy.me/pages/admin-processes.html