### Android 框架层面

#### App 启动的详细流程

#### ClassLoder 的种类

#### 插件化

#### 热修复

热修复原理：Java 代码、Native 代码、资源
资源热修复：反射更改所有保存的 AssetManager 和 Resource 对象
Native 代码热修复：反射修改 ClassLoader 加载 so 文件路径
Java 代码热修复：自定义 ClassLoader，优先加载补丁包里的类

#### Android 签名机制

V1 和 V2 在技术上和物业上的区别

#### Apk 构建流程

App bundle？

#### Apk 的安装过程
