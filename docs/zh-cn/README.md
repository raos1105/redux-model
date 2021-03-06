Redux Model是为了弥补原生Redux繁琐的开发流程，开发者重复劳动效率低下，模板文件导致代码量臃肿，以及因action和reducer文件分散造成代码追踪困难的问题而设计的。

众多知名的状态管理框架，基本都是为JS用户设计的。离散的代码结构、严格的设计模式、不合时宜的细节封装，都意味着想完美融入TypeScript，就必须经常手动注入类型。而Redux Model专门为Typescript设计，强健的自动推导能力，允许类型一次注入，到处使用。

[![License](https://img.shields.io/github/license/redux-model/redux-model)](https://github.com/redux-model/redux-model/blob/master/LICENSE)
[![GitHub Workflow Status (branch)](https://img.shields.io/github/workflow/status/redux-model/redux-model/CI/master)](https://github.com/redux-model/redux-model/actions)
[![Codecov](https://img.shields.io/codecov/c/github/redux-model/redux-model)](https://codecov.io/gh/redux-model/redux-model)

总的来说，模型拥有以下特性：

* 深度封装，超高开发效率
* 使用mvvm快速处理reducer
* **👍真正意义上的Typescript框架，写起来和JS一样流畅**
* 内置http服务，请求action自带loading追踪、节流
* React/Vue Hooks
* 数据持久化

!> 只有使用vscode编辑器开发项目，才能发挥TS的最大优势
