https方式每次都要输入密码,可以在命令行中配置Git，来记住密码，得到和SSH一样的体验：

设置记住密码（默认15分钟）：

```bash
git config --global credential.helper cache
```

如果想自己设置时间，可以这样做：

```bash
git config credential.helper 'cache --timeout=3600'
```

这样就设置一个小时之后失效

长期存储密码：

```bash
git config --global credential.helper store
```

如果想禁用记住密码可以用

```bash
 git config --system --unset credential.helper
```



更多用法请参考git文档

>https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E5%87%AD%E8%AF%81%E5%AD%98%E5%82%A8
