
> [!NOTE] Function Components Different from Classes
> <https://overreacted.io/how-are-function-components-different-from-classes/>
><https://codesandbox.io/s/pjqnl16lm7>
> 本质是this问题
> UI在概念上是展示当前应用状态的一个函数
> 如何解决：
> - 缓存（解构、闭包）
> - bind 不能解决
> 	- 因为this没变，是this上面得prop变了
> 	- ![[Pasted image 20230316160540.png]]
> - 后面例子为啥非要用ref，message不是会变吗
