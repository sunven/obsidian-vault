
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


