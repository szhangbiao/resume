### Android 常见问题

#### 1.消息机制

Handler，IPC

Handler： sendMessage(Message 实例) -> MessageQueue -> Looper.loop() -> handleMessage()

q:post()和 sendMessage()的区别
相同：都是通过 sendMessageAtTime()进行消息发送
post():getPostMessage(Runnable r)获取 Message -> 把 r 赋值给 message.callback -> dispatchMessage -> message.callback!=null -> message.callback.run()
sendMessage(): dispatchMessage -> Handler.mCallback != null -> Handler.mCallback.handleMessage() 返回 true 直接结束、返回 false 则 -> Handler.handleMessage()

#### 2.View 绘制过程

#### 3.事件传递机制
