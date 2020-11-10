# tpns_flutter_plugin

## 安装
在工程 pubspec.yaml 中加入 dependencies
```yaml
      dependencies:
        tpns_flutter_plugin:
          git:
            url: https://git.code.tencent.com/tpns/XG-Flutter-Plugin.git
            ref: V1.0.5
```

- 注意：由于TPNS插件名变更xg_flutter_plugin->tpns_flutter_plugin，更新插件时V1.0.4及以上版本请使用tpns_flutter_plugin


## 使用

### 集群域名配置(如果您的应用非广州集群请按照以下方法进行域名配置，广州集群请忽略)
#### 集群域名：
       中国上海：tpns.sh.tencent.com
       中国香港：tpns.hk.tencent.com
       新加坡：tpns.sgp.tencent.com
- iOS端需要在注册方法startXg之前调用以下域名配置函数
  - domainStr 对应集群域名
```dart
      void configureClusterDomainName(String domainStr);
```
- Android端需要在Manifest 文件 application 标签内添加以下元数据：

```
  <application>
    // 其他安卓组件
    <meta-data
        android:name="XG_SERVER_SUFFIX"
        android:value="其他地区域名" />
  </application>
```

  
      

###  iOS

- 在 xcode8 之后需要点开推送选项： TARGETS -> Capabilities -> Push Notification 设为 on 状态

```dart
      import 'package:tpns_flutter_plugin/tpns_flutter_plugin.dart';
```

      说明(接口使用参考/tpns_flutter_plugin/example/lib/main.dart和/tpns_flutter_plugin/example/lib/ios/homeTest.dart文件)




###   Android
#### 1. 环境配置
```groovy
      android: {
         ....
         defaultConfig {
           applicationId "替换成自己应用 ID"
           ...
           ndk {
        /// 选择要添加的对应.so 库。
        abiFilters 'armeabi', 'armeabi-v7a', 'x86', 'x86_64', 'mips', 'mips64', 'arm64-v8a',
           }
           //
           manifestPlaceholders = [
               XG_ACCESS_ID : "替换自己的ACCESS_ID",  // 信鸽官网注册所得ACCESS_ID
               XG_ACCESS_KEY : "替换自己的ACCESS_KEY",  // 信鸽官网注册所得ACCESS_KEY
    
           ]
         }
       }
```

 

#### 2. 代码混淆
```
      -keep public class * extends android.app.Service
      -keep public class * extends android.content.BroadcastReceiver
      -keep class com.tencent.android.tpush.** {*;}
      -keep class com.tencent.tpns.baseapi.** {*;} 
      -keep class com.tencent.tpns.mqttchannel.** {*;}
      -keep class com.tencent.tpns.dataacquisition.** {*;}
    
      -keep class com.tencent.bigdata.baseapi.** {*;}   // TPNS-Android-SDK 1.2.0.1 及以上版本不需要此条配置
      -keep class com.tencent.bigdata.mqttchannel.** {*;}  // TPNS-Android-SDK 1.2.0.1 及以上版本不需要此条配置
```

#### 3. 厂商通道接入说明

**说明** : 提供安卓各厂商通道接入方法。

[点击查看](./documents/vendor.md)


### APIs

**说明** : 提供TPNS的所有业务接口。

[点击查看](./documents/APIs.md)


