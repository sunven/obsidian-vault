
- 内存空间由于某些原因没有被及时释放(回收)，
- 导致系统中出现了无法使用的内存块。
- 占用的内存空间也会越来越多，最终可能导致系统崩溃或者运行缓慢


- 全局变量
- 闭包
- 定时器
- dom 引用
	- 局部创建
	- 全局创建
- 循环引用
```js
function Obj() {
  this.obj = null;
}

var obj1 = new Obj();
var obj2 = new Obj();

obj1.obj = obj2;
obj2.obj = obj1;


obj1.obj = null;
obj2.obj = null;

```
- 事件监听器
- 缓存
	- map
	- WeakMap