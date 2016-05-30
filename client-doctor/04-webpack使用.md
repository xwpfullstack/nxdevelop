    
    参考的链接

http://www.jianshu.com/p/8adf4c2bfa51

http://segmentfault.com/a/1190000002551952

http://webpack.github.io/docs/webpack-dev-server.html  这个是官方的，有给出非静态文件的解决方案


    改动的地方

```javascript
 entry: {
    bundle: [
    'webpack/hot/dev-server',
    'webpack-dev-server/client?http://localhost:8080',    //webpack-dev-server 的运行位置
    path.resolve(__dirname, 'app/menus.js'),　　　　　　　  //menus.js，我需要引用的js文件
    ]
  },
  output: {
    path: path.resolve(__dirname, 'build'),
    publicPath: "http://127.0.0.1:8080/",　　　　　　　　　　//设置一下 output.publicPath, 把所有静态资源指向该path
    path:'./build/',
    filename: 'menus.js',
  },
```

    DJANGO需要引用JS的地方：<script src="http://127.0.0.1:8080/menus.js"></script>


    说明，开个webpack-dev-server服务器负责文件的更新，django引用webpack-dev-server更新的文件
    文件修改时, webpack-dev-server 通过 socket.io 通知客户端更新

    引用官方的一段话：
    Summary and example:

```javascript
webpack-dev-server on port 8080.
backend server on port 9090.
generate HTML pages with <script src="http://localhost:8080/assets/bundle.js">.
webpack configuration with output.publicPath = "http://localhost:8080/assets/".
when compiling files for production, use --output-public-path /assets/.
inline mode:
--inline.
open http://localhost:9090.
or iframe mode:
webpack-dev-server contentBase = "http://localhost:9090/" (--content-base).
open http://localhost:8080/webpack-dev-server/.
```
