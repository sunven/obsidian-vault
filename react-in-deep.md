createRoot > createFiberRoot

- load scroll nonDelegatedEvents
![[react-creactCoor-render.excalidraw]]

- priorityLevel 越小，优先级越高
- 优先级越高过期时间越小
- 过期时间越小, 任务越排在最前面

任务的过期时间 与 执行时间5s 有啥关系  重复？

react
- 提供api控制react应用的工作

## scheduler
- 接受`reconciler`注册的任务（回调函数）
- 内部维护任务队列，优先级
- 消费任务队列，直至队列清空
- 控制任务的执行时机, 来达到时间（任务）分片的目的, 实现可中断渲染

## reconciler
- react-reconciler实现
- 综合协调renderer,react,scheduler各包之间的调用与配合
- 把回调函数送入scheduler调度
	- fiber树构造
- 接收renderer发起的render请求（初次渲染）
- 接收react发起的setState的请求（更新）
- 调用renderer将fiber呈现到ui上

## renderer
- react-dom、react-native等实现
- render方法
- 实现react-reconciler构造出来的fiber转换为dom的功能


firber构造
第1次performUnitOfWork
beginWork 得到App的fiber

第2次performUnitOfWork
beginWork 得到main的fiber

第3次performUnitOfWork
beginWork 得到a的fiber,也创建了a的sibling FC

第4次performUnitOfWork
beginWork 得到null
completeUnitOfWork
	completeWork 创建a的dom 返回null
	workInProgress = FC a的sibling 重新进performUnitOfWork

第5次performUnitOfWork
beginWork 得到div的fiber

第6次performUnitOfWork
beginWork 得到p的fiber,也创建了p的sibling span 重新进performUnitOfWork

第7次performUnitOfWork
beginWork 得到null
completeUnitOfWork
	completeWork 创建p的dom 返回null
	workInProgress = span p的sibling

第8次performUnitOfWork
beginWork 得到null
completeUnitOfWork
	第1次completeWork 创建span的dom 返回null
	workInProgress = div span的return
	第2次completeWork 创建div的dom 返回null
	workInProgress = FC div的return
	第3次completeWork 创建 返回null
	workInProgress = main FC的return
	第4次completeWork 创建main的dom 返回null
	workInProgress = App main的return
	第5次completeWork 创建 返回null
	workInProgress = FiberRoot App的return
	第6次completeWork 创建 返回null
	workInProgress = null FiberRoot的return

- [ ] 预设
	- [ ] 大流程
	- [ ] 名词
- [ ] 数据结构
	- [ ] fiber
	- [ ] 数据间关联
	- [ ] 堆
- [ ] 工作循环
	- [ ] 调度循环
	- [ ] fiber构造循环
	- [ ] 总结
- [ ] 优先级
	- [ ] 调度优先级
	- [ ] land模型


## reference

<https://react.iamkasong.com/>
<https://7kms.github.io/react-illustration-series/>