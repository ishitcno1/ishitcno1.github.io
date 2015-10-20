title:  使用Markdown撰写简历
date:   2013-12-31 17:21:03
tags: resume markdown blog
---

这里用到的工具是markdown-resume，[Github地址](https://github.com/there4/markdown-resume)  
我fork了下，写了个中文版的sample.md，见[这里](https://github.com/ishitcno1/markdown-resume/tree/zhsample)

# 1.安装php和wkhtmltopdf

```
sudo apt-get install php5
sudo apt-get install wkhtmltopdf
```

# 2.获取markdown-resume  
原作者地址

```
git clone https://github.com/there4/markdown-resume.git
```

我修改后的地址

```
git clone https://github.com/ishitcno1/markdown-resume.git
```

# 3.生成简历    
resume目录下的sample.md展示了语法，按其修改使用即可。如果你clone的我的版本，checkout zhsample分支后，resume中还会存在一个zhsample.md。这是一个中文版的示例。

生成html版简历

```
php ./bin/resume.php --source resume/sample.md
```

生成pdf版和html版简历

```
php ./bin/resume.php --source resume/sample.md --pdf
```

# 4.使用模板  
默认使用的模板是modern，项目还包含了blockish和unstyled，当然完全可以自定义。

```
php ./bin/resume.php --source resume/sample.md -t blockish
```

默认部分字体偏小，可以修改模板下的CSS文件，如修改resume.css

```css
dl {
    dd {
        margin: 0 0 1.5em;
        padding: 0;
        font-size: 100%;
        line-height: 1.4em;
    }
}

#footer + p {
    width: 100%;
    font-size: 16px;
    text-align: center;
}
```
