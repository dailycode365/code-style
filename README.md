[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)

# 开发规范

[TOC]

## 命名规范篇

1. 文件名大写开头驼峰式

   ```
   AudioMgr.js, LoginScene.js
   ```

2. 文件夹小写开头驼峰式

   ```
   audioMgr, loginScene
   ```

3. 按钮回调事件,为方便识别，以 onBtnClick 开头

   ```javascript
   function onBtnClickLogin() {
   	console.log("onBtnClick");
   }
   ```

4. 常量全部大写，使用大写字母和下划线来组合命名，下划线用以分割单词

   ```javascript
   const MAX_COUNT = 10;
   const URL = "http://www.foreverz.com";
   ```

5. 函数小驼峰式命名，前缀应当为动词，语义化

   可参考如下：

   | 动词 | 含义                         | 返回值                                                |
   | ---- | ---------------------------- | ----------------------------------------------------- |
   | can  | 判断是否可执行某个动作(权限) | 函数返回一个布尔值。true：可执行；false：不可执行     |
   | has  | 判断是否含有某个值           | 函数返回一个布尔值。true：含有此值；false：不含有此值 |
   | is   | 判断是否为某个值             | 函数返回一个布尔值。true：为某个值；false：不为某个值 |
   | get  | 获取某个值                   | 函数返回一个非布尔值                                  |
   | set  | 设置某个值                   | 无返回值、返回是否设置成功或者返回链式对象            |
   | load | 加载某些数据                 | 无返回值或者返回是否加载完成的结果                    |

   ```javascript
   // 是否可阅读
   function canRead(): boolean {
   	return true;
   }
   // 获取名称
   function getName(): string {
   	return this.name;
   }
   ```

6. 类、构造函数，大驼峰式命名，前辍为名称，语义化

   ```javascript
   class Person {
     public name: string;
     constructor(name) {
       this.name = name;
     }
   }
   const person = new Person('mevyn');
   ```

7. 如果你的文件导出一个类，你的文件名应该与类名完全相同。

   ```javascript
   // file contents
   class CheckBox {}
   module.exports = CheckBox;
   // in some other file
   // bad
   var CheckBox = require("./checkBox");
   // bad
   var CheckBox = require("./check_box");
   // good
   var CheckBox = require("./CheckBox");
   ```

## 代码规范篇-ESLint

### ESLint 简介

ESLint 是在 ECMAScript/JavaScript 代码中识别和报告模式匹配的工具，它的目标是保证代码的一致性和避免错误。在许多方面，它和 JSLint、JSHint 相似，除了少数的例外：

- ESLint 使用 [Espree](https://github.com/eslint/espree) 解析 JavaScript。
- ESLint 使用 AST 去分析代码中的模式。
- ESLint 是完全插件化的。每一个规则都是一个插件并且你可以在运行时添加更多的规则。

### ESLint 安装

安装参考：https://cn.eslint.org/docs/user-guide/getting-started

### ESLint 规则

代码开发规则参考

- 英文版：https://github.com/airbnb/javascript
- 中文版：https://juejin.cn/post/6844903620648026120
- typescript-eslint: https://github.com/typescript-eslint/typescript-eslint/tree/master/packages/eslint-plugin/docs/rules

### 当前采用规则

此处设置多为关闭 airbnb-base 中的各别 rule

```json
{
	//开启的规则
	"extends": ["airbnb-base", "prettier"],
	//一个对Babel解析器的包装，使其能够与 ESLint 兼容
	"parser": "babel-eslint",
	//脚本在执行期间访问的额外的全局变量
	"globals": {
		"cc": true,
		"sp": true,
		"CC_EDITOR": true
	},
	//启用的规则及其各自的错误级别
	//"off"或0-关闭规则,
	//"warn"或1-开启规则，使用警告级别的错误：warn (不会导致程序退出),
	//"error"或2-开启规则，使用错误级别的错误：error (当被触发的时候，程序会退出)
	"rules": {
		//导入/无外部依赖项
		"import/no-extraneous-dependencies": 0,
		//导入/无循环依赖
		"import/no-cycle": "warn",
		//箭头函数的参数使用圆括号
		"arrow-parens": 0,
		//优先使用数组和对象解构
		"prefer-destructuring": 0,
		//禁止使用异步函数作为 Promise executor
		"no-async-promise-executor": "warn",
		//导入/首选默认导出
		"import/prefer-default-export": 0,
		//强制类方法使用 this
		"class-methods-use-this": 0,
		//禁用 console
		"no-console": 0,
		//"no-console": ["warn", { "allow": ["error", "warn"] }],
		//要求使用模板字面量而非字符串连接
		"prefer-template": "off",
		//禁用一元操作符 ++ 和 --
		"no-plusplus": 0,
		//禁止标识符中有悬空下划线
		"no-underscore-dangle": "off",
		//禁用嵌套的三元表达式
		"no-nested-ternary": "warn",
		//导入/未命名为默认
		"import/no-named-default": 0,
		//Forbid Webpack loader syntax in imports.
		"import/no-webpack-loader-syntax": 0,
		//导入扩展名
		"import/extensions": [
			"error",
			"always",
			{
				"ts": "never",
				"tsx": "never",
				"js": "never"
			}
		],
		//导入默认导出
		"import/default": "error",
		//禁止对函数参数再赋值
		"no-param-reassign": [
			"error",
			{
				"props": false
			}
		],
		//强制使用骆驼拼写法命名约定
		"camelcase": 0,
		//禁用按位运算符
		"no-bitwise": "off",
		//要求箭头函数体使用大括号
		"arrow-body-style": ["error", "as-needed"],
		//禁用特定的全局变量
		"no-restricted-globals": "off",
		//要求或禁止类成员之间出现空行
		"lines-between-class-members": [
			"error",
			"always",
			{
				"exceptAfterSingleLine": true
			}
		]
	},
	//覆盖
	"overrides": [
		{
			//匹配的特定文件
			"files": ["**/*.ts"],
			//将TypeScript转换成与estree 兼容的形式，以便在ESLint中使用
			"parser": "@typescript-eslint/parser",
			"parserOptions": {
				//使用的ECMAScript版本
				"ecmaVersion": 2018,
				//设置为"script"(默认)或"module"（如果你的代码是 ECMAScript 模块)。
				"sourceType": "module",
				//对不支持的ts版本给出警告
				"warnOnUnsupportedTypeScriptVersion": true
			},
			//第三方插件，定义额外的规则、环境和配置等
			"plugins": ["@typescript-eslint"],
			"rules": {
				//要求switch语句中有default分支
				"default-case": "off",
				//禁止类成员中出现重复的名称
				"no-dupe-class-members": "off",
				//禁用Array构造函数
				"no-array-constructor": "off",
				//This rule extends the base eslint/no-array-constructor rule. It adds support for the generically typed Array constructor (new Array<Foo>()).
				"@typescript-eslint/no-array-constructor": "warn",
				//Disallow the use of custom TypeScript modules and namespaces
				"@typescript-eslint/no-namespace": "error",
				//禁止在变量定义之前使用它们
				"no-use-before-define": "off",
				//This rule extends the base eslint/no-use-before-define rule. It adds support for type, interface and enum declarations.
				"@typescript-eslint/no-use-before-define": [
					"warn",
					{
						"functions": false,
						"classes": false,
						"variables": false,
						"typedefs": false
					}
				],
				//禁止出现未使用过的变量
				"no-unused-vars": "off",
				//This rule extends the base eslint/no-unused-vars rule. It adds support for TypeScript features, such as types.
				"@typescript-eslint/no-unused-vars": [
					"error",
					{
						"args": "none",
						"ignoreRestSiblings": true
					}
				],
				//禁用不必要的构造函数
				"no-useless-constructor": "off",
				// This rule extends the base eslint/no-useless-constructor rule. It adds support for:1.constructors marked as protected / private (i.e. marking a constructor as non-public),2.public constructors when there is no superclass,3.constructors with only parameter properties.
				"@typescript-eslint/no-useless-constructor": "warn",
				"import/extensions": 0,
				//Ensures an imported module can be resolved to a module on the local filesystem
				"import/no-unresolved": 0
			}
		}
	],
	"parserOptions": {
		//额外的语言特性
		"ecmaFeatures": {
			//允许装饰器写法
			"legacyDecorators": 1
		}
	}
}
```

### ESLint 配置文件

1. JavaScript - 使用 .eslintrc.js 然后输出一个配置对象。
2. YAML - 使用 .eslintrc.yaml 或 .eslintrc.yml 去定义配置的结构。
3. JSON - 使用 .eslintrc.json 去定义配置的结构，ESLint 的 JSON 文件允许 JavaScript 风格的注释。
4. (弃用) - 使用 .eslintrc，可以使 JSON 也可以是 YAML。
5. package.json - 在 package.json 里创建一个 eslintConfig 属性，在那里定义你的配置。

如果同一个目录下有多个配置文件，ESLint 只会使用一个。优先级顺序如下：

1.  .eslintrc.js
2.  .eslintrc.yaml
3.  .eslintrc.yml
4.  .eslintrc.json
5.  .eslintrc
6.  package.json

简要配置说明

```json
{
  "rules": {
  "semi": ["error", "always"],
  "quotes": ["error", "double"]
  }
}
"semi" 和 "quotes" 是 ESLint 中 规则 的名称。第一个值是错误级别，可以使下面的值之一：
"off" or 0 - 关闭规则
"warn" or 1 - 将规则视为一个警告（不会影响退出码）
"error" or 2 - 将规则视为一个错误 (退出码为1)
```

### ESLint 忽略文件

可以通过在项目根目录创建一个 .eslintignore 文件告诉 ESLint 去忽略特定的文件和目录。

### ESLint 临时禁止/开启规则

- 整个文件范围内启用或禁用规则出现警告（注释需要放在文件顶部）

  `/* eslint-disable */*`

  `/* eslint-enable */`

- 对指定的规则启用或禁用警告

  `/* eslint-disable no-alert, no-console */`

  `/* eslint-enable no-alert, no-console */`

- 在某一特定的行上禁用所有规则

  `/* eslint-disable-line */`

  `/* eslint-disable-next-line */`

- 在某一特定的行上禁用某个指定的规则

  `/* eslint-disable-line no-alert */`

  `/* eslint-disable-next-line no-alert */`

- 在某个特定的行上禁用多个规则

  `/* eslint-disable-line no-alert, quotes, semi */`

  `/* eslint-disable-next-line no-alert, quotes, semi */`

## 格式化篇-Prettier

### Prettier 简介

- 一个“有态度”的代码格式化工具
- 支持大量编程语言
- 已集成到大多数编辑器中
- 几乎不需要设置参数

### Prettier 安装

安装参考： https://prettier.bootcss.com/docs/install.html

### Prettier 配置文件

- "prettier" key in your package.json file.
- .prettierrc file written in JSON or YAML.
- .prettierrc.json, .prettierrc.yml, .prettierrc.yaml, or .prettierrc.json5 file.
- .prettierrc.js, .prettierrc.cjs, prettier.config.js, or prettier.config.cjs file that exports an object using module.exports.
- .prettierrc.toml file.

```javascript
{
  "trailingComma": "es5",
  "tabWidth": 4,
  "semi": false,
  "singleQuote": true
}
```

### Prettier 忽略文件

可以通过在项目根目录创建一个 .prettierignore 文件告诉 Prettier 去忽略特定的文件和目录。

## 自动化篇-ESLint-Stage/Husky

### Lint-Stage/Husky 简介

lint-staged 一个在 git 暂存文件上运行 linters 的工具。

husky 是一个为 git 增加 hook 的工具。

### 安装

安装参考：https://github.com/okonet/lint-staged#readme

安装前请先配置代码检验工具，lint-staged 会自动安装 husky

### 配置文件

可在 package.json 中直接配置

```json
{
	"lint-staged": {
		"*": "your-cmd"
	},
	"husky": {
		"hooks": {
			"pre-commit": "lint-staged"
		}
	}
}
```

参考例子

```json
"husky": {
  "hooks": {
    "pre-commit": "lint-staged"
  }
},
"lint-staged": {
  "*.{js,ts}": "eslint --cache --fix",
  "*.{js,css,md}": "prettier --write"
}
```

## Git 提交规范

commit message 是开发的日常操作, 写好 log 不仅有助于他人 review, 还可以有效的输出 CHANGELOG, 对项目的管理实际至关重要。

推荐工具：

1. commitizen
2. conventional-changelog
3. standard-version
4. commitlint

### Commit Message 格式

目前规范使用较多的是 Angular 团队的规范，它的 message 格式如下：

```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

如上这个结构, 大致分为三个部分(使用空行分割):

- 标题行: 必填, 描述主要修改类型和内容
- 主题内容: 描述为什么修改, 做了什么样的修改, 以及开发的思路等等
- 页脚注释: 放 Breaking Changes 或 Closed Issues

分别由如下部分构成:

- type: commit 的类型
- feat: 新特性
- fix: 修改问题
- refactor: 代码重构
- docs: 文档修改
- style: 代码格式修改, 注意不是 css 修改
- test: 测试用例修改
- chore: 其他修改, 比如构建流程, 依赖管理
- scope: commit 影响的范围
- subject: commit 的概述
- body: commit 具体修改内容, 可以分为多行
- footer: 一些备注, 通常是 BREAKING CHANGE 或修复的 bug 的链接

### commitizen

#### 工具简介

一个可以实现规范的**提交说明**的工具。

借助它提供的 git cz 命令替代我们的 git commit 命令, 帮助我们生成符合规范的 commit message。

#### 安装参考

https://github.com/commitizen/cz-cli

安装参考中的 cz-conventional-changelog 为符合 Angular 提交规范的适配器。

#### 使用说明

凡是用到 git commit 命令的时候统一改为 git cz,然后就会出现选项，生成符合格式的 Commit Message。

### conventional-changelog

#### 工具简介

是一款可以根据项目的`commit` 和 `metadata`信息自动生成 `changelogs` 和 `release notes`的系列工具。

#### 安装参考

```shell
npm install -g conventional-changelog
npm install -g conventional-changelog-cli
```

执行

```shell
npm ls -g -depth=0
```

检验上面两个工具是否安装成功，得到结果如下，表示成功：

```sh
/usr/local/lib
├── commitizen@2.9.6
├── conventional-changelog@1.1.7
├── conventional-changelog-cli@1.3.5
└── npm@5.5.1
```

#### 使用说明

```shell
conventional-changelog -p angular -i CHANGELOG.md -s
```

以上命令中参数`-p angular`用来指定使用的 commit message 标准

参数`-i CHANGELOG.md`表示从 CHANGELOG.md 读取 changelog, `-s` 表示读写 changelog 为同一文件。需要注意的是，上面这条命令产生的 changelog 是基于上次 tag 版本之后的变更（Feature、Fix、Breaking Changes 等等）所产生的，所以如果你想生成之前所有 commit 信息产生的 changelog 则需要使用这条命令：

```bash
conventional-changelog -p angular -i CHANGELOG.md -s -r 0
```

其中 `-r` 表示生成 changelog 所需要使用的 release 版本数量，默认为 1，全部则是 0。

### standard-version

#### 工具简介

一款遵循 语义化版本 semver 和 commit message 标准规范的版本和 changlog 自动化工具。

#### 安装参考

https://github.com/conventional-changelog/standard-version

#### 使用说明

```bash
standard-version
```

执行 standard-version 命令

##### –release-as, -r 指定版本号

默认情况下，工具会自动根据 主版本（major）,次版本（ minor） or 修订版（patch） 规则生成版本号，例如如果你 package.json 中的 version 为 1.0.0, 那么执行后版本号则是：1.0.1。自定义可以通过：

```bash
$ standard-version -r minor
# output 1.1.0
$ standard-version -r 2.0.0
# output 2.0.0
$ standard-version -r 2.0.0-test
# output 2.0.0-test
```

需要注意的是，这里的版本名称不是随便的字符，而是需要遵循语义化版本 semver 规范的。

##### –prerelease, -p 预发版本命名

用来生成预发版本, 如果当期的版本号是 2.0.0，例如

```bash
$ standard-version --prerelease alpha
# output 2.0.0-alpha.0
```

##### –tag-prefix, -t 版本 tag 前缀

用来给生成 tag 标签添加前缀，例如如果前版本号为 2.0.0，则：

```bash
$ standard-version --tag-prefix "stable-"
# output tag: stable-v2.0.0
```

还有其他选项可以通过 `standard-version --help` 查看。

### commitlint

#### 工具简介

校验提交说明是否符合规范。

#### 安装参考

https://commitlint.js.org/#/guides-local-setup

其中`@commitlint/config-conventional` 是符合 Angular 风格的校验规则

#### 使用说明

可配合 husky 使用。参考如下：

```json
{
	"husky": {
		"hooks": {
			"commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
		}
	}
}
```

### gitflow 工作流

#### 工具简介

git flow 定义了一个项目发布的分支模型，为管理具有预定发布周期的大型项目提供了一个健壮的框架，是由 Vincent Driessen 提出的一个 git 操作流程标准、解决当分支过多时 , 如何有效快速管理这些分支。

#### 安装说明

```ruby
brew install git-flow-avh
```

默认 git 中已安装有 git flow。

#### 使用说明

- git flow init：初始化一个现有的 git 库,将会设置一些初始的参数，如分支前缀名等，建议用默认值。
- git flow feature start [featureBranchName]: 创建一个基于 develop 的 feature 分支，并切换到这个分支之下。
- git flow feature publish [featureBranchName]：将 feature 分支上传至远端，也可以使用 git 的 push 命令
- git flow feature finish [featureBranchName]: 结束 feature 分支，并 merge 至 develop, 删除本地分支、远程分支(如已推送至仓库), 切换回 develop 分支。
- git flow release start [releaseBranchName]：开始准备 release 版本，从 develop 分支开始创建一个 release 分支。
- git flow release publish [releaseBranchName]：将 release 分支上传至远端, 也可以使用 git 的 push 命令。
- git flow release finish [releaseBranchName]：完成 release 测试，自动将代码 merge 到 master 和 develop 分支，用 release 分支名打 Tag，删除本地分支、远程分支(如已推送至仓库)。
- git flow hotfix start [hotfixBranchName]：基于 master 分支新建 hotfix 分支。
- git flow hotfix publish [hotfixBranchName]：将 hotfix 分支上传至远端, 也可以使用 git 的 push 命令。
- git flow hotfix finish [hotfixBranchName]：结束 hotfix 分支，并 merge 到 master 分支和 develop 分支, 自动打 tag,删除本地分支、远程分支(如已推送至仓库)。

#### 参考文档

1. https://www.jianshu.com/p/9d1c997b7613

### forking 工作流

#### 原理说明

forking 工作流不是使用单个服务端仓库作为『中央』代码基线，而让各个开发者都有一个服务端仓库。 这意味着各个代码贡献者有 2 个`git`仓库而不是 1 个：一个本地私有的，另一个服务端公开的。

`forking`工作流的一个主要优势是，贡献的代码可以被集成，而不需要所有人都能`push`代码到仅有的中央仓库中。 开发者`push`到自己的服务端仓库，而只有项目维护者才能`push`到正式仓库。 这样项目维护者可以接受任何开发者的提交，但无需给他正式代码库的写权限。

效果就是一个分布式的工作流，能为大型、自发性的团队（包括了不受信的第三方）提供灵活的方式来安全的协作。 也让这个工作流成为开源项目的理想工作流。

#### 工作方式及示例

参考文档：https://github.com/oldratlee/translations/blob/master/git-workflows-and-tutorials/workflow-forking.md

## 附录

### [Glob 模式](http://www.ruanyifeng.com/blog/2018/09/bash-wildcards.html)

| 模式              | 说明                                                           |
| ----------------- | -------------------------------------------------------------- |
| `*`               | 匹配除了斜杠(/)之外的所有字符。 Windows 上是斜杠(/)和反斜杠(\) |
| `**`              | 匹配零个或多个目录及子目录。不包含 `.` 以及 `..` 开头的。      |
| `?`               | 匹配任意单个字符。                                             |
| `[seq]`           | 匹配 seq 中的其中一个字符。                                    |
| `[!seq]`          | 匹配不在 seq 中的任意一个字符。                                |
| `\`               | 转义符。                                                       |
| `!`               | 排除符。                                                       |
| `?(pattern_list)` | 匹配零个或一个在 `pattern_list` 中的字符串。                   |
| `*(pattern_list)` | 匹配零个或多个在 `pattern_list` 中的字符串。                   |
| `+(pattern_list)` | 匹配一个或多个在 `pattern_list` 中的字符串。                   |
| `@(pattern_list)` | 匹配至少一个在 `pattern_list` 中的字符串。                     |
| `!(pattern_list)` | 匹配不在 `pattern_list` 中的字符串。                           |

### mrm 工具

#### 工具简介

命令行工具，以帮助您的开源项目保持配置（`package.json`，`.gitignore`，`.eslintrc`等等)同步。

特点：

- 如果您不想要它，不会覆盖您的数据
- 最小的更改：将保留原始文件格式或从 EditorConfig 中读取样式
- 最小配置：将尝试从项目本身或从环境推断配置
- 包含一堆可定制 任务
- 使用 JSON，YAML，INI，Markdown 和隔行格式文件的工具
- 容易编写属于你的任务
- 通过 npm 分享任务，并将它们分组到预设

#### 安装及使用

参考文档：https://github.com/chinanf-boy/mrm-zh

### 常用的 mrm-preset

Npm 地址：https://www.npmjs.com/package/@zpf518518/mrm-preset
