## [webpack-dev-server](http://webpack.github.io/docs/webpack-dev-server.html)

1. a little node.js [Express](http://expressjs.com/) server

2. use the [webpack-dev-middleware](http://webpack.github.io/docs/webpack-dev-middleware.html) to serve a web pack bundle

3. has a little runtime which connected to the server via [Socket.IO](http://socket.io/)

4. 服务器会给出有关客户端编译状态的信息，并且会对这些事件作出响应。可以根据个人需要，选择不同的模式。比如你的`webpack.config.js`长下面这样:

   ```javascript
   import path from 'path'
   module.exports = {
     entry:{
       app:["./src/main.js"]
     },
     output:{
       path:path.resolve(__dirname,"build"),
       publicPath:"/assets/",
       filename:"bundle.js"
     }
   }
   ```

   > `webpack-dev-server` 是一个单独的NPM 模块，使用前先安装:`npm i -D webpack-dev-server`

5. *Content Base* — The *webpack-dev-server* will serve the files in the current directory, unless you configure a specific content base.

   ```javascript
   $ webpack-dev-server --content-base build

   //使用上面这个配置命令，server 将会在build目录下serve the static files.** 它会监控源文件的变化，当文件发生变化时，bundle.js就会重新被编译生成新的   bundle.js。修改过的bundle文件是从内存被伺服的。*This modified bundle is   served from memory at the relative path specified inpublicPath (see API). It  will not be written to your configured output directory. Where a bundle  already exists at the same url path the bundle in memory will take precedence (by default).
   ```



## 使用方法

* Iframe mode
* Inline mode(使用inline mode)
  * 在命令行中用`--inline`指定，这个是没法写进webpack的配置文件的。
  * `--inline` 使用inline mode
  * `--hot` 使用'Hot Module Replacement'
  * 带有`[HMR]`前缀的消息来自于`webpack/hot/dev-server`模块。带有`WDS`前缀的消息来自模块`webpack-dev-server client`
  * ​

