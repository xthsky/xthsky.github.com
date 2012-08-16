---
layout: page
title: Bootstrap——快速开发Web应用的前端工具包
author: xthsky
---

Bootstrap是一个快速开发Web应用的前端工具包，它为开发者提供了下面三种工具。

* 基础：样式重置，栅格系统，响应式设计支持等
* 零件：按钮，导航，面包屑，分页，进度条，各种常用icon等
* 组件：对话框，下列菜单，tabs，浮出提示，轮播等

有了这样一套风格统一的基础工具、小零件、成品组件，快速搭建美观易用的Web应用会让你轻松不少。

Bootstrap开源不久，很快就成为GitHub上最热门的项目之一。许多开发者们也把它应用在了自己维护的站点上。事实上，在Bootstrap推出前，前端工具包已经有很多了，也不乏非常流行的如 jQuery + jQuery UI, YUI 等。为什么Bootstrap依然能脱颖而出呢？我们先大致看下它是怎么设计的吧。

Bootstrap现在已经发布了2.0版本，架构更加清晰。其核心部分是在less.css的基础上构建的，入口文件有2个，bootstrap.less 和 responsive.less 。后者是Bootstrap实现响应式设计的配置文件；前者是它的主入口文件，依序包含了下面几部分：

1. CSS Reset
2. Core variables and mixins
3. Grid system and page structure
4. Base CSS
5. Components
6. Utilities

这里第1，第3部分是许多其他前端工具包都有的部分，Bootstrap也提供了自己的版本。

第2部分是less.css扩展的变量、混入功能的应用。它为Bootstrap提供了最大的灵活性，给二次开发带来了许多便利。这是许多其他前端工具包所没有的优势。

第4，第5部分是Twitter贡献的各种零部件风格。其中4是各种基础元素——字型、表单、表格等。而第5部分是各种自定义零部件，其中有十分全面的图标，有各种按钮，以及各种复杂的组件风格等。

Bootstrap发布的是less编译后的文件，bootstrap.css 与 bootstrap-responsive.css。另外，Bootstrap还提供了一些自己风格的jQuery插件。

用户使用时，只要依葫芦画瓢，按Bootstrap提供的demo，写上同样的class，美观、统一的页面就生成了。得益于Bootstrap零部件的全面，只关心html，无需在htlml/css/js间切换，给页面开发带来一气呵成的快感。如果你要自定义风格，修改几个less变量即可实现，极大地解放了生产力。

当然，Bootstrap还有许多其他优点，比如文档丰富、跨平台、社区发展势头好等，这些都可以让开发者放心大胆地选择Bootstrap。
