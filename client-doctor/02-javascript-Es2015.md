## class创建类

1. 类名首字母必须大写,不然会加载不出来
2. 类中不能直接定义变量
3. constructor()函数中必须先要调用super()初始化父类


## js语法入门

菜鸟教程 

  http://www.runoob.com/js/js-tutorial.html




## ES5规范

    https://github.com/airbnb/javascript/tree/master/es5


## ES6（既ES2015）入门

    http://wiki.jikexueyuan.com/project/es6/let.html
    http://gank.io/post/564151c1f1df1210001c9161

## ES6规范

    https://github.com/airbnb/javascript
    
## babel简介

http://www.cnblogs.com/whitewolf/p/4357916.html

## 无框架js

http://web.jobbole.com/81990/



## ecma官方

    http://www.ecma-international.org/ecma-262/6.0/index.html

## React规范

    https://github.com/airbnb/javascript/tree/master/react

## html与css规范

class和id用小写字母，并且class用“-”分割命名，id用用“_”分割命名因为很多浏览器会把id直接添加到全局scope，容易和js里起的变量名冲突，但如果id里面带有下划线，就只能像window['xxx_xx']这样访问，而不能直接当作变量名访问，就不会和js里的变量名冲突了。
    
    <div id="s_lm_wrap" class="s-isindex-wrap">

