

统一不同项目间的tslint规范，在此规范和react规范的基础上再出一份ts最佳实践的文档。

# mlz-lint
一个包含eslint，stylelint, tsconfig的配置文件合集。方便不同项目间统一和共享ts规范。
下面是在当前项目中新添加的配置。

#### Usage
- `npm i -D @mlz/lint`

- 在项目根目录新建tsconfig.json文件，并写入下面👇代码

```js
// tsconfig.json
{
  "extends": "./node_modules/@mlz/lint/tsconfig.json",
  "compilerOptions": {
    "baseUrl": ".", // 必填
    // 自定义
  },
}
``` 
- 在项目根目录新建tslint.json文件，并加入下面👇代码

```js
// tslint.json
{
  "extends": [
    "@mlz/lint/tslint.json", 
  ],
  "rules": {
    // 自定义
  }
}
``` 

#### tsconfig  
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


#### tslint

详情请见tslint.json


#### Prettier集成

- 安装vscode的Prettier插件”Prettier - Code formatter“
- 在在项目根目录下新建prettier.config.js文件
- 将如下配置放到文件中并保存
- 右键"Format Document"来帮助你完善代码风格

具体配置项请参考： https://prettier.io/docs/en/options.html#bracket-spacing

```js
// prettier.config.js
{
  module.exports = {
  ...require("@mlz/lint/prettier.config.js"),
  // 自定义
};
}
```


