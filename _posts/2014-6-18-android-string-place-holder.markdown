---
layout: post
title:  "Android字符串中使用占位符"
date:   2014-6-18 17:30:00
categories: android
tags: android
---

一是可以通过Java的 `String.format(String format, Object... args)` 方法来实现

二则是通过Android自带的 `getResources().getString(int id, Object... formatArgs）` 实现

占位符的语法可以参考[Java文档](http://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#syntax)

简单演示下第二种方法

strings.xml

```xml
<string name="boolean_conversion">Boolean: %1$b\n</string>
<string name="string_conversion">String: %1$s\n</string>
<string name="integer_conversion">Integer: %1$d\n</string>
<string name="float_conversion">Float: %1$.2f\n</string>
<string name="date_or_time_conversion">Year: %1$tY, Month: %1$tM, Day:%1$td</string>
```

MainActivity.java

```java
public class MainActivity extends ActionBarActivity {

    @Override
        protected void onCreate(Bundle savedInstanceState) {
 		super.onCreate(savedInstanceState);
	        setContentView(R.layout.ac_main);

	        TextView text = (TextView) findViewById(R.id.ac_main_text);
	        StringBuilder builder = new StringBuilder();
	        builder.append(
	                getResources().getString(R.string.boolean_conversion, true));

	        builder.append(
	                getResources().getString(R.string.string_conversion, "hello world"));

	        builder.append(
	                getResources().getString(R.string.integer_conversion, 1234));

	        builder.append(
	                getResources().getString(R.string.float_conversion, 1234.5678));

	        Calendar calendar = Calendar.getInstance();
	        builder.append(
	                getResources().getString(R.string.date_or_time_conversion, calendar));

	        text.setText(builder.toString());
	}
}
```
