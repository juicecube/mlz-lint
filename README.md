

统一不同项目间的tslint规范，在此规范和react规范的基础上再出一份ts最佳实践的文档。

# mlz-lint
一个包含eslint，stylelint, tsconfig的配置文件合集。方便不同项目间统一和共享ts规范。

## tsconfig  
|  配置  | 值 | 原因 |
|  ----  | ----  | ---- |
| target  | es2015 | 保留import语法，以便实现模块按需加载，配合`@babel/preset-env`
| noImplicitAny  | true | 类型安全更加严格
| strictNullChecks  | true | null 和 undefined检查，避免错误
| noUnusedLocals  | true | 不需要不用的变量
| moduleResolution  | node | 模块解析策略

#### tslint

|  配置  | 值 | 原因 |
|  ----  | ----  | ---- |
| no-parameter-reassignment  | true | 禁止对函数的参数重新赋值
| prefer-object-spread  | true | `object-spread`比`Object.assign`ts类型检查更完善
| comment-format  | true | 限制单行注释的规则为空格开头
| object-literal-shorthand  | true | 必须使用 `a = {b}` 而不是 `a = {b: b}`
| no-magic-numbers  | `[true, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 100, 1000, 10000, 200]` | 禁止使用魔法数字，仅允许使用一部分白名单中的数字，魔法数字无法理解
| object-curly-spacing  | true | 保持大括号内的空格一致性


#### Usage
- `npm i -D mlz-lint`

- 
```js
// tsconfig.json
{
  "extends": "./node_modules/mlz-lint/tsconfig.json",
  "compilerOptions": {
    // 自定义
  }
}

// tslint.json
{
  "extends": [
    "mlz-lint/tslint.json", 
  ],
  "rules": {
    // 自定义
  }
}
``` 

#### Prettier集成



