### Android 常见问题

#### 1.消息机制

Handler，IPC

Handler： sendMessage(Message 实例) -> MessageQueue -> Looper.loop() -> handleMessage()

q:post()和 sendMessage()的区别
相同：都是通过 sendMessageAtTime()进行消息发送
post():getPostMessage(Runnable r)获取 Message -> 把 r 赋值给 message.callback -> dispatchMessage -> message.callback!=null -> message.callback.run()
sendMessage(): dispatchMessage -> Handler.mCallback != null -> Handler.mCallback.handleMessage() 返回 true 直接结束、返回 false 则 -> Handler.handleMessage()

#### 2.View 绘制过程

UI 的刷新机制：ViewRootImpl.scheduleTraversals() -> 加入到待执行队列并给刷新信号注册监听 -> VSync 信号到来时取出对应的 scheduleTraversals()并加入到主线程的消息队列 -> 消息取出并执行 measure()、layout()、draw()
同步屏障：Looper.loop()  调用 MessageQueue 的 next()方法取出队列头部 Message 执行 -> 遇到同步消息（一种特殊机制）后会寻找异步消息执行，不然就会一直阻塞，除非同步屏障取出 -> 界面刷新是异步操作，具有最高优先级

ViewRootImpl.requestLayout() -> ViewRootImpl.scheduleTraversals() -> 加入待执行队列并给刷新信号注册监听 -> VSync 信号到来时取出对应的 scheduleTraversals()并加入到主线程的消息队列 -> 消息取出调用 ViewRootImpl.performTraversals()执行 measure()、layout()、draw()

#### 3.事件传递机制

ViewGroup.dispatchTouchEvent() -> ViewGroup.onInterceptTouchEvent() -> (true) onTouchEvent()
-> (false) View.dispatchTouchEvent()

getParent().requestDisallowInterceptTouchEvent(true)

#### 4.RecyclerView 常见面试题
