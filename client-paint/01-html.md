## html入门
菜鸟教程
  http://www.runoob.com/html/html-tutorial.html

## json请用双引号 

官方要求双引号，json就是一段有格式的字符串，如果数据的封装与解析都是我们自己做的时候，单引号和双引号是没啥关系的，但是如果用到一些别的json相关的库的时候，或者像笔者这样是发给别人用的时候，这个就特别需要注意了！ 

python中，json字符串是字典变量类型的字符串的时候，对应字典中的key部分，注意是用双引号括起来，而不能是单引号，否则也是会导致json.loads出错的。 

## 手机禁用缓存

JS或CSS代码改变，可手机浏览器怎么刷新都不更新，手机浏览器的缓存特别恶劣。记得，本地调试的时候贴上，上线后要删除，免得访问者浏览体验慢。把下面的代码贴到HEAD里面即可。

```
<meta http-equiv="expires" content="0">
<meta http-equiv="pragma" content="no-cache">
<meta http-equiv="cache-control" content="no-cache">
```
