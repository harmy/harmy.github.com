Title: Codebase

## I. Codebase/代码库
### One codebase tracked in revision control, many deploys
### 一个代码库，无数次部署

A twelve-factor app is always tracked in a version control system, such as [Git](http://git-scm.com/), [Mercurial](http://mercurial.selenic.com/), or [Subversion](http://subversion.apache.org/).  A copy of the revision tracking database is known as a *code repository*, often shortened to *code repo* or just *repo*.

一个12原则应用通常托管于版本控制系统，比如[Git](http://git-scm.com/)，[Mercurial](http://mercurial.selenic.com/)， 或[Subversion](http://subversion.apache.org/)。用于跟踪修订版本的数据库被称作*code repository*，经常简称为*code repo*或者*repo*。

A *codebase* is any single repo (in a centralized revision control system like Subversion), or any set of repos who share a root commit (in a decentralized revision control system like Git).

一个*代码库*是个单独的repo（在集中式版本控制系统比如Subversion），或共享一个根提交的任意多个repo的集合（在分布式版本控制系统比如Git）。

![One codebase maps to many deploys](/images/codebase-deploys.png)

There is always a one-to-one correlation between the codebase and the app:

代码库和应用总是一对一的关系：

* If there are multiple codebases, it's not an app -- it's a distributed system.  Each component in a distributed system is an app, and each can individually comply with twelve-factor.

* 如果对应多个代码库，那么它不是一个应用 -- 它是一个分布式系统。分布式系统的每个组件是一个应用，可以单独应用12原则。

* Multiple apps sharing the same code is a violation of twelve-factor.  The solution here is to factor shared code into libraries which can be included through the [dependency manager][1].

* 多个应用共享相同的代码库有悖12原则。解决方案是将共享代码作为库，通过[依赖管理][1]去使用它。


There is only one codebase per app, but there will be many deploys of the app.  A *deploy* is a running instance of the app.  This is typically a production site, and one or more staging sites.  Additionally, every developer has a copy of the app running in their local development environment, each of which also qualifies as a deploy.

每个应用只有一个代码库，但会有无数次的部署。一个*部署*是应用的一个运行实例。典型是一个生产环境，一个或多个测试环境。另外，每个开发者都有一份运行于本地开发环境下的拷贝，对应也算是一个部署。

The codebase is the same across all deploys, although different versions may be active in each deploy.  For example, a developer has some commits not yet deployed to staging; staging has some commits not yet deployed to production.  But they all share the same codebase, thus making them identifiable as different deploys of the same app.

代码库在所有的部署中保持一致，虽然每个部署可能用的是不同的版本。举例来说，开发者有一些尚未部署到测试环境的提交，测试环境有一些尚未部署到生产环境的提交。但他们都基于相同的代码库，所以可以被识别为相同应用的不同部署。
[1]: http://www.harmy.me/pages/dependencies.html