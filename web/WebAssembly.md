## Introduce

- 是一种二进制指令格式
- 用于基于堆栈的虚拟机
- Wasm 被设计为编程语言的可移植编译目标
- 可在网络上部署客户端和服务器应用程序
- 低级的类汇编语言
- 现代浏览器中附带了 WebAssembly 虚拟机

## WAT
WebAssembly 的文本格式，浏览器Response展示的格式

https://mbebenita.github.io/WasmExplorer/

https://webassembly.org/getting-started/developers-guide/
## Compile a WebAssembly module from…


WebAssembly.compile()
编译 WebAssembly 二进制代码到一个WebAssembly.Module 对象

WebAssembly.compileStreaming()
从一个流式的底层源编译一个WebAssembly.Module

```js
const module = await WebAssembly.compileStreaming(fetch(url))
const { exports } = await WebAssembly.instantiate(module, {})
```

可以替换为：

```js
  const {
    instance: { exports },
  } = await WebAssembly.instantiateStreaming(fetch(url), {})
  return exports
```

## Use the compiled WebAssembly…

## Inspect WebAssembly…