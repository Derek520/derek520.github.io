---
layout: post
title: Pycharm扩展JS检查插件ESLint
categories:
  - Pycharm
description: Pycharm扩展JS检查插件ESLint
keywords: Pycharm,JS,ESLint,javascript
comments: true
---


# Pycharm扩展JS检查插件ESLint

ESLint 是用来检查我们写的 JavaScript 代码是否满足指定规则的静态代码检查工具

通过用 ESLint 来检查一些规则，我们可以：

* 统一代码风格规则，如：代码缩进用几个空格；是否用驼峰命名法来命名变量和函数名等。
减少错误， 如：相等比较必须用 === ，变量在使用前必须被声明，在条件语句中不能使用赋值语句等。
* 提高代码质量，如：函数最多有多少条件分支；最多有几个参数，代码块最多能嵌套多少层等。
* 其他。如： 禁用 alert。这可以提高用户体验，因为 alert 框的外观不是那么好看，而且往往与网站的风格不搭，一般都会自定义 alert 框。

JSHint 和 JSLint 也是静态代码检查工具，但 ESLint 比它们功能强大也更灵活。

ESLint 是用 Node.js 写的，可以通过 npm 来安装。ESLint 也可以在 webpack(eslint-loader) 和 Gulp.js(gulp-eslint) 中使用。

### 打开Pycharm终端本地或者本地终端，安装ESLint
```
npm install -g eslint
```
![eslint00](/images/posts/Pycharm/eslint00.png)
> /home/kuture/.npm/lib/node_modules/eslint/bin/eslint.js为安装路径

如果安装报错，使用以下命令创建安装路径，并重新进行安装
```
npm config set prefix ‘~/.npm’
```
### 打开Pycharm添加ESLint
File->Setting->Languages & Frameworks->ESLint
![eslint00](/images/posts/Pycharm/eslint01.png)

> ESLint package路径为之前的安装路径写到eslint包即可






