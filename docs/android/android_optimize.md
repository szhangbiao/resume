### Android 下的优化

在日常的开发过程中常用的优化手段。

#### 启动优化

App 启动 -> 加载空白 Window -> 创建进程 -> 创建 Application -> 创建 Main 线程 -> 创建入口 Activity -> 加载布局 View -> 在屏幕上执行 View 的绘制过程 measure、layout、draw。

| 优化方向 | 优化手段                                                                                      |
| -------- | --------------------------------------------------------------------------------------------- |
| 视觉优化 | 入口 Activity 主题设置图片                                                                    |
| 时间统计 | adb 命令、线上代码统计（Application -> attachBaseContext 到 Activity -> onWindowFocusChanged) |
| 检测工具 | TraceView、SysTrace                                                                           |
| ReDex    | dex 类重排                                                                                    |
| MutilDex | multiDex 在 attachBaseContext 启动子进程加载                                                  |

#### UI 渲染优化

造成界面卡顿的原因 -> 过度绘制、自定义 View 里 onDraw 方法里有重叠、内存抖动
考虑使用对象池，最后使用完要释放

优化技巧：

1. 减少 overdraw,减少不必要的背景绘制
2. 较少嵌套层次及控件个数
3. 自定义 View 的 onDraw 方法里限制 View 的绘制区域
4. ImageView 的 bg 和 src 重叠
5. 借助 ViewStub 按需加载
6. 选择合适的布局类型

#### 内存优化

1. 单例模式引发的内存泄露
2. 集合操作不当，导致的内存泄露
3. 线程操作不当：线程持有的对象引用在后台执行，与对象的生命周期不一致
4. 匿名内部类/非静态内部类导致持有对象无法释放
5. 常用资源未关闭回收，像 BroadcastReceiver，File，Cursor，IO 流、Bitmap 等
6. Handler 使用不当：持有 Activity 引用
7. 加载大图时先调整尺寸再加载，不要创建过多的静态变量

#### 网络优化

-   使用 IP 建立连接，减少 DNS 解析时间
-   Gzip 压缩数据包大小：压缩数据包可以减少流量消耗，也可以让请求更快或 Protocol Buffer 更快
-   请求图片的 Url 中添加格式、质量、宽高等参数
-   使用缓存：统一图片加载框架，统一网络数据缓存框架
-   监听设备网络状态、根据不同状态使用不同的请求策略
-   减少活跃时间：减少网络数据获取的频次
-   Okhttp： 复用 http 连接池，适当的重试策略

优化手段：

-   API 设计、Gzip 压缩、Protocol Buffer、根据网络或者场景获取不同分辨率的图片
-   合理使用缓存（打包网络请求、监听设备状态做一些资源下发）
-   弱网测试及优化（模拟器、网络代理工具）

#### 耗电量优化

上升到如何监控，以后台耗电为主。类似 Alarm wakeup、WakeLock、Wifi scans、Network 等使用
Facebook 的 Battery-Metrics 开源库

#### 安装包大小优化

| 优化方法           | 优化实现                                                                               |
| ------------------ | -------------------------------------------------------------------------------------- |
| 清理无用资源       | Refactor -> Remove unused resources                                                    |
| Lint 工具扫描      | 列出优化的点                                                                           |
| shrinkResources    | 使用 shrinkResources 配置去除无用资源                                                  |
| 国际化支持         | 在配置里去除语言国际化支持                                                             |
| 资源压缩           | 大图压缩、只保留一套图片、使用 svg 或 webp 格式的图片、打包时使用 AndResGuard 压缩方案 |
| 插件化             | 资源动态加载                                                                           |
| 只支持主流架构     | 只支持 arm 架构，对于 mips 和 x86 架构不支持                                           |
| 非透明大图使用 JPG | JPG 格式图片大小上占优                                                                 |
| 选择第三方库小的   | 技术选型方面的决策                                                                     |
| redex              | 黑科技                                                                                 |
