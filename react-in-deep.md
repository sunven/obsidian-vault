createRoot > createFiberRoot

- load scroll nonDelegatedEvents
![[react-creactCoor-render.excalidraw]]

- priorityLevel 越小，优先级越高
- 优先级越高过期时间越小
- 过期时间越小, 任务越排在最前面

任务的过期时间 与 执行时间5s 有啥关系  重复？


因此，我们有3个优先系统

1.  调度程序优先级 - 用于确定调度程序中任务的优先级
2.  事件优先级 - 标记用户事件的优先级
3.  车道优先级 - 标记工作优先级

lane
https://github.com/facebook/react/pull/18796
https://jser.dev/react/2022/03/26/lanes-in-react
lane 更新优先级
- 为啥有更新优先级?

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


beginWork：创建fiber
completeUnitOfWork 创建dom
	completeWork 如果有sibling，则重新进入一次performUnitOfWork，否则一直向上

## firber初次创建

```js
<script type="text/babel">
  const Component = React.Component;
  const createRoot = ReactDOM.createRoot;
  const root = createRoot(document.getElementById('container'));
  const FC = ()=>{
    return (
      <div>
        <p>p</p>
        <span>span</span>
      </div>
    )
  }
  class App extends Component{
    render() {
      return (
        <main>
          <a>a</a>
          <FC />
        </main>
      )
    }
  }
  root.render(<App />);
</script>
```

1. 第1次performUnitOfWork
	1. beginWork 得到App的fiber
2. 第2次performUnitOfWork
	1. beginWork 得到main的fiber
3. 第3次performUnitOfWork
	1. beginWork 得到a的fiber,也创建了a的sibling FC
4. 第4次performUnitOfWork
	1. beginWork 得到null
	2. completeUnitOfWork
		-  completeWork 创建a的dom 返回null
		- workInProgress = FC a的sibling 重新进performUnitOfWork
5. 第5次performUnitOfWork
	1. beginWork 得到div的fiber
6. 第6次performUnitOfWork
	1. beginWork 得到p的fiber,也创建了p的sibling span 重新进performUnitOfWork
7. 第7次performUnitOfWork
	1. beginWork 得到null
	2. completeUnitOfWork
		- completeWork 创建p的dom 返回null
		- workInProgress = span p的sibling
8. 第8次performUnitOfWork
	1. beginWork 得到null
	2. completeUnitOfWork
		- 第1次completeWork 创建span的dom 返回null，workInProgress = div span的return
		- 第2次completeWork 创建div的dom 返回null，workInProgress = FC div的return
		- 第3次completeWork 创建 返回null，workInProgress = main FC的return
		- 第4次completeWork 创建main的dom 返回null，workInProgress = App main的return
		- 第5次completeWork 创建 返回null，workInProgress = FiberRoot App的return
		- 第6次completeWork 创建 返回null，workInProgress = null FiberRoot的return


update

标记自己lanes
向上到hostrootfiber 标记childLanes
`fiber(<App />)`lanes 1
hostRootFiber childLanes 1

bailoutOnAlreadyFinishedWork用lanes判断

## fiber 对比更新

```js
<script type="text/babel">
   const root = ReactDOM.createRoot(document.getElementById('container'));
   class Header extends React.PureComponent {
     render() {
       return (
         <React.Fragment>
           <h1>title</h1>
           <h2>title2</h2>
         </React.Fragment>
       );
     }
   }
   class App extends React.Component{
     constructor(){
       super();
       this.state = {
         list: ['A', 'B', 'C'],
       }
     }
     add = ()=>{
       this.setState({ list: ['C', 'A', 'X'] })
     }
     render() {
       return (
         <React.Fragment>
           <Header />
           <button onClick={this.add}> add </button>
           <div className="content">
             {this.state.list.map(item => (
               <p key={item}>{item}</p>
             ))}
           </div>
         </React.Fragment>
       )
     }
   }
   root.render(<App />);
 </script>
```

1. 第1次 performUnitOfWork
	1. beginWork 本身不需要更新，子节点需要更新，bailoutOnAlreadyFinishedWork > cloneChildFibers ，返回`fiber(<App />)`
			clone 前 current.child === workInProgress.child 为true
			clone 后 current.child === workInProgress.child 为false
2. 第2次 performUnitOfWork
	1. beginWork > updateClassComponent 返回`fiber(<Header />)` 也创建了Header的sibling
3. 第3次 performUnitOfWork
	1. beginWork > updateClassComponent > bailoutOnAlreadyFinishedWork(本身和子节点都无需更新)返回null
	2. completeUnitOfWork
			completeWork workInProgress = `fiber(<button />)`
4. 第4次 performUnitOfWork
	1. beginWork 返回null
	2. completeUnitOfWork
			completeWork workInProgress = `fiber(<div />)`
5. 第5次 performUnitOfWork
	1. beginWork 返回 `fiber(<p>C</p>)`
6. 第6次 performUnitOfWork
	1. beginWork 返回null
	2. completeUnitOfWork
			completeWork workInProgress = `fiber(<p>A</p>)`
7. 第7次 performUnitOfWork
	1. beginWork 返回null
	2. completeUnitOfWork
			completeWork workInProgress = `fiber(<p>X</p>)`
8. 第8次 performUnitOfWork
	1. beginWork 返回null
	2. completeUnitOfWork
		1. completeWork 创建  `dom(<p>X</p>)` workInProgress = `fiber(<div />)`
		2. completeWork workInProgress = `fiber(<App />)`
		3. completeWork workInProgress = `HostRootFiber`
		4. completeWork workInProgress = null
	
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