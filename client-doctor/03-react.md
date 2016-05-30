#React学习

## react点滴

## 1. [编程规范](https://github.com/airbnb/javascript/blob/master/react/README.md) 
## 2. reaction 运行流程
* 准备
    * npm3.3.12
    * babel相关 v6.1.4
        1. [Babel-现在开始使用 ES6](http://www.cnblogs.com/whitewolf/p/4357916.html)
    * browsersync
    * [下载react](http://facebook.github.io/react/downloads.html)，将六个js文件放到build文件夹中
    * [react的补充工具](https://github.com/facebook/react/wiki/Complementary-Tools)
```shell
     # 安装npm
     npm install -g babel-cli
     npm install -g browserify
     npm install -g babelify babel-preset-react babel-preset-es2015
     # babel编译
     babel --presets es2015,react src/main.js -o lib/main.js
     babel --presets es2015,react src/ -d lib/
     # 安装browsersync
     sudo npm install -g browser-sync
     # browser-sync运行
     browser-sync start --server --files "*.*"
```
* 测试（[官方网站](https://facebook.github.io/react/))
    # html:格式相对固定

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8" />
    <!-- 用于屏幕适配 -->
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
    <!-- 用于禁用缓存，在发布版中需要注释掉 -->
    <meta http-equiv="expires" content="0">
    <meta http-equiv="pragma" content="no-cache">
    <meta http-equiv="cache-control" content="no-cache">

	<title>hello react</title>
    <!-- 引入react相关的js模块 -->
	<script src="build/react.min.js"></script>
	<script src="build/react-dom.min.js"></script>
	<script src="build/jquery.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.23/browser.min.js"></script>
	<link rel="stylesheet" type="text/css" href="app.css">
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
</head>
<body>
	<div id="example"></div>
	<script src="lib/main.js"></script>
</body>
</html>
```
    # jsx

## react学习网站
中文react： http://reactjs.cn/react/docs/getting-started.html


## 实例网站

三联书社：  http://daren.slaclinic.com/

## 讲react的好贴

    父子组件通信：http://www.tuicool.com/articles/AzQzEbq
    todo例子：http://www.reqianduan.com/2297.html
    mixin透彻分析：http://segmentfault.com/a/1190000002704788
    
    

##React学习路线
    
    1.关于React的学习，首先看视频，7节视频。1.5~2倍速度快速过一遍
    然后根这个中文网，快速理解一下。
    http://reactjs.cn/react/docs/getting-started.html
    
    2.这里的文章都不错。至少先看快速入门的前三章节
    
    快速入门，教程，深入理解React这三节，务必把代码粘到sublime上，
    亲自体验一把。
    
    3.理解一些关键点，尝试写代码。。。
    
##React需要理解的要点
    
###React需要理解的两个东东
    
    props属性字段，用来存一些父组件传给子组件的数据，子组件可以通
    过this.props.属性名 的方式获取父组件传递给子组件的值，一般可用
    来初始化静态数据，即下文中不期望会改变的值
    
    state状态字段，用来存放将来可能会因为某种情况改变的字段，例如
    当界面有个字段1.当用户点击一下按钮时，这个字段就会变成2，为了
    让它能在改变后及时渲染到页面上，可以将这个字段设置为一个state，
    然后在鼠标的点击让其加1并且重新设置state
    
```javascript
    construct(){
        super();
        this.state = {num:1};
    }
    
    onclick(){
        let num = this.state.num;
        this.setState({num:num++});
    }
```
    
    当调用state时，与state相关联的组件会被重新render,就是所谓的React状态机
    的机制，当state改变时，其相关的东东跟着变
    在确定state的时候以尽量精简为原则，比如你已经有了列表，就没必要吧列表的
    长度设置为state.因为你完全可以根据list.length得到。
    如何确定state的值是一个值得深入思考的问题，需要在实践中慢慢感悟。。。
    
###关于父组件与子组件的传值
    
####父组件给子组件传值
    这个比较简单可以直接通过props或者state
    
```javascript
    //子组件
    class Child extends React.Component{
        render(){
            <div>
                {this.props.value}
            </div>
        }
    }
    //父组件
    class Parent extends React.Component{
        render(){
            <div>
                <Child value={1} />
            </div>
        }
    }
```

    说明：父组件在render子组件的时候可以为子组件赋予一些自定义的属性，属性名
    可以是任意的，比如在父组件里定义了value=... ，那么子组件就可以通过
    this.props.value获取。也可以通过state给子组件传值
    
```javascript
    //子组件
    class Child extends React.Component{
        render(){
            <div>
                {this.props.value}
            </div>
        }
    }
    //父组件
    class Parent extends React.Component{
        construct(){
            super();
            this.state = {value:1};
        }
    
        render(){
            <div>
                <Child value={this.state.value} />
            </div>
        }
    }
```    
    
    说明：这样一来，父组件的state.value的值改变后，子组件的值也将会跟着渲染
    因为value值变化导致props.value的值也跟着变化，跟state有关的变化会跟着联动。
    
####子组件为父组件传值

    亦或者，父组件获得子组件的值。
    主要通过两种方式：
    
    1.为子组件需要被父组件获得的地方加上ref,这样父组件就可以通过this.refs.子组件的ref名。
    获得子组件的内容，可以通过子组件的ref找到子组件，然后通过它的ref再找到子组件的组件。
    嵌套层次可以无限制，但是嵌套太深逻辑也将变得复杂。这种处理的方式有一个很大的限制就是
    只能通过父组件主动的寻找子组件去获取值，不能更智能，这种方式一旦使用意味着，只有当父组件
    主动调用方法时，才能获得值。与回调函数成对比
    
    2.回调函数。例如子组件里有个文本框和按钮，父组件想要当子组件点击按钮时候获得到子组件的
    文本框的值，那么父组件可以提前定义一个函数参数为一个的函数。以属性的方式传递给子组件，
    子组件通过click事件，执行this.props.父组件预留的函数 的方式，这样就会执行到父组件提前
    写好的逻辑里。是一种非常灵活的方法，但是同样由于层次太深，导致的不方便是存在的。这种方式
    在react里将大量使用，习惯就好。。。
    
```javascript
    //子组件
    class Child extends React.Component{
        myclick(msg){
            //此处调用父组件传给他的方法
            this.props.parentMed(this.refs.t1.value);
        }
    
        render(){
            <div>
                <input type='text' ref="t1"/>
                <input onClick={()=>{this.myclick()} />
            </div>
        }
    }
    //父组件
    class Parent extends React.Component{
        construct(){
            super();
        }
        
        Med(msg){
            alert(msg);
        }
        
        render(){
            <div>
                <Child value={this.state.value} parentMed={(msg)=>{this.Med(msg)}}/>
            </div>
        }
    }
    
```

    这个demo演示父组件是如何通过回调函数获得子组件的值，当得到子组件的值后父组件就可以进行
    编写相应的逻辑使用它的值
    
####兄弟节点的值得交互

    A------B
        |
        |__C
        
    假设B和C是兄弟组件，那么要想交互的话可以通过为它们建立公共的组件A，
    然后通过A为双方提供数据。
    
    
##React组件编写实战经验

    用React编程的重要体验就是不在是单纯的写html。而是用代码逻辑的方式去思考，怎么组织
    组件可以被后面重复利用，当需要在使用相同功能的情况下，不是在去吧代码写一遍，而是
    直接把代码拿过来用就可以。

###组件的设计构建

    方案1：
    在组件设计的时候，我有想过两种方案，一种是父组件得到的数据，当子组件需要的时候，直接
    让父组件通过props属性传递给子组件，那么子组件就不需要访问网络，查询数据库，这种方案的
    优点是一次性获取的数据，不需要再第二次重复获得，节省了带宽和与服务器的数据交互，当子
    组件修改数据后，再通过父组件的回调函数，对父组件的一些数据做相应的同步，那么子组件与
    父组件的整体就同步了。这种方案在实际当中编写起来相对复杂，但是一旦实现后可以做为独立
    模块维护，但是缺点也很明显，数据耦合性太高，东西太死。很大的可能性就是在这个页面用完
    以后，很难移植到下一个页面
    
    方案2：
    父组件设计的时候通过ajax请求获得想要的数据，当数据需要向下传递时候，子组件虽然也要用到
    与父组件的相同一部分数据，但是子组件不接受全部数据。例如父组件需要订单的信息以及订单的
    状态信息，这需要两张表的查询，子组件也需要这些数据，这时候只给子组件传递一个订单id,让子
    组件根据订单id再次发送ajax请求去查询自己需要的数据。这种方式的好处就是父组件与子组件
    的耦合性降低，当子组件被应用到其他场合时，不需要依赖父组件的数据，可以随时分离出来应用于
    其他场合，但是缺点也显而易见，父组件已经获得到的数据，还需要子组件去请求一遍，增加了一次
    与服务器的交互，与多花费了一些流量。如果服务器的响应速度比较慢，那么性能损失上还是比较明
    显的。但是这种交互方式的好处就是配合路由使用的时候，每次发ajax请求，得到的都是最新的数据。
    父子组件在数据更新时，不需要做太多处理，只要是数据提交到了服务器，那么另一个组件重新请求
    时候获得的当时是最新的了。
    
    方案3：
    1和2的折中，既抽象部分的接口，又提供部分的数据，在解耦上面做文章。难度大，不易抽象出来
    思考需要大量的时间，当需求提出变更时候，组件是否需要做相应的改动是个问题，维护起来比较费劲
    
    个人倾向第二种解决方案，这样开发起来方便。需求变更时候更改起来容易
    
###组件设计的大小

    当一个组件设计的足够大时候，它的功能也就意味着更加复杂，职责更加多。当然带来的便利性也是
    显而易见的，当需要使用这一坨功能的时候，把它引入就OK。
    当一个组件设计的太小的时候，会很灵活，但也可能会导致引用过多，变的麻烦
    一切以需求为导向，在不断的尝试中找到合适的平衡点很重要。。。
    
###组件使用--套路

    目前的解决套路：
    1.组件类的构造函数内部初始化state为空或者默认值，为将来通过ajax请求获取数据做准备。
    
#####这里有个坑需要关注的是
    
    如果数据不存入state中，很有可能页面渲染完了，ajax的请求的响应结果才过来，
    虽然数据已经来了。但此时不会重新渲染界面。而导致非目标结果
    
    2.在组件已经挂载时调用ajax请求数据，在success时候，更新state，渲染页面数据.
    
    3.提前布局回调函数，当子组件触发某些事件，例如按钮点击，通过回调函数，将数据返回给父组件，
    父组件内做相关逻辑处理。
    
###实现路由(路由原理)。

    路由的本质还是通过对React状态机机制的一层包装，即在不同的情况下渲染不同的页面，
    那么这个不同的体现就是通过state的值做判断
    
    那么直接上代码，假设有页面A和页面B，初始化的时候是页面A，当点击A上的一个项时候跳到B。
    在B中点返回，返回A
    
```javascript
    class Manager extends React.Component{
        construct(){
            this.state = {pageName:'A'};
        }
        
        setPage(pageName,args){
            //args为页面参数，js对象做参数，可以传输大量信息
            this.setState({pageName:pageName,pageArgs:args});
        }
        
        render(){
            let child;
            if(this.state.pageName =='A'){
                child = <A setPage={(p,a)=>{this.setPage(p,a)}/>
            }else if(this.state.pageName =='B'){
                child = <B setPage={(p,a)=>{this.setPage(p,a)}/>
            }
        
            <div oncClick={}>
                {child}
            </div>
        }
    }
    

    
    class A extends React.Component{
        
        goToB(){
            this.props.setPage('B',{});
        }
        
        render(){
            <div onClick={()=>{this.goToB()}}>
                我是A组件，点我进入B组件
            </div>
        }
    }
    
    class B extends React.Component{
        construct(){
            super();
        }
        
        returnToA(){
            this.props.setPage('A',{});
        }
        
        render(){
            <div onClick={()=>{this.returnToA()}}>
                我是B组件，点我返回组件
            </div>
        }
    }
```
    
##后记

    当做惯后端后，再去接触前端，会发现，前端东西很乱很杂，但是很多细节不会还真做不出来某些效果
    确实是比较蛋疼的事情，有时候后台代码BUG见多了，一般无非就那些，一会就能调完，可是前端做起来
    并不是那么一帆风顺，不熟是一个原因，但是其他因素也有很多，有时候确实会感觉，做前端也不比后端
    简单多少。传统的HTML模板机制，mvc思想，给我们一种编程体验，让代码显得更有逻辑，更可控制，
    React更是给了我们一种关于界面层的编程的新思想，深入学习REACT，不只是因为它太高大尚，更是学习
    一种编程思想，至少通过这种组件化的编程体验带给我们的收获是，不断的写组件，复用组件，在这种
    可以快速见效的东西面前，不断探索。一个组件设计的好坏，就是看下次遇到相同需求时候，能不能直接
    复用自己的组件，虽然否定自己是件痛苦的事情。但是修改代码后获得更好的组件体验也很重要。
    其实前端后端做久了，感觉编程思想还是蛮重要滴，不断地在实践中感悟吧。
    
##经典语录大放松

    路叔，你可以的
    
    路叔，你真棒
    
    加油，路叔。
    
    都快要猝死的人了。。。
    
    
