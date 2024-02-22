### Android 下的优化

在日常的开发过程中常用的优化手段。

#### 启动优化

App 启动 -> 加载空白 Window -> 创建进程 -> 创建 Main 线程 -> 创建入口 Activity -> 加载布局 View -> 在屏幕上执行 View 的绘制过程 measure、layout、draw。

| 优化方向 | 优化手段                                                                                      |
| -------- | --------------------------------------------------------------------------------------------- |
| 视觉优化 | 入口 Activity 主题设置图片                                                                    |
| 时间统计 | adb 命令、线上代码统计（Application -> attachBaseContext 到 Activity -> onWindowFocusChanged) |
| 检测工具 | TraceView、SysTrace                                                                           |

#### UI 渲染优化

造成界面卡顿的原因 -> 过度绘制、自定义 View 里 onDraw 方法里有重叠、内存抖动
考虑使用对象池，最后使用完要释放

#### 内存优化

#### 网络优化

#### 耗电量优化

#### 安装包大小优化
