### Android 框架层面

#### Binder

1. 为了保证进程空间不被其他进程破坏或干扰，Linux 中的进程是相互独立或相互隔离的
2. 进程空间分为用户空间和内核空间。用户空间不可以进行数据交互，内核空间可以进行数据交互，所有进程共用一个内核空间
3. Binder 机制相对于 Linux 内传统的进程间通信方式：
   1）性能更好：Binder 机制只需要拷贝数据一次，管道、消息队列、Socket 等都需要拷贝数据两次；而共享内存虽然不需要拷贝，但实现复杂度高
   2）安全性更高：Binder 机制通过 UID/PID 在内核空间添加了身份标识，安全性更高
4. Binder 跨进程通信机制：基于 C/S 架构，由 Client、Server、ServerManage 和 Binder 驱动组成
5. Binder 驱动的实现原理：通过内存映射，即系统调用了 mmap()函数
6. Server Manage 的作用：管理 Service 的注册和查询
7. Binder 驱动的作用：1）传递进程间的数据，通过系统调用 mmap()函数
   2）实现线程控制，通过 Binder 驱动的线程池，并由 Binder 驱动自身进行管理。
8. Server 进程会创建很多线程处理 Binder 请求，这些线程采用 Binder 驱动的线程池，有 BInder 驱动自身进行管理。一个进程的 Binder 线程池默认最大是 16 个，超过的请求会阻塞等待空闲的线程
9. Android 中进行进程间通信主要通过 Binder 类，即具备了跨进程通信的能力。

#### App 启动的详细流程

1. 点击 app 图标，Launcher 进程使用 Binder IPC 向 System Server 进程发起 startActivity 请求
2. System Server 进程收到请求后，向 zygote 进程发送创建新进程的请求
3. zygote 进程 fork 出新的 App 进程
4. App 进程通过 Binder IPC 向 System Server 进程发起 attachApplication 请求
5. System Server 进程收到上面的请求后，通过 Binder IPC 向 App 进程发送 scheduleLauncherActivigty 请求
6. App 进程的 ApplicationThread 线程收到 5 的请求后，通过 Handler 向主线程发送 LAUNCHER_ACTIVITY 消息
7. 主线程收到 6 中发送来的 Message 后，反射创建目标 Acitivity，回调 onCreate 等方法，开始执行生命周期方法

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
