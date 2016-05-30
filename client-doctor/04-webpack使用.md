    
    参考的链接
    
    
https://fakefish.github.io/react-webpack-cookbook/Introduction-to-Webpack.html

http://www.jianshu.com/p/8adf4c2bfa51

http://segmentfault.com/a/1190000002551952

http://webpack.github.io/docs/webpack-dev-server.html  这个是官方的，有给出非静态文件的解决方案


## webpack是什么

它是一个模块合并的工具，本质就是一个能够把各种组件（HTML，CSS，JS）构建成项目。最方便的是你只需要初始化配置一次，Webpack 会替你做那些繁琐的事情，同时也保证了让你可以在项目中混合使用各种技术而不头疼。

参考：

    https://fakefish.github.io/react-webpack-cookbook/?utm_source=tuicool&utm_medium=referral

## 我们的项目怎么用

先下载我们的项目目录

    git clone https://github.com/nuanxin1111/react.git

webpacktest目录是安装配置好的目录，react和babel等都已经安装到此目录中，进入此目录

### 开发调试

1. 在/home/itcast/workspace/nuanxin1111/react/webpacktest目录下
    
    npm run dev

2. 打开chrome浏览器,服务器默认用的8080端口
   
    http://127.0.0.1:8080/

3. 开发时，修改component.js里的“helloworld”,当保存时，可以看到浏览器自动加载刷新
```
.
├── app
│   ├── a.jpg
│   ├── component.js
│   ├── main.js
│   └── myapp.css
├── build
│   ├── bundle.js
│   ├── index.html
│   └── myapp.css
```



### 发布

开发时bundle.js文件过大，有１Ｍ左右。真正部署时，使用如下命令

    npm run deploy

此时生成的bundle.js文件大约300k。

### 测试发布文件

进入到/home/itcast/workspace/nuanxin1111/react/webpacktest/build

借助python自带的httpserver

　　　　python -m SimpleHTTPServer 8080

查看浏览器，此时使用的bunld.js就是发布时使用的。
