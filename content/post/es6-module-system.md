+++
categories = [""]
date = "2016-03-28T10:14:24Z"
description = ""
keywords = []
title = "[转] ES6 的模块系统（附CommonJS & AMD 相关）"

+++

> [原文](https://segmentfault.com/a/1190000003410285) by [Jury Xiong's Blog](https://segmentfault.com/blog/juryxiong) 依照[知识共享署名-相同方式共享 3.0 中国大陆许可协议](http://creativecommons.org/licenses/by-sa/3.0/cn/)发布

此文为翻译，原文地址在这儿：https://hacks.mozilla.org/2015/08/es6-in-depth-modules/

ES6 是 ECMAScript 第 6 版本的简称，这是新一代的 JavaScript 的标准。[ES6 in Depth][] 是关于 ES6 的一系列新特性的介绍。

遥想 2007 年，笔者开始在 Mozilla 的 JavaScript 团队工作的时候，那个时候典型的 JavaScript 程序只有一行代码。

两年之后， Google Map 被发布。但是在那之前不久，JavaScript 的主要用途还是表单验证，当然啦，你的`<input onchange=>`处理器平均来说只有一行。

事过情迁，JavaScript 项目已经变得十分庞大，社区也发展出了一些有助于开发可扩展程序的工具。首先你需要的便是模块系统。模块系统让你得以将你的工作分散在不同的文件和目录中，让它们之前得以互相访问，并且可以非常有效地加载它们。自然而然地，JavaScript 发展出了模块系统，事实上是多个模块系统（AMD，CommonJS，CMD，译者注）。不仅如此，社区还提供了包管理工具（NPM，译者注），让你可以安装和拷贝高度依赖其他模块的软件。也许你会觉得，带有模块特性的 ES6，来得有些晚了。


模块基础
--------

一个 ES6 的模块是一个包含了 JS 代码的文件。ES6 里没有所谓的 `module` 关键字。一个模块看起来就和一个普通的脚本文件一样，除了以下两个区别：

ES6 的模块自动开启严格模式，即使你没有写 `'use strict'`。
你可以在模块中使用 `import` 和 `export`。
让我们先来看看 `export`。在模块中声明的任何东西都是默认私有的，如果你想对其他模块 Public，你必须 `export` 那部分代码。我们有几种实现方法，最简单的方式是添加一个 `export` 关键字。

```Node
// kittydar.js - Find the locations of all the cats in an image.
// (Heather Arthur wrote this library for real)
// (but she didn't use modules, because it was 2013)

export function detectCats(canvas, options) {
  var kittydar = new Kittydar(options);
  return kittydar.detectCats(canvas);
}

export class Kittydar {
  ... several methods doing image processing ...
}

// This helper function isn't exported.
function resizeCanvas() {
  ...
}
...
```

你可以在 `function`、`class`、`var`、`let` 或 `const` 前添加 `export`。

如果你想写一个模块，有这些就够了！再也不用把代码放在 IIFE 或者一个回调函数里了。既然你的代码是一个模块，而非脚本文件，那么你生命的一切都会被封装进模块的作用域，不再会有跨模块或跨文件的全局变量。你导出的声明部分则会成为这个模块的 Public API。

除此之外，模块里的代码和普通代码没啥大区别。它可以访问一些基本的全局变量，比如 `Object` 和 `Array`。如果你的模块跑在浏览器里，它将可以访问 `document` 和 `XMLHttpRequest`。

在另外一个文件中，我们可以导入这个模块并且使用 `detectCats()` 函数：

```Node
// demo.js - Kittydar demo program

import {detectCats} from "kittydar.js";

function go() {
    var canvas = document.getElementById("catpix");
    var cats = detectCats(canvas);
    drawRectangles(canvas, cats);
}
```

要导入多个模块中的接口，你可以这样写：

```Node
import {detectCats, Kittydar} from "kittydar.js";
```

当你运行一个包含 `import` 声明的模块，被引入的模块会先被导入并加载，然后根据依赖关系，每一个模块的内容会使用深度优先的原则进行遍历。跳过已经执行过的模块，以此避免依赖循环。

这便是模块的基础部分，挺简单的。


导出表
------

如果你觉得在每个要导出的部分前都写上 export 很麻烦，你可以只写一行你想要导出的变量列表，再用花括号包起来。

```Node
export {detectCats, Kittydar};

// no `export` keyword required here
function detectCats(canvas, options) { ... }
class Kittydar { ... }
```

导出表不一定要出现在文件的第一行，它可以出现在模块顶级作用域中的任何一行。你可以写多个导出表，也可以在列表中再写上其他 `export` 声明，只要没有变量名被重复导出即可。

重名命导出和导入
----------------

如果导入的变量名恰好和你模块中的变量名冲突了，ES6 允许你给你导入的东西重命名：

```Node
// suburbia.js

// Both these modules export something named `flip`.
// To import them both, we must rename at least one.
import {flip as flipOmelet} from "eggs.js";
import {flip as flipHouse} from "real-estate.js";
...
```

类似地，你在导出变量的时候也能重命名。这个特性在你想将同一个变量名导出两次的场景下十分方便，举个栗子：

```Node
// unlicensed_nuclear_accelerator.js - media streaming without drm
// (not a real library, but maybe it should be)

function v1() { ... }
function v2() { ... }

export {
  v1 as streamV1,
  v2 as streamV2,
  v2 as streamLatestVersion
};
```

默认导出
--------

新一代的标准的设计理念是兼容现有的 `CommonJS` 和 `AMD` 模块。所以如果你有一个 Node 项目，并且刚刚执行完 `npm install lodash`，你的 ES6 代码可以独立引入 Lodash 中的函数：

```Node
import {each, map} from "lodash";

each([3, 2, 1], x => console.log(x));
```

然而如果你已经习惯了 `_.each` 或者看不见 `_` 的话就浑身难受，当然这样使用 Lodash 也是不错的方式。

这种情况下，你可以稍微改变一下你的 import 写法，不写花括号：

```Node
import _ from "lodash";
```

这个简写等价于 `import {default as _} from "lodash";`。所有 `CommonJS` 和 `AMD` 模块在被 ES6 代码使用的时候都已经有了默认的导出，这个导出和你在 `CommonJS` 中 `require()` 得到的东西是一样的，那就是 `exports` 对象。

ES6 的模块系统被设计成让你可以一次性引入多个变量。但对于已经存在的 CommonJS 模块来说，你能得到的只有默认导出。举个栗子，在撰写此文之时，据笔者所知，著名的 [colors](https://github.com/Marak/colors.js) 模块并未特意支持 ES6。这是一个由多个 CommonJS 模块组成的模块，正如 npm 上的那些包。然而你依然可以直接将其引入到你的 ES6 代码中。

```Node
// ES6 equivalent of `var colors = require("colors/safe");`
import colors from "colors/safe";
```

如果你想写自己的默认导出，那也很简单。这里面并没有什么高科技，它和普通的导出没什么两样，除了它的导出名是 `default`。你可以使用我们之前已经介绍过的语法：

```Node
let myObject = {
  field1: value1,
  field2: value2
};
export {myObject as default};
```

这样更好：

```Node
export default {
  field1: value1,
  field2: value2
};
```

`export default` 关键字后可以跟随任何值：函数，对象，对象字面量，任何你能说得出的东西。

模块对象
--------

抱歉，这篇文章的内容有点多，但 JavaScript 已经算好的了：因为一些原因，所有语言的模块系统都有一大堆没什么卵用的特性。所幸的是，咱们只有一个话题要讨论了，呃，好吧，两个。

```Node
import * as cows from "cows";
```

当你 `import *`，被引入进来的是一个 `module namespace object`。它的属性是那个模块的导出，所以如果 “cows” 模块导出了一个名为 `moo()` 的函数，当你像这样引入了 “cows” 之后，你可以这样写 `cows.moo()`。

聚合模块
--------

有时候一个包的主模块会引入许多其他模块，然后再将它们以一个统一的方式导出。为了简化这样的代码，我们有一个 import-and-export 的简写方法：

```Node
// world-foods.js - good stuff from all over

// import "sri-lanka" and re-export some of its exports
export {Tea, Cinnamon} from "sri-lanka";

// import "equatorial-guinea" and re-export some of its exports
export {Coffee, Cocoa} from "equatorial-guinea";

// import "singapore" and export ALL of its exports
export * from "singapore";
```

这种 `export-from` 的表达式和后面跟了一个 `export` 的 `import-from` 表达式类似。但和真正的导入不同，它并不会在你的作用域中加入二次导出的变量绑定。所以如果你打算在 `world-foods.js` 写用到了 `Tea` 的代码，就别使用这个简写形式。

如果 "singapore" 导出的某一个变量恰巧和其他的导出变量名冲突了，那么这里就会出现一个错误。所以你应该谨慎使用 `export *`。

Whew！我们介绍完语法了，接下来进入有趣的环节。

`import` 到底干了啥
-------------------

啥也没干，信不信由你。

噢，你好像看起来没那么好骗。好吧，那你相信标准几乎没有谈到 `import` 该做什么吗？你认为这是一件好事还是坏事呢？

ES6 将模块的加载细节[完全交给了实现](http://www.ecma-international.org/ecma-262/6.0/index.html#sec-hostresolveimportedmodule)，其余的执行部分则[规定得非常详细](http://www.ecma-international.org/ecma-262/6.0/index.html#sec-toplevelmoduleevaluationjob)。

大致来说，当 JS 引擎运行一个模块的时候，它的行为大致可归纳为以下四步：

1. 解析：引擎实现会阅读模块的源码，并且检查是否有语法错误。
2. 加载：引擎实现会（递归地）加载所有被引入的模块。这部分咱还没标准化。
3. 链接：引擎实现会为每个新加载的模块创建一个作用域，并且将模块中的声明绑定填入 

其中，包括从其他模块中引入的。
当你尝试 `import {cake} from "paleo"` 但是 “paleo” 模块并没有导出叫 `cake` 的东西时候，你也会在此时得到错误。这很糟糕，因为你离执行 JS，品尝 `cake` 只差一步了！

4. 执行：终于，JS 引擎开始执行刚加载进来的模块中的代码。到这个时候，`import` 的处理过程已经完成，因此当 JS 引擎执行到一行 import 声明的时候，它啥也不会干。
看到了不？我说了 `import` “啥也没干”，没骗你吧？有关编程语言的严肃话题，哥从不说谎。

不过，现在咱们可以介绍这个体系中有趣的部分了，这是一个非常酷的 trick。正因为这个体系并没有指定加载的细节，也因为你只需要看一眼源码中的 `import` 声明就可以在运行前搞清楚模块的依赖，某些 ES6 的实现甚至可以通过预处理就完成所有的工作，然后将模块全部打包成一个文件，最后通过网络分发。像 [webpack](http://www.2ality.com/2015/04/webpack-es6.html) 这样的工具就是做这个事情的。

这非常的了不起，因为通过网络加载资源是非常耗时的。假设你请求一个资源，接着发现里面有 `import` 声明，然后你又得请求更多的资源，这又会耗费更多的时间。一个 naive 的 loader 实现可能会发起许多次网络请求。但有了 webpack，你不仅可以在今天就开始使用 ES6，还可以得到一切模块化的好处并且不向运行时性能妥协。

原先我们计划过一个详细定义的 ES6 模块加载规范，而且我们做出来了。它没有成为最终标准的原因之一是它无法与打包这一特性调和。模块系统需要被标准化，打包也不应该被放弃，因为它太好了。

动态 VS 静态，或者说：规矩和如何打破规矩
----------------------------------------

作为一门动态编程语言，JavaScript 令人惊讶地拥有一个静态的模块系统。

* `import` 和 `export` 只能写在顶级作用域中。你无法在条件语句中使用引入和导出，你也不能在你写的函数作用域中使用 `import`。
* 所有的导出必须显示地指定一个变量名，你也无法通过一个循环动态地引入一堆变量。
* 模块对象被封装起来了，我们无法通过 polyfill 去 hack 一个新 feature。
* 在模块代码运行之前，所有的模块都必须经历加载，解析，链接的过程。没有可以延迟加载，惰性 `import` 的语法。
* 对于 `import` 错误，你无法在运行时进行 `recovery`。一个应用可能包含了几百个模块，其中的任何一个加载失败或链接失败，这个应用就不会运行。你无法在 `try/catch` 语句中 `import`。（不过正因为 ES6 的模块系统是如此地静态，webpack 可以在预处理时就为你检测出这些错误）。
* 你没办法 hook 一个模块，然后在它被加载之前运行你的一些代码。这意味着模块无法控制它的依赖是如何被加载的。

只要你的需求都是静态的话，这个模块系统还是很 nice 的。但你还是想 hack 一下，是吗？

这就是为啥你使用的模块加载系统可能会提供 API。举个栗子，[webpack 有一个 API](http://webpack.github.io/docs/code-splitting.html)，允许你 “code splitting”，按照你的需求去惰性加载模块。这个 API 也能帮你打破上面列出的所有规矩。

ES6 的模块是非常静态的，这很好——许多强大的编译器工具因此收益。而且，静态的语法已经被设计成可以和动态的，可编程的 loader API 协同工作。

我何时能开始使用 ES6 模块？
--------------------------

如果你今天就要开始使用，你需要诸如 [Traceur](https://github.com/google/traceur-compiler#what-is-traceur) 和 [Babel](http://babeljs.io/) 这样的预处理工具。这个系列专题之前也有文章介绍了[如何使用 Babel 和 Broccoli](https://hacks.mozilla.org/2015/06/es6-in-depth-babel-and-broccoli/) 去生成可用于 Web 的 ES6 代码。那篇文章的栗子也被[开源在了 GitHub 上](https://github.com/givanse/broccoli-babel-examples/tree/master/es6-modules)。笔者的[这篇文章](http://www.2ality.com/2015/04/webpack-es6.html)也介绍了如何使用 Babel 和 webpack。

ES6 模块系统的主要设计者是 Dave Herman 和 Sam Tobin-Hochstadt，此二人不顾包括笔者在内的数位委员的反对，始终坚持如今你见到的 ES6 模块系统的静态部分，争论长达数年。Jon Coppeard 正在火狐浏览器上实现 ES6 的模块。之后包括 JavaScript Loader 规范在内的工作已经在进行中。HTML 中类似 `<script type=module>` 这样的东西之后也会和大家见面。

这便是 ES6 了。

欢迎大家对 ES6 进行吐槽，请期待下周 [ES6 in Depth][] 系列的总结文章。
<small style="float:right">2015年08月21日发布</small>

[ES6 in Depth]: https://hacks.mozilla.org/category/es6-in-depth/

> 除此文之外，还推荐其他参考资料，因版权不明，我尽量多导流少转载：

> * [CommonJS规范 - 阮一峰](http://javascript.ruanyifeng.com/nodejs/module.html)
* [exports 和 module.exports 的区别](https://cnodejs.org/topic/5231a630101e574521e45ef8)
* [浏览器加载 CommonJS 模块的原理与实现 - 阮一峰](http://www.ruanyifeng.com/blog/2015/05/commonjs-in-browser.html)
* [Javascript模块化编程（一）：模块的写法 - 阮一峰](http://www.ruanyifeng.com/blog/2012/10/javascript_module.html)
* [Javascript模块化编程（二）：AMD规范 - 阮一峰](http://www.ruanyifeng.com/blog/2012/10/asynchronous_module_definition.html)
* [Javascript模块化编程（三）：require.js的用法 - 阮一峰](http://www.ruanyifeng.com/blog/2012/11/require_js.html)
* ["AMD"文档（中文版）存档](https://github.com/amdjs/amdjs-api/wiki/AMD-(%E4%B8%AD%E6%96%87%E7%89%88))
