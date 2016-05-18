## Ios离线包打包过程:

1.编辑projectApp/ios/projectApp/AppDelegate.m文件,取消jsCodeLocation=[[NSBundle mainBundle...这一行的注释;

2.在Xcode中,project的info中,修改Bundle name 为要发布的app名称;

3.在xcode中打开Image.xcassets/AppIcon,将不同icon图片拖进去作为icon图标;

4.在Xcode中,project的Supported ubterface orientations 中选择或删除手机支持的横屏和竖屏模式;

5.在Xcode中,选择Product/Scheme/Edit Scheme 选择编译模式,debug和release,选择release;

6.点击run,打包到手机上,生成release版本的app;


## ios发布账号

### 邓白氏编码

水木品格科技（北京）有限公司

Shuimupinge Technology (Beijing) Co., Ltd.

北京海淀区清华同方科技广场D座东楼503

Room 503, East Building, Block D, Tsinghua Tongfang Technology Plaza,Haidian District, Beijing

申请邮箱:xwp_fullstack@163.com
D-U-N-S Number: 544392010

### APPdevID

APPdevID:xwp_fullstack@163.com

passwd:问jack

### itunes Connect上app展示图片尺寸

网址：

    https://itunesconnect.apple.com/WebObjects/iTunesConnect.woa/ra/ng/

切图尺寸：

    4.7寸   750x1334
    5.5寸   1242x2208
    4寸     640x1136
    3.5寸   640x960

ipad暂时不用上传



