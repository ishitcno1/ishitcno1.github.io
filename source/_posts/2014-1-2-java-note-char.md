title:  Java笔记——字符
date:   2014-1-2 10:00:00
tags: java char unicode blog
---

# 1.基本概念

Code Point： 一个Code Point表示一个Unicode字符，例如U+0041表示A，U+2122表示™，U+03C0表示π，U+1D56B表示𝕫。对于基本字符（basic multilingual），Code Point取值从U+0000到U+FFFF。对于扩展字符（supplementary characters），Code Point取值从U+10000到U+10FFFF。

Code Unit：Code Unit是Java对Code Point的表示单元，固定为16-bit。对于基本字符，一个Code Unit对应一个Code Point。而对于扩展字符，需要用两个Code Unit表示一个Code Point，这些unit是用基本字符中的备用point编码来表示。第一个unit取值从U+D800到U+DBFF，第二个unit取值从U+DC00到U+DFFF。

# 2.输出unicode字符

对于基本字符，可以直接编码在字符串中

```
System.out.println("U+0041 is \u0041");
System.out.println("U+2122 is \u2122");
System.out.println("U+03C0 is \u03C0");
```

结果：

```
U+0041 is A
U+2122 is ™
U+03C0 is π
```

对于扩展字符，需要使用Character类中的 `static char[] toChars(int codePoint)`

```
char[] c = Character.toChars(0x1D56B);
System.out.println(c);
System.out.println("U+1D56B is " + new String(c));
```

结果：

```
𝕫
U+1D56B is 𝕫
```

# 参考

- *Core Java Volume I-Fundamentals 9th Edition*
