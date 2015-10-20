title:  Android源码下载中的错误与解决办法
date:   2014-10-28 20:49:00
tags: android source
---

使用 `python ./repo sync -f` 同步，可自动修复同步错误的文件

设置shell代理

```
$ export HTTP_PROXY=http://<proxy_user_id>:<proxy_password>@<proxy_server>:<proxy_port>

$ export HTTPS_PROXY=http://<proxy_user_id>:<proxy_password>@<proxy_server>:<proxy_port>
```

Not a git repository错误
多试几次，如果还不行，可查看相应目录下的config文件，找到仓库地址后手动同步

```
git clone --bare <repo_url>
```

若有checkout分支，根目录要用 `git init` 初始化
