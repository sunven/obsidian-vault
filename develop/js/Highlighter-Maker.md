
## 核心问题：

- 高亮选中
- 持久化、还原

```js
{
	collapsed: false,
	endContainer: text, // nodeType 3
	endOffset: 5,
	startContainer: text, // nodeType 3
	startOffset: 2,
}
```


childNodes  返回节点
children 返回元素

splitText

入参：要中断文本节点之前的索引
返回：节点包含指定偏移点之后的文本

```html
<p>Document.createRange()</p>
<p><m>Document</m>.createRange()</p>
<p><m>Do<m>cu
</m>ment</m>.createRange()</p>
```

$0 的 childNodes 有1个，即：$0.childNodes[0] 为 Document.createRange()
执行 $0.childNodes[0].splitText(2)
$0 的 childNodes 有2个
$0.childNodes[0] 为 Do
$0.childNodes[1] 为 cument.createRange()


获取选中的 textNode

```html
// 选中 me
<p>Document.createRange()</p>
// 选中 d R
<span>method</span> <span>Range objects</span>
// 选中 eD
<div>
	the
	<p>Document</p>
</div>
```


标识 DOM 节点：
- 使用 xPath
- 使用 CSS Selector 语法
- 使用 tagName + index


```js
{tagName, index, childIndex}
```

问题：
- 下次访问时，程序必须按上次用户高亮的顺序还原。
- 用户不能随意取消（删除）高亮区域，只能按添加顺序从后往前删

都会改变childNodes，导致定位不准确