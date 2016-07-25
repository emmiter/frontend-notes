# [Babel transforms your javascript](https://babeljs.io/)

Babel 是一个编译器。在较高级别上，它会有3个运行代码的阶段：解析(parsing),转换(transforming)和生成(generation)，和其他编译器差不多。

> 想要一份很厉害/很简单的关于编译器的教程，查看 [the-super-tiny-complier](https://github.com/thejameskyle/the-super-tiny-compiler),里面也介绍了 Babel 是如何在高层工作的。

Now, out of the box Babel doesn’t do anything. It basically acts like `const babel = code => code;` by parsing the code and then generating the same code back out again.

You will need to add some plugins for Babel to do anything (they affect the 2nd stage, transformation).

Don’t know where to start? Check out some of our [presets](https://babeljs.io/docs/plugins/#presets).

## devDependencies



1. ### ES2015 and beyond(已经用到)

   Babel 借助语法转换器已经开始支持最新版本的 Javascript 了。这些插件允开发者现在就可以使用最新的(ES6 或者是存在于ES7草案中) JS 语法来编写代码，而不用去等待浏览器的支持。

   安装:

   `npm i -D babel-preset-es2015`

   安装好这个插件后，在`.babellrc`的`presets`数组中配置"es2015"

2. ### Polyfill

   因为 Babel 只是起到转换语法的作用(比如箭头函数这种)，你可以使用`babel-polyfill`来支持新的全局变量，比如`Promise`或者新的本地方法，比如`String.padStart(left-pad)`.Polyfill 使用了 [core-js](https://github.com/zloirock/core-js) 和 [regenerator](https://facebook.github.io/regenerator/)。 查看 [babel-polyfill](https://babeljs.io/docs/usage/polyfill) 文档了解更多。

   安装：`npm i -D babel-polyfill`

   注: 在入口文件的最顶层导入该模块，或者写在bundler配置中。

3. ### JSX and Flow(已经使用)

   Babel 可以转换 JSX 语法，并且去掉类型注释。查看 [React preset](https://babeljs.io/docs/plugins/preset-react/)。可以和 [babel-sublime](https://github.com/babel/babel-sublime) ,(就是一个可以让包含JSX语法高亮的插件)。

   安装:

   `npm i -D babel-preset-react`

   安装好这个插件后，在`.babellrc`的`presets`数组中配置"react"

4. ### Pluggable

   Babel is built out of plugins.Babel 是用插件构成的。使用已存在的插件或者自己写一些插件来组成你自己的变换管道。使用插件嘛是很容易的，使用/创建 [preset](https://babeljs.io/docs/plugins/#presets) 就行。[了解更多](https://babeljs.io/docs/plugins/)

   # [npm 上由社区维护的可用的`presets`](https://www.npmjs.com/search?q=babel-preset)

   ​

   ​