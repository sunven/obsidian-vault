
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


selectionchange不会冒泡
Document API 与 HTMLInputElement API 有区别
```js
// <input type="text" rows="2" cols="20" id="mytext" />
const myinput = document.getElementById('mytext')
myinput.addEventListener('selectionchange', () => {
  const { selectionStart, selectionEnd, selectionDirection } = myinput
  console.log('Document API', selectionStart, selectionEnd, selectionDirection)
})
document.addEventListener('selectionchange', () => {
	// 目前Firefox支持
  console.log('HTMLInputElement API', document.getSelection())
})
```

window.event
只读的 Window 属性 event 返回当前由站点代码处理的事件。在事件处理程序之外的上下文中，该值始终为 undefined。
```js
console.log(1, window.event
document.addEventListener('DOMContentLoaded', () => 
  console.log(2, window.event
}
console.log(3, window.event)
```

## Proxy
```js
const arr = [1, 2, 3, 4]
const p = new Proxy(arr, {
  get(target, prop, receiver) {
    const value = Reflect.get(target, prop, receiver)
    console.log('get', prop, value)
    return value
  },
  set(target, prop, value, receiver) {
    console.log('set', prop, value)
    Reflect.set(target, prop, value, receiver)
    return true
  },
})
p.splice(1, 1)
// get splice ƒ splice() { [native code] }
// get length 4
// get constructor ƒ Array() { [native code] }
// get 1 2
// get 2 3
// set 1 3
// get 3 4
// set 2 4
// set length 3
```
- vue?
- p.splice(1, 1, 5, 6)
	- 先把删除位置后面的元素，放到未来准确位置（从后往前先4再3 ...）
	- 在设置新元素