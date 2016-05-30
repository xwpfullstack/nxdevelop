#FlexBox是模块而不是一个属性。

    父元素：伸缩容器
    子元素：伸缩项目

## 一些概念:

    主轴
    主轴起点
    主轴尺寸
    侧轴
    侧轴起点
    侧轴尺寸

#FlexBox的属性：


    display:flex|inline-flex　用来定义是内联还是块，所有子元素变为flex文档流

    flex-direction:row|row-reverse|column|column-reverse
    row(默认值):左到右
    column:上到下
    -reverse:与原定的反向

    flex-wrap:nowrap|wrap|wrap-reverse

    nowrap(defalut):单行显示
    wrap:多行显示
    wrap-reverse:反向

    flex-flow:direction || wrap
    defalut:row nowrap

    justify-content:flex-start | flex-end | center | space-between | space-around   
    主轴线上的控制,对元素内部多余或者溢出的控件进行利用
    flex-start:类似float:left
    flex-end:类似float:right
    center:居中
    space-between:平均分布在一行里，空填充
    space-around:伸缩项目会平均分布在行里，两端保留一半的空间

    align-item:flex-start | flex-end | center | baseline | stretch  
    flex-start:类似左上对其
    flex-end:类似左下对其
    center:居中对其
    baseline:伸缩项目根据基线对其
    stretch:拉伸使充满

    aligin-content:flex-start | flex-end | center | space-between | space-around | stretch  
    这个属性用来调准伸缩行在伸缩容器里的对齐方式。类似主轴上使用justify-content.
    对于只有一行的伸缩容器没有效果
    justify-content是对某一行设置规则,
    这个属性是对里面的每一行应用这个规则
    space-between:各行在伸缩容器中平均分布，可能会产生垂直方向的空隙
    space-around:与上相似

    order:控制元素出现的顺序，是一个整数值

    flex-grow:伸缩项目的伸缩能力，主要用来伸,需要一个整数做比例。

    flex-shrink:伸缩能力。主要用来缩
    
    flex-basis:伸缩的基准值，剩余控件按比例进行伸缩


#参考
####大体认识
http://www.w3cplus.com/css3/a-guide-to-flexbox.html
####具体缩放控制
http://segmentfault.com/a/1190000002490633
    
