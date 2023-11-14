
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

  

vscode 安装 `ESLint` 插件：<https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint>

  

安装依赖`eslint-config-airbnb`：

  

```sh

npx install-peerdeps --dev eslint-config-airbnb

```

  

安装其它依赖：

  

```sh

yarn add @babel/eslint-parser @babel/preset-react eslint-config-prettier eslint-plugin-prettier prettier -D

```

  

老项目安装, 解决 eslint 不能识别别名问题：

  

```sh

yarn add eslint-import-resolver-custom-alias -D

```

  

添加`.prettierrc`文件：

  

```json

{

  "semi": false,

  "singleQuote": true

}

```

  

添加`.eslintrc`文件：

  

```js

{

  "parser": "@babel/eslint-parser",

  "env": {

    "browser": true

  },

  "extends": ["airbnb", "plugin:prettier/recommended"],

  "overrides": [

    {

      "env": {

        "node": true

      },

      "files": [".eslintrc"],

      "parserOptions": {

        "sourceType": "script"

      }

    }

  ],

  "parserOptions": {

    "sourceType": "module"

  },

  "settings": {

    "import/resolver": {

      "eslint-import-resolver-custom-alias": {

        "alias": {

          "@": "./src"

        },

        "extensions": [".js", ".jsx"]

      }

    }

  },

  "plugins": ["prettier"],

  "rules": {

    "prettier/prettier": "error",

    "react/jsx-filename-extension": 0,

    "react/prop-types": 0,

    "no-unused-vars": 0,

    "react/react-in-jsx-scope": 0

  }

}

```

  

添加/修改vscode配置文件`.vscode/settings.json`：

  

```json

{

  "[javascript][typescript][javascriptreact][typescriptreact]": {

    "editor.formatOnSave": false,

    "editor.codeActionsOnSave": {

      "source.fixAll": true

    }

  }

}

```

  

修改文件`config-overrides.js`, 禁用cra中的ESLint：

  

修改文件`package.json`, 增加scripts:

  

```json

{

  "scripts": {

    "lint": "eslint ./src",

    "lint:fix": "eslint ./src --fix"

  }

}

```

  

删除 `package.json` 中的 eslint, pretier 相关配置，避免与配置文件冲突：

  

## TODO

  

- [ ] WebStorm 环境配置

- [ ] react typescript 环境配置