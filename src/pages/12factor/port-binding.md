Title: VII. 端口绑定
Slug: port-binding

### 通过端口绑定(*Port binding*)来提供服务

互联网应用有时会运行于服务器的容器之中。例如PHP经常作为 [Apache HTTPD](http://httpd.apache.org/) 的一个模块来运行，正如Java运行于 [Tomcat](http://tomcat.apache.org/) 。

**12-factor应用完全自我加载** 而不依赖于任何网络服务器就可以创建一个面向网络的服务。互联网应用 **通过端口绑定来提供服务** ，并监听发送至该端口的请求。

本地环境中，开发人员通过类似 `http://localhost:5000/` 的地址来访问服务。在线上环境中，请求统一发送至公共域名而后路由至绑定了端口的网络进程。

通常的实现思路是，将网络服务器类库通过 [依赖声明][1] 载入应用。例如，Python的[Tornado](http://www.tornadoweb.org/), Ruby的[Thin](http://code.macournoyer.com/thin/) , Java以及其他基于JVM语言的 [Jetty](http://jetty.codehaus.org/jetty/) 。完全由 *用户端* ，确切的说应该是应用的代码，发起请求。和运行环境约定好绑定的端口即可处理这些请求。

HTTP并不是唯一一个可以由端口绑定提供的服务。其实几乎所有服务器软件都可以通过进程绑定端口来等待请求。例如，使用 [XMPP](http://xmpp.org/) 的 [ejabberd](http://www.ejabberd.im/)  ， 以及使用 [Redis协议](http://redis.io/topics/protocol) 的 [Redis](http://redis.io/) 。

还要指出的是，端口绑定这种方式也意味着一个应用可以成为另外一个应用的 [后端服务][3] ，调用方将服务方提供的相应URL当作资源存入 [配置][2] 以备将来调用。

[上一页：进程][5]

[下一页：并发][7]

[0]: http://www.harmy.me/pages/codebase.html
[1]: http://www.harmy.me/pages/dependencies.html
[2]: http://www.harmy.me/pages/config.html
[3]: http://www.harmy.me/pages/backing-services.html
[4]: http://www.harmy.me/pages/build-release-run.html
[5]: http://www.harmy.me/pages/processes.html
[6]: http://www.harmy.me/pages/port-binding.html
[7]: http://www.harmy.me/pages/concurrency.html
[8]: http://www.harmy.me/pages/disposability
[9]: http://www.harmy.me/pages/dev-prod-parity.html
[10]: http://www.harmy.me/pages/logs.html
[11]: http://www.harmy.me/pages/admin-processes.html