# 前沿
我们在做后台接口api设计的时候如果没有一定的原则或者理论指导，往往会陷入混乱之中。
早期国内的api设计往往都是只用GET、POST，接口名称随意，多数以动词开头，仿佛一个方法名。
然后restful风格开始被广大coder接受，并流行开来。
但是restful只是一种风格，并未做严格规范。
细节上有很多迷惑的地方。
所以很多人，包括我在哪，在学习完restful后仍然在业务逻辑落地的时候，仍然难以把控。
下面总结一下我在学习github开放的api时候的经验。

# 准备
本文假设你已经对restful风格的api有一定了解。
首先我们找到github API的网址。
https://developer.github.com/v3/
v3代表第三版的意思。v3是resutful风格的api，v4是GRAPH_QL风格的。
我们单看v3。

# 案例
这里拿出具有代表逻辑的repo模块来说。
所有repo仓库相关的接口都在下面的链接中进行了说明总结。
https://developer.github.com/v3/repos/#create-a-repository-for-the-authenticated-user

让我们先简单回忆一下repo有那些常用业务逻辑，
* 登录后，查看我的所有仓库列表
* 登录后，查看我某一仓库详情
* 未登录，查看所有仓库
* 查看某一用户所有仓库
* 查看某一组织下所有仓库
* 查看某一用户的某个仓库详情
* 自己新增一个仓库
* 自己删除一个仓库
* 修改一个仓库信息
... ...


|说明|方法|API|
|---|---|---|
|List repositories for the authenticated user	|GET| /user/repos|
|List repositories for a user	|GET| /users/:username/repos|
|List organization repositories	｜GET｜ /orgs/:org/repos|
|List public repositories	|GET| /repositories|
|Create a repository for the authenticated user	|POST| /user/repos|
|Create an organization repository	|POST| /orgs/:org/repos|
|Create a repository using a template	|POST| /repos/:template_owner/:template_repo/generate|
|Get a repository	|GET| /repos/:owner/:repo|
|Update a repository	|PATCH| /repos/:owner/:repo|
|Get all repository topics	|GET| /repos/:owner/:repo/topics|
|Replace all repository topics	|PUT| /repos/:owner/:repo/topics|
|Check if vulnerability alerts are enabled for a repository	|GET| /repos/:owner/:repo/vulnerability-alerts|
|Enable vulnerability alerts	|PUT| /repos/:owner/:repo/vulnerability-alerts|
|Disable vulnerability alerts	|DELETE| /repos/:owner/:repo/vulnerability-alerts|
|Enable automated security fixes	|PUT| /repos/:owner/:repo/automated-security-fixes|
|Disable automated security fixes	|DELETE| /repos/:owner/:repo/automated-security-fixes|
|List contributors	|GET| /repos/:owner/:repo/contributors|
|List languages	|GET| /repos/:owner/:repo/languages|
|List teams	|GET| /repos/:owner/:repo/teams|
|List tags	|GET| /repos/:owner/:repo/tags|
|Delete a repository	|DELETE| /repos/:owner/:repo|
|Transfer a repository	|POST| /repos/:owner/:repo/transfer|
|Create a repository dispatch event	|POST| /repos/:owner/:repo/dispatches|
|Create a repository using a template	|POST| /repos/:template_owner/:template_repo/generate|
|Create a repository using a template	|POST| /repos/:template_owner/:template_repo/generate|


上面是我将接口整理成了表格。然而并不能直观总结出规律。

于是有了下面的

![GITHUB](https://github.com/Luomusha/blog/blob/master/assets/GITHUB.png)

上图为不全面总结，只为说明距离。

看到上面的图相信不用我多说已经很明了了。

单为了记录，还是针对说明一下。
首先针对当前登录用户资源，提供一个特殊的域“user”
如果访问接口资源具有以下属性，则需要挂在user域下————这是当前登录用户在操作自己的资源。
例如：
给当前用户自己新建一个仓库
查看当前用户仓库列表。

然后对于其他的资源集合，用复数的资源名称作为域。
例如：
```
/repos
/users
/orgs
```
对于特定资源的访问，需要在api中加入特定条件。
例如：
```
/repos/:owner/:repo
/repos/:owner/:repo/tags
```
这样的设计方法很像数据库中的Schema方法。
例如：
```
/repos/:owner/:repo  => Repo.findByOwner(repo)
/orgs/:org/repos => Org.findRepoByOrg(org)
```



写的比较凌乱。后续有空再完善。








