## [测试框架 Mocha](http://www.ruanyifeng.com/blog/2015/12/a-mocha-tutorial-of-examples.html)

参考资料:

1. [测试框架Mocha实例教程](http://www.ruanyifeng.com/blog/2015/12/a-mocha-tutorial-of-examples.html)

Mocha 是现在最流行的测试框架之一，在浏览器和Node环境都可以使用。

所谓“测试框架”，就是运行测试的工具。通过它，可以为Javascript应用添加测试，从而保证代码质量。

类似的测试框架还有 [Jasmine](http://jasmine.github.io/)，[Karma](http://karma-runner.github.io/1.0/index.html)，[Tape](https://github.com/substack/tape/)等，也很值得学习。

全局安装`mocha`

```javascript
npm i --global moch
```

### 测试脚本的写法

`Mocha`的作用是运行测试脚本，首先必须学会写测试脚本。所谓测试脚本，就是用来测试源码的脚本。

总结:

1. 通常测试脚本与所要测试的源码脚本同名，后缀名为`.test.js` / `.spec.js`
2. 一个测试脚本里应该有一个或多个`describle`块，每个`describle`块应该包括一个或多个`it`块。`describle`块也被成为测试套件，表示一组相关的测试，它是一个函数，第一个参数是测试套件的名称，第二个参数是一个实际执行的函数
3. `it`块称为`测试用例`，表示一个单独的测试，是测试的最小单位。
4. 断言库:这里用的是[chai.expect](http://chaijs.com/)
5. 使用方法
   * 基本用法: mocha file.test.js, mocha file1.test.js file2.test.js,紧跟测试脚本的路径和文件名，可以指定多个脚本
   * 默认运行`test`子目录里的测试脚本，要递归执行的话，需要 `mocha --recursive`
   * 使用 `--reporter`参数指定测试报告格式，默认是`spec`，还可以用`html`(需要使用mochawesome模块)，`markdown`，`tap`等
   * 配置文件`mocha.opts`
   * es6风格的代码需要先进行转码`npm install babel-core babel-preset-es2015 --save-dev`,配置`.babelrc`,指定转码器`../node_modules/mocha/bin/mocha --compilers js:babel-core/register`
   * 默认是2000ms，异步调用一般会超过默认值，此时需要使用`--timeout`重新指定超时阈值
   * 异步测试
   * 测试钩子
   * 测试用例管理