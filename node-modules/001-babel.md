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

3. ### JSX and Flow(已经用到)

   Babel 可以转换 JSX 语法，并且去掉类型注释。查看 [React preset](https://babeljs.io/docs/plugins/preset-react/)。可以和 [babel-sublime](https://github.com/babel/babel-sublime) ,(就是一个可以让包含JSX语法高亮的插件)。

   安装:

   `npm i -D babel-preset-react`

   安装好这个插件后，在`.babellrc`的`presets`数组中配置"react"

4. ### Pluggable

   Babel is built out of plugins.Babel 是用插件构成的。使用已存在的插件或者自己写一些插件来组成你自己的变换管道。使用插件嘛是很容易的，使用/创建 [preset](https://babeljs.io/docs/plugins/#presets) 就行。[了解更多](https://babeljs.io/docs/plugins/)

   # [npm 上由社区维护的可用的`presets`](https://www.npmjs.com/search?q=babel-preset)

   ​

   ## 参考资料;

   1. [Babel入门教程](http://www.ruanyifeng.com/blog/2016/01/babel.html)

      * 配置文件` .babelrc`

        Babel 的配置文件是`.babelrc`,存放在项目根目录下。使用 Babel 第一步就是配置这个文件。

        ```javascript
        {
          "presets":[],
          "plugins":[]
        }
        //presets 字段设定预转码规则
        ```

        官方提供以下的规则集，可以根据需要安装。

        ```javascript
        //es2015转码规则
        $ npm i -D babel-preset-es2015

        //react转码规则
        $ npm i -D babel-preset-react

        //es7不同阶段语法提案的转码规则(共4个阶段，选装一个就好啦)
        $ npm i -D babel-preset-stage-0
        $ npm i -D babel-preset-stage-1
        $ npm i -D babel-preset-stage-2
        $ npm i -D babel-preset-stage-3
        ```

        然后将这些规则加入`.babelrc`

        ```javascript
        {
          "presets":[
            "es2015",
            "react",
            "stage-0"
          ],
          "plugins":[
          
          ]
        }
        ```



注意事项:

1. babel-core: 如果某些代码需要调用 Babel 的API进行转码，就要使用`babel-core`模块

   `npm i -S babel-core`

2. 与其他工具配合

   许多工具需要Babel进行前置转码，举两个例子: ESLint和Mocha

   [ESLint](http://eslint.org/)用于静态检查代码的语法和风格，安装命令如下:

   ```javascript
   npm i -D eslint babel-eslint
   ```

   [Mocha](http://www.ruanyifeng.com/blog/2015/12/a-mocha-tutorial-of-examples.html)是一个测试框架，如果需要执行使用ES6语法的测试脚本，可以修改`package.json`的`scripts.test`。

   ```javascript
   "scripts": {
     "test": "mocha --ui qunit --compilers js:babel-core/register"
   }
   ```

   ​