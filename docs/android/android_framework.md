### Android 框架层面

#### 插件化和热修复

热修复原理：Java 代码、Native 代码、资源
资源热修复：反射更改所有保存的 AssetManager 和 Resource 对象
Native 代码热修复：反射修改 ClassLoader 加载 so 文件路径
Java 代码热修复：自定义 ClassLoader，优先加载补丁包里的类

#### LruCache 原理

Least Recently Used 缓存策略

#### Android 签名机制

V1 和 V2 在技术上和物业上的区别

#### Apk 构建流程

App bundle？

#### Apk 的安装过程

#### Andorid 版本特性

#### Android 屏幕适配
