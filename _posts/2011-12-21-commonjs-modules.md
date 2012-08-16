---
layout: page
title: CommonJS Modules/1.1.1笔记
author: xthsky
---

先简单说明下CommonJS模块。每个模块都有对应的标示符，而标示符有两种：相对标示符与绝对标示符。模块的上下文中，有require、exports以及module三个变量。

模块的引入是通过模块中的require函数完成的，参数是要引入的模块标示符，返回值是被引入模块暴露的API。require可以有一个main属性，这个属性是只读的，一般指向主模块的”module”对象（没有主模块时为undefined）。比如，在nodejs环境中，你可以使用require.main === module来判断当前模块是否为主模块。如果不是沙箱环境，require还可以有一个paths属性，这个属性是一个字符串数组，内容是顶级标示符对应的模块查找目录。paths属性是全局唯一的，对它的修改会影响模块的搜索行为。需要注意的是，paths内容的格式是由模块的loader程序决定的，规范没有统一规定。

模块引入部分最让我费解的是模块出现循环依赖时的处理方式。不过，在承玉同学的帮助下，终于搞明白了。比如下面的例子：

a.js

    exports.done = false;
    var b = require(‘./b.js’);
    exports.done = true;

b.js

    var a = require(‘./a.js’);
    console.log(‘in b, a.done = %j’, a.done);

如果直接运行a.js，在b.js中引入模块a时，a实际上并没有完全执行。这个时候，按规范的要求，require至少会返回被require时已经执行的部分，这里是exports.done = false。因此，这段代码会输出“in b, a.done = false”。（如果你有兴趣，可以用nodejs测试一下循环依赖的问题。不过需要注意，在nodejs中，模块在第一次执行后，会被缓存下来）

与引入相反，模块向外界暴露API是通过exports对象实现的。

模块最后一个属性：”module”有一个必选属性”id”和一个可选属性”uri”。模块的id的值是改模块的顶级标示符，这个值是只读的。而”uri”属性指向该模块所在的资源文件的URI。在沙箱环境里是没有”uri”属性的。

模块的标示符是一个字符串，内容是由’/'分割的”terms”，每个”term”都是驼峰式的标示符、”.”或”..”。如果标示符以”.”或”..”开始，该标示符就是相对标示符。相对标示符是相对调用”require”的模块，顶级标示符是相对于模块的根命名空间。最后一点，标示符可以没有”.js”这样的文件后缀。

个人感觉顶级标示符这里，规范的解释并不是很清晰，使用时还是应该以模块的loader为准。

整体看下来，Modules/1.1.1规范还有不少不清楚或有争议的地方，这个在CommonJS的wiki里也承认。不过模块的组织思想应该不会变了。人们的实践也走在了规范的前面，比如seajs 
