# javascript transpiler

源到源的编译器

将一种高级编程语言的程序代码翻译成另一种高级编程语言

ts > js

```text
Code --(parse)--> AST --(transform)--> AST --(generate)--> Code
```

oxc

Babel
- js

esbuild
- go
- bundler

swc
- rust
- minifier  bundler

minifier
用于压缩代码的工具。通常，它们会删除代码中的所有不必要的字符（如空格、换行、注释等），并尽可能地缩短变量名和函数名，以降低文件大小，从而提高页面加载速度。另外，某些压缩工具还提供了例如删除未使用的代码、优化代码逻辑等高级功能。
- UglifyJS
- Terser

Bundler
是一种可以把多个文件合并成一个或几个文件的工具，通常在前端项目中用来处理 JavaScript、CSS、HTML和图片等文件。在这个过程中，它能够解决文件依赖的问题，并且还可以和其他工具（如转译器或压缩工具）配合，实现代码转译、压缩或其他功能。
- Webpack
- Rollup
- Parcel