title: Android Studio 实现百度地图地位
date: 2015-12-16 13:46:10
categories:
- 学习
tags:
- Android 百度sdk 
---

百度就是坑，明明都引入地图的sdk了，但是要使用定位的功能还是需要另外引入定位的sdk，下面是我自己整理的教程，百度也有自己的教程，[百度定位教程](http://developer.baidu.com/map/index.php?title=android-locsdk/guide/v5-0 "")。
<!--more-->

## 首先去百度的开放平台里面下载定位的sdk，[百度定位sdk地址](http://developer.baidu.com/map/index.php?title=android-locsdk/geosdk-android-download "")
下载完sdk就集成到项目里面，这个和全部的教程差不多，不再描述。
## 申请百度key
同理，也是要申请百度key的，如果已经申请过就不用再申请，key是公用的，只要包名不变！申请百度key百度自己有详细的教程，[教程](http://developer.baidu.com/map/index.php?title=androidsdk/guide/key "")

## build.gradle中配置SO的使用
~~~bash
		sourceSets {
        main {
            jniLibs.srcDirs = ['libs']
        }
    }
~~~

## 注意事项，下面是百度的原话
开发者如果开发的是系统应用，则只在工程中配置SO还是不够的，还需要手动把对应架构的SO拷贝到/system/lib下，如果是64位系统的话需要将64位的SO拷贝到/sytem/lib64下。

注意：每次新版本的定位SDK，开发者除了要更新JAR包之外，也要注意一下SO有无更新，如果SO名称不一样了，也要及时替换老的SO版本，不然会导致定位失败！ 

* 当然相关的权限也是要申请的，但是如果操作过上一篇文就不用重复申请了，上一篇我是全部申请的。

## 设置AndroidManifest.xml
百度原文，在application标签中声明service组件,每个app拥有自己单独的定位service
~~~bash
<service
            android:name="com.baidu.location.f"
            android:enabled="true"
            android:process=":remote" >
        </service>
~~~
好，环境已经配置好，下面是代码的实现

## MainActivity.java实现
~~~bash
public class MainActivity extends Activity {
    private MapView mMapView = null;

    // 定位相关
    private LocationClient mLocClient;
    private MyLocationListenner myListener = new MyLocationListenner();
    private MyLocationConfiguration.LocationMode mCurrentMode;
    private BitmapDescriptor mCurrentMarker;
    private BaiduMap mBaiduMap;
    private boolean isFirstLoc = true; // 是否首次定位

    // UI相关

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        //获取地图控件引用
        mMapView = (MapView) findViewById(R.id.bmapView);

        mCurrentMode = MyLocationConfiguration.LocationMode.NORMAL;

        initMap();
    }

    private void initMap() {
        // 地图初始化
        mBaiduMap = mMapView.getMap();
        // 开启定位图层
        mBaiduMap.setMyLocationEnabled(true);
        // 定位初始化
        mLocClient = new LocationClient(this);
        mLocClient.registerLocationListener(myListener);
        LocationClientOption option = new LocationClientOption();
        option.setOpenGps(true); // 打开gps
        option.setCoorType("bd09ll"); // 设置坐标类型
        option.setScanSpan(1000);
        mLocClient.setLocOption(option);
        mLocClient.start();
    }

    /**
     * 定位SDK监听函数
     */
    public class MyLocationListenner implements BDLocationListener {

        @Override
        public void onReceiveLocation(BDLocation location) {
            // map view 销毁后不在处理新接收的位置
            if (location == null || mMapView == null) {
                return;
            }
            MyLocationData locData = new MyLocationData.Builder()
                    .accuracy(location.getRadius())
                            // 此处设置开发者获取到的方向信息，顺时针0-360
                    .direction(100).latitude(location.getLatitude())
                    .longitude(location.getLongitude()).build();
            mBaiduMap.setMyLocationData(locData);
            if (isFirstLoc) {
                isFirstLoc = false;
                LatLng ll = new LatLng(location.getLatitude(),
                        location.getLongitude());
                MapStatusUpdate u = MapStatusUpdateFactory.newLatLng(ll);
                mBaiduMap.animateMapStatus(u);
            }
        }

        public void onReceivePoi(BDLocation poiLocation) {
        }
    }

    @Override
    protected void onDestroy() {
        // 退出时销毁定位
        mLocClient.stop();
        // 关闭定位图层
        mBaiduMap.setMyLocationEnabled(false);
        mMapView.onDestroy();
        mMapView = null;
        super.onDestroy();
    }
    @Override
    protected void onResume() {
        //在activity执行onResume时执行mMapView. onResume ()，实现地图生命周期管理
        mMapView.onResume();
        super.onResume();
    }
    @Override
    protected void onPause() {
        //在activity执行onPause时执行mMapView. onPause ()，实现地图生命周期管理
        mMapView.onPause();
        super.onPause();
    }
}


~~~

## activity_main.xml不用修改，用上一个的代码
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


好，运行应用，定位终于实现了！！！！

[项目地址](https://github.com/chendisun/BaiDuMapDemo "")




# 转发请标明出处，谢谢！