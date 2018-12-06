# libstdc++
升级到Xcode 10后，在真机和模拟器上跑项目会报错：<br>
```Xcode 10 ld: library not found for -lstdc++.6``` 或者 ```Library not loaded: /usr/lib/libstdc++.6.dylib```
### 原因
这是因为 Xcode 10 彻底废弃了 libstdc++. 实际上 libstdc++ 在5年前被弃用了。<br>
相关的库文件```libstdc++.6.0.9.dylib```、```libstdc++.6.dylib```、```libstdc++.dylib```、```libstdc++.6.0.9.tbd```、```libstdc++.6.tbd```、```libstdc++.tbd``` 也从Xcode10中删除了

### 解决方案
##### 1. 使用 libc++
这是最好的解决方案，但是项目中的一些第三方静态库也用到了，而且第三方库又不能及时更新。所以暂时采用方案2。

##### 2. 添加缺失的文件
clone 项目到本地。把文件中的libstdc++库拷贝到对应的目录下。
```
/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/Library/CoreSimulator/Profiles/Runtimes/iOS.simruntime/Contents/Resources/RuntimeRoot/usr/lib/

/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX.sdk/usr/lib/

/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/usr/lib/

/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/SDKs/iPhoneSimulator.sdk/usr/lib/
```
添加完成后，重启Xcode。
