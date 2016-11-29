title: 网站开发总结
date: 2016-11-29 19:31:29
tags:
---
## 说明
近期做了个小网站，这里回顾下用到的技术和坑点

## Docker
以前没有实践过，这次用在实际布置中配合jenkins使用，确实很方便。镜像可在hub.docker.com找到，
也可自制后上传。

mongo，使用官方镜像，用 `-v /path/to/data/db:/data/db` 挂载数据库就行。

nginx，配置文件在 `/etc/nginx/conf.d/` 中，build前端镜像时使用以下指令替换
`COPY /path/to/conf.d /etc/nginx/conf.d/`

node:6.9.1，官方的镜像太大，近700M，所以基于ubuntu:latest（127.2MB）自制了一个，大小
169.8MB。国内apt-get默认源的速度不理想，于是手动下载后ADD进去。
Dockerfile如下
```
FROM ubuntu:latest

ENV NPM_CONFIG_LOGLEVEL info
ENV NODE_VERSION 6.9.1

ADD node-v6.9.1-linux-x64.tar.xz /usr/local/
ENV NODE_HOME /usr/local/node-v6.9.1-linux-x64
ENV PATH=$PATH:$NODE_HOME/bin

CMD [ "node" ]
```

## Nginx 
启动后接到大量图片请求，http referer指向一个1080网站，于是在 `location /` 节点中进行屏敝
`if ($http_referer ~* shedake\.net) {return 403;}` 。

这个ip可能被做过1080的下载站，目前ping的速度也不理想，果断换了台机器。

## Jenkins
首次启动后出现引导界面，有2个安装插件的选项，怎么点都会报错，Jenkins的文档也是无力吐糟，折腾
半个多小时才发现右上角居然可以关闭引导。
关闭引导后进入系统管理手动安装插件。

安装ssh-agent，并新建一个credential，填入私钥，并在git服务器上添加公钥，这样就可以基于
git协议pull代码，而不需要填入git服务器的帐号密码。

安装Bitbucket Plugin，在Bitbucket添加webhooks `JENKINS_URL/bitbucket-hook/` ，
在Jenkins 项目中勾选 `Build when a change is pushed to BitBucket` 。
当代码push到Bitbucket后会通知Jenkins处理。Jenkins收到通知后会自动pull代码并切到相应分支，
仓库存放在 `/var/lib/jenkins/workspace/` ，可以用 `$(pwd)` 获得当前目录。

构建命令简单的填入 `bash ./build.sh` ，然后在项目中维护脚本，主要是编译代码，build docker
镜像，删除原有container，运行新的container。

Jenkins的内存占用还是比较惊人的，只跑了mongodb、nodejs、nginx、jenkins的情况下，768M的内
存会出现out of memory。只好在发布前手动开起 `/etc/init.d/jenkins restart` ，
发布完后关闭 `/etc/init.d/jenkins stop` 。即使如此build后nodejs如果执行任务过多还是会
out fo memory。

## Webpack
为了支持React和Bootstrap需要添加下面的loader，相应的loader通过npm安装
```
module: {
        loaders: [
            { 
                test: /\.jsx?$/, 
                exclude: /node_modules/, 
                loader: 'babel-loader', 
                query: { presets: ['es2015', 'react'] } 
            },
            { 
                test: /\.css$/, 
                loader: 'style!css' 
            },
            {
                test: /\.(woff|woff2)(\?v=\d+\.\d+\.\d+)?$/,
                loader: 'url?limit=10000&mimetype=application/font-woff'
            },
            {
                test: /\.ttf(\?v=\d+\.\d+\.\d+)?$/,
                loader: 'url?limit=10000&mimetype=application/octet-stream'
            },
            {
                test: /\.eot(\?v=\d+\.\d+\.\d+)?$/,
                loader: 'file'
            },
            {
                test: /\.svg(\?v=\d+\.\d+\.\d+)?$/,
                loader: 'url?limit=10000&mimetype=image/svg+xml'
            }
        ]
    }
```

调试和代码映射
```
debug: true,
devtool: "source-map"
```