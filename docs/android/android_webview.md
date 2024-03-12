### Android Webview 实践

#### Hybrid 应用 native 与 js 如何互相调用

#### WebView 优化

1. 进程化-> Webview 对象池 -> Webview 对象复用 （缺点是进程间的通信）
2. Webview url host 和客户端 Api host 保持一致 -> DNS 缓存复用 / Webview 网络请求被客户端托管
3. H5 离线包：提前下载离线的 H5 数据包，通过 WebView 加载离线包实现 Webview 秒开
