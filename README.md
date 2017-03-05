# react-native-baidumap [![npm version](https://img.shields.io/npm/v/react-native-baidu-map.svg?style=flat)](https://www.npmjs.com/package/react-native-baidu-map)

*** 这个模块是基于[react-native-baidumap](https://github.com/lovebing/react-native-baidu-map)修改而来 ***
Baidu Map SDK modules and view for React Native(Android & IOS), support react native 0.30+

百度地图 React Native 模块，支持 react native 0.30+

![Android](https://raw.githubusercontent.com/jimmydaddy/react-native-baidumap/master/images/android.jpg)
![IOS](https://raw.githubusercontent.com/jimmydaddy/react-native-baidumap/master/images/ios.jpg)

### Install 安装
    npm install react-native-baidumap --save
### Import 导入

#### Android Studio
- settings.gradle `
include ':react-native-baidumap'
project(':react-native-baidumap').projectDir = new File(settingsDir, '../node_modules/react-native-baidumap/android')`

- build.gradle `compile project(':react-native-baidumap')`

- MainApplication`new BaiduMapPackage(getApplicationContext())`
- AndroidMainifest.xml `<meta-data
            android:name="com.baidu.lbsapi.API_KEY" android:value="xx"/>`

#### Xcode
- Project navigator->Libraries->Add Files to 选择 react-native-baidumap/ios/RCTBaiduMap.xcodeproj
- Project navigator->Build Phases->Link Binary With Libraries 加入 libRCTBaiduMap.a
- Project navigator->Build Settings->Search Paths， Framework search paths 添加 react-native-baidumap/ios/lib，Header search paths 添加 react-native-baidumap/ios/RCTBaiduMap
- 添加依赖, react-native-baidumap/ios/lib 下的全部 framwordk， CoreLocation.framework和QuartzCore.framework、OpenGLES.framework、SystemConfiguration.framework、CoreGraphics.framework、Security.framework、libsqlite3.0.tbd（xcode7以前为 libsqlite3.0.dylib）、CoreTelephony.framework 、libstdc++.6.0.9.tbd（xcode7以前为libstdc++.6.0.9.dylib）、CoreTelephony.framework
- 添加 BaiduMapAPI_Map.framework/Resources/mapapi.bundle

- 其它一些注意事项可参考百度地图LBS文档

##### AppDelegate.m init 初始化
    #import "RCTBaiduMapViewManager.h"
    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
        ...
        [RCTBaiduMapViewManager initSDK:@"api key"];
        ...
    }

### Usage 使用方法

    import { MapView, MapTypes, MapModule, Geolocation } from 'react-native-baidumap

#### MapView Props 属性
| Name                    | Type  | Default  | Extra
| ----------------------- |:-----:| :-------:| -------
| zoomControlsVisible     | bool  | true     | Android only
| trafficEnabled          | bool  | false    |
| baiduHeatMapEnabled     | bool  | false    |
| mapType                 | number| 1        |
| zoom                    | number| 10       |
| center                  | object| null     | {latitude: 0, longitude: 0}
| marker                  | object| null     | {latitude: 0, longitude: 0, title: ''}
| markers                 | array | []       | [marker, maker]
| onMapStatusChangeStart  | func  | undefined| Android only
| onMapStatusChange       | func  | undefined|
| onMapStatusChangeFinish | func  | undefined| Android only
| onMapLoaded             | func  | undefined|
| onMapClick              | func  | undefined|
| onMapDoubleClick        | func  | undefined|
| gesturesEnabled         | bool  | true     |
| showMapScaleBar           | bool  | true     |
| rotateEnabled           | bool  | true     |
| zoomEnabledWithTap           | bool  | true     |
| scrollEnabled           | bool  | true     |
| zoomEnabled           | bool  | true     |
| overlookEnabled           | bool  | true     |





#### MapModule Methods (Deprecated)
    setMarker(double lat, double lng)
    setMapType(int mapType)
    moveToCenter(double lat, double lng, float zoom)
    Promise reverseGeoCode(double lat, double lng)
    Promise reverseGeoCodeGPS(double lat, double lng)
    Promise geocode(String city, String addr),
    Promise getCurrentPosition()

#### Geolocation Methods

| Method                    | Result
| ------------------------- | -------
| Promise reverseGeoCode(double lat, double lng) | `{"address": "", "province": "", "city": "", "district": "", "streetName": "", "streetNumber": "", "nearbyPOI": []}`
| Promise reverseGeoCodeGPS(double lat, double lng) |  `{"address": "", "province": "", "city": "", "district": "", "streetName": "", "streetNumber": ""}`
| Promise geocode(String city, String addr) | {"latitude": 0.0, "longitude": 0.0}
| Promise getCurrentPosition() | IOS: `{"latitude": 0.0, "longitude": 0.0}` Android: `{"latitude": 0.0, "longitude": 0.0, "direction": -1, "altitude": 0.0, "radius": 0.0, "address": "", "countryCode": "", "country": "", "province": "", "cityCode": "", "city": "", "district": "", "street": "", "streetNumber": "", "buildingId": "", "buildingName": ""}`
| Promise geoCodeCityKeyWord(string keyword, int pageNum, int pageCapacity) | `{"result": [{"address": "", "name": "", "street": "", "streetNumber": "", "latitude": "", "longitude": "", ···}]}`
