title: Vim快速复习
date: 2016-03-09 18:27:07
tags:
---
## 说明
用则进，不用则废。此篇用于快速复习Vim。

## 编辑
```
i 在光标前插入
I 在一行的开头处插入
a 在光标后追加
A 在一行的结尾处追加
o 在光标位置的下一行插入一行
O 在光标位置的上一行插入一行
r 替换单个字符
R 替换，直到<esc>退出
v 进入选择模式
ctrl+v 进行矩形选择模式
c change，修改，配合光标移动命令使用
cw 修改单词
c$ 修改光标处到行尾
10I*<esc> 在一行开头插入10个*，处理速度较慢
J 合并下一行
y 复制
yy 复制行
p 粘贴到光标后
P 粘贴到光标前
d 剪切
dd 剪切行
```

## 移动光标
```
h 左移1列
j 下移1行
k 上移1行
l 右移1列
10h 左移10列
gj 下移一行（包括折行）
gk 上移一行（包括折行）
ctrl+f 下翻一页
ctrl+b 上翻一页
ctrl+d 下翻半页
ctrl+u 上翻半页
gg 移到第一行
G 移到文件尾
12G 移到第12行
H 移到该页顶
M 移到该页中间
L 移到该页尾
75% 移到75%处
0 移到行首
$ 移到行尾
w 移到下一个单词词首
b 移到上一个单词词首
e 移到下一个单词词尾
ge 移到上一个单词词尾
zt 将光标所在行移到窗口顶部
zz 将光标所在行移到窗口中部
zb 将光标所在行移到窗口底部
```

## 查找与替换
### 查找
```
/ 正向搜索
? 反向搜索
n 搜索下一个匹配的单词
N 搜索上一个匹配的单词
\* 在Normal下，正向搜索当前光标下的单词
\# 在Normal下，反向搜索当前光标下的单词
g* 在Normal下，正向搜索包含当前光标下单词的所有单词
g# 在Normal下，反向搜索包含当前光标下单词的所有单词
```

### 替换
```
:[range]s/from/to/[flags]
range 搜索范围，如不指定，则作用于当前行
:1,10s/from/to/ 在第1到第10行之间搜索替换
:%s/from/to/ 在所有行中搜索替换
```

flags有四种
```
c 每次替换前询问
e 不显示错误
g 整行替换，如不加，则只替换每行的第一个匹配的字符串
i 忽略大小写
```

### 元字符
元字符  |  说明
----   | ----
.      |  匹配任意字符
[abc]  | 匹配方括号中的任意一个字符，可用-表示字符范围
[^abc] | 匹配除方括号中字符之外的任意字符
\d     | 匹配阿拉伯数字，等同于[0-9]
\D     | 匹配阿拉伯数字之外的任意字符，等同于[^0-9]
\w     | 匹配字母与数字，等同于[0-9A-Za-z]
\W     | 与\w相反
\t     | 匹配<TAB>字符
\s     | 匹配空白字符
\S     | 匹配非空白字符
\*     | 匹配0到任意个
\+     | 匹配1到任意个
\?     | 匹配0到1个
\{n,m} | 匹配n到m个
\{n}   | 匹配n个
\{n,}  | 匹配n到任意个
\{,m}  | 匹配0到m个
$      | 匹配行尾
^      | 匹配行首
\<     | 匹配单词词首
\\>     | 匹配单词词尾

## 文件管理与window操作
```
:w 保存
:q 退出
:e <filename> 打开文件
:sp <filename> 打开文件并水平分割window
:vsp <filename> 打开文件并垂直分割window
:ls 列出buffer
:b <buffer num> 切换到相应的buffer
:bn 下一个buffer
:bp 上一个buffer
:bd 关闭当前buffer
:bd <buffer num> 关闭相应的buffer
ctrl+w+n 打开一个水平分割的window
ctrl+w+v 打开一个垂直分割的window
ctrl+w+h/j/k/l 切换window
ctrl+w+w 切换到下一个window
ctrl+w+c 关闭当前window
ctrl+w+o 关闭其它window，只保留当前window
```

## 其它
```
u 撤销
ctrl+c 中断命令
ctrl+z 回到shell，在shell中fg返回Vim
```

## Vimrc
<script src="https://gist.github.com/ishitcno1/efc19f094cca5bedb762.js"></script>
