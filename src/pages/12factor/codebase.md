Title: I. 代码库
Slug: codebase

### 一个代码库，无数次部署

一个12原则应用通常托管于版本控制系统，比如[Git](http://git-scm.com/)，[Mercurial](http://mercurial.selenic.com/)， 或[Subversion](http://subversion.apache.org/)。用于跟踪修订版本的数据库被称作*code repository*，经常简称为*code repo*或者*repo*。

一个*代码库*是个单独的repo（在集中式版本控制系统比如Subversion），或共享一个根提交的任意多个repo的集合（在分布式版本控制系统比如Git）。

![One codebase maps to many deploys](/images/codebase-deploys.png)

代码库和应用总是一对一的关系：

* 如果对应有多个代码库，那么它不是一个应用 -- 它是一个分布式系统。分布式系统的每个组件是一个应用，可以单独应用12原则。
* 多个应用共享相同的代码库有悖12原则。解决方案是将共享代码作为库，通过[依赖管理][1]去使用它。

每个应用只有一个代码库，但会有无数次的部署。一个*部署*是应用的一个运行实例。典型的场景是一个生产环境，一个或多个测试环境。另外，每个开发者都有一份运行于本地开发环境下的拷贝，对应也算是一个部署。

虽然每个部署可能用的是不同的版本，但代码库在所有的部署中保持一致。举例来说，开发者有一些尚未部署到测试环境的提交，测试环境有一些尚未部署到生产环境的提交。但他们都基于相同的代码库，所以可以被识别为相同应用的不同部署。

[1]: http://www.harmy.me/pages/dependencies.html