+++
categories=["开发", "dev", "English", "中文"]
tags=["前端","frontend","webpack","PostCSS"]
date = "2016-04-03T16:40:00Z"
title = "Frontend Learning Notes 2 - Direction Shifted"

+++

My Confession
---------

> Only the ignorant person fears nothing.

I gotta say that I was way too over ambitious about the frontend stack. When companys like Google and Mozilla start to push the standardization of new innovations of the Web. The frontend standards keeps changing everyday, so does the Toolchain. Chasing the tool could be harmful, so I realised a realistic learning plan could be more benificial for me.
After a few days of extensive research, my mind changed. The more I learn, I become less bold, so that I become more and more eager for a shorter learning curve. Compareing with "Flawless on paper", I prefer a more practical stack.
Here is what I learnt:

### `PostCSS` => `SCSS`

I know the PostCSS is the future, and CssNext/preCss plugins appears like a great replacement of Scss. Also according to Boostrap & many others SCSS is way better than LESS. But then I find that if I want to custom and build Boostrap, I have to import SCSS anyway. So SCSS+Autoprefixer beat my original ideal buy ignorant plan.

### Build Tool & Module Bundler

There is a little bit backgound I have learnt.
- [gulp](http://gulpjs.com/) beats [grunt](http://gruntjs.com/).
- [Webpack](https://webpack.github.io) beats [browserify](http://gbrowserify.org) beats [RequireJS](http://grequirejs.org).
- ~~With the viral of `NodeJS`, `CommonJs` becomes the de facto standard importing syntax(I believe). It Beats AMD, CMD and otheres, moreover `ES6 module` is compatiable with it, so it is also future-proof.~~(Completely Wrong...explained below)
- Webpack is capable to do some jobs of gulp.
 
I was thinking of using gulp + webpack. But since nowadays, webpack have plenty of plugins and loaders, and most importantly, I found at least 2 boostrap-loaders which claims that they can process Boostrap v4. I can simply say good bye to Gulp. *I might meet you again, don't know why, don't know when, but I might meet you again some other day~*

Webpack can minify Js, provide source map for dev stage, build SCSS, build typescript, build Vue/JSX, build Boostrap, include jQuery support without expose global access to it, process PostCSS(Autoprefixer), custom the dist path, watch the dev folder, live-reload. What else do you need? What else do you need? What else do you need?


### Keep Practicing

> It is the only way to reveal the imperfection of your tool and to pursue perfection of understanding at the same time!

Before practise, you won't know if the tool is gonna suit your needs. 
That is exactly why I dropped the semantic UI, because it follows "*Convention over Configuation*", so it has to sacrifice "*Explicit is better than implicit*"<small>\*Refering to [The Zen of Python](https://www.python.org/dev/peps/pep-0020/)</small>

Before practise, you won't know NodeJS have many dependency issue with Windows platform, so the `Vagrant` become mandatory! no longer *Good to have*. That is a good thing also, If I could compose my `Vagrantfile`.

> Nevertheless, this is absolutely worth our attention. However, it is neither stable nor mature. https://blogs.windows.com/buildingapps/2016/03/30/run-bash-on-ubuntu-on-windows/


Again, references
----------


### NodeJS:

- [What is Node.js Exactly? - a beginners introduction to Nodejs(YouTube)](https://youtu.be/pU9Q6oiQNd0)
- [Modular Javascript - Javascript Tutorial on the Object Literal Pattern(YouTube)](https://youtu.be/HkFlM73G-hk?list=PLoYCgNOIyGABs-wDaaxChu82q_xQgUb4f)


### WebPack:

- [Getting Started with webpack(YouTube)](https://youtu.be/TaWKUpahFZM)
- [Webpack Tutorial - Replace Gulp/Grunt plugins with a single tool(YouTube)](https://youtu.be/9kJVYpOqcVU)
- [一小时包教会 —— webpack 入门指南](http://www.cnblogs.com/vajoy/p/4650467.html)
- [Webpack傻瓜式指南（一）- 张轩(知乎)](http://zhuanlan.zhihu.com/p/20367175)
- [Webpack傻瓜指南（二）开发和部署技巧- 张轩(知乎)](http://zhuanlan.zhihu.com/p/20367175)


### Vue:

- [Getting Started - vue.js](http://vuejs.org/guide/)
- [VueJs 官方指南](http://vuejs.org.cn/guide/)
- [Vuex 官方指南](http://vuex.vuejs.org/zh-cn/quickstart.html)
- [Vue-router 官方指南](http://router.vuejs.org/zh-cn/basic.html)
- [如何用Vue.js来搭建一个简易的APP](https://sally-xiao.gitbooks.io/book/content/index.html)


### Vagrant:

- [Ruby Programming in One Video(Youtube)](https://youtu.be/Dji9ALCgfpM): In one video series is great for syntax-learning.
- [VAGRANT DOCUMENTATION](https://www.vagrantup.com/docs/)
- [vagrant-node-env(Github)](https://github.com/drmyersii/vagrant-node-env)
- [laravel/homestead(Github)](https://github.com/laravel/homestead)


### Page Load Effect:

- [ContentLoaded(2010)](http://javascript.nwbox.com/ContentLoaded/) A page load library,used by webpack.github.io
- [Animated page trasition](https://codyhouse.co/gem/animated-page-transition/) Worth investigation
- [History.js](https://github.com/browserstate/history.js) Need no introduction
- [Non-Jquery Page Transitions lightweight](http://www.fasw.ws/faswwp/non-jquery-page-transitions-lightweight/) A great proof of concept
- [TurboReact](https://turbo-react.herokuapp.com/) A react based implementation
- [Turbolinks](https://github.com/turbolinks/turbolinks) extraction of above solution, the best library to use by far
 

Corrigendum
-----------


### ES6 Modules is not an official recognition of CommonJS

ECMAScript 6 modules is a completely different thing, comparing with `CommonJs`.

- First of all, ES6 Modules are statically loaded!!!!
- Then It requires all the dependencies to be fully imported at the beginning.
- So that the tricks like `tree-shaking` becomes possible. (AST parsing becomes much more effient and easy)
- There is performance improvement as well.

Can't believe how assertive I was.

### References

- [ECMAScript 6 modules: the final syntax](http://www.2ality.com/2014/09/es6-modules-final.html)
- [Tree-shaking with webpack 2 and Babel 6](http://www.2ality.com/2015/12/webpack-tree-shaking.html)
- [Rollup.js - The next-generation JavaScript module bundler](http://rollupjs.org/)
- [如何评价 Webpack 2 新引入的 Tree-shaking 代码优化技术？](https://www.zhihu.com/question/41922432/answer/93346223)
- [The Importance of import and export by Ben Newman on EmpireNode 2015 ](http://benjamn.github.io/empirenode-2015)