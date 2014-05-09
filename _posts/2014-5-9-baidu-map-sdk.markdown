---
layout: post
title:  "百度地图sdk的简单使用"
date:   2014-5-9 22:00:00
categories: blog
tags: baidu map
---

# 准备  
去百度申请一个KEY，申请KEY时提供的keystore的sha1值与包名必须与使用的一致。下载sdk并包含到工程中。



# 初始化  
新建一个Application的SubClass（比如MyApplication），并在AndroidManifest.xml中注册。

```java  
public class MyApplication extends Application {
	private static final String BAIDU_MAP_KEY = "yourKey";
	private BMapManager mBMapManager = null;

	@Override
	public void onCreate() {
		super.onCreate();

		initBaiduMapManager();
	}

	public boolean initBaiduMapManager() {
		if (mBMapManager == null) {
			mBMapManager = new BMapManager(getApplicationContext());
		}

		if (mBMapManager.init(BAIDU_MAP_KEY, null)) {
			// success
		} else {
			// error
		}
	}
}
```  



# 使用  
在layout中加入  

```xml  
<com.baidu.mapapi.map.MapView
            android:id="@+id/map"
	    android:layout_width="match_parent"
	    android:layout_height="match_parent"
	    android:clickable="true"/>

```  



```java
MapView mapView = (MapView) findViewById(R.id.map);
MapController controller = mapView.getController();
double lat = 39.915;
double lon = 116.404;
GeoPoint geoPoint = new GeoPoint((int) (lat * 1E6), (int) (lon * 1E6));
controller.setCenter(geoPoint);
controller.setZoom(15);
```



# 解决与ScrollView冲突  
有时候MapView要嵌套到ScrollView中使用，此时会产生冲突，可用如下方法解决  

```java
mapView.setOnTouchListener(new View.OnTouchListener() {
	@Override
	public boolean onTouch(View v, MotionEvent event) {
		if (event.getAction() == MotionEvent.ACTION_UP) {
			scrollView.requestDisallowInterceptTouchEvent(false);
		} else {
			scrollView.requestDisallowInterceptTouchEvent(true);
		}
	}
});
```



# 添加标记物  
需要新建一个ItemizedOverlay的SubClass  

```java
public class MarkOverlay extends ItemizedOverlay<OverlayItem> {
	public MarkOverlay(Drawable mark, MapView mapView) {
		super(mark, mapView);
	}
}
```


```java
Drawable mark = getResources().getDrawable(R.drawable.location);
OverlayItem item = new OverlayItem(geoPoint, "", "");
item.setMarker(mark);
MarkOverlay markOverlay = new MarkOverlay(mark, mapView);
markOverlay.add(item);
mapView.getOverlays().clear();
mapView.getOverlays().add(markOverlay);
mapView.refresh();
```


