### Android 下的优化

在日常的开发过程中常用的优化手段。

#### 启动优化

App 启动 -> 加载空白 Window -> 创建进程 -> 创建 Main 线程 -> 创建入口 Activity -> 加载布局 View -> 在屏幕上执行 View 的绘制过程 measure、layout、draw。

| 优化方向 | 优化手段                                                                                      |
| -------- | --------------------------------------------------------------------------------------------- |
| 视觉优化 | 入口 Activity 主题设置图片                                                                    |
| 时间统计 | adb 命令、线上代码统计（Application -> attachBaseContext 到 Activity -> onWindowFocusChanged) |
| 检测工具 | TraceView、SysTrace                                                                           |
| ReDex    | dex 类重排                                                                                    |

#### UI 渲染优化

造成界面卡顿的原因 -> 过度绘制、自定义 View 里 onDraw 方法里有重叠、内存抖动
考虑使用对象池，最后使用完要释放

#### 内存优化

#### 网络优化

-   减少活跃时间：减少网络数据获取的频次
-   压缩数据包大小：压缩数据包可以减少流量消耗，也可以让请求更快

优化手段：

-   API 设计、Gzip 压缩、Protocol Buffer、根据网络或者场景获取不同分辨率的图片
-   合理使用缓存（打包网络请求、监听设备状态做一些资源下发）
-   弱网测试及优化（模拟器、网络代理工具）

#### 耗电量优化

上升到如何监控，以后台耗电为主。类似 Alarm wakeup、WakeLock、Wifi scans、Network 等使用
Facebook 的 Battery-Metrics 开源库

#### 安装包大小优化

| 优化方法        | 优化实现                                                                               |
| --------------- | -------------------------------------------------------------------------------------- |
| 清理无用资源    | Refactor -> Remove unused resources                                                    |
| Lint 工具扫描   | 列出优化的点                                                                           |
| shrinkResources | 使用 shrinkResources 配置去除无用资源                                                  |
| 国际化支持      | 在配置里去除语言国际化支持                                                             |
| 资源压缩        | 大图压缩、只保留一套图片、使用 svg 或 webp 格式的图片、打包时使用 AndResGuard 压缩方案 |
| 插件化          | 资源动态加载                                                                           |
| 只支持主流架构  | 只支持 arm 架构，对于 mips 和 x86 架构不支持                                           |
