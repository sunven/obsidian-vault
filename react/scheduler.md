
- 接受`reconciler`注册的任务（回调函数）
- 内部维护任务队列，优先级
- 消费任务队列，直至队列清空
- 控制任务的执行时机, 来达到时间（任务）分片的目的, 实现可中断渲染

![[scheduler.excalidraw]]

![[scheduler.svg]]