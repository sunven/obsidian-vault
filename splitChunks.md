https://stackoverflow.com/questions/50127185/webpack-what-is-the-difference-between-all-and-initial-options-in-optimizat

# 1

同步导入

``` js
import "./my-static-module-0";
```

异步导入
```js
import("./my-dynamic-module-0");
```

async
- 异步模块必定生成单独chunk
- 异步模块中使用同步模块，这个同步模块也生成单独chunk

initial
- 异步模块必定生成单独chunk
- 异步模块中使用同步模块，这个同步模块生成在异步模块的chunk中，不是单独的
- initial且单入口，模块被多次在不同文件中引用，实际是一次引用，minChunks > 2 不会生效