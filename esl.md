## 适用环境

- react js
- vscode
## 思路

ESLint将弃用代码风格相关规则: <https://eslint.org/blog/2023/10/deprecating-formatting-rules/>
  
- 不能与项目耦合（cra）
- Prettier 负责代码风格
- ESLint 负责代码检查

### 如何简化配置

继承一套通用配置：[eslint-config-airbnb](https://www.npmjs.com/package/eslint-config-airbnb)
参考一个知名项目：[ant-design](https://github.com/ant-design/ant-design/blob/master/.eslintrc.js)

  

### ESlint 与 Prettier 的冲突与协作

关闭所有不必要或可能与 Prettier 冲突的规则：[eslint-config-prettier](https://www.npmjs.com/package/eslint-config-prettier)
将Prettier作为ESLint规则运行，并将差异报告为单独的ESLint问题：[eslint-plugin-prettier](https://www.npmjs.com/package/eslint-plugin-prettier)
## 实现

安装依赖`eslint-config-airbnb`

```sh
npx install-peerdeps --dev eslint-config-airbnb
```

安装

```sh
yarn add @babel/eslint-parser @babel/preset-react eslint-config-prettier eslint-plugin-prettier prettier -D
```

删除 package.json 中的 eslint pretier 相关配置，避免与配置文件冲突