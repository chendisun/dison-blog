title: Android Studio 集成百度地图开发
date: 2015-12-15 18:01:15
categories:
- 学习
tags:
- Android 百度sdk 
---

简单介绍在Android Studio集成百度sdk开发，废话不多说，直接开始。
<!--more-->

## 首先去百度的开放平台里面下载需要的sdk，[百度sdk地址](http://developer.baidu.com/map/index.php?title=androidsdk/sdkandev-download "")
![](http://120.24.60.216:4000/img/20151215181123.png)
建议选择自定义的下载，只下自己需要的包
![](http://120.24.60.216:4000/img/20151215181539.png)
## 申请百度key
申请百度key百度自己有详细的教程，[教程](http://developer.baidu.com/map/index.php?title=androidsdk/guide/key "")

## 工程配置
* AndroidManifest.xml设置
添加权限
~~~bash
		<uses-permission android:name="com.android.launcher.permission.READ_SETTINGS" />
    <uses-permission android:name="android.permission.WAKE_LOCK" >
    </uses-permission>
    <!-- SDK1.5需要android.permission.GET_TASKS权限判断本程序是否为当前运行的应用? -->
    <uses-permission android:name="android.permission.GET_TASKS" />
    <uses-permission android:name="android.permission.WRITE_SETTINGS" />
    <!-- 这个权限用于进行网络定位 -->
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <!-- 这个权限用于访问GPS定位 -->
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <!-- 用于访问wifi网络信息，wifi信息会用于进行网络定位 -->
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    <!-- 获取运营商信息，用于支持提供运营商信息相关的接口 -->
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <!-- 这个权限用于获取wifi的获取权限，wifi信息会用来进行网络定位 -->
    <uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
    <!-- 用于读取手机当前的状态 -->
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
    <!-- 写入扩展存储，向扩展卡写入数据，用于写入离线定位数据 -->
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <!-- 访问网络，网络定位需要上网 -->
    <uses-permission android:name="android.permission.INTERNET" />
    <!-- SD卡读取权限，用户写入离线定位数据 -->
    <uses-permission android:name="android.permission.MOUNT_UNMOUNT_FILESYSTEMS" />
    <!-- 允许应用读取低级别的系统日志文件 -->
    <uses-permission android:name="android.permission.READ_LOGS" />
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
~~~

* 配置key
~~~bash
			<meta-data
            android:name="com.baidu.lbsapi.API_KEY"
            android:value="你的申请的key" />
~~~

* 导入相关的jar包
把下载的jar包放在app/libs目录下面，之后在菜单栏选择File->Project Structor->Modules->Dependencies,点击+号，选择File dependency，选择jar包导入
![](http://120.24.60.216:4000/img/20151215183745.png)

* 导入so
src/main/目录下新建jniLibs目录，放入所以.so文件
![](http://120.24.60.216:4000/img/20151215184200.png)
如果工程报错，具体错误忘记了，不过到这步的错误一般都是下面的问题引起的
添加armeabi-v7a文件夹，导入相关的so文件
![](http://120.24.60.216:4000/img/20151215184955.png)

* 建议重写Application，在使用SDK各组件之前初始化context信息
~~~bash
public class MyApplication extends Application{
    @Override
    public void onCreate() {
        super.onCreate();

        //在使用SDK各组件之前初始化context信息，传入ApplicationContext
        //注意该方法要再setContentView方法之前实现
        SDKInitializer.initialize(getApplicationContext());
    }
}
~~~

## MainActivity.java实现
~~~bash
public class MainActivity extends Activity {
    MapView mMapView = null;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        //获取地图控件引用
        mMapView = (MapView) findViewById(R.id.bmapView);

        initMap();
    }

    private void initMap() {
       BaiduMap mBaiduMap = mMapView.getMap();
        //普通地图
        mBaiduMap.setMapType(BaiduMap.MAP_TYPE_NORMAL);
        //卫星地图
//        mBaiduMap.setMapType(BaiduMap.MAP_TYPE_SATELLITE);
        mBaiduMap.setTrafficEnabled(true);

    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        //在activity执行onDestroy时执行mMapView.onDestroy()，实现地图生命周期管理
        mMapView.onDestroy();
    }
    @Override
    protected void onResume() {
        super.onResume();
        //在activity执行onResume时执行mMapView. onResume ()，实现地图生命周期管理
        mMapView.onResume();
    }
    @Override
    protected void onPause() {
        super.onPause();
        //在activity执行onPause时执行mMapView. onPause ()，实现地图生命周期管理
        mMapView.onPause();
    }
}


~~~

## activity_main.xml实现
~~~bash
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="www.disonchen.com.map.test.MainActivity">

    <com.baidu.mapapi.map.MapView
        android:id="@+id/bmapView"
        android:layout_width="fill_parent"
        android:layout_height="fill_parent"
        android:clickable="true" />


</RelativeLayout>
~~~

## 如果程序报打开数据库错误，应该是百度地图SDK相关的方法被混淆了，在proguard-rules.pro文件里面添加下面的代码就可以了
~~~bash
-keep class com.baidu.** {*;}
-keep class vi.com.** {*;}    
-dontwarn com.baidu.**
~~~
至此，百度地图可以显示出来了。



# 转发请标明出处，谢谢！