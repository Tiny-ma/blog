---
title: webpack入门学习
date: 2019-03-31 12:43:46
tags:
---

## 前言

现如今，前端工作从传统网站到SPA再到同构JavaScript,前端工程师的工作内容不断加重，客户端逻辑不断复杂化。原始的开发流程早已不能满足现状，故web开发者们开始尝试在开发、测试和部署等各个环节寻求更高效的协作方式。

前端后端分离似乎就是为了解决这个问题。

前后端分离的核心是解耦，从开发、测试以及部署3个方面入手，从而提高工作效率。

前端端分离策略是前端工程化解决方式的方针之一。前端工程化的目的是实现更合理、更便利的前后端分离的开发环境。

目前市场上流行的前端工具大体分为3类：

1. 工作流管理工具，比如Grunt、Gulp.
2. 构建工具，比如webpack、rollup.
3. 整体解决方案，比如FIS、WebFlow.

这次，主要介绍webpack基本介绍

## webpack基本概念

基于前端模块的思想，为了保持实现每个模块功能单一、模块间耦合度低，我们的程序基本上是会分为几个甚至几十个更多的文件。从而使用打包工具进行打包封装，就比如是把一张张的纸张，通过整理装订成为书籍。

> 本质上，webpack 是一个现代 JavaScript 应用程序的静态模块打包工具。

来看一下webpack的核心概念：
- 入口(entry)
- 输出(output)
- loader
- 插件(plugin)
- 模式(mode)


### 入口(entry)

入口，是文件执行的起始部分，可以理解成，程序执行的入口。

配置文件中的字段是**entry**，默认值是 ./src/index.js

> 用法：entry: {[entryChunkName: string]: string|Array<string>}

``` JavaScript
module.exports = {
  entry: './path/to/my/entry/file.js'
};
```

### 输出(output)

告诉 webpack 在哪里输出它所创建的 bundle，以及如何命名这些文件。

配置文件中的字段是**output**，默认值是 ./dist/main.js

``` JavaScript
const path = require('path');

module.exports = {
  entry: './path/to/my/entry/file.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'my-first-webpack.bundle.js'
  }
};
```
而在多入口文件，由于输出只能有一个，因此输出可以用占位符

模板 |	描述|
--- | --- |
[hash] | 模块标识符(module identifier)的 hash |
[chunkhash] | chunk 内容的 hash |
[name] | 模块名称 |
[id] | 模块标识符(module identifier) |
[query] | 模块的 query，例如，文件名 ? 后面的字符串 |
[function] | The function, which can return filename [string]

### [loader](https://webpack.docschina.org/loaders/)

webpack 本身只能理解 JavaScript 和 JSON 文件。

loader 让 webpack 能够去处理其他类型的文件，并将它们转换为有效 模块，以供应用程序使用，以及被添加到依赖图中。

在 webpack 的配置中 loader 有两个属性：
- test 属性，用于标识出应该被对应的 loader 进行转换的某个或某些文件。
- use 属性，表示进行转换时，应该使用哪个 loader。

``` JavaScript
const path = require('path');

module.exports = {
  output: {
    filename: 'my-first-webpack.bundle.js'
  },
  module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  }
};
```

### [插件(plugin)](https://webpack.docschina.org/plugins/)

loader 用于转换某些类型的模块，而插件则可以用于执行范围更广的任务。包括：打包优化，资源管理，注入环境变量。

``` JavaScript 
const HtmlWebpackPlugin = require('html-webpack-plugin'); // 通过 npm 安装
const webpack = require('webpack'); // 用于访问内置插件

module.exports = {
  module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
};
```

### 模式(mode)

通过选择 development, production 或 none 之中的一个，来设置 mode 参数，你可以启用 webpack 内置在相应环境下的优化。其默认值为 production。

``` JavaScript 
module.exports = {
  mode: 'production'
};
```

选项 |	描述 |
--- | --- |
development | 会将 DefinePlugin 中 process.env.NODE_ENV 的值设置为 development。启用 NamedChunksPlugin 和 NamedModulesPlugin。|
production | 会将 DefinePlugin 中 process.env.NODE_ENV 的值设置为 production。启用 FlagDependencyUsagePlugin, FlagIncludedChunksPlugin, ModuleConcatenationPlugin, NoEmitOnErrorsPlugin, OccurrenceOrderPlugin, SideEffectsFlagPlugin 和 TerserPlugin。|
none | 退出任何默认优化选项 |

## 总结

以上便是webpack里的最基本的核心思想。理解后便能基本使用webpack。

个人推荐在官网上进入深度学习:

[官网指南](https://webpack.docschina.org/guides/installation/)


后记：要谨记工程化是为了解决前端问题，而webpack是前端实现工程化的一种工具，而不代表工程化本身。
