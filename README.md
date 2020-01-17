
# mlz-lint
一个包含eslint（内置tslint规则）、stylelint、tsconfig、prettier的配置文件合集。方便不同项目间统一和共享lint规范。

## Installation

`npm i -D @mlz/lint`

#### 1、安装相应的代码检查工具
以下根据实际情况选择性安装

- `npm i -D eslint stylelint typescript`

#### 2、安装编辑器对应插件

--- 
## Usage
mlz-lint的使用有两种方式
#### 一、通过 `yuumi` 插件安装使用（待补充）

#### 二、项目直接继承 `mlz-lint` 配置

- typescript：在项目根目录新建 `tsconfig.json` 文件，并写入下面👇代码

```js
// tsconfig.json
{
  "extends": "@mlz/lint/tsconfig.json",
  "compilerOptions": {
    "baseUrl": ".", // 必填
    // 自定义
  }
}
``` 
- eslint（内置tslint规则）：在项目根目录新建 `.eslintrc.js` 文件，并加入下面👇代码

```js
// .eslintrc.js
module.exports = {
  "extends": "./node_modules/@mlz/lint/ts-eslintrc.js",
  "rules": {
    // 自定义
  }
}
``` 

- eslint && react(内置tslint规则) ：在项目根目录新建 `.eslintrc.js` 文件，并加入下面👇代码
```js
// .eslintrc.js
module.exports = {
  "extends": "./node_modules/@mlz/lint/ts-eslintrc-react.js",
  "rules": {
    // 自定义
  }
}
```

- stylelint：在项目根目录新建 `.stylelintrc.json` 文件，并加入下面👇代码（注意配置 `.stylelintignore` 文件，可参照本项目 `.stylelintignore` 文件）

```js
// .stylelintrc.json
{
  "extends": "@mlz/lint/stylelintrc.json",
  "rules": {
    // 自定义
  }
}
```

#### 不生效可能原因及解决方法：
- 1、eslint未启用或执行报错：

  调出eslint控制台（点击vscode右下角eslint打开控制台， 如找不到，则，点击左下角设置按钮 --> 选择setting --> 输入eslint --> 把 ```Eslint:Always Show Status``` 和 ```Eslint:Enable```勾选上 --> 点击任意js或ts文件则会出现，若还未出现请升级vscode版本），查看是否执行过程中出现错误


- 2、vscode版本过低（请升级到1.41.1或以上）

  mac中如果遇到无法升级，则确认```vscode```是否在应用程序中，如不在则手动把```vscode```移到应用程序中方可进行升级

---
## AutoFix

1、打开编辑器设置文件（以vscode为例）：
```js
command + P  -->  输入setting  --> 选择 settings.json文件
```

2、在文件中添加如下代码并保存：
```js
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true,
    "source.fixAll.stylelint": true,
  },
```
3、修改文件后保存，便会自动修复空格、顺序等风格问题

---
## 配置说明
++++++

该项目中的配置为公司前端统一配置，除一些标明可自定义的配置外，其他配置最好不要随意更改，以保持前端代码风格的统一

++++++
#### tsconfig  

详情请见：tsconfig.json

|  配置  | 值 | 原因 |
|  ----  | ----  | ---- |
| target  | es2015 | 保留import语法，以便实现模块按需加载，配合`@babel/preset-env`
| module | commonjs | 使用commonjs的方式组织代码
| lib | ["dom", "es2015", "es2016.array.include"] | 把这些库文件包含进编译的过程中保证编译的正确快速执行
| allowJs  | true | 允许检查js文件，保证js文件的质量
| checkJs  | true | 允许ts检查js文件的错误，保证js文件的质量
| jsx  | preserve | 输出.jsx且dom编译后还是原dom方便后续babel等编译
| sourceMap  | true | 输出.map文件，方便调试
| outDir  | build | 指定输出目录为build
| removeComments  | true | 删除编译后的所有的注释（使代码安全简洁，减少代码量）
| noImplicitAny  | true | 类型安全更加严格（强制类型检验）
| strictNullChecks  | true | null 和 undefined检查，避免错误（严格空校验）
| noUnusedLocals  | true | 不需要不用的变量
| noImplicitReturns  | true | 函数的所有路径都必须有返回值
| moduleResolution  | node | 使用node的模块解析策略
| baseUrl | . | 把tsconfig所在的目录当成是解析非相对模块的基准目录
| paths | - | 模块名到基于 baseUrl 的路径映射的列表
| allowSyntheticDefaultImports | true | 允许从没有设置默认导出的模块中默认导入
| experimentalDecorators | true | 启用装饰器

#### eslint

详情请见ts-eslintrc.js、ts-eslintrc-react.js

#### stylelint

官方标准 + 些许自定义，详情请见：
- [官方](https://github.com/stylelint/stylelint-config-standard/blob/master/index.js#L15:5)

-  自定义： 详见`stylelintrc.json`

