title:  使用jekyll在github上写blog
date:   2013-12-25 22:37:23
tags: jekyll github markdown blog
---

# 1.安装jekyll

```
gem install jekyll
```

# 2.创建帐号
在github上新建repo，形式为username.github.io，其中username与你的用户名相同。具体可以看[Github Pages](http://pages.github.com/)

将repo clone到本地，并用jekyll初始化项目 

```
git clone git.url
cd username.github.io
jekyll new myblog
mv myblog/* ./
mv myblog/.gitignore ./
rmdir myblog/
```

# 3.开发与测试  
运行开发服务器，加入 `--watch` 后，jekyll会监视文件的改动并即时生成页面，方便开发。  

```
jekyll server --watch
```
用浏览器访问 `localhost:4000` 就能看到生成的页面。  
具体的开发参看[jekyll官网](http://jekyllrb.com/docs/home/)和其他人搭建的blog。  

# 4.推送到github  

```
git push -u origin master
```

等10分钟左右，用浏览器打开username.github.io就可以看到生成的页面了。  

# 5.后记  
这只是一篇简单的流程，具体使用jekyll还是看官方文档。  
